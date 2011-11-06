Reading Message Server (RMSN)
=============================
Built for and currently powering [Reading.am](http://reading.am).
Intended as a drop-in replacement for [Pusher](http://pusher.com),
specifically on [Heroku](http://www.heroku.com) but generally anywhere.
Kept afloat by [now.js](http://nowjs.com) on top of [node.js](http://nodejs.org).

Application Server
------------------
###Configuration Variables

* `REDIRECT_URL` - When this is set, all non-nowjs GET requests will be
  redirected to the specified URL
* `USE_SOCKETS` true (default) | false - Disables websockets when set to
  `false`. This is useful when deploying to platforms that decline to
  support sockets, such as Heroku

###Credentials
Credentials are set through environmental variables using the following
format:

    CRED_APPID_KEY=SECRET

For instance, an API credential for app `1234` with key `asdfjkl` and
secret `qwerty` would look like this:

    CRED_1234_asdfjkl=qwerty

You can set as many credentials as you like.

Client API
----------
###now.ready();
It's important to note that you'll probably need to wrap your code in a
`now.ready(function(){});` function call. If you're seeing errors like
`Object has no method 'subscribe'` it's because your code is being executed
before nowjs has had a chance to load. Only code that accesses RMSN
immediately on page load needs this wrapper.

Publisher APIs
--------------
###Ruby Gem
RMSN works with the standard [Pusher Gem](https://github.com/pusher/pusher-gem).
Simply install it as you would normally but when configuring, use the [URL
method](https://github.com/pusher/pusher-gem/blob/master/lib/pusher.rb#L50)
with this scheme:

    http://KEY:SECRET@example.com/apps/APP_ID

An example configuration in `config/environments/development.rb` of a
Rails application might look like this:

    Pusher.url = 'http://123qweasd1:098poilkj0@rmsn.example.com/apps/1234'

If you're using Heroku, make sure to remove the Pusher add-on, otherwise
your configuration will more than likely be overwritten upon deployment.

Deploying to Heroku
-------------------

* Create your Heroku app `heroku create --stack cedar`
* [Disable sockets](https://twitter.com/#!/NowJsTeam/status/115861105032708096) by adding `heroku config:add USE_SOCKETS=false`
* Setup your NODE_ENV variable for Express `heroku config:add NODE_ENV=production`
* Add a credential, ex. `heroku config:add CRED_1234_asdfjkl=qwerty`
  (explained in **Credentials** above)
* Push the code to master `git push heroku master`

Additional instructions for running Node.js applications on Heroku can
be [found here](http://devcenter.heroku.com/articles/node-js).

RMSN
----
RMSN, the acronym, is an homage to [Shipping News](http://www.shippingnews.org),
a seminal band from the birthplace of post-rock – Louisville KY.
You've been done a disservice by your friends and your family if this is
the first mention of Shipping News that you've come across,
especially here in the age of real time messaging systems.

Shipping News' [Kyle Crabtree](http://history.louisvillehardcore.com/index.php?title=Kyle_Crabtree) is one of the most tasteful and nuanced
drummers in music today. His timing is, surely, even better than that 
of the humble Reading Message Server; we strive to replicate his timing.
It's critical that you listen to Shipping News while implementing RMSN.
In fact, the entire thing hinges on it.

* [Save Everything](http://grooveshark.com/#/album/Save+Everything/649951)
* [Very Soon, and in Pleasant Company](http://grooveshark.com/#/album/Very+Soon+And+In+Pleasant+Company/459292)
* [Flies the Fields](http://grooveshark.com/#/album/Flies+The+Fields/248240)
* [One Less Heartless to Fear](http://shippingnews.bandcamp.com/album/one-less-heartless-to-fear)
