OwinHttpMessageHandler
=

An implementation of [System.Net.Http.HttpMessageHandler] that translates an [HttpRequestMessage] into an [OWIN] compatible  environment dictionary, calls the supplied AppFunc and translates the result to an [HttpResponseMessage]. This allows you to call an OWIN application / component using [HttpClient] without actually hitting the network stack. Useful for testing and embedded scenarios.

Using
-
```csharp
Func<IDictionary<string, object>, Task> appFunc;
...
var httpClient = new HttpClient(new OwinHttpMessageHandler(appFunc));
```

By default, the OWIN enviroment is defined to look as though the source of the request is local. You can adjust the OWIN environment by passing in a closure:

```csharp
Func<IDictionary<string, object>, Task> appFunc;
...
var httpClient = new HttpClient(new OwinHttpMessageHandler(app, env =>
    {
        env[Constants.ServerRemoteIpAddressKey] ="10.1.1.1.";
    }));
```

Follow me [@randompunter]

  [System.Net.Http.HttpMessageHandler]: http://msdn.microsoft.com/en-us/library/system.net.http.httpmessagehandler.aspx
  [HttpRequestMessage]: http://msdn.microsoft.com/en-us/library/system.net.http.httprequestmessage.aspx
  [OWIN]: http://owin.org/
  [HttpResponseMessage]: http://msdn.microsoft.com/en-us/library/system.net.http.httpresponsemessage.aspx
  [HttpClient]: http://msdn.microsoft.com/en-us/library/system.net.http.httpclient.aspx
  [@randompunter]: http://twitter.com/randompunter