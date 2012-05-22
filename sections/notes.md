Notes
=====

For the full XML representation of notes, [check out the data reference](https://github.com/37signals/highrise-api/blob/master/sections/data_reference.md#note).


Get note
--------

* `GET /notes/#{id}.xml` returns a single note.

Attachments are included, but comments are kept separate at `/notes/#{id}/comments.xml`.

**Response:**

``` xml
<note>
  <id type="integer">7</id>
  <body>Hello world!</body>
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
</note>
```


Get notes
---------

* `GET /#{ people || companies || kases || deals }/#{subject-id}/notes.xml` returns a collection of notes that are visible to the authenticated user and related to a specific person, company, case or deal.

The list is paginated using offsets. If 25 elements are returned (the page limit), use `?n=25` to fetch the next 25 and so on.

**Response:**

``` xml
<notes>
  <note>
    ...
  </note>
  <note>
    ...
  </note>
</notes>
```


Create note
-----------

* `POST /notes.xml (or like: /people/#{person-id}/notes.xml)` creates a new note with the currently authenticated user as the author.

The XML for the new note is returned on a successful request with the timestamps recorded and ids for the contact data associated.

The subject of the note (who it belongs to) can either be set through the url or through the subject-type and subject-id tags. Using `/companies/5/notes.xml` as the target for the POST is the same as using /notes.xml with subject-type `Party` and subject-id `5`.

By default, a new note is assumed to be visible to `Everyone`. You can also chose to make the note only visible to the creator using `Owner` as the value for the `visible-to` tag. Or `NamedGroup` and pass in a `group-id` tag too.

Note: Adding attachments to a note is not yet supported.

As always, the URL for the newly-created note is passed back in the `Location` header.

**Request:**

``` xml
<note>
  <body>Hello world!</body>
  <subject-id type="integer">4</subject-id>
  <subject-type>Party</subject-type>
</note>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/notes/#{new-note-id}.xml

    <note>
      ...
    </note>


Update note
-----------

* `PUT /notes/#{id}.xml` updates an existing note with new details from the submitted XML.

**Request:**

``` xml
<note>
  <body>Hello world is now part of a case!</body>
  <subject-id>1</subject-id>
  <subject-type>#{ Party || Deal || Kase }</subject-type>
</note>
```

**Response:**

    Status: 200 OK


Destroy note
------------

* `DELETE /notes/#{id}.xml` destroys the note at the referenced URL.

**Response:**

    Status: 200 OK
