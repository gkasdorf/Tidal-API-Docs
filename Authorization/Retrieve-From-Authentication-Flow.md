# Retrieving a user's Tidal `access_token` and `refresh_token` from the authentication flow
If you want to implement Tidal into your application in a way that interfaces with the end-user's Tidal account, you will need to retrieve their `access_token`. Depending on implementation, it may be ok to simply ask the user to retrieve these on their own by following [the instructions]() to do so. However, if you want to provide a good experience to the user, you likely don't want to do this.

Instead, you will need to create an implementation that will sign in the user to Tidal's web player and retrieve the `authorization_code` from the redirect in that process. Below we will explain the process.

In my own implementation, I used a `WebView` inside of a React-Native application. I will provide a few snippets of the process to give you an idea of what to do in your own application. I also use a PHP backend to retrieve the URL and to process the actual retrieving of the tokens, so some snippets will be provided of that as well. 

**NOTE:** Attempting to retrieve the URL from, say, a JavaScript `window` reference will not work as modern web browsers have built-in CORS protections. For this reason, you will need to actually create an application (whether mobile or desktop) that will present a web session that you have more control over.

## Step 1: Generating the `code_verifier` and `code_challenge`
You need to generate a PKCE token for the `code_verifier` then hash this token for `code_challenge`. There are plenty of examples online of how to do this, and there are various libraries depending on which language you are using. Here is a quick example in PHP.

```php
$verifier_bytes = random_bytes(64);
$codeVerifier = rtrim(strtr(base64_encode($verifier_bytes), "+/", "-_"), "=");

$challengeBytes = hash("sha256", $codeVerifier, true);
$codeChallenge = rtrim(strtr(base64_encode($challengeBytes), "+/", "-_"), "=");
```

Remember, you will need to access the `code_verifier` and `code_challenge` at different points in the authorization process. Be sure these will be accessible to you throughout the process.

## Step 2: Creating the URL
We will need to direct the client to `https://listen.tidal.com/login/auth` with the following GET parameters.

```
appMode = WEB
client_id = CzET4vdadNUFQ5JU - The Tidal client ID. This may change, and you will need to update it.
code_challenge = <Hash you generated>
code_challenge_method = S256
lang = en
redirect_uri = https://listen.tidal.com/login/auth
response_type = code
restrictSignup = true
scope = r_usr w_usr
autoredirect = true
```

## Step 3: Wait for redirect
Regardless of implementation, you will need to wait for the user to be redirected to `https://listen.tidal.com/login/auth`. Below is an example of how this was implemented using React-Native and the `react-native-webview` component.

```js
const stateChange = (e) => {
    // See if the URL is what we are looking for
    if(e.url.toString().includes("https://listen.tidal.com/login/auth")) {
        // Get the code from the URL
        const code = e.url.split("code=")[1].split("&state=")[0];

        // Handle the rest of auth.
    }
}

// Render the component
return (
    <WebViewIos
        source={{uri: url}} // The URL that we generated is presented to the user.
        onNavigationStateChange={stateChange}
    />
)
```

## Step 4: Retrieve the `access_token` and `refresh_token`
You need to make a `POST` request to `https://login.tidal.com/oauth2/token` with the following parameters:

```text
client_id = CzET4vdadNUFQ5JU
code = <The authorization code we just retrieved>
code_verifier = <The code you generated earlier>
grant_type = authorization_code
redirect_uri = https://listen.tidal.com/login/auth
scope = r_usr w_usr
```

Once you make this request, as long as everything was done correctly, you will receive a JSON response. The response will contain all of the user data (email, name, username, etc.) as well as the `access_token`, `refresh_token`, and the `expires_in`. The expiration will occur 24 hours after the token has been generated. As we will explain, you should always check that the current time has not exceeded 24 hours from the time of authorization. If it has, you should refresh the token.
