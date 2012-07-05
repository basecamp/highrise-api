Recordings
----------

* `GET /recordings.xml` returns recordings (notes, comments, emails)
* `GET /recordings.xml?since=20070425154546` returns the recordings (notes, comments, emails) that have updated since the time in the query parameter.

The collection is ordered from oldest to newest. The `since` parameter is expressed as `yyyymmddhhmmss` in the UTC timezone. Recordings are paginated using offsets. If 25 elements are returned (the page limit), use `?n=25` to fetch the next 25, and so on.

For details on the individual recording contents see the [notes](https://github.com/37signals/highrise-api/blob/master/sections/notes.md), [comments](https://github.com/37signals/highrise-api/blob/master/sections/comments.md), and [emails](https://github.com/37signals/highrise-api/blob/master/sections/emails.md) references.

**Response:**

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
