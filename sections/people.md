People
======

For the full XML representation of people, [check out the data reference](https://github.com/37signals/highrise-api/blob/master/sections/data_reference.md#person).


Get people
----------

* `GET /people.xml` returns a collection of people that are visible to the authenticated user.
* `GET /people.xml?n=500` returns a collection of people that are visible to the authenticated user offset by the given amount. (page limit of 500)
* `GET /people.xml?title=CEO` returns a collection of people that have a specific title.
* `GET /people.xml?tag_id=#{tag_id}` returns a collection of people that have been tagged with the tag responding to `#{tag_id}`.
* `GET /people.xml?since=20070425154546` returns a collection of people that have been created or updated since the time passed in through the URL.
* `GET /companies/#{company_id}/people.xml` returns a collection of people that belong to the company referenced in the URL.

If no people are returned for the given parameters, an empty `<people>` container will be in the response.

When filtering with the `since` parameter, the collection is ordered by ascending `updated_at` (oldest to newest). The `since` parameter should be in the `yyyymmddhhmmss` format and in UTC.

**Response:**

``` xml
<people>
  <person>
    ...
  </person>
  <person>
    ...
  </person>
</people>
```


Search people
-------------

* `GET /people/search.xml?term=David` returns a collection of people that have a name matching the term passed in through the URL.
* `GET /people/search.xml?criteria[state]=CA&criteria[zip]=90210&criteria[custom_field]=foobar` returns people who match your search criteria. Search by any criteria you can on the Contacts tab, including custom fields. Combine criteria to narrow results.

If no people with the given criteria or term exist an empty people container will be returned. Results are paged in groups of 25. Use `?n=25` to check for the next 25 results and so on.

**Response:**

``` xml
<people>
  <person>
    ...
  </person>
  <person>
    ...
  </person>
</people>
```


Get person
----------

* `GET /people/#{id}.xml` returns a single person.

**Response:**

``` xml
<person>
  <id type="integer">1</id>
  <first-name>John</first-name>
  <last-name>Doe</last-name>
  <title>Stand-in</title>
  <background>A popular guy for random data</background>
  <linkedin-url>http://us.linkedin.com/in/john-doe</linkedin-url>
  <avatar-url></avatar-url>
  <company-id type="integer">5</company-id>
  <company-name>Doe Inc.</company-name>
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
        <address>john.doe@example.com</address>
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
        <number>555-666-6666</number>
        <location>Home</location>
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
    <subject_data>
      <id type="integer">5</id>
      <value>John</value>
      <subject_field_id type="integer">2</subject_field_id>
      <subject_field_label>Account Manager</subject_field_label>
    </subject_data>
  </subject_datas>
  <tags type="array">
    <tag>
      <id type="integer">1</id>
      <name>Partner</name>
    </tag>
  </tags>
</person>
```


Create person
-------------

* `POST /people.xml` creates a new person with the currently authenticated user as the author.

The XML for the new person is returned on a successful request with the timestamps recorded and ids for the contact data associated.

Additionally, the `company-name` is used to either lookup a company with that name or create a new one if it didn’t already exist. You can also refer to an existing company instead using `company-id`.

By default, a new person is assumed to be visible to `Everyone`. You can also chose to make the person only visible to the creator using `Owner` as the value for the `visible-to` tag. Or `NamedGroup` and pass in a `group-id` tag too.

If the account doesn’t allow for more people to be created, a `507 Insufficient Storage` response will be returned.

**Request:**

``` xml
<person>
  <first-name>John</first-name>
  <last-name>Doe</last-name>
  <title>CEO</title>
  <company-name>Doe Inc.</company-name>
  <background>A popular guy for random data</background>
  <linkedin_url>http://us.linkedin.com/in/john-doe</linkedin_url>
  <contact-data>
    <email-addresses>
      <email-address>
        <address>john.doe@example.com</address>
        <location>Work</location>
      </email-address>
    </email-addresses>
    <phone-numbers>
      <phone-number>
        <number>555-555-5555</number>
        <location>Work</location>
      </phone-number>
      <phone-number>
        <number>555-666-6666</number>
        <location>Home</location>
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
</person>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/people/#{new-person-id}.xml

    <person>
      ...
    </person>

Update person
-------------

* `PUT /people/#{id}.xml` updates an existing person with new details from the submitted XML.

Contact data and Subject data that include an id will be updated, data that doesn’t will be assumed to be new and created from scratch. To remove a piece of data, prefix its id with a minus sign (e.g. `-1`).

Use `?reload=true` to get XML of the successfully updated person.

**Request:**

``` xml
<person>
  <first-name>John</first-name>
  <last-name>Doe</last-name>
  <title>CEO</title>
  <company-id>1</company-id>
  <background>A popular guy for random data</background>
  <linkedin_url>http://us.linkedin.com/in/john-doe</linkedin_url>
  <contact-data>
    <email-addresses>
      <email-address>
        <id type="integer">1</id>
        <address>john.doe@example.com</address>
        <location>Work</location>
      </email-address>
      <email-address>
        <address>john.doe.home@example.com</address>
        <location>Home</location>
      </email-address>
    </email-addresses>
  </contact-data>
  <subject_datas type="array">
    <!-- Updates custom field using subject_data id -->
    <subject_data>
      <id type="integer">3</id>
      <value>Chicago</value>
    </subject_data>
    <!-- Updates/creates custom field using subject_field id -->
    <subject_data>
      <subject_field_id type="integer">5</subject_field_id>
      <value>Mark</value>
    </subject_data>
  </subject_datas>
</person>
```

**Response:**

    Status: 200 OK

Destroy person
--------------

* `DELETE /people/#{id}.xml` destroys the person at the referenced URL.

**Response:**

    Status: 200 OK
