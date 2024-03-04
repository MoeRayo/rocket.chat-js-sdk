# Overview

Are you building a collaborative workspace, a customer support portal, or a social networking platform, and looking for a way to integrate real-time messaging features? Designed especially for chat automation, the Rocket.Chat JavaScript SDK makes it easy for bot and integration developers to provide the best solutions and experience for their community.

Using this package third party apps can control and query a Rocket.Chat server instance, via Asteroid login and method calls as well as DDP for subscribing to stream events.

For example, the [Hubot Rocketchat adapter](https://github.com/RocketChat/hubot-rocketchat) uses this package to enable chat-ops workflows and multi-channel, multi-user, public and private interactions.

## How it works

### Making the Connection

The Rocket.Chat JS SDK establishes a connection between your application and the Rocket.Chat server. You provide your application's credentials and connect to the server using the SDK. This opens a communication channel, allowing your application to interact with the Rocket.Chat platform.

### Real-time Communication

Instead of directly dialing another device, the Rocket.Chat JS SDK utilizes two key protocols for real-time communication:

- **DDP (Distributed Data Protocol)**: This protocol acts like a conversation channel, enabling your application to:
  - Subscribe to specific chat rooms or data streams on the server, receiving real-time updates whenever something changes.
  - Publish messages or data from your application to the server, updating the information for other users.
- **API**: The SDK also provides access to the Rocket.Chat API, allowing you to perform specific actions and retrieve data using HTTP requests. This can be used for functionalities like:
  - User authentication and authorization.
  - Creating, editing, or deleting messages, channels, and other data.

## Quickest start in 30 seconds

Get started right way by creating a ready-to-run chatbot for any Rocket.Chat server in 30 seconds at [glitch.com](https://glitch.com/~rocketchat-bot).
