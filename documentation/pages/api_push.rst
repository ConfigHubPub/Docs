===============
REST PUSH Api
===============

Push API allows clients to update or create properties, context values and tags.

Configuration PUSH

- API URL (with token):  ``https://confighub-api/rest/push``
- API URL (no token):  ``https://confighub-api/rest/push/<account>/<repositoryName>``


.. note:: - All data returned is in JSON format.
   - No data is returned.
   - Response code: 200 (Success); 304 (Not modified).
   - Method: POST



Example Push Request/Response
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   curl -i https://api.confighub.com/rest/push \
        -H "Content-Type: application/json" \
        -H "Client-Token: <token>" \
        -H "Client-Version: v1.5" \
        -H "Application-Name: myApp" \
        -X POST -d '
           "changeComment": Adding a new key and value",
           "enableKeyCreation": true,
           "data":'[
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
                   ]'