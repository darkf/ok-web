**ok-web** is a platform for serving Web applications written in K.

This means that you can write Web services/applications in the [K programming language](https://en.wikipedia.org/wiki/K_(programming_language)), making use of the [oK interpreter](https://github.com/JohnEarnest/ok).

## Usage

Any `.k` files in the current working directory where `web.js` (the server) is invoked will be served.

For example, if you have `index.k`, then you may browse to `http://localhost:8080/index.k` to see the result.

The server serves on port 8080 by default, but this is changeable in `web.js`.

## API

All of oK's features are available, with some modifications:

Monadic `0:` reads from files on disk as usual.

Dyadic `0:` both writes to the response stream (given an empty symbol), and writes to files on disk (given a path name).

Examples:

    "foo.txt" 0: "Hi!" / write foo.txt
    0:"foo.txt" / read foo.txt
    `0:"Hello World!" / display Hello World! to the browser
    `0:0N / Send error code 500 (Internal Server Error) as a response

Some useful globals about the request are bound by default, including:

- `path` returns the path -- e.g. `/index.k`
- `host` is the `Host` HTTP header -- e.g. `localhost:8080`
- `query` returns a K dictionary containing either the decoded query string in the case of GET requests, or the decoded urlencoded POST data for POST requests.

For a more complete example of using this, see [kukai](https://github.com/darkf/kukai), a minimalistic pastebin written in K using ok-web.