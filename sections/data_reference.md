Data Reference
==============

Case
----

``` xml
<kase>
  <id type="integer">1</id>
  <closed-at type="datetime"></closed-at>
  <name>A very important matter</name>
  <created-at type="datetime"></created-at>
  <updated-at type="datetime">2007-03-19T22:34:22Z</updated-at>
  <visible-to>#{Everyone || Owner || NamedGroup}</visible-to>
  <owner-id type="integer">#{ user_id -- when visible-to is "Owner"}</owner-id>
  <group-id type="integer">#{ group_id -- when visible-to is "NamedGroup"}</group-id>
  <author-id type="integer">3</author-id>
  <parties type="array">
    <party>...</party>
  </parties>
</kase>
```

Comment
-------

``` xml
<comment>
  <id type="integer">1</id>
  <parent-id type="integer">2</parent-id>
  <author-id type="integer">1</author-id>
  <created-at type="datetime">2006-05-19T20:26:00Z</created-at>
  <body>I agree, taxes are no fun</body>
</comment>
```

Company
-------

``` xml
<company>
  <id type="integer">1</id>
  <name>Doe Inc.</name>
  <background>A popular company for random data</background>
  <created-at type="datetime">2007-02-27T03:11:52Z</created-at>
  <updated-at type="datetime">2007-03-10T15:11:52Z</updated-at>
  <visible-to>#{Everyone || Owner || NamedGroup}</visible-to>
  <owner-id type="integer">#{ user_id -- when visible-to is "Owner"}</owner-id>
  <group-id type="integer">#{ group_id -- when visible-to is "NamedGroup"}</group-id>
  <author-id type="integer">3</author-id>
  <contact-data>
    ...
  </contact-data>
  <tags type="array">
    ...
  </tags>
</company>
```

Contact data for person and company
-----------------------------------

``` xml
<contact-data>
  <email-addresses>
    <email-address>
      <id type="integer">1</id>
      <address>john.doe@example.com</address>
      <location>#{ Work || Home || Other }</location>
    </email-address>
  </email-addresses>
  <phone-numbers>
    <phone-number>
      <id type="integer">2</id>
      <number>555-555-5555</number>
      <location>#{ Work || Mobile || Fax || Pager || Home || Skype || Other }</location>
    </phone-number>
    <phone-number>
      <id type="integer">3</id>
      <number>555-666-6666</number>
      <location>Home</location>
    </phone-number>
  </phone-numbers>
  <addresses>
    <address>
      <id type="integer">1</id>
      <city>Sampleville</city>
      <country>United States</country>
      <state>IL</state>
      <street>123 Example Ave</street>
      <zip>55555</zip>
      <location>#{ Work || Home || Other }</location>
    </address>
  </addresses>
  <instant-messengers>
    <instant-messenger>
      <id type="integer">1</id>
      <address>example</address>
      <protocol>#{
        AIM || MSN || ICQ || Jabber || Yahoo || Skype || QQ ||
        Sametime || Gadu-Gadu || Google Talk || other
      }</protocol>
      <location>#{ Work || Personal || Other }</location>
    </instant-messenger>
  </instant-messengers>
  <twitter-accounts>
    <twitter-account>
      <id type="integer">1</id>
      <location>Personal</location>
      <username>heyjohndoe</username>
      <url>http://twitter.com/heyjohndoe</url>
    </twitter-account>
  </twitter-accounts>
  <web-addresses>
    <web-address>
      <id type="integer">1</id>
      <url>http://www.example.com</url>
      <location>#{ Work || Personal || Other }</location>
    </web-address>
  </web-addresses>
</contact-data>
```

Custom fields
-------------

``` xml
<subject_datas type="array">
  <subject_data>
    <id type="integer">3</id>
    <value>Chicago</value>
    <subject_field_id type="integer">1</subject_field_id>
    <subject_field_label>Sales Region</subject_field_label>
  </subject_data>
</subject_datas>
```

Deal
----

``` xml
<deal>
  <account-id type="integer">1</account-id>
  <author-id type="integer">1</author-id>
  <background></background>
  <category-id type="integer">1</category-id>
  <created-at type="datetime">2010-02-24T18:40:32Z</created-at>
  <currency>USD</currency>
  <duration type="integer" nil="true"></duration>
  <group-id type="integer" nil="true"></group-id>
  <id type="integer">1</id>
  <name>Example</name>
  <owner-id type="integer" nil="true"></owner-id>
  <party-id type="integer">6915469</party-id>
  <price type="integer">1000</price>
  <price-type>fixed</price-type>
  <responsible-party-id type="integer">1</responsible-party-id>
  <status>pending</status>
  <status-changed-on type="date" nil="true"></status-changed-on>
  <updated-at type="datetime">2010-02-24T18:44:29Z</updated-at>
  <visible-to>Everyone</visible-to>
  <category>
    <id type="integer">1</id>
    <name>Examples</name>
  </category>
  <parties type="array">
    <party>...</party>
  </parties>
  <party>...</party>
</deal>
```

Deletions
---------

``` xml
<deletions type="array">
  <deletion type="Company">
    <id type="integer">88602616</id>
    <deleted-at type="datetime">2011-10-06T10:03:41Z</deleted-at>
  </deletion>
  <deletion type="Person">
    <id type="integer">88602673</id>
    <deleted-at type="datetime">2011-10-06T10:05:31Z</deleted-at>
  </deletion>
  <deletion type="Task">
    <id type="integer">88602694</id>
    <deleted-at type="datetime">2011-10-06T10:07:19Z</deleted-at>
  </deletion>
  <deletion type="Note">
    <id type="integer">88602703</id>
    <deleted-at type="datetime">2011-10-06T10:13:36Z</deleted-at>
  </deletion>
  <deletion type="Email">
    <id type="integer">88602718</id>
    <deleted-at type="datetime">2011-10-06T10:20:54Z</deleted-at>
  </deletion>
  <deletion type="Comment">
    <id type="integer">88602723</id>
    <deleted-at type="datetime">2011-10-06T10:28:06Z</deleted-at>
  </deletion>
  <deletion type="TaskRecording">
    <id type="integer">88602734</id>
    <deleted-at type="datetime">2011-10-06T10:33:23Z</deleted-at>
  </deletion>
  <deletion type="DealRecording">
    <id type="integer">88602741</id>
    <deleted-at type="datetime">2011-10-06T10:39:31Z</deleted-at>
  </deletion>
  <deletion type="ProjectRecording">
    <id type="integer">88602750</id>
    <deleted-at type="datetime">2011-10-06T10:45:12Z</deleted-at>
  </deletion>
</deletions>
```

Email
-----

``` xml
<email>
  <id type="integer">1</id>
  <title>This is the subject of the email</title>
  <body>This is the body</body>
  <author-id type="integer">3</author-id>
  <subject-id type="integer">1</subject-id>
  <subject-type>#{ Party || Deal || Kase }</subject-type>
  <subject-name>John Doe</subject-name>
  <collection-id type="integer">1</subject-id>
  <collection-type>#{ Deal || Kase }</subject-type>
  <visible-to>#{Everyone || Owner || NamedGroup}</visible-to>
  <owner-id type="integer">#{ user_id -- when visible-to is "Owner"}</owner-id>
  <group-id type="integer">#{ group_id -- when visible-to is "NamedGroup"}</group-id>
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
</email>
```

Group
-----

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

Membership
----------

``` xml
<membership>
  <id type="integer">1</id>
  <group-id type="integer">1</group-id>
  <user-id type="integer">1</user-id>
  <created-at type="datetime">2007-04-23T20:25:29Z</created-at>
  <updated-at type="datetime">2007-04-23T20:25:29Z</updated-at>
</membership>
```

Note
----

``` xml
<note>
  <id type="integer">1</id>
  <body>Hello world!</body>
  <author-id type="integer">3</author-id>
  <subject-id type="integer">1</subject-id>
  <subject-type>#{ Party || Deal || Kase }</subject-type>
  <subject-name>John Doe</subject-name>
  <collection-id type="integer">1</subject-id>
  <collection-type>#{ Deal || Kase }</subject-type>
  <visible-to>#{Everyone || Owner || NamedGroup}</visible-to>
  <owner-id type="integer">#{ user_id -- when visible-to is "Owner"}</owner-id>
  <group-id type="integer">#{ group_id -- when visible-to is "NamedGroup"}</group-id>
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

Person
------

``` xml
<person>
  <id type="integer">1</id>
  <first-name>John</first-name>
  <last-name>Doe</last-name>
  <title>Stand-in</title>
  <background>A popular guy for random data</background>
  <company-id type="integer">2</company-id>
  <created-at type="datetime">2007-02-27T03:11:52Z</created-at>
  <updated-at type="datetime">2007-03-10T15:11:52Z</updated-at>
  <visible-to>#{Everyone || Owner || NamedGroup}</visible-to>
  <owner-id type="integer">#{ user_id -- when visible-to is "Owner"}</owner-id>
  <group-id type="integer">#{ group_id -- when visible-to is "NamedGroup"}</group-id>
  <author-id type="integer">3</author-id>
  <contact-data>
    ...
  </contact-data>
  <tags type="array">
    ...
  </tags>
</person>
```

Recordings
----------

``` xml
<recordings type="array">
  <recording type="Email">
    ...
    <updated-at>2007-04-26T13:12:52Z</updated-at>
  </recording>
  <recording type="Note">
    ...
    <updated-at>2007-04-25T17:11:52Z</updated-at>
  </recording>
</recordings>
```

Tag
---

``` xml
<tag>
  <id type="integer">1</id>
  <name>Partner</name>
</tag>
```

Task
----

``` xml
<task>
  <id type="integer">1</id>
  <author-id type="integer">1</author-id>
  <owner-id type="integer">1</owner-id>
  <recording-id type="integer"></recording-id>
  <subject-id type="integer"></subject-id>
  <subject-type></subject-type>
  <subject-name></subject-name>
  <body>Remember to do something important</body>
  <frame>#{ today || tomorrow || this_week || next_week || later }</frame>
  <alert-at type="datetime"></alert-at>
  <done-at type="datetime"></done-at>
  <category-id type="integer"></category-id>
  <created-at type="datetime"></created-at>
  <updated-at type="datetime">2007-04-26T02:04:03Z</updated-at>
</task>
```

User
----

``` xml
<user>
  <id type="integer">1</id>
  <name>John Doe</name>
  <email-address>john.doe@example.com</email-address>
  <created-at type="datetime">2007-04-23T20:25:29Z</created-at>
  <updated-at type="datetime">2007-04-23T20:25:29Z</updated-at>

  <!-- when requested as /me.xml -->
  <token>#{api_token}</token>
  <dropbox>#{dropbox_email_address}</dropbox>
</user>
```

