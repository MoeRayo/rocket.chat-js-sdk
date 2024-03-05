# Driver Methods

This section contains the methods available on a `driver` instance.

[[toc]]

## `driver.connect(options[, cb])`

The `driver.connect` function initiates a connection to a Rocket.Chat server using options such as the host and timeout. It can be invoked either with a promise or a callback function following the error-first pattern.

Upon successful connection, it resolves with an [Asteroid](https://www.npmjs.com/package/asteroid) instance, facilitating further interactions with the Rocket.Chat server.

## `driver.disconnect()`

The `driver.disconnect` function performs necessary cleanup operations, including unsubscribing, logging out the current user, and disconnecting from the Rocket.Chat server.

It returns a promise which indicates successful disconnection.

## `driver.subscribe(topic, roomId)`

This function enables subscribing to a Meteor subscription with specified parameters such as `topic` and `roomId` which, typically relates to the Rocket.Chat streamer. It returns a promise that resolves with a subscription instance containing an ID for the subscription.

## `driver.unsubscribe(subscription)`

The `driver.unsubscribe` function cancels a subscription identified by the provided subscription instance.

## `driver.unsubscribeAll()`

The `driver.unsubscribeAll` function cancels all active subscriptions and returns a promise indicating successful unsubscription from all subscriptions.

## `driver.subscribeToMessages()`

The `driver.subscribeToMessages` function is a convenient shortcut for subscribing to the user's message stream. It uses default arguments for subscription, including:

- topic: `stream-room-messages` and
- roomId` __my_messages__`.
