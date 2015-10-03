# Pomodoro timer

The program allows you to set a pomodoro timer and share it with your team
in order to be in sync, avoid interrupting each other and share breaks.

## Interface

**Starting a session**

* `POST /`
* Redirects (302) the user to a session path

**Displaying a session**

* `GET /<session_id>`
* Returns a HTTP response with code 200 and a body like:

``` javascript
{
  "now": 1443872224,
  "end_at": 1443873393
}
```

All the properties are timestamps (with second precision):

* `now` is the current server time and
* `end_at` is the time when the timer should end,
  it is `null` when no timer is running.

**Starting the timer**

* `POST /<session_id>`
* Returns the same thing as the `GET` method but with a `end_at` value

## Other properties

- Session path are unique
- The time for the timer is 20 minutes
- A client should see when a timer is started by another client

## Going further

**Customizable duration**

Maybe the 20 minutes timer isn't well suited for everybody.

A `POST /<session_id>?duration=1800` should create a timer for 30 minutes.

**Server Sent Event**

To notify the clients that the timer started, you can use Server Sent Events.
Maybe you already did that ;-)

In this case, the `GET /<session_id>` response will be an stream of `timer-started`
events with a `data` string like the response we've seen (JSON).

All the clients connected to the `/<session_id>` will get the events.

**Resources cleanup**

After 10 minutes without any timer running, session's resources can be discarded,
those resource can be memory, database records or anything you allocated for your
session.
