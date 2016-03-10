Party & Deal Custom Fields
=============

Use the custom fields API to define, rename, and delete party and deal custom fields on an account.

For the full XML representation of custom fields, [check out the data reference](https://github.com/basecamp/highrise-api/blob/master/sections/data_reference.md#custom_field).


Get party custom fields
-----------------

* `GET /subject_fields.xml?type=party` return all fields used in the account.

**Response:**

``` xml
<subject-fields type="array">
  <subject-field>
    <id type="integer"></id>
    <label></label>
    <type>party</type>
  </subject-field>
  ...
</subject-fields>
```

Create party custom field
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
      <type>party</type>
    </subject-field>


Update party custom field
-------------------

* `PUT /subject_fields/#{id}.xml` renames a field on this account.

**Request:**

``` xml
<subject-field><id>#{id}</id><label>#{label}</label><type>party</type></subject-field>
```

**Response:**

    Status: 200 OK


Destroy party custom field
--------------------

* `DELETE /subject_fields/#{id}.xml` removes a party custom field from the account.

**Response:**

    Status: 200 OK


Get deal custom fields
-----------------

* `GET /subject_fields.xml?type=deal` return all deal fields used in the account.

**Response:**

``` xml
<subject-fields type="array">
  <subject-field>
    <id type="integer"></id>
    <label>Close Date</label>
    <type>deal</type>
  </subject-field>
  ...
</subject-fields>
```

GET /subject_fields.xml?type=deal


Create deal custom field
-------------------

At the moment, you cannot create deal custom fields via the API. Only retrieve, update, and destroy. 

Update deal custom field
-------------------

* `PUT /subject_fields/#{id}.xml` renames a field on this account.

**Request:**

``` xml
<subject-field><id>#{id}</id><label>#{label}</label></subject-field>
```

**Response:**

    Status: 200 OK


Destroy deal custom field
--------------------

* `DELETE /subject_fields/#{id}.xml` removes a deal custom field from the account.

**Response:**

    Status: 200 OK

Get all custom fields
-----------------

* `GET /subject_fields.xml?type=all` return all deal fields used in the account.

**Response:**

``` xml
<subject-fields type="array">
  <subject-field>
    <id type="integer"></id>
    <label></label>
    <type>party or deal</type>
  </subject-field>
  ...
</subject-fields>
```

