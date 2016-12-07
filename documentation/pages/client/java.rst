.. _java_client:

Java Client API
^^^^^^^^^^^^^^^

Java API provides full interface for configuration pull. In addition it adds several convenience utilities.



.. code-block:: java

    public static void main(String... args)
    {
        String token = "..."
        String context = "Production;Application;Instance";
        ConfigHub configHub = new ConfigHub(token, context)
                .applicationName("HelloConfigApp");

        CHProperties properties = configHub.getProperties();

        // Backup properties to a local file
        properties.toFile("properties.json");

        int dbPort = properties.getInteger("db.port");
        String dbHost = properties.get("db.host");
        String dbUser = properties.get("db.user");
        String dbPassword = properties.get("db.password");

        // Get a few files
        configHub.requestFile("demo.props");
        configHub.requestFile("foo");

        CHFiles files = configHub.getFiles();
        files.writeFile("demo.props", "demo.props");
        files.writeFile("foo", "foo");
    }

