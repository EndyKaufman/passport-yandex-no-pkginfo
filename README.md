# Passport-Yandex

[Passport](http://passportjs.org/) strategy for authenticating with [Yandex](http://yandex.ru/)
using the OAuth 2.0 API.

This module lets you authenticate using Yandex in your Node.js applications.
By plugging into Passport, Yandex authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Installation

    $ npm install passport-yandex-no-pkginfo

## Usage

#### Configure Strategy

The Yandex authentication strategy authenticates users using a Yandex
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

    passport.use(new YandexStrategy({
        clientID: YANDEX_CLIENT_ID,
        clientSecret: YANDEX_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/yandex/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ yandexId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'yandex'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/yandex',
      passport.authenticate('yandex'),
      function(req, res){
        // The request will be redirected to Yandex for authentication, so
        // this function will not be called.
      });

    app.get('/auth/yandex/callback', 
      passport.authenticate('yandex', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Examples

For a complete, working example, refer to the [login example](https://github.com/endykaufman/passport-yandex-no-pkginfo/tree/master/examples/login).

## Tests

    $ npm install --dev
    $ make test

[![Build Status](https://secure.travis-ci.org/endykaufman/passport-yandex-no-pkginfo.png)](http://travis-ci.org/endykaufman/passport-yandex-no-pkginfo)

## Credits

  - [Sergey Sergeev](http://github.com/endykaufman)
  - [Jared Hanson](http://github.com/jaredhanson)

## License

(The MIT License)

Copyright (c) 2012 Sergey Sergeev

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
