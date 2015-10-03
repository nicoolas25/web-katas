# TODO list

The program allows you to tracks things to do. It is single user intended.
Its purpose is to open one session a day in the morning, list the thing you
plan to do and stop working once they are done.

Sometime we work too much, this will help to keep reasonable goals and
avoid burnouts.

## Interface

**Starting a session**

* `POST /`
* Redirects (302) the client to a session path

**Displaying the session**

* `GET /<session_id>`
* Returns a HTTP response with code 200 and a body like:

``` javascript
{
  "tasks": [
    {
      "name": "Create the Todolist kata",
      "done": false
    },
    {
      "name": "Wake up happy",
      "done": true
    }
  ]
}
```

**Updating the tasklist**

* `PUT /<session_id>` with a JSON body that is the same as the previous one
* Returns a HTTP response with code 200 and the same body as the one

## Other properties

- Session path are unique

## Going further

This kata is quite easy for the back-end side. It is very close to a
key-value store.

On the other hand, the front-end can be more complex. Here are a few ideas
to explore:

* Allow reordering the tasks
* Automatically hide done tasks
* Handle gracefully an unavailable network when updating the tasks
