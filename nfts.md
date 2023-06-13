# ✌ NFTs

We've put together some best practices for using IPFS and Pinata with NFTs. If you are minting an NFT, this documentation will apply to you especially. However, if you own NFTs, you'll also find value in being able to extract the asset you own and pin it to IPFS yourself.

Let's dive in!

## Why Should NFT Assets Be Hosted on IPFS

You may come across NFT assets that are hosted on platforms such as Amazon S3, Google Cloud, or even Dropbox. None of these solutions are well suited for something that you almost certainly want to prove the authenticity of. Think back to trading cards. Some of the rarest trading cards have an authority come in to verify their authenticity and provide certificates proving that authenticity. For digital items, this isn't possible.

At least, not by just looking at the digital asset. Instead, we can leverage [content addressability](https://docs.ipfs.io/concepts/content-addressing/) to prove the authenticity of a digital asset. When the asset is created, it can be added to the IPFS network. In doing so, a content identifier (CID) is generated. That identifier is unique to that asset. If someone had a copy of the assets and made a slight modification, the CID would change and anyone in the world would be able to see that the copy was not the original and thus (maybe) not as valuable.

We've covered this concept quite a few times, [but this post is a good place to start](https://medium.com/pinata/the-file-requirements-for-nfts-a20ea3ac524b) if you want to learn more.

## How To Upload Your Asset With Pinata

Before minting an NFT, you'll normally want to have the asset that will be associated with your token uploaded to IPFS. With Pinata, we make this easy.

Simply go to the Pin Manager, click the upload button, choose a file, and upload your file. When the upload is complete, you'll see your file in the grid and can copy the IPFS CID (the string of characters that starts with "Qm"). You'll need this CID later, so keep it handy. You can also come back to the Pin Manage page and copy it again at any time.

## How To Create a JSON Metadata File

While the asset is what you are selling, the blockchain that you mint your token on needs to store a "pointer" to that asset. This pointer takes the form of a JSON file with properties that relate to your NFT. Think of these properties as rows and columns in a spreadsheet. You might have a row called "Name" and in the associated column, you might have "John Doe". That is essentially what a JSON file is doing.

Let's take a look at a very basic example of some JSON specifically designed for NFT metadata:

```
{
  "description": "Description of your NFT", 
  "image": "ipfs://YOUR_ASSET_CID", 
  "name": "A name for your NFT"
}
```

The `image` property is especially important because this is the actual pointer we mentioned before. It points to your asset which is hosted on IPFS.

### Why don't we use a "normal" URL for the image property?

The format of the image value is `ipfs://` and not `https://someurl.com`. This is for good reason. Blockchain data is permanent. If you put a link to your asset in the form of some URL owned by Pinata or any other company, you run the risk of that URL not being available at some point in the future. How many sites use to exist on the web in the 90s and 2000s that no longer do?

To avoid this, we reference IPFS assets with the `ipfs://YOUR_CID` pointer. Most platforms can resolve this format, and even if they can't, it's easy to pull out the CID and load the content using a public gateway like the main IPFS gateway, for example.

### Now, how do I create a file like this?

Creating your JSON file is pretty simple. Open up the notepad app on your computer, copy the JSON example from above, and paste it into the notepad. Change the values however you need to, but make sure both the properties and the values are wrapped in double-quotes.

Save your file and give it a useful name like `asset_metadata.json`. You can call it whatever you'd like, but you need to make sure to save it with the `.json` file extension.

Now, you can upload this JSON to Pinata. When you do, you will once again get a CID. This time, the CID is for your metadata JSON which is a pointer to the file you uploaded before.

## How To Associate Metadata With Your NFT

When you mint your token, most platforms will ask for this metadata. You should be able to provide the metadata in the same format as you did for your asset value in the metadata itself:

`ipfs://YOUR_METADATA_CID`

Now you have a future proof NFT that you can hold, transfer, or sell. Anyone can fetch the asset you created without needing to worry about any specific service existing in the future.
