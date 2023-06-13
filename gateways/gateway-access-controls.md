---
description: Improved gateway security
---

# 🔓 Gateway Access Controls

Pinata's Dedicated Gateways make it possible to fetch and serve IPFS content quickly and reliably. There are, however, risks in exposing your gateway to the world. To mitigate the dangers of this security vector, we created **Gateway Access Controls.**

These controls will allow you to further limit your gateway, making sure only your platform is using it. This is accomplished with the following 3 access control methods:

1. [**Access Tokens**](gateway-access-controls.md#access-tokens)
2. [**IP Address Restrictions**](gateway-access-controls.md#ip-address)
3. [**Host Origin Restrictions**](gateway-access-controls.md#host-origin)&#x20;

To start, navigate to the 'Access Control' tabs under the [Developers](https://app.pinata.cloud/developers/) section.

#### Why do I need gateway access controls?

By default, Dedicated Gateways are restricted with the lowest level restriction possible. They will only serve content that is pinned to your account. This restriction is helpful for creators and for those just getting started. But if you want to restrict access further, **or if you want to access IPFS content from the wider network that may not be pinned to your account, you'll need to add security restrictions.**&#x20;

### Access Tokens

Adding an access token restriction means that content served through your gateway will only be served successfully if the access token is present with the request. **Importantly, you should note that even if the content is pinned to your account, it will not longer serve through your gateway if you have added an access token restriction and don't include that token in requests for content.**&#x20;

To create an access token, click on "Request Token"

![](<../.gitbook/assets/CleanShot 2023-03-21 at 13.05.14@2x.png>)

When you create an access token you will have the ability to preview the token by clicking the "eye" icon, or copy the token to your clipboard with the "copy" icon. At any point you can delete an access token by clicking the three small dots on the right.

![](<../.gitbook/assets/CleanShot 2023-03-21 at 12.57.11@2x.png>)

Once you have the token, there are two ways you can use it in the gateway request.&#x20;

#### 1. Query Parameter

To use the query parameter method, simply add this to the end of a gateway request url:

```
?pinataGatewayToken=PASTE_IN_ACCESS_TOKEN
```

#### 2. Header

Another way to use the access token is in the request header. The Key Value would look like this:

| Key                    | Value         |
| ---------------------- | ------------- |
| x-pinata-gateway-token | ACCESS\_TOKEN |

{% hint style="info" %}
Please keep in mind that using the access token in the request header may not work in a client side application, consider using IP Address restriction instead for those use cases.
{% endhint %}

### IP Address

You can also restrict your gateway by IP Address. You can add up to 100 different IP addresses (individually). When you add this restriction, only content requested from an IP address that you've added will be served through your gateway.&#x20;

To start click "Set IP Address" on the right side of the menu.&#x20;

![](<../.gitbook/assets/CleanShot 2023-03-21 at 13.02.59@2x.png>)

You will get window asking for a valid IP Address that will allow any requests being made from the IP Address to go through!

![](<../.gitbook/assets/CleanShot 2023-03-21 at 13.07.07@2x.png>)

### Host Origin&#x20;

With the Host Origin restriction you can make sure your gateway can only be used on a specific Domain like `app.pinata.cloud`.

To get started, click on "Add Host Origin"

![](<../.gitbook/assets/CleanShot 2023-03-21 at 13.04.08@2x.png>)

After that you can add the domain you would like your gateway to be used from!&#x20;

![](<../.gitbook/assets/CleanShot 2023-03-21 at 13.06.38@2x.png>)

Keep in mind that if you are rendering content on the client side using host origins, you will need to include a crossorigin tag in your `img`, `video`, `audio`, `link`, or `script` elements. Here is an example with an img element in React:

```javascript
<img 
 src="<https://pinata-media.mypinata.cloud/ipfs/CID>"
 crossOrigin='anonymous' 
 alt="pinnie" 
/>
```

For more info on crossorigin, read this article [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/crossorigin).

### Multiple Restrictions

You can add multiple Access Controls and they will perform as an "OR" operator, meaning if you have Host Origins and Access Token set, you can use either one for content to go through.&#x20;
