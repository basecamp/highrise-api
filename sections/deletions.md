Deletions
---------


* `GET /deletions.xml` returns a list of deleted resources (companies, people, deals, tasks, notes, emails, comments, task recordings, deal recordings, project recordings).
* `GET /deletions.xml?since=20070425154546` returns the deletions that have ocurred since the time in the query parameter.

The collection is ordered from oldest to newest. The `since` parameter is expressed as `yyyymmddhhmmss` in the UTC timezone. Deletions are paginated using offsets. If 500 elements are returned (the page limit), use `?n=500` to fetch the next 500, and so on.

**Response:**

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
  <deletion type="Deal">
    <id type="integer">88602677</id>
    <deleted-at type="datetime">2011-10-06T10:06:31Z</deleted-at>
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
