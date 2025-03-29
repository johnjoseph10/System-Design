# TEST

The Index Tool facilitates the migration of indexes metadata (excluding data) between document databases deployments.

Supported source: 
 - Amazon DocumentDB (any version)
 - MongoDB (2.x and later versions) standalone, replicaset or sharded cluster
 - Azure Cosmos DB

Supported target: 
 - Amazon DocumentDB (any version)


## TEST

- Export indexes metadata from a running MongoDB or Amazon DocumentDB deployment
- Checks for any unsupported indexes types or collections options with Amazon DocumentDB
- Check index and collections options compatibility against a logical backup, taken with mongodump. The backup has to be uncompressed.
- Restores supported indexes to Amazon DocumentDB (instance based or Elastic cluster)
- Output is a json file, similar to mongodump format
- Supports creation of 2dsphere indexes using the *--support-2dsphere* command line option