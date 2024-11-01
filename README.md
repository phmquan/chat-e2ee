## chat-e2ee
**Disposable chat session**: this app will allow two mutually agreed users to have a chat in _end-to-end_ encrypted environment. The app itself doesn't track you or ask for any information from you. Data is owned by **only you** and **only while chatting**. Your private key is generated on your device and never leaves your device. This is not a replacement for your usual chat application.  

The project is still in **development** phase and open for contribution.  
Demo: https://chat-e2ee-2.azurewebsites.net  

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/muke1908/chat-e2ee)

---
  

[![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=muke1908_chat-e2ee&metric=code_smells)](https://sonarcloud.io/project/issues?id=muke1908_chat-e2ee&resolved=false&types=CODE_SMELL)  [![](https://img.shields.io/github/issues/muke1908/chat-e2ee?style=flat)](https://github.com/muke1908/chat-e2ee/issues) 

## Features

1. :negative_squared_cross_mark: No login/signup - the end users **don't identify** themselves.
2. :closed_lock_with_key:	End-to-end encrypted Audio-Call  (Experimental - added on [19th September, 2024](https://github.com/muke1908/chat-e2ee/commit/efae545c4c378dd7cae3c133843c1d58fded8a56)).  
:warning: Note that Audio encryption in webrtc call is done diffrently, please refer [Wiki](https://github.com/muke1908/chat-e2ee/wiki/End%E2%80%90to%E2%80%90end-encryption-in-Webrtc-audio-call). It internally uses RTCRtpSender API: `createEncodedStreams` that has [limited Support](https://caniuse.com/mdn-api_rtcrtpsender_createencodedstreams)
4. :no_entry_sign: Data is **not** stored on any remote server, encrypted data is just relayed to other users, the data can't be decrypted by any man in the middle. **No history** i.e. once chat is closed the data is not recoverable, however encrypted data can be found on memory trace. [Read More](https://github.com/muke1908/chat-e2ee/wiki/How-and-when-your-data-can-be-compromised%3F)  

## :star: JS SDK 
[<img align="center" width="200" src="https://i.imgur.com/O3Wr6fK.png">](https://github.com/muke1908/chat-e2ee/tree/master/service)  

**Spin up your own frontend**: 
JS SDK and use chat-e2ee backend as service - `@chate2ee/service`  
[ :page_with_curl: Documentation](https://github.com/muke1908/chat-e2ee/tree/master/service)

This is a client-side SDK to interact with chat-e2ee service. It allows dev to build own chat client on top of chate2ee service. It uses socket.io for websocket connection and webrtc to facilitate 1-1 audio call.   


---

For installation instruction, go to [developer section](https://github.com/muke1908/chat-e2ee#computer-for-developers).  

### How to initiate chat

1. Generate a unique link.
2. Share the link or PIN with the person you want to chat with.
3. Start chatting.
4. The messages are end-to-end encrypted; therefore, no one can decrypt your message other than you.

**How the encryption works**

1. Alice and Bob generate a public and private key pair.
2. Alice and Bob share their public keys with each other.
3. Alice encrypts her message with Bob's public key and sends it to Bob.
4. Bob receives the encrypted message and decrypts it with his private key.

In this way, no one else can decrypt the message because your private key is never exposed/shared to the internet.
More detailed explanation: https://www.youtube.com/watch?v=GSIDS_lvRv4&t=1s

> We are using browser [window.crypto library](https://developer.mozilla.org/en-US/docs/Web/API/crypto_property)  for encryption.  

---

### Flow

![flow](https://i.imgur.com/2GrBQMz.jpg)

---

### :computer:	 For developers
![Open Source Love](https://img.shields.io/badge/Open%20Source-with%20love-CRIMSON.svg) ![GitHub last commit](https://img.shields.io/github/last-commit/muke1908/chat-e2ee) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=muke1908_chat-e2ee&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=muke1908_chat-e2ee) [![Gitter](https://badges.gitter.im/chat-e2ee/community.svg)](https://gitter.im/chat-e2ee/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

**Frontend (UI):**  
This project includes a light weight frontend UI - bootstrapped with [create-react-app](https://reactjs.org/docs/create-a-new-react-app.html). The FE client is located in `./client` folder.  

**Backend:**  
The backend runs on express/nodejs. In production mode, express server exposes the API endpoints and serves the static frontend from `./client/build`.   

**JS SDK:**  
`@chat-e2ee/service` - located in `./service` - A SDK that client uses to interact with backend. More info: [Readme](https://github.com/muke1908/chat-e2ee/tree/master/service)

**Custom frontend**  
Import `@chat-e2ee/service` SDK in your client project and build your own chat client.

### Installation

1. Fork this repository by clicking on the fork button on the top of this page. This will create a copy of this repository in your account.
2. Now clone the forked repository to your machine. 
3. Run `npm install` in root dir i.e. inside cloned repo.
4. Run `npm run dev` to spin up your client/server. This will run your react app in dev mode and server in watch mode by nodemon.

:exclamation::exclamation:**Important:**
If you are making changes to `./service` i.e. `@chat-e2ee/service`, make sure you run `npm run build-service-sdk` to reflect changes.

NOTE: by default, `create-react-app` runs webpack-dev-server on port `3000`. The server is configured to run on `3001` port. So, make sure that these ports are not blocked on your system.

**Important:**  
Check `.env.sample` to configure your `.env` file.  
Please use node 16 or above.   

To start with docker read the [instructions](https://github.com/muke1908/chat-e2ee/tree/master/docker).   
For native build read the [instructions](https://github.com/muke1908/chat-e2ee/tree/master/native).

### Folder structure

- The FE client is located in `./client` which is coupled with the backend.
- All the backend controllers go to `./backend` folder.
- Client uses a package `@chate2ee/service` to communicate with the backend. Located in `./service`.  
- Express instance is on `./app.js`.
- Entry point is `./index.js`.


Please follow the convention for the commit message.  
https://github.com/conventional-changelog/commitlint/#what-is-commitlint

Example:  
`git commit -m"feat: some relevant message"`

---
