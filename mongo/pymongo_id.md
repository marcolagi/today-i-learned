# PyMongo mutates objects without an `_id`

Here's something funny with `pymongo`:

    >>> from pymongo import MongoClient
    >>> collection = MongoClient()['db']['coll']
    >>> doc = {'key': 'value'}
    >>> collection.insert(doc)
    ObjectId('56c7330bca0929344c1505be')
    >>> doc
    {'key': 'value', '_id': ObjectId('56c7330bca0929344c1505be')}

So `pymongo` modifies the document to be inserted by adding an `_id` field, if
the document doesn't contain one already. Other drivers do the same thing. From their
[documentation](http://api.mongodb.org/python/current/faq.html#why-does-pymongo-add-an-id-field-to-all-of-my-documents),
here's the rationale:

> * All MongoDB documents are required to have an `_id` field.
> * If PyMongo were to insert a document without an `_id`, MongoDB would add
one itself, but it would not report the value back to PyMongo.
> * Copying the document to insert before adding the `_id` field would be
prohibitively expensive for most high write volume applications.

So the real problem is with MongoDB not returning an `_id`. If you want to
avoid this behavior and keep your data intact, you can either add an `_id`
yourself or:

    >>> doc = {'key': 'value'}
    >>> collection.insert(doc, manipulate=False)
    >>> doc
    {'key': 'value'}

Now if the document doesn't include an `_id`, one will be added by the server.
The server does not return the `_id` it created, so `None` is returned.

Here is an advantage to this design of adding the `_id` client side.
If the communication fails due to a network issue during an insert, you can
retry. If you get a `DuplicateKeyError`, then you know
the original attempt succeeded and vice-versa.






