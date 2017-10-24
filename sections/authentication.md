# How to authenticate requests made to the audioboom.com api

# API Authentication #

To make API calls that are marked as authenticated you will need to ensure your application has been authorized by a user. Authenticated calls will typically access or publish data that is restricted to that particular user.

## OAuth Scheme ##
The API supports the OAuth standard to make authenticated calls on behalf of a user. To find out more about the OAuth specification and to find a library that implements it in your language, see http://oauth.net/.

You should use OAuth 2.0 to make your requests.  You might like to examine our [example Ruby code](https://github.com/audioBoom/audioboo-ruby-oauth) to see how things are supposed to work.

We support the 'Authorization Code' flow which is described nicely in [this article](https://aaronparecki.com/2012/07/29/2/oauth2-simplified#authorization)

## Consumer Keys ##
To make authenticated requests you'll need to get hold of a consumer-token key and secret. These are long seemingly random strings that ensure we can identify your application when it makes calls.

To register for key and token, head over to https://audioboom.com/account/services and click "Request new API Key". This will ask for some information regarding the application you're writing and, once submitted, should provide you with the token key and secret.

## OAuth Request URLs ##
When configuring your OAuth library, you will require URLs to access the OAuth calls. As we use standard paths, most libraries should just request the site's base address, which is `https://api.audioboom.com/`

For completeness, the two specific OAuth URLs are;

* Authorization URL: `https://api.audioboom.com/oauth/authorize` (GET)

* Access Token URL: `https://api.audioboom.com/oauth/token` (POST)
