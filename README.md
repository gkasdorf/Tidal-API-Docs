# Tidal API Docs
This is a collection of information on the Tidal API. It is NOT complete, and there are numerous endpoints that are not provided here. However, the point of this repo is to give you an idea of how to interact with the Tidal API.

## Authorization
Please review the `Authorization` section for information about authorization. In short, you will need to do one of the following:

- Manually retrieve your `access_token` and `refresh_token` from the [Tidal Web Player](https://listen.tidal.com)
- Intercept the authorization code during the OAuth authorization code flow.

Both methods will be described. You will only need to do the latter if you are attempting to retrieve credentials for *other users*. If you are only using the Tidal API for your own purposes (i.e. retrieving song data) you will just need to manually retrieve the tokens.

## Limitations
The primary limitation is in retrieving *other users* tokens. It is possible, however, you will likely need to modify your approach.

OAuth - when using a public API like Spotify's for example - will redirect back to *your own server or application* with the required authorization code which you can then use to retrieve your `access_token`. However, because we cannot manipulate Tidal into redirecting to our own URI, we will need to allow Tidal to act as if it is authorizing for it's own application.

This will be explained in full under the `Authorization` section, however, note that (to the best of my knowledge) there is not a way to do this without your own *non-web-based* application. This is because of the CORS restrictions put in place in modern web browsers. In my use case, I require users to initially authorize with Tidal by downloading the iOS app - using a `WebView` - that is available in conjunction with the web-based app. Once they have done this, then they can continue to use their Tidal account on either the web or iOS applications

## Finding endpoints on your own
If you want to find any endpoints on your own, you will need to use [Fiddler]() or similar software to capture the requests being made to the Tidal API. You can do this fairly easily by setting up Fiddler to filter out requests made to Tidal's API, primarily `GET`, `POST`, and `PUT` requests. Then, you can simply use their own app and perform the actions that you are wanting to automate.

## Remember...
This is **NOT** a public API, and as such Tidal may implement changes to their API, to their authorization flow, or otherwise blacklist your account or IP address from accessing their service at all. **Use this at your own risk**.

Also know that Tidal is liable to change their `client_id` at any time, so you may need to modify this in the future. Ideally, your implementation will dynamically retrieve the `client_id` from Tidal before making any requests.

## Contribution
Please feel free to submit any pull requests for endpoints that you have used. Like I said, this is far from an exhaustive list. However, I wished to share the information for anyone who is looking to implement Tidal into their own application. Especially useful will be the OAuth authorization method that was used.
