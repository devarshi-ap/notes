---
description: Intro to WSD
---

# Week 1

`Internet` - a world-wide network of computer network

`TCP/IP` (Transmission Control Protocol/Internet Protocol) - communication protocols used to interconnect network devices on the internet.

* every node has a unique numeric address (32bit on IPv4, 128bit on IPv6)

`FQDN` (Fully Qualified Domain Name) - complete domain name for an internet node (ie. _cbc.ca_)

`DNS` (Domain Name System) - phonebook of the internet; servers that connect web browsers with websites by converting FQDN --> IP addresses

Web Browser (Clients) request && Web Servers (Server) respond.

* Most client requests use HTTP/HTTPS

`HTTP/HTTPS` (_HyperText Transfer Protocol_) - set of rules for transferring files over the web. REQ/RES protocol between clients/servers.

* When a user opens a browser, they're indirectly using HTTP

`Web Server` - background OS process which monitors a communications port on the host, accepting HTTP/HTTPS messages when they appear.

* two main directories: _**Document root (servable docs)**_ & _**Server root (server system software)**_

**URL Paths Syntax**

* `protocol` + `domain` + `port` +`document`
  * ex. `https://` + `espn.ca` + `:443` + `/index.html`
  * (port 443 default for https; port 80 default for http)

`MIME Types` (Multi-purpose Internet Mail Extensions) - Used to specify to the browser the form of a file returned by the server (attached by the server to the beginning of the document).

* `type/subtype` - ie. text/plain, text/html, image/gif, image/jpeg, ...
* Server gets the type from the requested file name’s suffix based on the configuration file (.html implies text/html)

Web programming can be either:

* `Client-side` (front-end) : runs on client machine (browser) dealing w/ UI
  * ie. HTML, CSS, JS, JQUERY, VBSCRIPT, XML, RSS, SVG
  * frameworks: React, Angular, Bootstrap
* `Server-side` (back-end) : runs on server dealing w/ generation of web page content
  * ie. Perl, PHP, ASP, Java Servlets, JSP, TCL, Python, Ruby
  * frameworks: Flask, .NET, Laravel

#### Client-Side Frontend

**HTML**

> HyperText Markup Language.
>
> Skeleton of websites (defines structure)
>
> Written in form of

**CSS**

> Cascading Style Sheets.
>
> Styling of websites (making it look good).
>
> Stylesheets = list of css-rules consisting of selector(s) and their styles

**SVG**

> Scalable Vector Graphics.
>
> XML-based vector image format for 2D graphics.
>
> SVG images can be scaled in size without loss of quality.
>
> SVG files can be created and edited with text editors or VG editors

**JavaScript**

> Dynamic, weakly-typed, prototype-based scripting language

#### Server-Side Backend

**Perl**

> Dynamic, weakly-typed, high-level general-purpose language with powerful regex & string parsing abilities.

**PHP**

> Server-side Scripting language embedded in HTML
>
> Used to manage dynamic content, DBs, session tracking, and more.

**ASP**

> Active Server Pages (aka _Classic ASP_) != ASP.NET
>
> Most ASP pages are written in VBScript

**JSP/Servlets**

> Jakarta Server Pages
>
> Similar to PHP & ASP but use Java
>
> High-level abstraction of Java servlets
>
> JSPs are translated into servlets at runtime, therefore JSP is a Servlet

**Python**

> Interpreted, object-oriented scripting language
>
> Python web.dev. is usually done w/ a Python-based framework (ie. Django, Flask), but it can be done stand-alone with CGI protocol.

**TCL**

> Tool Command Language
>
> High-level, quicker to program but slower to execute scripting language generally used in conjunction with the Tk GUI library for building quick & easy X windows GUIs on Unix platforms

**Ruby**

> dynamic, reflective, general purpose object-oriented language
>
> Combines syntax inspired by Perl w/ Smalltalk-like features.
>
> Supports many programming paradigms (functional, OOP, imperative, reflection).
>
> Dynamic type system & automatic memory management, making it similar to Python/Perl.
>
> Ruby web.dev. is usually done w/ the Ruby-on-Rails framework, but it can be done stand-alone with CGI protocol.

**HTTP** - HyperText Transfer Protocol

Upon receiveing a REQUEST string, the server can send back:

* RESPONSE string (ie. "200 OK")
* \[personalized message]
* \[body] (requested file(s))
* \[error message]
* or some other info

HTTP Codes:

* `1xx` : Informational
* `2xx` : Success
* `3xx` : Redirection
* `4xx` : Client Error
* `5xx` : Server Error

**HTTPS** - HyperText Transfer Protocol Secure

Allows transferring the data in an encrypted form for security.

**Transport Layer Security** (Secure Sockets Layer aka **SSL**)

* encryption protocol used by HTTPS.
* uses _asymmetric public key infrastructure_ and it uses 2 different keys:
  * Private Key : available on web server, managed by website owner.
  * Public Key : available to everyone, converts data into encrypted form

**HTTPS is slower than HTTP because of the additional SSL layer.**

**Security issues for Client-Server architecture**:

* `Privacy` : comm. must not be intercepted
* `Integrity` : content must not be modified
* `Auth` : identity must be confirmed
* `Non-repudiation` : comm. must be legallly proved as being taken place

**Encryption**

* Basic tool to support privacy and integrity
* Everyone uses your **public key** to encrypt messages sent to you. You _decrypt_ them with your **matching private key**.
* It works because it's impossible to compute the private key from a given public key.

**RSA Encryption Algorithm**

> Rivest-Shamir-Adleman : public-key cryptosystem widely used for SSL.

> ie. A client (browser) sends its _public key_ to the server and REQ some data. The server encrypts the data using the client’s _public key_ and sends the _encrypted data_. The client receives the data and decrypts it using the their _private key_. Since it's asymmetric, nobody else except the client browser can decrypt the data.
