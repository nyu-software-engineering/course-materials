---
layout: presentation
title: App Authentication
permalink: /slides/authentication/
---

class: center, middle

# App Authentication

Dealing with user accounts.

---

# Agenda

1. [Overview](#overview)
1. [HTTP Basic Authentication](#http-auth)
1. [Sessions](#sessions)
1. [JSON Web Tokens](#jwt)
1. [OAuth](#oauth)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

---

template: overview

## Concept

Apps that allow users to create accounts must authenticate those users in some way. There are several common techniques for app authentication:

--

- HTTP Basic Authentication (not commonly used by apps, but exists)

--

- Session-based authentication

--

- JSON Web Token-based authentication

--

- Authentication using "Single Sign-On" services, such as Facebook, Google, etc.

---

name: http-auth

# HTTP Basic Authentication

--

## Concept

While HTTP is a stateless protocol, it does come with a native ability to handle passing authentication credentials between a client and server. This is known as **HTTP Basic Authentication**.

--

- When an incoming request attempts to access a protected resource, the server looks for an HTTP request header called `Authorization` containing **encoded credentials**.

--

- If not present, the server responds with a special HTTP response header, `WWW-Authenticate`.

--

- This triggers a web browser to automatically pop open a log-in form for the user.

--

- Once the user submits it, the browser sends an `Authorization` request header to the server with the user's credentials.

--

- If those credentials are correct, the server responds with the requested content.

---

template: http-auth

## UML sequence diagram

![HTTP Basic Authentication](../images/auth_http_sequence_diagram.png)

---

template: http-auth

## Considerations

HTTP Basic Authentication has some nice advantages:

--

- Natively supported and 'understood' by all web browsers and web servers.

--

- Log in form is automatically generated by browser.

--

- Easy to add manage user access on server side (e.g. managed in `.htaccess` and `.htpasswd` simple text files on Apache )

---

template: http-auth

## Considerations (continued)

HTTP Basic Authentication has some aspects that make it unsuitable for some common app use cases:

--

- Access control is managed by server settings files, while other app content is managed in in databases.

--

- Log in form is automatically generated by browser and cannot be designed to match app design.

--

- Developers have no control over the encoding and encryption - passwords are sent in simple `base64` encoding, which is easily decoded.

--

- Credentials must be passed with every request, increasing the attack window.

---

name: sessions

# Session Authentication

--

## Concept

Because all web browsers support cookies, it is possible for a web browser used by a logged-in user to identify itself to the server with every request by sending a unique ID along with every request. This is called a session cookie.

--

- When an incoming request attempts to access a protected resource, the server looks for an HTTP request header called `Cookie` containing a unique **session identifier**.

--

- If not present, the server doesn't return the requested resource, but rather sends back a log in page.

--

- The browser displays the log-in form to the user.

--

- Once the user submits it, the browser sends an `HTTP POST` request to the server with the user's credentials.

--

- If those credentials are correct, the server responds with the requested content and a `Set-Cookie` header containing a unique session id.

---

template: sessions

## UML sequence diagram

![Session Authentication](../images/auth_sessions_sequence_diagram.png)

---

template: sessions

## Considerations

Session authentication mechanisms have a few features that make them more suitable for web applications.

--

- Access control can be managed in the same databases used to manage other app content.

--

- Passwords need only be sent once to the server, reducing the password attack window.

--

- Browsers automatically store session IDs and send them automatically with every request to the server, requiring less custom code.

--

- Cookies automatically self-destruct at an expiration date set by the server, or the server can decide to invalidate the session id, immediately logging out the user, if desired.

---

template: sessions

## Considerations (continued)

Despite having several advantages over HTTP Basic Authentication for app developers, sessions have their limitations as well.

--

- Cookies require the server to validate the session by hitting the database with every request.

--

- Cookies are supported by web browsers, but not necessarily by other kinds of clients like native mobile apps, desktop apps, bots, and others.

--

- Sessions _require the server to maintain state_ of the session.... one more thing to worry about.

---

name: jwt

# JSON Web Token Authentication

--

## Concept

Today's apps often have multiple interfaces: web, native mobile app clients, desktop app clients, bots, etc, and monolithic servers are increasingly being replaced by cloud microservices. JSON Web Tokens are well-suited for this.

--

- When an incoming request attempts to access a protected resource, the server looks for an HTTP request header called `Authentication` containing a unique **token**.

--

- If not present, the server returns an `HTTP 401` response code indicating unauthorized access.

--

- The client logic asks the user for their credentials in any manner it deems appropriate.

--

- Once the user submits credentials, the browser sends an `HTTP POST` request to the server with the user's credentials.

--

- If those credentials are correct, the server responds with a **token**. The client stores this token in any way it chooses.

---

template: jwt

## UML sequence diagram

![JSON Web Token Authentication](../images/auth_jwt_sequence_diagram.png)

---

template: jwt

## Considerations

JSON Web Tokens (JWT) offer a few benefits over other authentication mechanisms.

--

- As with sessions, user passwords must only be sent once to the server, reducing the attack window.

--

- While the token itself is encoded but not encrypted, tokens can contain arbitraary _payload_ data that can be encrypted however developers desire, allowing for strong encryption of sensitive content.

--

- Tokens are _cryptographically signed_ by the server with a secret key. Once signed, the token can be easily validated by the server with every request. The token includes data about what access privileges the user should be granted. There is _no need to maintain any session data or state_ on the server. This also allows a single token to be used across multiple servers or microservices that don't share a credentials database.

--

- Tokens are most often stored in browsers' local storage, but can be stored in cookies or any client-side data storage for other kinds of apps.

---

template: jwt

## Considerations (continued)

As with any authentication scheme, there are limitations and concerns in regard to JWT as well.

--

- As with other credentials, tokens must be stored and transported securely.

--

- Since tokens are can be validated independent of any server state, they are more difficult to destroy than sessions.

--

- To be able to immediately invalidate a JWT token, the server must maintain the current state of each token in a server-side database of some kind. This defeats one of purported benefits of tokens not requiring the server to maintain session state.

---

name: oauth

# OAuth

--

## Concept

OAuth is an open standard for _delegated access control_ offered by many tech giants, such as Amazon, Google, Facebook, Microsoft, Twitter, etc.

--

- OAuth is most typically used to allow a 3rd-party application to access the protected resources related to a user's account with one of these tech services.

--

- For example, a university may offer students to sign into university systems using their Google account. Thus, the university's delegate account creation and validation to Google servers and Google's servers use OAuth to grant the university applications some access to the user's private data stored in their Google accounts.

--

- Whereas JWT is a token format - specifying what encryption is being used, what access the token grants, and including a cryptographic signature, JWT does not specify how to create and use these tokens. In contrast, OAuth is an entire protocol from start-to-finish specifying the steps a client and user must go through to gain access credentials to a protected resource and how these credentials must be passed back and forth.

---

template: oauth

## Considerations

In practical terms of developing application authentication systems, OAuth is more complex and multilayered than JSON Web Tokens. It provides some flexibiliy in implementation which leads to a wide variety of implementations.

--

- Covering OAuth in detail will require more dedication and example code than possible in a simple slide deck.

--

- You are encouraged to [read more about it](https://stackoverflow.com/questions/32964774/oauth-or-jwt-which-one-to-use-and-why/48333725#48333725).

--

- To simply implement sign-in to your applications using a tech giant's OAuth authentication system, there are many detailed code tutorials available that do not require you to master all the details of the protocol.

---

name: conclusions

# Conclusions

--

This has been a short survey of common authentication methods.

--

- The article, [Cookies vs. Tokens: The Definitive Guide](https://dzone.com/articles/cookies-vs-tokens-the-definitive-guide) provides a detailed comparison between the two.

--

- You are _recommended to use JSON Web Token-based authentication_ for your own apps, since it provides the most flexibility.

--

- The YouTube series, [API Authentication With Node](https://www.youtube.com/playlist?list=PLSpJkDDmpFZ7GowbJE-mvX09zY9zfYatI), by CodeWorkr, provides a very detailed code tutorial of sessions, JSON web tokens, and OAuth authentication code using Express, React, and MongoDB with mongoose. Highly recommended.

--

- [This example repository](https://github.com/nyu-software-engineering/data-storage-example-app) contains a full app (front-end and back-end) that includes code to do JWT authentication.

--

- Thank you. Bye.
