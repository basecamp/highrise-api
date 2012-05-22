Memberships
===========

For linking users and groups together. The authenticated user needs to be an administrator to perform these actions.


Get membership
--------------

* `GET /memberships/#{id}.xml` show an existing membership.

**Response:**

``` xml
<membership>
  <id type="integer">1</id>
  <group-id type="integer">1</group-id>
  <user-id type="integer">1</user-id>
  <created-at type="datetime">2007-04-23T20:25:29Z</created-at>
  <updated-at type="datetime">2007-04-23T20:25:29Z</updated-at>
</membership>
```


Get memberships
---------------

* `GET /memberships.xml` returns a collection of all the memberships.

**Response:**

``` xml
<memberships>
  <membership>
    ...
  </membership>
  <membership>
    ...
  </membership>
</memberships>
```


Create membership
-----------------

* `POST /memberships.xml` creates a new membership between a user and a group.

**Request:**

``` xml
<membership>
  <user_id type="integer">1</user_id>
  <group_id type="integer">2</group_id>
</membership>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/memberships/#{new-membership-id}.xml

    <membership>
      ...
    </membership>


Destroy membership
------------------

* `DELETE /memberships/#{id}.xml` removes the membership between the user and the group.

**Response:**

    Status: 200 OK
