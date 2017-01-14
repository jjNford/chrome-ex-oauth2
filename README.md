<p align="center">
  <img src="https://whoisjuan.github.io/alt-images/chromeauth2.png" alt="ChromeAuth2: Chrome Extension OAuth2 Library"/>
</p>
===============================

ChromeAuth2 is Chrome Extension OAuth2 Library that provides a straight-forward and easy to use alternative to launch an OAuth2 Flows within a Chrome Extension.

By using ChromeAuth2 you would be able to start an authorization process from a Chrome Extension popup.html view and retrieve an OAuth2 token that can be later used from your popup.js or background.js scripts.


How To Use
----------
1. Add the following to your extension manifest:

	Note: The `permissions` url and `content_script` > `matches` URL are determined by the API you are requesting authorization for. We will be requesting permission to launch tabs and use the Chrome native storage.
	
	```text
	{
		...
		...
		
		"permissions":{
			"https://github.com/login/oauth/access_token",
			"tabs",
			"storage"
		},
		
		"content_scripts":[{
			"matches":["https://github.com/robots.txt*"],
			"js":["libs/chrome-ex-oauth2/injection.js"],
			"run_at":"document_start"
		}],
		
		...
		...
	}
	```
	
 Also make sure to give Web Accesible Resources permissions to your 'libs' folders. The extension would need explicit access to this folder after adding the library.

	```text
	{
	      "web_accessible_resources": [
    			"libs/*"
		  ]
	}
	```

2. Add application and API information to `libs/chrome-ex-auth/oauth2.js`:

	```javascript
		(function() {
			window.oauth2 = {
			
			access_token_url: "{your-access-token-url}",
			authorization_url: "{your-authorization-url}",
			client_id: "{your-client-id}",
			client_secret: "{your-client-secret}",
			redirect_url: "{your-redirect-url}",
			scopes: [{your-array-of-scopes}],
			
			...
			...
		
		})();			
			
	```

	***Note:*** The provided function is only a boiler-plate. The variable names and the variables you pass to the Authorization API would be specific to the API you are using. Some authorization APIs would require other parameters like  `scope` and `response-type`. 

	You would need to include those parameters in your initial variables and modify the 'start' function to include the newly added parameters.


3. Include the authorization script in your project:

	```html
	<html>
	...
	...
	<body>
		...
		...
		
		<script src="libs/chrome-ex-oauth/oauth2.js"></script>
		
		...
		...
	</body>
	</html>
	```

4. To authorize the application from your script:

	```javascript
	window.oauth2.start();
	```
	
5. Include attribution to library.

API
---

>**start()**
><br><br>
>Starts the authorization process.

<br>

>**getToken()**
><br><br>
>Retrieves the applications authorization token from the browsers local storage.

<br>

>**clearToken()**
><br><br>
>Clears the applications token from the browsers local storage.

--
<sub>This library has only been tested with the [GitHub API v3](http://developer.github.com/v3/)</sub>
