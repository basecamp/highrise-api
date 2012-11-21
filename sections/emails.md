Emails
======

For the full XML representation of emails, [check out the data reference](https://github.com/37signals/highrise-api/blob/master/sections/data_reference.md#email).


Get email
---------

* `GET /emails/#{id}.xml` returns a single email.

Attachments are included, but comments are kept separate at `/emails/#{id}/comments.xml`.

**Response:**

``` xml
<email>
  <id type="integer">7</id>
  <title>Regarding the purchase</title>
  <body>It's very important</body>
  <author-id type="integer">3</author-id>
  <subject-id type="integer">1</subject-id>
  <subject-type>#{ Party || Deal || Kase }</subject-type>
  <subject-name>John Doe</subject-name>
  <collection-id type="integer">1</subject-id>
  <collection-type>#{ Deal || Kase }</subject-type>
  <visible-to>#{Everyone || Owner || NamedGroup}</visible-to>
  <owner-id type="integer">#{ user_id -- when visble-to is "Owner"}</owner-id>
  <group-id type="integer">#{ group_id -- when visble-to is "NamedGroup"}</group-id>
  <updated-at type="datetime">2007-02-27T18:42:28Z</updated-at>
  <created-at type="datetime">2006-05-16T17:26:00Z</created-at>
  <attachments>
    <attachment>
      <id type="integer">1</id>
      <url>https://example.highrisehq.com/files/1</url>
      <name>picture.png</name>
      <size type="integer">72633</name>
    </attachment>
    <attachment>
      <id type="integer">2</id>
      <url>https://example.highrisehq.com/files/2</url>
      <name>document.txt</name>
      <size type="integer">8837</name>
    </attachment>
  </attachments>
</email>
```


Get emails
----------

* `GET /#{ people || companies || kases || deals }/#{subject-id}/emails.xml` returns a collection of emails that are visible to the authenticated user and related to a specific person, company, case or deal.

* `GET /#{ people || companies || kases || deals }/#{subject-id}/emails.xmlsince=20070425154546` returns only the emails that have been updated since the time in the query parameter. The collection will be ordered from oldest to newest. The `since` parameter is expressed as `yyyymmddhhmmss` in the UTC timezone.

Emails are paginated using offsets. If 25 elements are returned (the page limit), use `?n=25` to fetch the next 25, and so on.

**Response:**

``` xml
<emails>
  <email>
    ...
  </email>
  <email>
    ...
  </email>
</emails>
```


Create email
------------

* `POST /emails.xml (or like: /people/#{person-id}/emails.xml)` creates a new email with the currently authenticated user as the author.

The subject of the email (who it belongs to) can either be set through the url or through the subject-type and subject-id tags. Using `/companies/5/emails.xml` as the target for the `POST` is the same as using `/emails.xml` with a `subject-type` of `Party` and a `subject-id` of `5`.

By default, a new email is assumed to be visible to `Everyone`. You can also chose to make the email only visible to the creator using `Owner` as the value for the `visible-to` tag. Or `NamedGroup` and pass in a `group-id` tag too.

Note: Adding attachments to a email is not yet supported.

**Request:**

``` xml
<email>
  <title>Regarding the purchase</title>
  <body>I just wanted to talk to you about the purchase.</body>
  <subject-id type="integer">4</subject-id>
  <subject-type>Party</subject-type>
</email>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/emails/#{new-email-id}.xml

    <email>
      ...
    </email>


Update email
------------

* `PUT /emails/#{id}.xml` updates an existing email with new details from the submitted XML.

**Request:**

``` xml
<email>
  <body>Hello world is now part of a case!</body>
  <subject-id>1</subject-id>
  <subject-type>#{ Party || Deal || Kase }</subject-type>
</email>
```

**Response:**

    Status: 200 OK


Destroy email
-------------

* `DELETE /emails/#{id}.xml` destroys the email at the referenced URL.

**Response:**

    Status: 200 OK
