OAuth2 for Chrome Extensions
============================
Provides a method to retrieve an OAuth2 token with no background page in a Google Chrome Extension.

Information about OAuth2 can be found [here](http://oauth.net/2/).

Why Use This Method
-------------------
The [Chrome API](http://code.google.com/chrome/extensions/tut_oauth.html) provides an example of how to use OAuth2 in an extension but you may find it very complicated or too in depth.  This is an easier way to achieve the same thing.

Another huge advantage is the fact that this method does not require a background page to be running Chrome.  This is something user love to hear, so using this method gives you some bragging rights for the Chrome Web Store!

This solution can also easily be tailored to fit your needs, from the OAuth2 methods availble to the look and feel of the adapter page (users will see this if they have a slower connection speed).

How To Use
----------
- The first thing you will need to do it merge your manifest with the oauth2-chrome-extesion manifest that declares a content script.
- Application information then must be filled into the specified areas of the oauth2.js and manifest files.
- The redirect URL you specify will have a script injected into, so most webpages will work but I would suggest using a webpage that is related to the provider you are requesting OAuth2 from and that is static (this way you are guaranteed to know that the page exists, and if the site is down then more than likely so is the provider).  A good redirect page is the providers robots.txt page.
- Starting the OAuth2 process is easy:

        myEventToTriggerAuthorization() {
            if((token = OAuth2.getToken()) === null) {
                OAuth2.begin();
            }
            else {
                console.log("My token is " + token);
            }
        }
        
- The user will then be prompted to authorize the extension with their account.  If accepted, the next time the extension is opened the getToken() method will return the token.

API
---
> **getToken()** <br/><br/>
`Returns OAuth2 token if available, false if not` <br/>

Gets the users OAuth2 token.

---

> **deleteToken()** <br/><br/>
`Returns true if a token was deleted from localStorage, false if not`

Deletes the users OAuth2 token (user will have to authenticate next time extension is used).

---

> **begin()** <br/>

Starts the OAuth2 process.

---

Notes
-----
This solution will not work out of the box for every API.  It was designed using the GitHub API v3 beta.  However the method that was used to get the OAuth2 token should work.  You may have to alter the source to fit your needs.  Methods can also be added to allow for OAuth2 refreshes and token expiration checks.

Please remember to contribute back to the project with any solutions you create!  Good Luck :P
