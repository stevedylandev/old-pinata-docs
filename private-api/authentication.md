# Authentication

To connect to the Pinata Submarine API, you will need to generate a Private API key. Visit the [Private API Keys](https://app.pinata.cloud/developers/v2-api-keys) page to generate new keys.

When you click "New Key", a new key will be generated and the key can be copied from the table directly.&#x20;

Any key can have its access revoked by clicking the Revoke button. Once a key has been revoked, it can no longer be utilized for any purpose.

## Connecting to the Private API

The base URL for Pinata requests is: `https://managed.mypinata.cloud/api/v1`

Authentication happens via a customer header:&#x20;

`x-api-key: YOUR PRIVATE API KEY`
