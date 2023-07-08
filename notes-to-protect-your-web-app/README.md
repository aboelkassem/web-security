# Notes to protect your web app and your API
## Web Application
- Don’t use Google DNS in your internal company
- Always protect your cookies with httpOnly flag
- Make your web server allow only need http methods (get, post, put)
    - Prevent dangerous methods like TRACE which enable you to copy request headers to the response (which if the user has XSS can steal your cookies even with httpOnly flag)
- When trying to access unauthorized resources, force user to redirect to login with Status code 301 not 302
- Don’t ever trust user input including html inputs (get or post) or http get query parameters
- Don’t make validations only on client side (Javascript)
- Don’t store sensitive data into hidden inputs
- Disable WebDav
- When use regx to match a pattern from input user, make sure of case sensitivity
- Prevent/Mitigate XSS attacks
    - Add x-xss-protection header in the response either in app code or web server (supported on all browser except firefox so its not recommended)
    - Add content-security-policy (CSP) response header
    - Filter user input either in backend by the framework like **`htmlspecialchars`** in php which make encoding/escaping to the special characters
    - Make cookies with secure(means over https) and httpOnly (cannot be used by js code) flags
- **Same Origin Policy (SOP)** requires the source host to be the same protocol, hostname and port in order to read responses from other hostname.
- **Cross Origin Resource Sharing (CORS)** specifies which hostnames able to talk/send requests to our host.
- **Content Security Policy (CSP)** specifies which hostnames able to run js (script-src), css (style-src) files or media like images, frames, videos, audios
- **WAF** (Web application firewall)
    - Is a firewall on the web server to handle incoming requests from browser and do some checks to validate the request and then forward it to the web server if valid
    - Very important for attacks like logical bugs and IDORs    
    - **Learning mode**: WAF will learn how your web app works in a normal way (what Get query parameters accepts and its datatype or POST data you entered)
    - **Passive mode**: monitor each input with logs but without taking any action
    - **Active mode**: monitor each input with logs with taking action
- To prevent CSRF attack, add referrer header and validate it, also validate the token and make variable not static
- https://portswigger.net/web-security/authentication/securing
- https://roadmap.sh/best-practices/api-security
- https://cheatsheetseries.owasp.org/cheatsheets/DotNet_Security_Cheat_Sheet.html

## API Checklist
- [ ]  Add SSL/TLS for any channel communication
- [ ]  Add API key authentication to know which client are able to access your api
    - [ ]  For better management like rate limit and quotas
- [ ]  Use JWE or JWS instead of JWT if you have sensitive data in the payload or if you log the token
- [ ]  [optional] add Mutual TLS (MTLS) for more security to enable the server and client know the each other while communicating
- [ ]  Check the expirations dates for all SSL/TLS certificates
- [ ]  https://github.com/shieldfy/API-Security-Checklist
