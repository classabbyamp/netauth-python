NetAuth for Python
==================

.. highlight:: python

A `NetAuth <https://netauth.org>`_ client library for Python.

To install: ``pip install netauth``

Usage
~~~~~

This library centers around the :class:`NetAuth` object::

   na = netauth.NetAuth("netauth.example.org")

   try:
       resp = na.system_status()
       print(resp)
   except netauth.error.NetAuthRpcError as e:
       print(f"Request failed: {e}")

   na.close()

:class:`NetAuth` can also be used as a context manager and be initialized from a NetAuth configuration file::


   with netauth.NetAuth.with_config(Path("/etc/netauth/config.toml")) as na:
       try:
           resp = na.system_status()
           print(resp)
       except netauth.error.NetAuthRpcError as e:
           print(f"Request failed: {e}")

For interactive or dynamic applications, operations that require authentication can use a callback to retrieve the user's secret::

   def secret_cb() -> str:
       return getpass(prompt="Secret: ")

   with netauth.NetAuth("netauth.example.org", entity="demo", secret=secret_cb) as na:
       try:
           na.entity_kv_add("demo", "foo", ["bar", "baz"])
       except error.NetAuthRpcError as e:
           print(f"Request failed: {e}")

API
~~~

.. currentmodule:: netauth

.. autoclass:: NetAuth
   :members:

Data Types
~~~~~~~~~~

.. autoclass:: EntityMeta
   :members:

.. autoclass:: Entity
   :members:

.. autoclass:: Group
   :members:

.. currentmodule:: netauth.v2

.. autoclass:: SubSystemStatus
   :members:

.. autoclass:: ServerStatus
   :members:

Enumerations
~~~~~~~~~~~~

.. currentmodule:: netauth

.. autoenum:: Capability

.. autoenum:: ExpansionMode

.. currentmodule:: netauth.v2

.. autoenum:: Action

.. autoenum:: RuleAction

Token Cache
~~~~~~~~~~~

.. currentmodule:: netauth.cache

.. autoclass:: TokenCache
   :members:

.. autoclass:: FSTokenCache
   :members:

.. autoclass:: MemoryTokenCache
   :members:


Exceptions
~~~~~~~~~~

.. currentmodule:: netauth.error

.. autoclass:: NetAuthException
   :members:

.. autoclass:: NetAuthRpcError
   :members:

.. autoclass:: RequestorUnqualifiedError
   :members:

.. autoclass:: MalformedRequestError
   :members:

.. autoclass:: InternalError
   :members:

.. autoclass:: UnauthenticatedError
   :members:

.. autoclass:: ReadOnlyError
   :members:

.. autoclass:: ExistsError
   :members:

.. autoclass:: DoesNotExistError
   :members:
