Custom Fields
=============

Use the custom fields API to define, rename, and delete custom fields on an account.

Get custom fields
-----------------

* `GET /subject_fields.xml` return all fields used in the account.

**Response:**

``` xml
<subject-fields type="array">
  <subject-field>
    <id type="integer"></id>
    <label></label>
  </subject-field>
  ...
</subject-fields>
```

Create custom field
-------------------

* `POST /subject_fields.xml` defines a new custom field on the account.

**Request:**

``` xml
<subject-field><label>#{label}</label></subject-field>
```

**Response:**

    Status: 201 Created
    Location: /subject_fields/#{new_id}.xml

    <subject-field>
      <id type="integer"></id>
      <label></label>
    </subject-field>


Update custom field
-------------------

* `PUT /subject_fields/#{id}.xml` rename a field on this account.

**Request:**

``` xml
<subject-field><id>#{id}</id><label>#{label}</label></subject-field>
```

**Response:**

    Status: 200 OK


Destroy custom field
--------------------

* `DELETE /subject_fields/#{id}.xml` removes a custom field from the account.

**Response:**

    Status: 200 OK
