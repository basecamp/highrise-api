Companies
=========

For the full XML representation of companies, [check out the data reference](https://github.com/37signals/highrise-api/blob/master/sections/data_reference.md#company).


Get company
-----------

* `GET /companies/#{id}.xml` returns an existing company.

**Response:**

``` xml
<company>
  <id type="integer">1</id>
  <name>Doe Inc.</name>
  <background>A popular company for random data</background>
  <created-at type="datetime">2007-02-27T03:11:52Z</created-at>
  <updated-at type="datetime">2007-03-10T15:11:52Z</updated-at>
  <visible-to>Everyone</visible-to>
  <owner-id type="integer"></owner-id>
  <group-id type="integer"></group-id>
  <author-id type="integer">2</author-id>
  <contact-data>
    <email-addresses>
      <email-address>
        <id type="integer">1</id>
        <address>corporate@example.com</address>
        <location>Work</location>
      </email-address>
    </email-addresses>
    <phone-numbers>
      <phone-number>
        <id type="integer">2</id>
        <number>555-555-5555</number>
        <location>Work</location>
      </phone-number>
      <phone-number>
        <id type="integer">3</id>
        <number>555-666-6667</number>
        <location>Fax</location>
      </phone-number>
    </phone-numbers>
  </contact-data>
  <!-- custom fields -->
  <subject_datas type="array">
    <subject_data>
      <id type="integer">3</id>
      <value>Chicago</value>
      <subject_field_id type="integer">1</subject_field_id>
      <subject_field_label>Sales Region</subject_field_label>
    </subject_data>
  </subject_datas>
  <tags type="array">
    <tag>
      <id type="integer">2</id>
      <name>Lead</name>
    </tag>
  </tags>
</company>
```


Get companies
-------------

* `GET /companies.xml` returns a collection of companies that are visible to the authenticated user.
* `GET /companies.xml?n=#{offset}` returns a collection of companies offset by the given amount.
* `GET /companies.xml?tag_id=#{tag_id}` returns a collection of companies that have a specific tag.
* `GET /companies.xml?since=20070425154546` returns a collection of companies that have been created or updated since the time passed in through the URL. 
The list is paginated using offsets. If 500 elements are returned (the page limit), use `?n=500` to check for the next 500 and so on.

When filtering with the `since` parameter, the collection is ordered by ascending `updated_at` (oldest to newest). The `since` parameter should be in the `yyyymmddhhmmss` format and in UTC.

If companies under a tag are requsted and no companies with that tag exist, an empty `<companies>` container will be returned.

**Response:**

``` xml
<companies>
  <company>
    ...
  </company>
  <company>
    ...
  </company>
</companies>
```


Search companies
---------------

* `GET /companies/search.xml?term=Apple` returns a collection of companies that have a name matching the term passed in through the URL.
* `GET /companies/search.xml?criteria[state]=CA&criteria[phone]=1-800-MY-APPLE&criteria[custom_field]=foobar` returns companies that match your search criteria. Search by any criteria you can on the Contacts tab, including custom fields. Combine criteria to narrow results.

If no companies with that name exist an empty companies container will be returned. Results are paged in groups of 25. Use `?n=25` to check for the next 25 results and so on.

``` xml
<companies>
  <company>
    ...
    <name>Apple Inc</name>
  </company>
  <company>
    ...
    <name>Apple Music</name>
  </company>
</companies>
```


Create company
--------------

* `POST /companies.xml` creates a new company with the currently authenticated user as the author.

The XML for the new company is returned on a successful request with the timestamps recorded and ids for the contact data associated.

By default, a new company is assumed to be visible to `Everyone`. You can also chose to make the company only visible to the creator using `Owner` as the value for the `visible-to` tag. Or `NamedGroup` and pass in a `group-id` tag too.

As always, the URL for the newly-created company is passed back in the `Location` header.

**Request:**

``` xml
<company>
  <name>Doe Inc.</name>
  <background>A popular company for random data</background>
  <visible-to>Owner</visible-to>
  <contact-data>
    <email-addresses>
      <email-address>
        <address>corporate@example.com</address>
        <location>Work</location>
      </email-address>
    </email-addresses>
    <phone-numbers>
      <phone-number>
        <number>555-555-5555</number>
        <location>Work</location>
      </phone-number>
      <phone-number>
        <number>555-666-6667</number>
        <location>Fax</location>
      </phone-number>
    </phone-numbers>
  </contact-data>
  <!-- custom fields -->
  <subject_datas type="array">
    <subject_data>
      <value>Chicago</value>
      <subject_field_id type="integer">2</subject_field_id>
    </subject_data>
  </subject_datas>
</company>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/companies/#{new-company-id}.xml

    <company>
      ...
    </company>


Update company
--------------

* `PUT /companies/#{id}.xml` updates an existing company with new details from the submitted XML.

Contact data and Subject data that include an id will be updated, data that doesn’t will be assumed to be new and created from scratch. To remove a piece of data, prefix its id with a minus sign (e.g. `-1`).

Use `?reload=true` to get XML of the successfully updated company.

The request 'Content-Type' header should be set to 'application/xml'

**Request:**

``` xml
<company>
  <id type="integer">1</id>
  <name>Doe Inc.</name>
  <background>A popular company for random data</background>
  <contact-data>
    <email-addresses>
      <email-address>
        <id type="integer">1</id>
        <address>corporate@example.com</address>
        <location>Work</location>
      </email-address>
    </email-addresses>
    <phone-numbers>
      <phone-number>
        <id type="integer">2</id>
        <number>555-555-5555</number>
        <location>Work</location>
      </phone-number>
      <phone-number>
        <id type="integer">3</id>
        <number>555-666-6667</number>
        <location>Fax</location>
      </phone-number>
      <phone-number>
        <number>555-666-6668</number>
        <location>Home</location>
      </phone-number>
    </phone-numbers>
  </contact-data>
  <subject_datas type="array">
    <!-- Updates custom field using subject_data id -->
    <subject_data>
      <id type="integer">3</id>
      <value>Chicago</value>
    </subject_data>
    <!-- Updates/create custom field using subject_field id -->
    <subject_data>
      <subject_field_id type="integer">5</subject_field_id>
      <value>Mark</value>
    </subject_data>
  </subject_datas>
</company>
```

**Response:**

    Status: 200 OK


Destroy company
---------------

* `DELETE /companies/#{id}.xml` destroys the company at the referenced URL.

**Response:**

    Status: 200 OK
