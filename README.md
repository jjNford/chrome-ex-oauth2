Chrome Extension OAuth2 Library
===============================
Provides a simple way to retrieve an OAuth2 token for API authorization within a Google Chrome Extension.


How To Use
----------
1. Add the following to your extension manifest:

	Note: The `permissions` url and `content_script` > `matches` URL are determined by the API you are requesting authorization for.
	
	```text
	{
		...
		...
		
		"permissions":{
			"https://github.com/login/oauth/access_token",
			"tabs"
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
