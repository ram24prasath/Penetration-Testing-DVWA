# Client Side Request Forgery

CSRF is an attack that forces an end user to execute unwanted actions on the web application in which they are currently authenticated.

CSRF requires a bit of social engineering, to trick the user of the application to perform or execute malicious activities.

## Description:

CSRF is an attack that tricks victim into submitting a malicious request, it inherits the identity and privileges of the victim to perform undesired 
actions on the application on victim's behalf.

For most sites, browser's request automatically include   any credential associated with the site, such as user's session cookie, IP address,
windows domain credentials. Therefore if a user is authenticated to a site, the site will not have a way to distinguish between the forged request and
valid request coming from a user's browser.

CSRF attacks target functionality that causes a state change on the server, such as changing user's password or email address. Forcing the victim to 
retrieve the data from server to vivtim does not benefit the atatcker. So attacker can use CSRF attack to obtain victim's personal data via login
CSRF, 
