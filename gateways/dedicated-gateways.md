---
description: A comprehensive guide to dedicated gateways.
---

# Dedicated Gateways

{% hint style="info" %}
Pinata's Dedicated Gateways are for users need faster speed or increased rate limits when retrieving content.
{% endhint %}

Dedicated Gateways are private IPFS gateways which allow you to access pinned content with faster speeds and increased rate limits. You can consider them the red carpet experiencing to accessing and serving content.

### **What are the Benefits of a Dedicated Gateway?**

* **Personalization:** Integrate custom domains and keep your branding consistent
* **Limitless:** No rate limits for requesting content
* **Security:** Control who can access your content
* **Reliability & High-Performance:** Enjoy unmatched speed through our 200+ edge-caching locations around the world

### Limited Dedicated Gateways <a href="#limited-dedicated-gateways" id="limited-dedicated-gateways"></a>

Users on our free plan have access to a **limited dedicated gateway.** In this version, users get a taste of the speed of dedicated gateways with the ability to serve individual files such as images, videos and audio. However, files containing HTML and scripts will not be served\*.

\*_Upload functionality is not affected._

{% hint style="info" %}
_Free plan users wanting more out of their limited dedicated gateway can simply upgrade to any of our_ [_flexible premium plans_](https://www.pinata.cloud/pricing) _(starting at just $20/month)_
{% endhint %}

## Getting Started

* First things first, [sign up for a Pinata account](https://app.pinata.cloud) :piñata:
* Pinata creates dedicated gateways for all new users by default. Navigate to your 'Gateways' tab and you will see your dedicated gateway waiting for you.

{% hint style="info" %}
If you'd like to start anew and create a new gateway, or if your plan allows the creation of more than 1, you can follow our [step-by-step guide below:](dedicated-gateways.md#getting-started-dedicated-gateway)
{% endhint %}

## How To Create Your Dedicated Gateway <a href="#getting-started-dedicated-gateway" id="getting-started-dedicated-gateway"></a>

1. On your dashboard, navigate to the 'Gateways' tab. Click on 'Create Gateway'. This will prompt our easy-to-use gateway wizard.

<figure><img src="../.gitbook/assets/gateways_retrievingcontent.gif" alt=""><figcaption><p>Step 1: Navigate to "Gateways'</p></figcaption></figure>

2. Choose a unique name for your Gateway. _Gateways are_ [_restricted_](dedicated-gateways.md#open-vs.-restricted) _by default._
3. Et voila! :magic\_wand: You should now be able to see your new gateway on your dashboard.

{% hint style="info" %}
_Optional:_ Add your own [custom domain](dedicated-gateways.md#adding-a-custom-domain) or [additional security measures](gateway-access-controls.md).
{% endhint %}

## How Do I Use My Gateway?

### How do I serve IPFS content through my gateway?

To view content through your gateway, grab the CID of the file you'd like to view and add it to your gateway URL like this:

`https://<Your Gateway Subdomain>.mypinata.cloud/ipfs/<Your CID>`

Simple as that!

### How do I convert other gateway URLs to use my gateway?

In many cases, projects will directly put an entire gateway URL on-chain (such as when minting NFTs).

If you find yourself reading from a location that may provide a gateway URL, Pinata created the [ipfs-gateway-tools](https://github.com/PinataCloud/ipfs-gateway-tools) toolkit to help you out.

This toolkit can easily convert any standard IPFS gateway URL, as well as URIs with the `ipfs://<CID>` format to a URL that utilizes your gateway.

### How can I add a custom domain?

Pinata also allows you to create a custom domain for your dedicated gateway. Simply click the menu button on the right side of your gateway row in the table on the Gateways page, then click Add Custom Domain. You'll need to own the domain you want to use. When you enter your domain, you will be prompted to enter DNS information through your registrar.

## Frequently Asked Questions

### What is the difference between Open vs. Restricted gateways? <a href="#open-vs-restricted-gateway" id="open-vs-restricted-gateway"></a>

What's the difference between an open gateway and a restricted gateway? In both cases, the content served by the gateway will be available to anyone with the link. However, the **restricted** gateway will only serve content that is pinned on your account.

{% hint style="info" %}
Dedicated gateways will be **restricted** by default.
{% endhint %}

An **open** gateway will (assuming it can find the content on the IPFS network) serve up any content even if it's not pinned to your account.

{% hint style="warning" %}
Open gateways are great for wide accessibility but without proper [Gateway Access Controls](gateway-access-controls.md) to safeguard your gateway, are susceptible to abuse (and can result in usage costs to go through the roof :exploding\_head:).
{% endhint %}

### **How do I change my gateway from restricted to open?**

To change a gateway from restricted to open, you would need to use the [gateway-access-controls.md](gateway-access-controls.md "mention"), by adding either an Access Token, Host Origin, or IP Address. When you add one of these access controls, the gateway will be able to fetch content outside your account as the restriction requirement is met.

### What is Bandwidth?

Bandwidth is the data that represents the item you or your users are viewing through your dedicated gateway. Each image, video, audio, and any other type of file that is displayed through the gateway or downloaded through the gateway is made of up data. That data is sent from an IPFS node to your computer. The size of this data is bandwidth.

You can track your bandwidth for any gateway you have set up by going to your Gateways page and clicking on the subdomain link for your gateway.

## We want your feedback! :speech\_balloon:

Have a suggestion? Have a complaint? Confused about something in the documentation? Just want to say hi?

We want to make Pinata the best product available. That involves listening to our users and addressing their needs.

Send us an email at [team@pinata.cloud](mailto:team@pinata.cloud) and we'll see how we can help.
