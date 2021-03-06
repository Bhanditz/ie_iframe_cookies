Rails: Enabled cookies inside IFrames for IE via P3P headers.<br/>

# Deprecated / Unmaintained

use something like this instead:

```Ruby
class AllowCookiesInIframesMiddleware
  def initialize(app)
    @app = app
  end

  def call(env)
    response, headers, body = @app.call(env)
    headers['P3P'] = %{CP="NOI DSP COR NID ADMa OPTa OUR NOR"}
    [response, headers, body]
  end
end
```

# Old Readme

IFrames in IE only get the same cookies as normal pages when P3P headers are added<br/>
=> 'iframe-using' IE users get P3P headers on every request<br/>
304 Not modified pages do not get P3P headers (via ETag)<br/>
=> 'iframe-using' IE users do not get 304

Install
=======

```Bash
gem install ie_iframe_cookies
```

Usage
=====
To cookie-tag users as 'iframe-using', add this to all actions rendered inside IFrames.<br/>
(only IE users are tagged)

```Ruby
before_action :normal_cookies_for_ie_in_iframes! # only: [:foo, :bar]
```

TIPS
====
 - Problems with Safari? try [this](http://saizai.livejournal.com/897522.html) or [that](http://stackoverflow.com/questions/2691864/facebook-iframe-app-with-multiple-pages-in-safari-session-variables-not-persisti/2725790#2725790)

Authors
=======

### [Contributors](https://github.com/grosser/ie_iframe_cookies/contributors)
 - [Eric Harrison](https://github.com/fuelxc)

[Sascha Depold](https://github.com/sdepold)

[Michael Grosser](http://grosser.it)<br/>
michael@grosser.it<br/>
License: MIT<br/>
[![Build Status](https://travis-ci.org/grosser/ie_iframe_cookies.png)](https://travis-ci.org/grosser/ie_iframe_cookies)
