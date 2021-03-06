Base for Everything
===================

To use the API, the :class:`Client <gcloud.bigtable.client.Client>`
class defines a high-level interface which handles authorization
and creating other objects:

.. code:: python

    from gcloud.bigtable.client import Client
    client = Client()

Long-lived Defaults
-------------------

When creating a :class:`Client <gcloud.bigtable.client.Client>`, the
``user_agent`` and ``timeout_seconds`` arguments have sensible
defaults
(:data:`DEFAULT_USER_AGENT <gcloud.bigtable.client.DEFAULT_USER_AGENT>` and
:data:`DEFAULT_TIMEOUT_SECONDS <gcloud.bigtable.client.DEFAULT_TIMEOUT_SECONDS>`).
However, you may over-ride them and these will be used throughout all API
requests made with the ``client`` you create.

Authorization
-------------

- For an overview of authentication in ``gcloud-python``,
  see :doc:`gcloud-auth`.

- In addition to any authentication configuration, you can also set the
  :envvar:`GCLOUD_PROJECT` environment variable for the project you'd like
  to interact with. If you are Google App Engine or Google Compute Engine
  this will be detected automatically. (Setting this environment
  variable is not required, you may instead pass the ``project`` explicitly
  when constructing a :class:`Client <gcloud.storage.client.Client>`).

- After configuring your environment, create a
  :class:`Client <gcloud.storage.client.Client>`

  .. code::

     >>> from gcloud import bigtable
     >>> client = bigtable.Client()

  or pass in ``credentials`` and ``project`` explicitly

  .. code::

     >>> from gcloud import bigtable
     >>> client = bigtable.Client(project='my-project', credentials=creds)

.. tip::

    Be sure to use the **Project ID**, not the **Project Number**.

Admin API Access
----------------

If you'll be using your client to make `Cluster Admin`_ and `Table Admin`_
API requests, you'll need to pass the ``admin`` argument:

.. code:: python

    client = bigtable.Client(admin=True)

Read-Only Mode
--------------

If on the other hand, you only have (or want) read access to the data,
you can pass the ``read_only`` argument:

.. code:: python

    client = bigtable.Client(read_only=True)

This will ensure that the
:data:`READ_ONLY_SCOPE <gcloud.bigtable.client.READ_ONLY_SCOPE>` is used
for API requests (so any accidental requests that would modify data will
fail).

Next Step
---------

After a :class:`Client <gcloud.bigtable.client.Client>`, the next highest-level
object is a :class:`Cluster <gcloud.bigtable.cluster.Cluster>`. You'll need
one before you can interact with tables or data.

Head next to learn about the :doc:`bigtable-cluster-api`.

.. _Cluster Admin: https://github.com/GoogleCloudPlatform/cloud-bigtable-client/tree/master/bigtable-protos/src/main/proto/google/bigtable/admin/cluster/v1
.. _Table Admin: https://github.com/GoogleCloudPlatform/cloud-bigtable-client/tree/master/bigtable-protos/src/main/proto/google/bigtable/admin/table/v1
