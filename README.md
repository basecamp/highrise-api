Highrise API
============

The Highrise API is implemented as vanilla XML over HTTP using all four verbs (GET/POST/PUT/DELETE). Every resource, like Person, Deal, or Party, has their own URL and are manipulated in isolation. In other words, we've tried to make the API follow the REST principles as much as we can.

You can explore the view part of the API (everything that's fetched with GET) through a regular browser. Using Firefox for this is particularly nice as it has a good, simple XML renderer (unlike Safari which just strips the tags and dumps the content). Pretty much any URL in Highrise can be viewed in its XML form by adding the .xml extension. So `/people/4` becomes `/people/4.xml` if you want to see the XML version.

Wrappers and example code
-------------------------

* [Ruby wrapper by tapajos](http://github.com/tapajos/highrise)
* [Pyrise by FeedMagnet](https://github.com/feedmagnet/pyrise)
* [Highton (Python) by bykof](https://github.com/seibert-media/Highton)
* [Highrise-PHP-Api](https://github.com/ignaciovazquez/Highrise-PHP-Api)
* [.NET 4.5 wrapper by scottschluer](https://github.com/scottschluer/highrise-api)
* [Highrise Java API](https://github.com/dnobel/highrise-java-api)

Wrote your own API wrapper? Feel free to open a pull request and add to this list!


API Endpoints
-------------

* [People](https://github.com/basecamp/highrise-api/blob/master/sections/people.md)
* [Categories (Tasks, Deals)](https://github.com/basecamp/highrise-api/blob/master/sections/categories.md)
* [Companies](https://github.com/basecamp/highrise-api/blob/master/sections/companies.md)
* [Cases](https://github.com/basecamp/highrise-api/blob/master/sections/cases.md)
* [Deals](https://github.com/basecamp/highrise-api/blob/master/sections/deals.md)
* [Notes](https://github.com/basecamp/highrise-api/blob/master/sections/notes.md)
* [Emails](https://github.com/basecamp/highrise-api/blob/master/sections/emails.md)
* [Comments](https://github.com/basecamp/highrise-api/blob/master/sections/comments.md)
* [Tags](https://github.com/basecamp/highrise-api/blob/master/sections/tags.md)
* [Tasks](https://github.com/basecamp/highrise-api/blob/master/sections/tasks.md)
* [Users](https://github.com/basecamp/highrise-api/blob/master/sections/users.md)
* [Groups](https://github.com/basecamp/highrise-api/blob/master/sections/groups.md)
* [Memberships](https://github.com/basecamp/highrise-api/blob/master/sections/memberships.md)
* [Account](https://github.com/basecamp/highrise-api/blob/master/sections/account.md)
* [Parties](https://github.com/basecamp/highrise-api/blob/master/sections/parties.md)
* [Recordings](https://github.com/basecamp/highrise-api/blob/master/sections/recordings.md)
* [Custom Fields](https://github.com/basecamp/highrise-api/blob/master/sections/custom_fields.md)
* [Deletions](https://github.com/basecamp/highrise-api/blob/master/sections/deletions.md)

(Hint: Press `t` to enable the file finder and type out the endpoint you need!)

Need a sample of each XML blob will look like? Check out the [Data Reference](https://github.com/basecamp/highrise-api/blob/master/sections/data_reference.md).


Authentication
--------------

When you're using the API, it's always through an existing user in Highrise. There's no special API user. So when you use the API as "david", you get to see and work with what "david" is allowed to. Authenticating is done with an authentication token, which you'll find on the "My Info" screen in Highrise, in the "Integrations" tab.

When using the authentication token, you don't need a separate password. But since Highrise uses [HTTP Basic Authentication](http://www.ietf.org/rfc/rfc2617.txt), and lots of implementations assume that you want to have a password, it's often easier just to pass in a dummy password, like X.

Here's an example using the authentication token and a dummy password through curl:

    curl -u 605b32dd:X https://example.highrisehq.com/people/1.xml

Remember that anyone who has your authentication token can see and change everything you have access to. So you want to guard that as well as you guard your username and password. If you come to fear that it has been compromised, you can regenerate it at any time from the "My Info" screen in Highrise.

You can also use OAuth 2 to authenticate users on their behalf without having to copy/paste API tokens or touch sensitive login info. Read the [Basecamp API Authentication Guide](https://github.com/basecamp/api/tree/master/sections/authentication.md) for more info on using OAuth.

Note that the `/me.xml` endpoint is the one exception to token authentication: you can use a username and password to authenticate against this action. This allows developers to obtain the token for a user, given that user's username and password, which makes it easier for users to authenticate on mobile platforms and the like.

Identify your app
-----------------

You should include a `User-Agent` header with the name of your application and a link to it or your email address so we can get in touch in case you're doing something wrong (so we may warn you before you're blacklisted) or something awesome (so we may congratulate you). Here's a couple of examples:

    User-Agent: Freshbooks (http://freshbooks.com/contact.php)
    User-Agent: Fabian's Ingenious Integration (fabian@example.com)

Reading through the API
-----------------------

The Highrise API has two category of actions for reading: Get one, or get many. All these actions are done through an HTTP GET, which also means that they're all easily explorable through a browser as described above.

Here's a few examples of reading with curl:

    curl -u 605b32dd:X https://example.highrisehq.com/kases/5.xml

    curl -u 605b32dd:X https://example.highrisehq.com/people/27/notes.xml

If the read is successful, you'll get an XML response back along with the status code `200 OK`.


Writing through the API
-----------------------

Creating, updating, and deleting resources through the API is almost as easy as reading, but you can't explore it as easily through the browser. Regardless of your implementation language, though, using curl to play first is a great idea. It makes it very easy to explore the API and is perfect for small scripts too.

When you're creating and updating resources, you'll be sending XML into Highrise. You need to let the system know that fact by adding the header `Content-type: application/xml`, so we know that it's not regular form-encoded data coming in. Then you just include the XML of the resource in the body of your request.

Here's a few examples creating new resources, first with the XML inline, second referencing the XML from a file:

    curl -u 605b32dd:X -H 'Content-Type: application/xml' \
    -d '<kase><name>Important matters</name></kase>' https://example.highrisehq.com/kases.xml

    curl -u 605b32dd:X -H 'Content-Type: application/xml' \
    -d @note.xml https://example.highrisehq.com/people/5/notes.xml

The response to a succesful creation is the status code `201 Created`. You can get the URL of the new resource in the Location header (such that you know where to update your new resource in the future). We also include the complete XML for the final resource in the response. This is because you can usually get away with creating a new resource with less than all its regular attributes. Especially attributes like `created_at` can be helpful to get back from the creation.

Updating resources is done through the PUT verb and against the URL of the resource you want to update. Here's a few examples:

    curl -u 605b32dd:X -X PUT -H 'Content-Type: application/xml' \
    -d '<kase><name>Really important matters</name></kase>' https://example.highrisehq.com/kases/5.xml

    curl -u 605b32dd:X -X PUT -H 'Content-Type: application/xml' \
    -d @note.xml https://example.highrisehq.com/notes/27.xml

The response to a successful update is "200 OK".  Finally, you can delete resources (if you're allowed to) using the DELETE verb. A few examples of that:

    curl -u 605b32dd:X -X DELETE https://example.highrisehq.com/kases/5.xml

    curl -u 605b32dd:X -X DELETE https://example.highrisehq.com/notes/27.xml

Note that you don't need to pass the content-type header because you're not sending any XML. The response to a successful delete is `200 OK`.


Dealing with failure
--------------------

If a request fails, the error information is returned with the HTTP status code. For instance, if a requested record could not be found, the HTTP response might look something like:

    HTTP/1.1 404 The record could not be found
    Date: Thu, 16 Mar 2006 17:41:40 GMT
    ...

Note that, in general, if a request causes a new record to be created (like a new message, or to-do item, etc.), the response will use the "201 Created" status. Any other successful operation (like a successful query, delete, or update) will use a 200 status code.

Rate limiting
-------------

**Please note:** We've lowered the API limit call to searching for contacts via an email address to 2 requests in a 10 second period. 

All other limits remain at up to 500 requests per 10 second period from the same IP address for the same account. 

Regardless of these limits, your integrations with our API should handle `503 Service Unavailable` errors returned. Those will be returned if you exceed our limit, or we may have a temporary limit in place to handle surges or problematic load to the API. 

Check for `503 Service Unavailable` response from your requests and be sure to check the `Retry-After` header to see how many seconds to wait before retrying the request.

SSL Usage
---------

A non-SSL request made against an account that has SSL enabled (and vice versa) will receive a "302 Found" response. The Location header will contain the correct URI.

If SSL is enabled for your account, ensure that you're using https. If it's not, ensure you're using http.


Alternative formats
-------------------

XML is not the only other language than HTML you can make Highrise speak. We're also fairly fluent in Atom, CSV, and vCards. To subscribe to recordings (notes, emails, and comments), it's often easier to use the Atom feeds than to go through the XML API. Try browsing around Highrise to find the recording feeds. They're linked up with link-tags in the head of the HTML. For example, there's `/recordings.atom` for the getting the 25 most recent recordings across all subjects (people, companies, and cases). And there's `/people/1/recordings.atom` for getting just the last 25 about the person with ID = 1.

All parties (people and companies) can be retrieved in vCard form too. Just append the .vcf extension to the URL, like `/people/4.vcf`.


Conventions in the API documentation
------------------------------------

In the documentation that follows, the following notation is used:

    #{text}: Indicates text that should be replaced by your own data

    ...: Indicates content from the response has been elided for brevity in documentation. See the list of data responses at the end of the page for a full description of the format of that response type.


Help us make it better
----------------------

Please tell us how we can make this API better. If you have a specific feature request or if you found a bug, please [open a support ticket](http://help.basecamp.com/tickets/new). Also, feel free to fork these docs and send a pull request with improvements!

To talk with us and other developers about the API, [post a question on StackOverflow](http://stackoverflow.com/questions/ask) tagged `highrise` or [open a support ticket](http://help.basecamp.com/tickets/new).
