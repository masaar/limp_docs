[Back to Index](/README.md)

# Technical Sepcs
LIMP is using `aiohttp` Python framework. It handles both `HTTP/2 Websocket` and `HTTP/1 GET` connections and requests using two different separate functions both located in `limpd.py`. LIMP uses a group of techniques to:
* Although websocket is not about this, LIMP implements request-response calls over websocket. This allows developers to have more options when building their apps, while maintaining the advantages of websocket protocol, like preserving session info over the confection and faster messages transmission both ways.
* Instead of using submodule Git structure, LIMP repo ignores all folders in `modules` folder except `core` folder, making it possible to include unlimited number of LIMP packages and keep LIMP local repo up-to-date without touching your files.
* Auto load all LIMP packages and modules located in `modules` folder.
* Scaffold all modules attributes and methods and abstract them unto class methods and attributes.
* Set required attributes for cross-module communication.
* LIMP implements methods that require the client to generate authentication hashes to make sure no passwords are being transmitted in an insecure way. This results in the users password being unrecoverable if lost.
* LIMP implements JWT for data transfer between both sides in order to add a layer of security. By default, all calls to and from LIMP are tokenised using `JWT` or `JSON Web Token` standard. Once a connection is established with LIMPd, a connection-specific session attribute is set in the loop handling the connection. By default, it uses the anonymous session to handle all the calls, thus requiring all the calls to be signed using `ANON_TOKEN` session token.