## Introduction

This is one of my favorite topics, and this would be a knowledge-heavy article. So read carefully.

**Domain Sharding**

- Domain sharding is a technique used to improve a website's speed and performance. 
- It involves splitting or "sharding" resources across multiple domains.  
- When a browser loads a website, it makes requests to the website's server to download different types of resources like HTML, CSS, JavaScript, images, etc.
- However, browsers limit the number of concurrent connections (downloads) they will make to a single domain. (6, depending on Browser)
- By sharding resources across multiple domains (for example, serving images from a different domain than scripts), you can bypass this limit and download more resources at the same time, which can lead to faster page load times.

**Multiplexing**
- which allows multiple requests and responses to be sent at the same time over a single connection (Default around 100)

**NOTE:-**

- However, it's important to note that **HTTP/2,** the latest version of the **HTTP protocol**, supports **multiplexing**, 



**How to adopt/change current protocol**

- To switch from HTTP/1 to HTTP/2, you need to configure your server to support HTTP/2.

- The exact steps depend on the server software you're using. Here are general steps for some common servers: 
 
**Apache:**

- Apache supports HTTP/2 from version 2.4.17 onwards. To enable it, you need to include the mod_http2 module in your Apache configuration and then add Protocols h2 http/1.1 to your configuration. 
 
**Nginx:**

- Nginx supports HTTP/2 from version 1.9.5 onwards. To enable it, include http2 in your listen directives in your Nginx configuration, like so: listen 443 ssl http2. 

**Node.js:** 

-If you're using Node.js, you can use the built-in http2 module to create an HTTP/2 server.
---

**NOTE:-**

Remember, HTTP/2 requires HTTPS in most browsers, so you'll also need to set up an SSL certificate for your server.

## 🔐 Python Server

### Option 1: Using `Hypercorn` with `Quart` (HTTP/2 support)

1. **Install dependencies**:
   ```bash
   pip install quart hypercorn
   ```

2. **Create a simple Quart app** (`app.py`):
   ```python
   from quart import Quart

   app = Quart(__name__)

   @app.route("/")
   async def hello():
       return "Hello over HTTP/2 with SSL!"

   if __name__ == "__main__":
       app.run()
   ```

3. **Run with SSL and HTTP/2**:
   ```bash
   hypercorn app:app --certfile cert.pem --keyfile key.pem --bind 0.0.0.0:443 --quic
   ```

   - `cert.pem` and `key.pem` are your SSL certificate and private key files.
   - `--quic` enables HTTP/3 as well, but HTTP/2 is supported by default.

---

## 🔐 Node.js Server (using `http2` module)

### Option 1: Native `http2` with SSL

1. **Generate SSL certificate** (for development):
   ```bash
   openssl req -x509 -newkey rsa:2048 -nodes -keyout key.pem -out cert.pem -days 365
   ```

2. **Create server** (`server.js`):
   ```javascript
   const http2 = require('http2');
   const fs = require('fs');

   const server = http2.createSecureServer({
     key: fs.readFileSync('key.pem'),
     cert: fs.readFileSync('cert.pem')
   });

   server.on('stream', (stream, headers) => {
     stream.respond({
       'content-type': 'text/html',
       ':status': 200
     });
     stream.end('<h1>Hello over HTTP/2 with SSL!</h1>');
   });

   server.listen(443);
   ```

3. **Run the server**:
   ```bash
   node server.js
   ```

---

## ✅ Notes

- For **production**, use certificates from **Let's Encrypt** or a trusted CA.
- Make sure your domain is properly configured to point to your server.
- HTTP/2 requires SSL/TLS in most browsers, so enabling HTTPS is essential.

**From Front-End perspective anything we do ?**

- No, the switch from HTTP/1 to HTTP/2 is handled at the server level, not at the client or front-end level.
- However, once your server supports HTTP/2, you might want to reconsider certain performance optimization techniques that are common with HTTP/1, such as domain sharding or asset concatenation, as they can be unnecessary or even detrimental with HTTP/2.

**How the connection Happening in Client and Server**

**HTTP/1**

- HTTP/1 operates on a single connection per request/response model. This means for each request from the client to the server, a separate TCP connection is established.

- If a web page requires multiple resources (like images, CSS, JavaScript files), multiple TCP connections need to be established. 

- This can lead to a problem known as "head-of-line blocking", where the loading of a resource can be blocked by the loading of a previous resource.

- HTTP/1 does not support server push, meaning the server can only send resources that the client has requested.

**HTTP/2**

- HTTP/2 introduces multiplexing, which allows multiple requests and responses to be sent at the same time over a single TCP connection. This effectively eliminates the head-of-line blocking problem.

- HTTP/2 also introduces server push, where the server can send resources to the client proactively before the client even asks for them. This can improve performance by reducing the need for round-trip requests between the client and server.

- HTTP/2 also supports header compression, which can reduce overhead and improve performance, especially for mobile users.

**HTTP/2 also supports header compression**

- HTTP/2 introduces a new feature called **Header Compression**, which reduces the overhead of HTTP headers. 

- In HTTP/1, headers are sent as plain text, which can be quite large and add significant overhead to each request and response.

- This is especially true for requests that include cookies or tokens in the headers.

- HTTP/2 uses a mechanism called **HPACK compression** to compress headers.

- HPACK is a simple and secure string compression scheme that reduces the size of headers, making HTTP/2 requests and responses faster and more efficient.

**HPACK compression works Internally**

- It by maintaining a list of previously sent header fields on both the client and server side, known as a **dynamic table**.

- When a header field is repeated in subsequent requests or responses, instead of sending the entire header field, an index referencing the entry in the dynamic table is sent.

- This significantly reduces the size of headers for requests and responses, especially when many headers are repeated across requests.

**HTTP/3**

- HTTP/3 is the next major version of the HTTP protocol. It's built on top of QUIC, a transport layer protocol **developed by Google**.

**Here are some of the advantages of HTTP/3 over HTTP/2:**

**Improved Speed:**

- HTTP/3 uses QUIC, which is designed to be faster and more reliable than TCP, the transport protocol used by HTTP/1 and HTTP/2.
- QUIC reduces connection establishment time, making the initial connection to a server faster.  

**Better Handling of Packet Loss:**

- In HTTP/2, a lost packet slows down all streams (requests/responses). QUIC solves this problem by handling streams independently, so a lost packet only affects a single stream.  

**Connection Migration:**

- QUIC supports connection migration, which means if a user changes their network (like switching from Wi-Fi to 4G), the existing connection can be kept alive and migrated to the new network.

- This is not possible with TCP, which is tied to the original IP address. 
 
**Encryption by Default:**

- QUIC includes TLS 1.3 encryption by default. This makes the protocol more secure and reduces the number of round trips required to set up a connection. 
 
**Server Push:**

- Like HTTP/2, HTTP/3 also supports server push, where the server can send resources to the client proactively, before the client even asks for them. 
 
**NOTE:-**

It's important to note that while HTTP/3 has several advantages, it's still not widely supported or used as of now.


![HTTP/3 Protocol Browser compatability](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/22s6cry9t8s9ipk0ht7s.png)


![HTTP/2 Protocol Browser compatability](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/e8cd73zxs2xajsqjyzuh.png)


Reference:-

1. https://frontendmasters.com/courses/realtime/
2. https://developer.mozilla.org/en-US/docs/Web/HTTP
3. https://developer.mozilla.org/en-US/docs/Glossary/HTTP_2
4. https://developer.mozilla.org/en-US/docs/Glossary/HTTP_3
