SortOrder: 2
## Terminology

### Topic

A topic entity represents the relevant Wix domain to transfer a support request.
It encapsulates the internal support platform properties to allow the correct routing of a created post ticket or a callback request ticket.
Specifically, it holds:
- `name`
- `languageCode` (ISO 2 letter language code)
- `description`
- `postGroupId` (The assigned group of the ticket)
- `callbackQueueId` (The matching callback queue of the topic)
- `callbackLineId` (The matching phone line for outbound calls)
- `id`
- `updatedDate`
- `createdDate`

The last three are metadata fields that aren't exposed to the client when querying topics or live availability/status of topics.
On top of that, querying topics are deduced with an additional `supportedChannels` fields (either `Ticket` or `Callback`) - while some topics may be relevant just for post or callbacks, but not both.

When creating a support request, for example, when adding a ticket on behalf of the user, the `topicId` is required for the action.
In addition, if a given topic's callback queue isn't available for calls at the time of the request, it will reject the action.

A complete mapping of the topic entities to the it's corresponding support platform entities (on top of Wix Answers) is held internally as part of the service related database.
