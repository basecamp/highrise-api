Deletions
---------

* `GET /deletions.xml` returns a list of deleted resources.
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
</deletions>
```
