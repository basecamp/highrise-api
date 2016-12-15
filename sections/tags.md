Tags
====

The tags API allows you to add, update, and delete tags from parties (people and companies), cases, and deals. In the documentation below, the generic `#{subject_type}` text must be replaced in practice with either `people`, `companies`, `kases`, or `deals`, and `#{subject_id}` should be the id of the subject (person, company, case or deal) that you want to manipulate or query the tags for.

For the full XML representation of tags, [check out the data reference](https://github.com/basecamp/highrise-api/blob/master/sections/data_reference.md#tag).


Get tags
--------

* `GET /tags.xml` return all tags used in the account.
* `GET /#{subject_type}/#{subject_id}/tags.xml` returns the tags on a person, company, case, or deal.

**Response:**

``` xml
<tags type="array">
  <tag>
    <id type="integer"></id>
    <name></name>
  </tag>
  ...
</tags>
```


Get tagged parties
------------------

* `GET /tags/#{id}.xml` return all parties (people and companies) associated with a given tag.

This endpoint will not include deals and cases for that tag.

The list is paginated using offsets. If 500 elements are returned (the page limit), use ?n=500 (e.g. `GET /tags/#{id}.xml?n=500`) to check for the next 500 and so on.

**Response:**

``` xml
<parties type="array">
  <party type="Person">
    ...
  </party>
  <party type="Company">
  ...
</parties>
```


Create tag
----------

* `POST /#{subject_type}/#{subject_id}/tags.xml` adds a tag to a person, company, deal, or case.

**Request:**

``` xml
<name>#{name}</name>
```

**Response:**

    Status: 201 Created
    Location: /tags/#{new_id}.xml

    <tag>
      <id type="integer"></id>
      <name></name>
    </tag>


Destroy tag
-----------

* `DELETE /#{subject_type}/#{subject_id}/tags/#{id}.xml` removes a tag from a person, company, deal, or case.

**Response:**

    Status: 200 OK
