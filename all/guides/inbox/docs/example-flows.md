SortOrder: 1
# Example Flows

This article shares some possible use cases your app could support,
as well as an example flow that could support each use case.
You're certainly not limited to these use cases,
but they can be a helpful jumping off point
as you plan your app's implementation.

## Syncing Messages from an External Service

Your app can enable business owners to communicate with their customers on any platform
by syncing messages to Wix Inbox.
The scenario below covers chat messages,
but this flow could support integrating phone call logs, SMS services,
chat sessions, or any other online or offline communication.

To do this, your app can follow this basic flow:

1. Set up the external service's webhooks.
    When a message webhook is triggered,
    parse the payload data for an email address.

    Save the message and any other relevant data.

2. Use [Query Contacts][query-contacts]
    to find a contact with the email address you extracted in step 1.
    You're looking for a contact ID here,
    so you can use the `fields` array to make sure the response only passes back `id`:

    ```json
    {
      "query": {
        "filter": {
          "info.emails.email": {
            "$eq": "<EMAIL_ADDRESS_FROM_INCOMING_MESSAGE>"
          }
        },
        "fields": [
          "id"
        ]
      }
    }
    ```

    The response includes matching contacts in the returned `contacts` array.
    An email address can belong to more than one contact,
    so your app must be able to handle situations when multiple contacts are returned.

3. Use [Send Message][send-message]
    to add the new message to contact's conversation.

    Set `visitor.id` in the path parameters to the `id` extracted in step 2.

    In the body, pass the incoming message in a [`PLAIN` message type][plain-message-type]:

    ```json
    {
      "message": {

        // Hides the message from the chat widget when the contact visits the site
        "visibility": "BUSINESS",

        "payload": {
          "type": "PLAIN",
          "plain": {
            "data": [
              {
                "type": "TEXT",
                "text": "<INCOMING_MESSAGE_FROM_EXTERNAL_SERVICE>"
              }
            ]
          }
        },

        // Indicates the message came from Facebook
        "badges": [
          {
            "text": "Facebook",
            "iconUrl": "https://static.wixstatic.com/media/aebe5b6fd55f471a936c72ff2c8289d7.png/v1/fill/w_43,h_43,al_c,q_85,usm_0.66_1.00_0.01/aebe5b6fd55f471a936c72ff2c8289d7.webp"
          }
        ]
      },

      // Displays the message as if the contact sent it
      "direction": "VISITOR_TO_BUSINESS"
    }
    ```

Your app can also store messages sent on behalf of the business
in the external chat tool.
In those cases, change the visibility settings to match your requirements,
and set `direction` to `BUSINESS_TO_VISITOR`.

## Adding Contact Activities from Another Service

Your app can capture contact activities from another platform
and display them in the contact's conversation in Inbox.

To do this, your app can follow this basic flow:

1. Set up the external service's webhooks.
    When a webhook is triggered,
    parse the payload data for an email address.

2. Use [Query Contacts][query-contacts]
    to find a contact with the email address you extracted in step 1.
    You're looking for a contact ID here,
    so you can use the `fields` array to make sure the response only passes back `id`:

    ```json
    {
      "query": {
        "filter": {
          "info.emails.email": {
            "$eq": "<CUSTOMER_EMAIL_ADDRESS>"
          }
        },
        "fields": [
          "id"
        ]
      }
    }
    ```

    The response includes matching contacts in the returned `contacts` array.
    An email address can belong to more than one contact,
    so your app must be able to handle situations when multiple contacts are returned.

3. Use [Send Message][send-message]
    to add the new message to the contact's conversation.

    Set `visitor.id` in the path parameters to the `id` extracted in step 2.

    In the body, pass the action in a [`MINIMAL` message type][minimal-message-type]:

    ```json
    {
      "message": {

        // Hides the message from the chat widget when the contact visits the site
        "visibility": "BUSINESS",

        "payload": {
          "type": "MINIMAL",
          "minimal": {
            "text": "Booked Spa Treatment",
            "iconUrl": "https://static.wixstatic.com/media/bd4a2aff643141cb8cbacde1a4007a2f.png/v1/fill/w_43,h_50,al_c,lg_1,q_85/bd4a2aff643141cb8cbacde1a4007a2f.webp"
          }
        }
      },

      // Displays the message as if the contact sent it
      "direction": "VISITOR_TO_BUSINESS"
    }
    ```

[query-contacts]: https://dev.wix.com/api/rest/contacts/contacts/contacts-v4/query-contacts
[send-message]: https://dev.wix.com/api/rest/all-apis/inbox/send-message
[plain-message-type]: ./message-types.md#plain-messages
[minimal-message-type]: ./message-types.md#minimal-messages