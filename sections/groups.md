Groups
======

The authenticated user needs to be an administrator to perform these actions.

For the full XML representation of groups, [check out the data reference](https://github.com/basecamp/highrise-api/blob/master/sections/data_reference.md#group).


Get group
---------

* `GET /groups/#{id}.xml` returns a single group and the users associated with it.

**Response:**

``` xml
<group>
  <id type="integer">1</id>
  <name>Partners</name>
  <users>
    <user>
      ...
    </user>
    <user>
      ...
    </user>
  </users>
</group>
```

Get groups
----------

* `GET /groups.xml` returns a collection of groups.

**Response:**

``` xml
<groups>
  <group>
    ...
  </group>
  <group>
    ...
  </group>
</groups>
```

Create group
------------

* `POST /groups.xml` creates a new empty group. Users are added to the group through memberships.

**Request:**

``` xml
<group>
  <name>Partners</name>
</group>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/groups/#{new-group-id}.xml

    <group>
      ...
    </group>

Update group
------------

* `PUT /groups/#{id}.xml` updates an existing group with a new name.

**Request:**

``` xml
<group>
  <name>Senior Partners</name>
</group>
```

**Response:**

    Status: 200 OK

Destroy group
-------------

* `DELETE /groups/#{id}.xml` destroys the group at the referenced URL.

**Response:**

    Status: 200 OK
