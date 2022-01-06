# Events with HTTP POST & SSE

Demo application for event driven communication in web applications.

## Overview

It is possible to send frontend events to backend using regular HTTP POST request (`fetch`) and to receive backend
events with `EventSource` ([Server Sent Events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events)):

![HTTP & SSE](./assets/http_sse.png)

This demo will send `tik` event from front to back on every `tok` event from back. Back, in turn, will send `tok` event
on every `tik` event received from front. Front starts sending when `EventSource` connection is opened:

![TIK & TOK](./assets/tik_tok.png)

This communication model can be used in mobile web
apps ([PWA](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)).

## Install

```shell
$ npm rebuild
```

## Run

Launch backend application (HTTP/1 server on port 8080) from `npm`:

```shell 
$ npm start // start backend application as HTTP/1 server on port 8080 with 'npm'
$ node ./bin/tequila.mjs web-server-start -1 -p 3000 // start as HTTP/1 server on port 3000
$ node ./bin/tequila.mjs web-server-start // start as HTTP/2 server on port 8080
```

## Usage

Start backend app then open URL http://localhost:8080/ in your browser. Front application will be loaded and connected
to backend app. After that front will send first `tik` event to back. Back will answer with `tok` event with random
delay (0.1-1 sec.). Front will get `tok` event from back then answer with `tik` event with the same random delay (0.1-1
sec.).

Open DevTools panel in browser and see logs in console. Server logs are flowed to standard output.

Front application will try to re-connect to back every 5 sec. in case of back application will be down or connection
will be lost.

You can open the same address in separate browsers, backend will serve all fronts with `tok` events. 
