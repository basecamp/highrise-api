Account
=======

The account API is currently just for reading, not writing. Any authenticated user has access.

Get account
-----------

* `GET /account.xml` returns info about the current user’s Highrise account.

This endpoint includes:

* account id, subdomain, and name
* plan name (max, plus, solo, etc.)
* account owner’s `user_id`
* total number of people (not companies) on the account
* total space used in bytes
* color theme name (see `/stylesheets/color/#{name}.css`)
* whether SSL is enabled
* creation and last-update timestamps

**Response:**

``` xml
<account>
  <id type="integer">1</id>
  <name>Your Company</name>
  <subdomain>yourco</subdomain>
  <plan>premium</plan>
  <owner-id type="integer">#{user_id of account owner}</owner-id>
  <people-count type="integer">9412</people-count>
  <storage type="integer">17374444</storage>
  <color_theme>blue</color_theme>
  <ssl_enabled>true</ssl_enabled>
  <created-at type="datetime">2007-01-12T15:00:00Z</created-at>
  <updated-at type="datetime">2007-01-12T15:00:00Z</updated-at>
</account>
```
