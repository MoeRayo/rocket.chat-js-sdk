# Quickstart

By completing this integration, you would have successfully created and deployed a basic Rocket.Chat bot on your local system (Linux, macOS, or Windows).

This bot, named "easybot," will:

- Connect to a specified Rocket.Chat server using the provided credentials.
- Join specified chat rooms on the server.
- Listen for messages in those rooms.
- Respond to messages starting with its name ("_easybot_") by offering assistance in those specific rooms.

::: tip
This integration is fitted for node version 8.x or higher. Please before you start building, make sure you have the latest version of nodeJs installed on your machine.
:::

To check your node version, run the command below in your terminal:

```js
node -v //command to check for the version
v8.9.3 //command output
```

### Install SDK

Create a project directory and install the Rocket.Chat JavaScript SDK as a dependency. You can do this by running the command below in your terminal:

```js
npm install @rocket.chat/sdk --save
```

### Creating the bot

In the project directory, create a new file named `easybot.js`. Now copy the code below into it:

```js
const { driver } = require("@rocket.chat/sdk");
// customize the following with your server and BOT account information
const HOST = "myserver.com";
const USER = "mysuer";
const PASS = "mypassword";
const BOTNAME = "easybot"; // name  bot response to
const SSL = true; // server uses https ?
const ROOMS = ["GENERAL", "myroom1"];

var myuserid;
// this simple bot does not handle errors, different message types, server resets
// and other production situations

const runbot = async () => {
	const conn = await driver.connect({ host: HOST, useSsl: SSL });
	myuserid = await driver.login({ username: USER, password: PASS });
	const roomsJoined = await driver.joinRooms(ROOMS);
	console.log("joined rooms");

	// set up subscriptions - rooms we are interested in listening to
	const subscribed = await driver.subscribeToMessages();
	console.log("subscribed");

	// connect the processMessages callback
	const msgloop = await driver.reactToMessages(processMessages);
	console.log("connected and waiting for messages");

	// when a message is created in one of the ROOMS, we
	// receive it in the processMesssages callback

	// greets from the first room in ROOMS
	const sent = await driver.sendToRoom(BOTNAME + " is listening ...", ROOMS[0]);
	console.log("Greeting message sent");
};

// callback for incoming messages filter and processing
const processMessages = async (err, message, messageOptions) => {
	if (!err) {
		// filter our own message
		if (message.u._id === myuserid) return;
		// can filter further based on message.rid
		const roomname = await driver.getRoomName(message.rid);
		if (message.msg.toLowerCase().startsWith(BOTNAME)) {
			const response =
				message.u.username +
				", how can " +
				BOTNAME +
				" help you with " +
				message.msg.substr(BOTNAME.length + 1);
			const sentmsg = await driver.sendToRoom(response, roomname);
		}
	}
};

runbot();
```

The above code uses async calls to login, join rooms, subscribe to message streams and respond to messages (with a callback) using provided options to filter the types of messages to respond to.

> Make sure you replace "**myserver.com**", "**myuser**", "**mypassword**", and other placeholders with your actual server and account information.

Now, you can run the bot using the script below:

```js
node easybot.js
```

### Demo

You can find a basic listener script to showcase the functionality locally. You can view the source code here or execute it using the command `yarn start`.

Once started, this script will log any message events to the console as they occur. It's designed to respond to specific commands, demonstrating the usage of API helpers.

You can interact with the bot by sending it one of the following commands:

- `tell everyone <something>`: This command will broadcast the message "**something**"to everyone.
- `who's online`: This command will provide you with a list of users who are currently online.
