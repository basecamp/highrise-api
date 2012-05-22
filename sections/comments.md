Comments
========

For the full XML representation of comments, [check out the data reference](https://github.com/37signals/highrise-api/blob/master/sections/data_reference.md#comment).

Get comment
-----------

* `GET /comments/#{id}.xml` returns a single comment.

The tag `parent-id` holds the id of the note or email this is associated with.

**Response:**

``` xml
<comment>
  <id type="integer">1</id>
  <parent-id type="integer">3</parent-id>
  <author-id type="integer">3</author-id>
  <created-at type="datetime">2006-05-19T20:26:00Z</created-at>
  <body>I agree, taxes are no fun</body>
</comment>
```


Get comments
------------

* `GET /notes/#{note-id}/comments.xml` returns a collection of comments that are visible to the authenticated user associated with the note specified in the URL.
* `GET /emails/#{email-id}/comments.xml` returns a collection of comments that are visible to the authenticated user associated with the email specified in the URL.

**Response:**

``` xml
<comments>
  <comment>
    ...
  </comment>
  <comment>
    ...
  </comment>
</comments>
```


Create comment
--------------

* `POST /comments.xml` creates a new comment with the currently authenticated user as the author.

The XML for the new comment is returned on a successful request with the timestamps recorded and ids for the contact data associated.

The `parent-id` holds the id of the note or email that this comment relates to.

**Request:**

``` xml
<comment>
  <body>I think that's exactly right!</body>
  <parent-id>1</parent-id>
</comment>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/comments/#{new-comment-id}.xml

    <comment>
      ...
    </comment>


Update comment
--------------

* `PUT /comments/#{id}.xml` updates an existing comment with new details from the submitted XML.

**Request:**

``` xml
<comment>
  <body>Allow me to rephrase.</body>
</comment>
```

**Response:**

    Status: 200 OK


Destroy comment
---------------

* `DELETE /comments/#{id}.xml` destroys the comment at the referenced URL.

**Response:**

    Status: 200 OK
