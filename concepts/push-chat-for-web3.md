# Push Chat for Web3

## An Introduction&#x20;

Since Push Protocol started with decentralized notifications, every chat message sent on the protocol has a notification built in. Whenever a message is sent to an address, the receiving address will receive a notification along with the message if they opt-in.

Unlike traditional messengers that require users to provide their information to sign up, like their email, phone number, or any other personal data about the user, Push Chat requires no personal information whatsoever to start messaging on the protocol.&#x20;

All the user needs is a **wallet address.**

All the messages are stored on IPFS and are encrypted as well as signed.&#x20;

It's important to note that only the addresses involved in the conversation shall be able to decrypt the messages, and anyone can verify that the message was indeed sent by the sender's address and that the messages are encrypted.

When sending a message to an address, it is sent through Push Nodes.&#x20;

_**Push Nodes**_ are a network of nodes, where each node can have a different role in the network that is responsible for validating each notification and chat message between addresses.&#x20;

Their main task is to validate that:

* &#x20;the payload is following the corresponding payload standard,
* the sender can actually send the message, and signature validation,
* if the payload is valid, the Push Nodes will store the message on IPFS and then send a notification (_considering that the address has opt-in_) to the receiver of the message.&#x20;
* Additionally, to read the messages, the receiver client will query the Push Nodes for any new message that was sent to it.

### Spam prevention

Spam prevention has always been one of our major priorities.&#x20;

There are countless examples of users spamming others with fake giveaways, random messages, or unwanted notifications.

For notifications, the core protocol itself adopts a user-centric approach. This means that all the notifications are opt-in or opt-out based.&#x20;

This means that users shall only receive notifications from protocols they opt in to. Users can fine-tune which notifications they see the value of and only opt-in for them while every other notification shall land in the user's spam box.&#x20;

Chat is no different. We are working on our spam prevention mechanism on the core protocol level (_more information about this soon_), but as of today, we have a chat request that enables spam prevention as it requires user acceptance before push notifications for those chats are enabled.

## Chat request

Push Chat has two types of message groups: _**Inbox and Request**_**.**&#x20;

The very first time an address wants to send a message to another peer, the address must send an intent request. This first message shall not land in this peer Inbox but instead in its Request box.

When the user sees this message in its Request box, the user has 2 options:

* It can accept it and start messaging back the address
* It can ignore it (blocking users will be launched on the next version)

It must be noted that addresses don’t get notified about messages on the Request box. The notifications are only received if the address accepts the Request to talk to the other peer.&#x20;

This prevents users from receiving notifications from any random address that sends them a message. So the user only receives notifications from the chat the user wants to talk to.

## Sending messages

The core protocol allows addresses to message any other address on Ethereum or Polygon. If the message is sent to an address that hasn’t authenticated itself yet on the protocol (generate a pair of encryption keys), those messages will be in plain text until the address you are talking to authenticates itself in the protocol. From that moment on, all the following messages will be encrypted.

If you send a message to an address that has already been authenticated into the protocol, the messages will be encrypted. The reason for this choice was to allow addresses to send messages to their friends regardless of whether they have accessed the application. This design choice was made for better UX, but it can easily be changed if the community decides to.

## Decentralization

Chat messages are sent between addresses via the Push Nodes. Push Nodes are the nodes responsible for validating notification and chat payload and for dispatching notifications to addresses. Push Nodes can have different roles in this Communication Network.

The vision for Push Protocol is for the Push Nodes to be run by the community and to get rewarded by contributing to the network's decentralization. As of today, Push Nodes are run by Push Protocol, but the team is working on decentralizing the nodes.

Although the Push Nodes are run by Push Protocol, users can always verify that the chat messages and notifications haven’t been tampered with and that they have indeed been sent by the correct address. Users can always verify this by the Verification Proof.

### Verification Proof

Verification Proof is a property that is sent along with the notifications and chats messages to help the network validate the sender, the chain from which the notification (or message) is sent, and the content of the notification (or message) along with any other validation that might be required.

For notifications, the verification proofs differ based on the platform from which they are sent. i.e., Smart contracts verification proof can be validated on-chain, and smart contract-based notifications will usually carry transaction hash proofs while off-chain/gasless notifications usually carry EIP-712 proofs, though they are capable of carrying smart contract verification proof as well, which makes it composable.

## Encryption

When an address logs in to the protocol for the first time, PGP encryption keys are generated for the address.&#x20;

The PGP private key is then encrypted with the address’ public key and then sent the encrypted PGP private key, along with the PGP public key, to Push Nodes to get stored.&#x20;

{% hint style="success" %}
This is extensible which means that the PGP key can be encrypted in the future with other methods paving way for a multi-chain future.
{% endhint %}

Messages are encrypted on the client by using the AES encryption algorithm.&#x20;

A different AES secret key is generated for each message. This secret key is then encrypted with the PGP public keys from the parties involved in the conversation and then sent the encrypted AES key is to Push Nodes.&#x20;

The message payload content also contains the encrypted AES key in order to decrypt the message.

## Whitelist access

Push Chat launched as an Alpha version on Devcon in Bogota, and its access is limited as of now. To start messaging, addresses need to have POAPs that are getting distributed to the community. If you haven’t had the chance to take one, stay tuned on our socials for more information.

For whitelisted addresses, they can message up to 10 other addresses, regardless if those addresses are whitelisted or not. The receiver of the message can then approve the intent and start messaging back.

{% hint style="success" %}
To enable dApps to adopt Push Chat while it's closed, we have enabled an optional API key that bypasses the whitelisted access for the dApp and their users. The API key will not be required when Push Chat access becomes public.\
\
To get the API key, please join our discord and ask a CM or a Dev for one. :point\_right: [https://discord.com/invite/pushprotocol](https://discord.com/invite/pushprotocol)
{% endhint %}

## Push Chat SDK

With the SDK, it will be easy for developers to integrate messaging into their dapps. The use cases are endless:

* You can provide customer support to your users
* Create groups to discuss governance proposals without relying on Discord
* Chat with the community on a web3 game
* DMs or DAO token gated conversation
* Any other cool, crazy feature you can think of

Alright. Now that you have a clear picture of the Push Chat and its SDK, let's dive in and try to integrate the push chat in your application.

{% content-ref url="../developer-guides/integrating-push-chat.md" %}
[integrating-push-chat.md](../developer-guides/integrating-push-chat.md)
{% endcontent-ref %}

{% content-ref url="../developer-tooling/push-sdk/sdk-packages-details/epnsproject-sdk-uiweb/uiweb-0.2.3-push-support-chat.md" %}
[uiweb-0.2.3-push-support-chat.md](../developer-tooling/push-sdk/sdk-packages-details/epnsproject-sdk-uiweb/uiweb-0.2.3-push-support-chat.md)
{% endcontent-ref %}
