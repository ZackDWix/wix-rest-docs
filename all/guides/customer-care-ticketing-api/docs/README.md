SortOrder: 0
# Customer Care Ticketing API

Customer Care service that exposes support actions for external or internal clients, specifically:
- Add ticket on behalf of a user
- Request callback on behalf of a user

The service hides any setup/implementation which is required when opening support requests within the paltform (Wix Answers), and lets a client perform support requests without internal knowledge of callback queues, callback lines, assignee groups and more.

## Main use case:
External "channel" accounts transfer their user's support requests to Wix by selecting either a post (ticket) or callback request on behalf of the user.
As the support tickets are handled internally by Wix experts, the channel is unaware of the mentioned platform specifics, and by providing the necessary payload to the API, they manage to transfer these requests to be handled by Wix.
