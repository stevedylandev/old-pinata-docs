---
description: What is their purpose? Why do I need them?
---

# Why Gateways?

{% hint style="info" %}
Gateways are the portal to access content pinned on IPFS on modern-day applications.
{% endhint %}

### How content is retrieved from IPFS

When you pin your content to Pinata, it will be available to all on the public IPFS network. This means that anybody running an IPFS node can access content stored on Pinata through their own IPFS node.

However, directly running a node isn't the only way to access content, nor is it the easiest. The most common way to retrieve content on the IPFS network is through an **IPFS gateway.**

#### The barrier of modern-day applications

Most applications, including your everyday browser, do not yet support IPFS natively. **Gateways** are IPFS nodes allow you to leverage the HTTP protocol (via a web URL) to request data by CID from the IPFS network.&#x20;

Gateways often take the following form:

&#x20;[`https://example.gateway.com/ipfs/CID`](https://example.gateway.com/ipfs/CID)

The `CID` is the content identifier (also known as a hash) for the content you want to retrieve.

In some ways, gateways are sort of like a _translator_ that allow your content to be understood and served properly on modern platforms.

### Pinata's Gateway Services

**Pinata** provides two types of gateway services: the [Public Pinata Gateway](retrieving-content.md) **a**nd [**Dedicated Gateways.**](dedicated-gateways.md)

## We want your feedback!

Have a suggestion? Have a complaint? Confused about something in the documentation? Just want to say hi?

We want to make Pinata the best product available. That involves listening to our users and addressing their needs.

Send us an email at [team@pinata.cloud](mailto:team@pinata.cloud) and we'll see how we can help.
