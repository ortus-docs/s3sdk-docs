# Configuration

The module is configured by default with a single migration service that interact with your database, optionally using qb. Multiple migration services with different managers may also be configured. The default manager for the cfmigrations is `QBMigrationManager`, but you may use others, such as those included with the `cbmongodb` and `cbelasticsearch` modules or roll your own.

The default configuration for the module settings are:

```cfc
moduleSettings = {
    "cfmigrations" : {
        "managers" : {
            "default" : {
                // The manager handling and executing the migration files
                "manager" : "cfmigrations.models.QBMigrationManager",
                // The directory containing the migration files
                "migrationsDirectory" : "/resources/database/migrations",
                // The directory containing any seeds, if applicable
                "seedsDirectory" : "/resources/database/seeds",
                // A comma-delimited list of environments which are allowed to run seeds
                "seedEnvironments" : "development",
                "properties" : {
                    "defaultGrammar" : "BaseGrammar@qb"
                }
            }
        }
    }
}
```

With this configuration, the `default` migration manager may be retrieved via WireBox at `migrationService:default`.

Here is an example of a multi-manager migrations system. Each separate manager will require their own configuration properties.

```cfc
moduleSettings = {
    "cfmigrations": {
        "managers": {
            "db1": {
                "manager": "cfmigrations.models.QBMigrationManager",
                "migrationsDirectory": "/resources/database/db1/migrations",
                "seedsDirectory": "/resources/database/db1/seeds",
                "properties": {
                    "defaultGrammar": "MySQLGrammar@qb",
                    "datasource": "db1",
                    "useTransactions": "false",    
                }
            },
            "db2": {
                "manager": "cfmigrations.models.QBMigrationManager",
                "migrationsDirectory": "/resources/database/db2/migrations",
                "seedsDirectory": "/resources/database/db2/seeds",
                "properties": {
                    "defaultGrammar": "PostgresGrammar@qb",
                    "datasource": "db2",
                    "useTransactions": "true"    
                }
            },
            "elasticsearch": {
                "manager": "cbelasticearch.models.migrations.Manager",
                "migrationsDirectory": "/resources/elasticsearch/migrations"
            }
        }
    }
};
```

With this configuration the individual migration managers would be retreived as such:

* `db1` - getInstance( "migrationService:db1" )
* `db2` - getInstance( "migrationService:db2" )
* `elasticsearch` - getInstance( "migrationService:elasticsearch" )
