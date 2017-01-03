.. _push:

Configuration PUSH
^^^^^^^^^^^^^^^^^^

Push API allows clients to update or create properties, context values and tags.

- API URL (with token):  ``https://confighub-api/rest/push``
- API URL (no token):  ``https://confighub-api/rest/push/<account>/<repository>``

.. note:: - All data returned is in JSON format.
   - No data is returned.
   - Response code: 200 (Success); 304 (Not modified).
   - Method: POST

Usage
-----

.. code-block:: bash

   curl -i https://api.confighub.com/rest/push \
        -H "Content-Type: application/json" \
        -H "Client-Token: <token>" \
        -H "Client-Version: v1.5" \
        -H "Application-Name: myApp" \
        -X POST -d '
        {
           "changeComment": "Adding a new key and value",
           "enableKeyCreation": true,
           "data": [
                     {
                       "key": "propertyKey",
                       "readme": "",
                       "deprecated": false,
                       "vdt": "Text",
                       "push": true,
                       "securityGroup": "",
                       "password": "",
                       "values": [
                         {
                           "context": "el;*;el2",
                           "value": "",
                           "active": true
                         },
                         {
                           "context": "el;*;*",
                           "value": "",
                           "active": true
                         }
                       ]
                     }
                   ]
          }'
.. code-block:: bash

   Successful Response:

   HTTP/1.1 200 OK
   Date: Tue, 15 Nov 2016 17:15:43 GMT
   Content-Length: 0
   Server: TomEE


   Error Response:

   HTTP/1.1 304 Not Modified
   Date: Tue, 15 Nov 2016 02:49:23 GMT
   ETag: "Invalid password specified."
   Server: TomEE


Request Headers
---------------

*Content-Type*  **Required**

   Content-type header attribute must be set to ``application/json``.

*Client-Token*

   Client token identifies a specific repository. This field is not required if the account and repository
   are specified as part of the URL.

*Client-Version*

   Version of the client API. If not specified, ConfigHub assumes the latest version. Even through this is
   not a required parameter, you are encouraged to specify a version.


*Application-Name*

   This field helps you identify application or a client pushing configuration.  Visible in Pull Request tab.
