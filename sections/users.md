Users
=====

For the full XML representation of users, [check out the data reference](https://github.com/basecamp/highrise-api/blob/master/sections/data_reference.md#user).


Get myself
----------

* `GET /me.xml` returns information about the currently authenticated user.

This endpoint may be requested using a username and password, rather than the API token. This allows applications to obtain the token from those credentials, rather than requiring their users to enter an obscure API token by hand.

**Response:**

``` xml
<user>
  <id type="integer">1</id>
  <name>John Doe</name>
  <email-address>john.doe@example.com</email-address>
  <token>#{api_token}</token>
  <dropbox>#{dropbox_email_address}</dropbox>
  <created-at type="datetime">2007-04-23T20:25:29Z</created-at>
  <updated-at type="datetime">2007-04-23T20:25:29Z</updated-at>
</user>
```


Get user
--------

* `GET /users/#{id}.xml` returns a single user.

**Response:**

``` xml
<user>
  <id type="integer">1</id>
  <name>John Doe</name>
  <email-address>john.doe@example.com</email-address>
  <created-at type="datetime">2007-04-23T20:25:29Z</created-at>
  <updated-at type="datetime">2007-04-23T20:25:29Z</updated-at>
</user>
```


Get users
---------

* `GET /users.xml` returns a collection of users.

**Response:**

``` xml
<users>
  <user>
    ...
  </user>
  <user>
    ...
  </user>
</users>
```
