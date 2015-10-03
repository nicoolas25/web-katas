# URL Shortener

The URL shortener creates a token from an URL. This token allows other users to
access the original URL passing through the shortner.

## Interface

**Creating a token**

* `POST /` with an `url` parameter
* Returns a HTTP response with code 201 and a body like:

``` javascript
{ "json": "<token>" }
```

**Consuming a token**

* `GET /<token>`
* Returns a HTTP response with code 302 and a `Location` header
* The `Location` is equal to the provided `url` while creating the token

**Getting statistics about a token**

* `GET /stats/<token>`
* Returns a HTTP response with code 200 and a body like:

``` javascript
{ "consumption_count": 42 }
```

More statistics could be added like:

* `consumer_count` that is the number of different IPs address that consumed the token
* `countries` that is a dictionary mapping country codes to  the unique consumer count for the country
* ...

In this kata, it will be okay to only have `consumption_count`.

## Other properties

- URL is not altered at all by the shortener
- Tokens are unique, even for the same URL
- Tokens can be consumed any number of times

