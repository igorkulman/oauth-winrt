# oauth-winrt
A Windows Phone 8.1 / Windows 8.1 port of the OAuth Sample Library for C# from [oauth.googlecode.com](http://oauth.googlecode.com)

### Generating authorization headers

First, generate the authorization header value

````
/// <summary>
/// Generates OAuth 1.0 authentication header for given URL (including query parameters)
/// </summary>
/// <returns>OAuth header value</returns>
private string GetAuthHeaderValue(string requestUrl)
{
    var oa = new OAuthBase();
    string url;
    string ps;
    var timestamp = oa.GenerateTimeStamp();
    var nonce = oa.GenerateNonce();
    var signature = oa.GenerateSignature(new Uri(requestUrl, UriKind.Absolute), ConsumerKey, ConsumerSecret, null, null, "GET", timestamp, nonce, OAuthBase.SignatureTypes.HMACSHA1, out url, out ps);
    return string.Format("OAuth oauth_signature=\"{0}\", oauth_timestamp=\"{1}\", oauth_nonce=\"{2}\", oauth_consumer_key=\"{3}\", oauth_version=\"1.0\", oauth_signature_method=\"HMAC-SHA1\"", WebUtility.UrlEncode(signature), timestamp, nonce, ConsumerKey);
}
````

and then use it add is as a `Authorization` header to your request.
