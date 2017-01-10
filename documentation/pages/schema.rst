.. _schema:

The following sections explain the REST API schema for various programmatic interactions
with the ConfigHub service.


****
PULL
****

With fully specified context, pull configuration from ConfigHub service.
The JSON response may contain key-value pairs, as well as resolved files (as per request).

- API URL (with token):  ``https://confighub-api/rest/pull``
- API URL (no token):  ``https://confighub-api/rest/pull/<account>/<repository>``


.. note:: - All data returned is in JSON format.
- All dates are expected and returned in ``ISO 8601`` format (UTC): ``YYYY-MM-DDTHH:MM:SSZ``.
   - All parameters are passed through HTTP header fields.
   - Returned data will contain resolved properties and files, unless limited by the ``No-Properties`` or ``No-Files`` flags.
   - Method: GET


Usage
-----

.. code-block:: bash

   curl -i https://api.confighub.com/rest/pull \
        -H "Client-Token: <token>"             \
        -H "Context: <context>"                \
        -H "Application-Name: myApp"           \
        -H "Client-Version: v1.5"

.. code-block:: json

    HTTP/1.1 200 OK
    Date: Fri, 10 Jun 2016 22:38:13 GMT
    Content-Type: application/json
    Content-Length: 2167
    Server: TomEE
    {
      "generatedOn": "06/10/2016 22:38:13",
      "account": "ConfigHub",
      "repo": "Demo",
      "context": "Production;TimeKepper",
      "files": {
        "demo.props": "dbUrl \u003d jdbc:mysql://prod.mydomain.com:3306/ProdDatabase\n\ndbUser \u003d admin\n\ndbPass \u003d prod-password"
      },
      "properties": {
        "db.host": {
          "val": "prod.mydomain.com"
        },
        "server.http.port": {
          "val": "80"
        },
        "db.name": {
          "val": "ProdDatabase"
        },
        ...
        "db.user": {
          "val": "admin"
        }
      }
    }



Request Headers
---------------

*Client-Token*

   Client token identifies a specific repository. This field is not required if the account and repository
   are specified as part of the URL.


*Context*

   Context for the pull request has to be a fully-qualified-context (each context rank has to be specified -
   no wildcards). Context items are semi-colon delimited, and are ordered in order of have to be in context
   rank order. For example, a repository with context size of 3 levels ``Environment > Application > Instance``
   could be defined as::

   -H "Context:  Production;MyApp;MyAppInstance "


*Repository-Date*

   ISO 8601 date format (UTC) ``YYYY-MM-DDTHH:MM:SSZ`` lets you specify a point in time for which to pull
   configuration. If not specified, latest configuration is returned.

*Tag*

   Name of the defined tag. Returned configuration is for a point in time as specified by the tag. If both
   Tag and *Repository-Date* headers are specified, Repository-Date is only used if the tag is no longer
   available.

*Security-Profile-Auth*

   If a repository is enabled for and uses Security-Profiles (SP) with encryption, choose any of several
   ways to decrypt resolved property values.

   #. Server-Side decryption by providing SP name(s) and password(s):
      - Token is created that specifies SP name/password pairs;
      - SP name/password pairs are specified using this request parameter.

   #. Client-Side decryption is also available by:
      - Use of ConfigHub API in a selected language come functionality for local decryption;
      - A client can implement its own decryption;

   Security-Profile-Auth uses JSON format: ``{'Security-Profile_1':'password', 'Security-Profile_2':'password',...}``

*Client-Version*

   Version of the client API. If not specified, ConfigHub assumes the latest version. Even through this is
   not a required parameter, you are encouraged to specify a version.


*Application-Name*

   This field helps you identify application or a client pulling configuration. Visible in Pull Request tab.

*Include-Comments*

   If value is ``true`` response includes comments for property keys.

*Include-Value-Context*

   If value is ``true`` response includes context of resolved property values.

*Pretty*

   If value is ``true``, returned JSON is 'pretty' - formatted.

*No-Properties*

  If value is ``true`` key-value pairs are not returned. This is useful if you are only interested in
  pulling files, and want to make transaction more efficient.

*No-Files*

  If value is ``true`` resolved files are not returned. This is useful if you are only interested in
  pulling properties, and want to make transaction more efficient.





****
PUSH
****

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





****
INFO
****

This API provides information about a specific repository.  It allows for glob syntax search of
configuration files, and context definition.


- API URL (with token):  ``https://confighub-api/rest/info``
- API URL (no token):  ``https://confighub-api/rest/info/<account>/<repository>``


.. note:: - All data returned is in JSON format.
- All dates are expected and returned in ``ISO 8601`` format (UTC): ``YYYY-MM-DDTHH:MM:SSZ``.
   - All parameters are passed through HTTP header fields.
   - Method: GET

Usage
-----

.. code-block:: bash

   curl -i https://api.confighub.com/rest/info      \
        -H "Client-Token: <token>"                  \
        -H "Repository-Date: <ISO 8601 date (UTC)>" \
        -H "Tag: <repo tag>"                        \
        -H "Client-Version: v1.5"                   \
        -H "Files: true/false"                      \
        -H "Files-Glob: <glob expression>"          \
        -H "Context-Elements: true/false"           \
        -H "Context-Labels: <comma delimited list>" \
        -H "Pretty: true/false"

.. code-block:: json

    HTTP/1.1 200 OK
    Date: Wed, 16 Nov 2016 18:12:33 GMT
    Content-Type: application/json
    Content-Length: 483
    Server: TomEE
    {
       "account": "ConfigHub",
       "repository": "HowItWorks",
       "generatedOn": "11/16/2016 18:12:33",
       "context": [ "Environment", "Application" ],
       "contextElements":
       {
          "Environment": [ "Production", "Development" ],
          "Application": [ "Analytics", "Collector", "WebDashboard" ]
       },
       "files": [
          {
             "name": "nginx2.conf",
             "path": "nginx/nginx2.conf",
             "lastModified": 1479260284272
          }
       ]
    }


Request Headers
---------------

*Client-Token*

   Client token identifies a specific repository. This field is not required if the account and repository
   are specified as part of the URL.

*Repository-Date*

   ISO 8601 date format (UTC) ``YYYY-MM-DDTHH:MM:SSZ`` lets you specify a point in time for which to pull
   repository information. If not specified, latest information is returned.

*Tag*

   Name of the defined tag. Returned information is for a point in time as specified by the tag. If both
   Tag and *Repository-Date* headers are specified, Repository-Date is only used if the tag is no longer available.


*Client-Version*

   Version of the client API. If not specified, ConfigHub assumes the latest version. Even through this is
   not a required parameter, you are encouraged to specify a version.

*Files*

   Boolean flag to indicate if all files should be returned. If *Files-Glob* header is specified, this
   flag is ignored and treated true by default.

*Files-Glob*

   Enables glob expressions while searching for files over their path and name.

*Context-Elements*

   Boolean flag to indicate if all context elements should be returned. If *Context-Labels* header is
   specified, this flag is ignored and treated true by default.

*Context-Labels*

   Limit context elements returned by the list of context labels. Comma delimited list of context labels.

*Pretty*

   If value is ``true``, returned JSON is 'pretty' - formatted.



************
Repositories
************

Use this API to get full details of settings for all defined repositories.

- API URL:  ``https://confighub-api/rest/info/all``

.. note:: - All data returned is in JSON format.
- All dates are expected and returned in ``ISO 8601`` format (UTC): ``YYYY-MM-DDTHH:MM:SSZ``.
   - All parameters are passed through HTTP header fields.
   - Method: GET

Usage
-----

.. code-block:: bash

   curl -i https://api.confighub.com/rest/info/all  \
        -H "Client-Version: v1.5"                   \
        -H "Pretty: true/false"

.. code-block:: json

    HTTP/1.1 200 OK
    Date: Fri, 25 Nov 2016 19:47:39 GMT
    Content-Type: application/json
    Content-Length: 2776
    Server: TomEE
    [
      {
        "account": "ConfigHub",
        "name": "Demo",
        "isPrivate": false,
        "isPersonal": false,
        "description": "This is a demo repository. Saving changes is disabled for all options, however all options are available for you to explore.",
        "created": "2016-05-05T16:26Z",
        "accessControlsEnabled": false,
        "vdtEnabled": true,
        "securityEnabled": true,
        "contextGroupsEnabled": true,
        "keyCount": 27,
        "valueCount": 42,
        "userCount": 1,
        "context": [
          "Environment",
          "Application"
        ]
      },
      {
        "account": "ConfigHub",
        "name": "HowItWorks",
        "isPrivate": false,
        "isPersonal": false,
        "created": "2016-10-04T21:19Z",
        "accessControlsEnabled": false,
        "vdtEnabled": true,
        "securityEnabled": true,
        "contextGroupsEnabled": false,
        "keyCount": 13,
        "valueCount": 23,
        "userCount": 0,
        "context": [
          "Environment",
          "Application"
        ]
      }
    ]


Request Headers
---------------

*Client-Version*

   Version of the client API. If not specified, ConfigHub assumes the latest version. Even through this is
   not a required parameter, you are encouraged to specify a version.

*Pretty*

   If value is ``true``, returned JSON is 'pretty' - formatted.




*************
System Status
*************

API returns details of ConfigHub License and version.

- API URL:  ``https://confighub-api/rest/info/system``

.. note:: - All data returned is in JSON format.
- All parameters are passed through HTTP header fields.
   - Method: GET

Usage
-----

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
---------------

*Client-Version*

   Version of the client API. If not specified, ConfigHub assumes the latest version. Even through this is
   not a required parameter, you are encouraged to specify a version.

*Pretty*

   If value is ``true``, returned JSON is 'pretty' - formatted.
