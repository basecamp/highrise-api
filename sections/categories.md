Categories (Tasks, Deals)
=========================

The categories API is identical for both Task categories, and Deal categories, with the only difference being the URL. For Task categories, the API should be prefixed with `task_categories`, and for Deal categories, `deal_categories`. In the documentation that follows, the generic `#{type}_categories` will be used, but you should replace that with the category collection you wish to query.

For the full XML representation of categories, [check out the data reference](https://github.com/basecamp/highrise-api/blob/master/sections/data_reference.md#category).


Get category
------------

* `GET /#{type}_categories/#{id}.xml` return a single category record.

**Response:**

``` xml
<#{type}-category>
  <id type="integer"></id>
  <name></name>
  <color></color>
  <account-id type="integer"></account-id>
  <created-at type="datetime"></created-at>
  <updated-at type="datetime"></updated-at>
  <elements-count type="integer"></elements-count>
</#{type}-category>
```


Get categories
--------------

* `GET /#{type}_categories.xml` returns all categories.

**Response:**

``` xml
<#{type}-categories type="array">
  <#{type}-category>
    ...
  </#{type}-category>
  ...
</#{type}-categories>
```


Create category
---------------

* `POST /#{type}_categories.xml` create a new category.

**Request:**

``` xml
<#{type}-category>
  <name>#{name}</name>
  <color>#{hex-color}</color>
</#{type}-category>
```

Color is optional. If provided, it should be a [web color in hexadecimal format](http://en.wikipedia.org/wiki/Web_colors), e.g., ffcc33. Defaults to 000000 (black).

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/#{type}_categories/#{new-id}.xml


Update category
---------------

* `PUT /#{type}_categories/#{id}.xml` update (rename) an existing category

**Request:**

``` xml
<#{type}-category>
  <name>#{name}</name>
</#{type}-category>
```

**Response:**

    Status: 200 OK


Destroy category
----------------

* `DELETE /#{type}_categories/#{id}.xml` destroys a category. 

**Response:**

    Status: 200 OK
