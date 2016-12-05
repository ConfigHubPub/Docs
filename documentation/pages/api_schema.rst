REST API Schema
===============

The **REST API** specifies an interface for configuration push, pull and info.

* :ref:`api-pull`
* :ref:`api-push`


.. _api-pull:

Configuration PULL
~~~~~~~~~~~~~~~~~~

- API URL (with token):  ``https://confighub-api/rest/pull``
- API URL (no token):  ``https://confighub-api/rest/pull/<account>/<repositoryName>``

.. info::
    - All data returned is in JSON format.
    - All dates are expected and returned in ISO 8601 format (UTC): YYYY-MM-DDTHH:MM:SSZ.
    - All parameters are passed through HTTP header fields.
    - Method: GET

**Example of API Pull Request/Response:**

.. code-block:: bash
    curl -i https://api.confighub.com/rest/pull \
         -H "Client-Token: <token>"             \
         -H "Context: <context>"                \
         -H "Application-Name: myApp"           \
         -H "Client-Version: v1.5"              \
         -H "Files: demo.props"

.. code-block:: json
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

.. _api-push:

Configuration PUSH
~~~~~~~~~~~~~~~~~~
