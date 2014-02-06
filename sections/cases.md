Cases
=====

Cases use `kase` and `kases` in the XML to work around the problem of `case` being a reserved word in Ruby.

For the full XML representation of cases, [check out the data reference](https://github.com/basecamp/highrise-api/blob/master/sections/data_reference.md#case).


Get case
--------

* `GET /kases/#{id}.xml` returns an existing case.

If `closed-at` is set, it means that the case is closed. If it’s not set, it’s still open. The `parties` field is a list of the people and companies involved with this case.

**Response:**

``` xml
<kase>
  <id type="integer">1</id>
  <author-id type="integer"></author-id>
  <closed-at type="datetime"></closed-at>
  <created-at type="datetime"></created-at>
  <updated-at type="datetime">2007-03-19T22:34:22Z</updated-at>
  <name>A very important matter</name>
  <visible-to>Everyone</visible-to>
  <group-id type="integer"></group-id>
  <owner-id type="integer"></owner-id>
  <parties type="array">
    <party>...</party>
  </parties>
</kase>
```


Get cases
---------

* `GET /kases/open.xml` returns a collection of cases that are visible to the authenticated user and have not been closed.
* `GET /kases/closed.xml` returns a collection of cases that are visible to the authenticated user and have been closed.

**Response:**

``` xml
<kases>
  <kase>
    ...
  </kase>
  <kase>
    ...
  </kase>
</kases>
```


Create case
-----------

* `POST /kases.xml` creates a new case with the currently authenticated user as the author.

By default, a new case is assumed to be visible to `Everyone`. You can also chose to make the company only visible to the creator using `Owner` as the value for the `visible-to` tag. Or `NamedGroup` and pass in a `group-id` tag too.

If the account doesn’t allow for more cases to be created, a `507 Insufficient Storage` response will be returned.

Adding parties to a case isn't supported at the moment.

**Request:**

``` xml
<kase>
  <name>Another very important matter</name>
</kase>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/kases/#{new-kase-id}.xml

    <kase>
      ...
    </kase>


Update case
-----------

* `PUT /kases/#{id}.xml` updates an existing case with new details from the submitted XML.

Contact data and Subject data that include an id will be updated, data that doesn’t will be assumed to be new and created from scratch.

A case is closed when the `closed-at` tag is passed.

Adding parties to a case isn't supported at the moment

**Request:**

``` xml
<kase>
  <name>Another very important matter</name>
  <closed-at type="datetime">2007-03-19T22:34:22Z</closed-at>
</kase>
```

**Response:**

    Status: 200 OK


Destroy case
------------

* `DELETE /kases/#{id}.xml` destroys the case at the referenced URL.

**Response:**

    Status: 200 OK
