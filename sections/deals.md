Deals
=====

For the full XML representation of deals, [check out the data reference](https://github.com/basecamp/highrise-api/blob/master/sections/data_reference.md#deal).


Get deal
--------

* `GET /deals/#{id}.xml` returns an existing deal.

The `currency` field is a three-character ISO 4217 currency identifier. The `price-type` field indicates whether the deal’s bid has a fixed price (`fixed`), or is based on an hourly (`hour`), monthly (`month`), or annual (`year`) price. The `duration` field indicates how many `price-type` units long the deal is expected to span. The `status` field indicates whether the deal is `pending`, `won`, or `lost`. The `party-id` field identifies the party that the deal is about, or for. The `responsible-party-id` field identifies which user is responsible for this deal. The `category-id` field is the id of the DealCategory record for this deal. The `background` field is arbitrary text describing this deal. The `parties` field is a list of the people and companies involved with this deal. The `party` field is the person or company the deal is with.

**Response:**

``` xml
<deal>
  <account-id type="integer"></account-id>
  <author-id type="integer"></author-id>
  <background></background>
  <category-id type="integer"></category-id>
  <created-at type="datetime"></created-at>
  <currency></currency>
  <duration type="integer"></duration>
  <group-id type="integer"></group-id>
  <name></name>
  <owner-id type="integer"></owner-id>
  <party-id type="integer"></party-id>
  <price type="integer"></price>
  <price-type></price-type>
  <responsible-party-id type="integer"></responsible-party-id>
  <status></status>
  <status-changed-on type="date"></status-changed-on>
  <updated-at type="datetime"></updated-at>
  <visible-to>Everyone</visible-to>
  <parties type="array">
    <party>...</party>
  </parties>
  <party>...</party>
</deal>
```


Get deals
---------

* `GET /deals.xml` returns a list of deals that are visible to the authenticated user.
* `GET /deals.xml?n=500` returns the next 500 deals
* `GET /deals.xml?status=won` returns deals that are `won`, could also request `lost` and `pending` deals
* `GET /deals.xml?since=20130225154546` returns the deals updated since the timestamp, oldest to newest. The `since` parameter is expressed as `yyyymmddhhmmss` in the UTC timezone.

**Response:**

``` xml
<deals type="array">
  <deal>
    ...
  </deal>
  ...
</deals>
```


Get new deal
------------

* `GET /deals/new.xml` returns a blank XML template that may be used as a guide for populating the fields of a new Deal record.

**Response:**

``` xml
<deal>
  ...
</deal>
```


Create deal
-----------

* `POST /deals.xml` creates a new deal with the currently authenticated user as the author.

By default, a new deal is assumed to be visible to `Everyone`. You can also choose to make the deal only visible to the creator using `Owner` as the value for the `visible-to` tag. Or `NamedGroup` and pass in a `group-id` tag too.

If the account doesn’t allow for more deals to be created, a `507 Insufficient Storage` response will be returned.

See the [Get deal](#get-deal) call for a description of what the different fields mean.

**Request:**

``` xml
<deal>
  <name>#{name}</name>

  <!-- optional fields -->
  <party-id type="integer">#{party_id}</party-id>
  <visible-to>Everyone</visible-to>
  <group-id type="integer">#{group_id}</group-id>
  <owner-id type="integer">#{owner_id}</owner-id>
  <responsible-party-id type="integer">#{responsible_party_id}</responsible-party-id>
  <category-id type="integer">#{category_id}</category-id>
  <background>#{background}</background>
  <currency>#{currency}</currency>
  <price type="integer">#{price}</price>
  <price-type>fixed</price-type>
  <duration type="integer">#{duration}</duration>
</deal>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/deals/#{new-deal-id}.xml


Update deal
-----------

* `PUT /deals/#{id}.xml` updates information about the given deal.

Note that changes to a deal’s status should be done via the [Update deal status](#update-deal-status) call, and not via this call. Attempts to update the status via this API call will silently ignore the status field.

Changes to a deal’s contacts cannot be made at this time. Any additions to the `parties` field will be ignored.

**Request:**

``` xml
<deal>
  <name>#{name}</name>

  <!-- optional fields -->
  <party-id type="integer">#{party_id}</party-id>
  <visible-to>Everyone</visible-to>
  <group-id type="integer">#{group_id}</group-id>
  <owner-id type="integer">#{owner_id}</owner-id>
  <responsible-party-id type="integer">#{responsible_party_id}</responsible-party-id>
  <category-id type="integer">#{category_id}</category-id>
  <background>#{background}</background>
  <currency>#{currency}</currency>
  <price type="integer">#{price}</price>
  <price-type>fixed</price-type>
  <duration type="integer">#{duration}</duration>
</deal>
```


Destroy deal
------------

* `DELETE /deals/#{id}.xml` destroys the given deal.

This endpoint will also destroy any notes, emails, or files that are associated with the deal.

**Response:**

    Status: 200 OK


Update deal status
------------------

* `PUT /deals/#{id}/status.xml` changes the status of the given deal.

The value of the status name must be `pending`, `won`, or `lost`. Note that changing the status of a deal to `pending` will fail with a `507 Insufficient Storage` if you have reached your account limit of pending deals.

**Request:**

``` xml
<status>
  <name>#{status}</name>
</status>
```

**Response:**

    Status: 200 OK
