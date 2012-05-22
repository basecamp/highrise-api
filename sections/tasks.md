Tasks
-----

Tasks either use the general frame tag, like the example below with `today`, or they'll use the specific `due-at` tag if they have a set time and specific day as well.


Get task
--------

* `GET /tasks/#{id}.xml` returns a single task.

**Response:**

``` xml
<task>
  <id type="integer">1</id>
  <recording-id type="integer"></recording-id>
  <subject-id type="integer"></subject-id>
  <subject-type></subject-type>
  <subject-name></subject-name>
  <category-id type="integer"></category-id>
  <body>A task for today</body>
  <frame>today</frame>
  <due-at type="datetime"></due-at>
  <alert-at type="datetime"></alert-at>
  <created-at type="datetime"></created-at>
  <author-id type="integer">1</author-id>
  <updated-at type="datetime"></updated-at>
  <public type="boolean">false</public>
</task>
```


Get tasks
---------

* `GET /#{ people || companies || kases || deals }/#{subject-id}/tasks.xml` returns a collection of upcoming tasks for the authenticated user that are related to either a person, a company, case or a deal.
* `GET /tasks/upcoming.xml` returns a collection of upcoming tasks (tasks that have not yet been completed, regardless of whether they’re overdue) for the authenticated user.
* `GET /tasks/assigned.xml` returns a collection of upcoming tasks (tasks that have not yet been completed, regardless of whether they’re overdue) that were created by the authenticated user, but assigned to somebody else.
* `GET /tasks/completed.xml` returns a collection of completed tasks.

**Response:**

``` xml
<tasks>
  <task>
    ...
  </task>
  <task>
    ...
  </task>
</tasks>
```


Create task for time frame
--------------------------

* `POST /tasks.xml` creates a new task for a generic frame like today or next week.

The possible frames are: `today`, `tomorrow`, `this_week`, `next_week`, and `later`.

If this task relates to a specific subject, like a person, company or case, you should set the `subject-id` and `subject-type` (use `Party` for person/company and `Kase` for case).

You can also set a `recording-id`, which will bind the task to that recording and to the subject of that recording. If you do that, you don’t need to specifically set `subject-id` and `subject-type`.

You can assign this task to someone else by setting the `owner-id` tag to the id of that user. You can let other users see this task by setting the public tag to true.

If you want to assign the task to someone else, but not trigger an assignment notification email, you can set the `notify` tag to `false`. It defaults to `true`.

**Request:**

``` xml
<task>
  <body>A task for today</body>
  <frame>today</frame>

  <!-- optional -->
  <subject-type>#{Party|Company|Kase|Deal}</subject-type>
  <subject-id>#{associated_subject.id}</subject-id>
  <category-id type="integer">#{task_category.id}</category-id>
  <recording-id type="integer">#{associated_recording.id}</recording-id>
  <owner-id type="integer">#{owner_user.id}</owner-id>
  <public type="boolean">#{true|false}</public>
  <notify type="boolean">#{true|false}</notify>
</task>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/tasks/#{new-task-id}.xml

    <task>
      ...
    </task>


Create for specific time
------------------------

* `POST /tasks.xml` creates a new task for a specific time, like April 9th at 7:30pm.

See the description for [Create task for time frame](#create_task_for_time_frame) for a description of the possible options.

**Request:**

``` xml
<task>
  <body>A timed task for the future</body>
  <frame>specific</frame>
  <due-at type="datetime">2007-03-10T15:11:52Z</due-at>
  <category-id>1</category-id>

  <!-- optional -->
  <subject-type>#{Party|Company|Kase|Deal}</subject-type>
  <subject-id>#{associated_subject.id}</subject-id>
  <category-id type="integer">#{task_category.id}</category-id>
  <recording-id type="integer">#{associated_recording.id}</recording-id>
  <owner-id type="integer">#{owner_user.id}</owner-id>
  <public type="boolean">#{true|false}</public>
  <notify type="boolean">#{true|false}</notify>
</task>
```

**Response:**

    Status: 201 Created
    Location: https://example.highrisehq.com/comments/#{new-comment-id}.xml

    <task>
      ...
    </task>


Complete task
-------------

* `POST /tasks/#{id}/complete.xml` completes an upcoming task and records the fact in the log.

**Response:**

``` xml
<task>
  ...
  <done-at>2007-03-10T15:11:52Z</done-at>
</task>
```


Update task
-----------

* `PUT /tasks/#{id}.xml` updates an existing task with new details from the submitted XML.

Use `?reload=true` to get XML of the successfully updated task.

**Request:**

``` xml
<task>
  <body>An untimed task for later</body>
  <frame>later</frame>
  <category-id type="integer">1</category-id>
  <owner-id type="integer">2</owner-id>
</task>
```

**Response:**

    Status: 200 OK


Destroy task
------------

* `DELETE /tasks/#{id}.xml` destroys the task at the referenced URL.

**Response:**

    Status: 200 OK
