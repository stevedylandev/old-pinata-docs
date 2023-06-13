# 🔓 Private API

The Pinata Private API can be used to upload content that remains private and off the public IPFS network. With Pinata Private Files, you can keep content private and generate access tokens programmatically that last for as long as you specify.&#x20;

This API can be used for uploading files and folders, listing content, and generating access tokens to view and download content.&#x20;

Viewing Private content requires a [Dedicated Gateway](https://knowledge.pinata.cloud/en/articles/5455525-how-to-set-up-a-dedicated-ipfs-gateway). When viewing Private content through a Dedicated Gateway, you must include a valid access token. The access token can be generated using [this API method](accessing-private-files/generate-access-token.md). This is how you should construct a link to view Private content:&#x20;

**Single File**

`GATEWAY_URL/ipfs/FILE_CID?accessToken=TOKEN`



**File Within a Folder**

`GATEWAYURL/ipfs/FOLDER_CID/FILE_NAME?accessToken=TOKEN`
