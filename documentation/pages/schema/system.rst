.. _system:

System Information
^^^^^^^^^^^^^^^^^^

API returns details of ConfigHub License and version.

.. rst-class:: fa fa-inbox

- API URL:  ``https://confighub-api/rest/info/system``

.. note:: - All data returned is in JSON format.
   - All parameters are passed through HTTP header fields.
   - Method: GET

Example Usage
~~~~~~~~~~~~~

.. code-block:: bash

   curl -i https://api.confighub.com/rest/info/system  \
        -H "Client-Version: v1.5"                   \
        -H "Pretty: true/false"

.. code-block:: json

    HTTP/1.1 200 OK
    Date: Fri, 25 Nov 2016 19:55:01 GMT
    Content-Type: application/json
    Content-Length: 635
    Server: TomEE
    {
       "version": {
          "version": "v1.2.0"
       },
       "license": {
          "First Name": "John",
          "Last Name": "Doe",
          "Email": "john.doe@acme.com",
          "Company": "Acme Inc.",
          "Title": "CTO",
          "Type": "Trial",
          "Expires": "Wed, Mar 1, 2017",
          "LicenseKey": "..."
       }
    }


Request Headers
~~~~~~~~~~~~~~~

*Client-Version*

   Version of the client API. If not specified, ConfigHub assumes the latest version. Even through this is
   not a required parameter, you are encouraged to specify a version.

*Pretty*

   If value is ``true``, returned JSON is 'pretty' - formatted.

.. rst-class:: fa fa-fontawesome

   the fontawesome flag will be attached to this paragraph


.. rst-class:: fa fa-inbox

   the fontawesome flag will be attached to inbox this paragraph