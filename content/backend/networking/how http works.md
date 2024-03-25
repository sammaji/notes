source: https://cs.fyi/guide/http-in-depth

http -> tcp/ip based protocol.

http is a layer of abstraction on top of tcp protocol that standardizes how applications communicate across the web.

By default, tcp uses port 80 and the default port for http is 443.

## HTTP/0.9 

It was a simple protocol for receiving html only. You can only make a GET request. There were no headers.

Client requests content:
GET /index.html

Server responds back with the html content:
(response-body)
(connection closed)

## HTTP/1.0

- It could deal with HTML content as well as images, videos, plain text, etc.
- More methods were added -> POST, HEAD
- Headers could be send with request & response
- Status codes could be sent.
- Caching, content encoding, etc were introduced. 

Client request would look something like:
```
GET / HTTP/1.0
Host: cs.fyi
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5)
Accept: */*
```

> Clients could include their information using headers, which enabled many features like authorisation, caching, etc.

Server response would look something like:
```
HTTP/1.0 200 OK 
Content-Type: text/plain
Content-Length: 137582
Expires: Thu, 05 Dec 1997 16:00:00 GMT
Last-Modified: Wed, 5 August 1996 15:55:28 GMT
Server: Apache 0.84

(response body)
(connection closed)
```

One of the drawbacks of HTTP/1.0 was that you cannot have multiple request per connection, so if you have two html files and one image, it means three connections. This led to performance issues as tcp connections requires a three way handshake.

HTTP/1.0 is also stateless, meaning, the server doesn't keep any state. So the request must have all the information required for the server to process the data. Hence, there's a lot of redundancy.

### Three way handshake

A three way hand-shake happens between client and server before clients starts requesting content.

SYN -> client sends a random number (say X)

SYN ACK -> server sends a random number (say Y) (syn) and acknowledges the client's data by adding it by one (X+1) and returning both.

ACK -> client acknowledges server's data and returns Y+1 to the server.

This way, both client and server makes sure data transmission is working as expected.

[Three way handshake](https://i.imgur.com/ohZthqB.png)

## HTTP/1.1

- New methods were added -> PUT, PATCH, OPTIONS, DELETE
- Host header was optional in HTTP/1.0 but was made compulsory in HTTP/1.1
- Connections don't close until the header `Connection: close` was included in the request.
- Client could send multiple requests to the server without waiting for a response (pipelining). Server response included a `Content-Length` header which told the client where the one response ended.
- For dynamic content, server keeps sending chunks and kept adding the content length. Then, finally sends an empty response with `Content-Length` set to zero. In order to notify the client about the chunked transfer, server includes the header Transfer-Encoding: chunked.
- Included digest and proxy authentication.
- Caching, Character Sets, Language Negotiation, Client Cookies, etc.

## Latency & Bandwidth

Latency is the delay i.e. how long it takes for data to travel between the source and destination (measured in milliseconds)

Bandwidth is the amount of data transferred per second (bits per second).

## HTTP/2.0

- Sends binary data instead of textual data.
- Multiplexing - multiple asynchronous http requests over a single connection.
- Server Push - multiple responses for a single request.
- Header compression using HPACK.
- Request prioritisation and security.