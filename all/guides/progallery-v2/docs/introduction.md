SortOrder: 0
# About Pro Gallery


With Wix Pro Gallery, you can help site owners manage their Pro Galleries.

The Pro Gallery API allows your app to:

*   Get, and update Pro Galleries
*   Create, get, update, and delete media items

Read more about how site owners can manage their [Pro Galleries](https://support.wix.com/en/article/wix-pro-gallery-about-the-wix-pro-gallery).


## Terminology


+ **Pro Gallery:** A responsive, and customizable gallery that displays media items.
+ **Media Items:** Images, videos, and text files uploaded to a Pro Gallery. You can read more about [supported media](https://support.wix.com/en/article/wix-pro-gallery-adding-media-to-the-gallery).


## Limitations


+ Currently, you can't create or delete a Pro Gallery via the API.
+ The [Gallery Created](https://dev.wix.com/api/rest/site-content/pro-gallery/gallery-created-webhook) and [Gallery Updated](https://dev.wix.com/api/rest/site-content/pro-gallery/gallery-updated-webhook) webhooks don't return the media items included in the gallery. To retrieve these items or their IDs you need to listen to the [Gallery Item Created](https://dev.wix.com/api/rest/site-content/pro-gallery/gallery-item-created-webhook) and [Gallery Item Updated](https://dev.wix.com/api/rest/site-content/pro-gallery/gallery-item-updated-webhook) webhooks in addition.