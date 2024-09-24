# IRC: Internet Relay Chat

## Introduction

The **IRC** (Internet Relay Chat) project is focused on building a simplified IRC server that adheres to the **RFC 2812 protocol**. Our goal is to create a server where multiple clients can connect, join channels, exchange messages, and use standard IRC commands such as `JOIN`, `PART`, `PRIVMSG`, and more. This project emphasizes network programming, concurrency, and the handling of multiple clients through socket communication.

## Key Components

1. **Network Layer** (`/srcs/network/`)
	- **Socket Programming:** The core of our IRC server relies on socket programming to manage client connections and handle communication.
	- **Polling:** We use the `poll()` system call to monitor multiple sockets, allowing our server to handle multiple clients concurrently. This ensures that we can accept new connections while processing messages from existing clients.
	- **Client Handling:** We efficiently manage client connections, disconnections, and activity, ensuring the server maintains proper communication with each user.

2. **User Management** (`/srcs/user/`)
	- **User Representation:** Each connected client is represented as a `User` object. These objects store attributes such as the client’s file descriptor, nickname, username, and registration status.
	- **User Services:** We provide functions to manage users, such as adding new users, removing disconnected users, and updating user information. Additionally, user commands like `NICK` and `USER` are handled to allow for proper registration and nickname changes.

3. **Channel Management** (`/srcs/channel/`)
	- **Channel Creation and Management:** Channels are the core chatrooms in IRC. Our server allows users to create, join, and leave channels. Channels are managed by the `Channel` class, which keeps track of members, channel topics, and permissions.
	- **Operators and Privileges:** Channels support operator privileges, allowing certain users to moderate the channel. Operators can set channel modes, kick users, and manage invitations for invite-only channels.

4. **Command Processing** (`/srcs/messages/`)
	- **Message Parsing:** The server parses and processes incoming commands from clients. Supported commands include:

		- `JOIN`: Users can join a specific channel.
		- `PART`: Users can leave a channel.
		- `PRIVMSG`: Users can send private messages to other users or to channels.
		- `KICK`: Operators can remove users from a channel.

	- **Command Execution:** Each command is parsed and validated to ensure that the user has sufficient permissions and that the target (e.g., user or channel) exists.

5. **Error Handling** (`/srcs/exceptions/`)
	- **Custom Error Messages:** We provide clear error messages to users when commands fail, whether due to insufficient permissions, invalid channels, or incorrect usage of commands. This ensures users have a smooth experience and understand why certain operations may fail.


## Project Structure
- `Channel/`: Implements the creation and management of chat channels.
- `Messages/`: Handles the processing of IRC commands, ensuring proper syntax and permissions.
- `Network/`: Contains functions related to network setup, socket management, and client communication.
- `User/`: Manages user-related functionality, including registration, nickname handling, and private messaging.

## How to Use

1. **Compile the Server**
	- To compile the project, we run the following command in the root directory:
	```bash
	make
	```

2. **Running the Server**
	- To start the server, we need to provide the port number and an optional password:
	```bash
	./ircserv <port> <password>
	```

3. **Connecting to the Server**
	- Once the server is running, we can connect using an IRC client like `irssi` or even `netcat` for basic testing.

	**Using** `netcat`:
	```bash
	nc localhost <port>
	```

	**Using** `irssi`:
	```bash
	irssi -c localhost -p <port> -w <password>
	```

 	or run the following commands:
	```bash
 	irssi
 	```

 	then within the irssi CLI:
	```bash
	/connect localhost <port> <password (if required)>
 	```

5. **Registering on the Server**
	- To register, we use the `NICK` command:
	```bash
	/nick <nickname>
	```

6. **Using IRC Commands**
	- **Join a Channel:**
	```
	/join #<channel_name>
	```

	- **Send a Message to a Channel:**
	```
	/msg #<channel_name> <message>
	```

	- **Send a Private Message to a User:**
	```
	/msg <nickname> <message>
	```

## Conclusion

The IRC project allowed us to build a fully functional IRC server where users can connect, chat, and manage channels in real-time. We explored critical concepts in network programming, client-server communication, and concurrency, creating a scalable and efficient messaging platform.

## Authors

Group project developed by [Myriam K.](https://github.com/mkerkeni42), [Yani K.](https://github.com/ykifadji) and myself, [Emin A.](https://github.com/emayia) as part of the École 42 curriculum.

Special thanks to my teammates for their amazing participation and implication during the whole duration of the project!
