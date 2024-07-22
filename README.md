# mongo-cmd

List out basic commands to use MongoDB Community Edition 7.0 with MacOS

## Installation:

1. Tap [the MongoDB Homebrew Tap](https://github.com/mongodb/homebrew-brew) to download the official Homebrew formula for MongoDB and the Database Tools:

```bash
brew tap mongodb/brew
```

2. To update Homebrew and all existing formulae:

```bash
brew update
```

3. To install MongoDB:

```bash
brew install mongodb-community@7.0
```

The installation includes the following binaries:

- The [mongod](https://www.mongodb.com/docs/manual/reference/program/mongod/#mongodb-binary-bin.mongod) server
- The [mongos](https://www.mongodb.com/docs/manual/reference/program/mongos/#mongodb-binary-bin.mongos) sharded cluster query router
- The MongoDB Shell, [mongosh](https://www.mongodb.com/docs/mongodb-shell/#mongodb-binary-bin.mongosh)

|                        | Intel Processor            | Apple Silicon Processor       |
| ---------------------- | -------------------------- | ----------------------------- |
| **configuration file** | /usr/local/etc/mongod.conf | /opt/homebrew/etc/mongod.conf |
| **log directory**      | /usr/local/var/log/mongodb | /opt/homebrew/var/log/mongodb |
| **data directory**     | /usr/local/var/mongodb     | /opt/homebrew/var/mongodb     |

## Run MongoDB Community Edition

### As a MacOS service

- To run MongoDB (i.e. the mongod process) as a macOS service, run:

  ```bash
  brew services start mongodb-community@7.0
  ```

- To stop a mongod running as a macOS service:

  ```bash
  brew services stop mongodb-community@7.0
  ```

- To verify that MongoDB is running

  ```bash
  brew services list
  ```

### As a background process

- To run mongod manually using a config file, run:

  For macOS running Intel processors:

  ```bash
  mongod --config /usr/local/etc/mongod.conf --fork
  ```

  For macOS running on Apple Silicon processors:

  ```bash
  mongod --config /opt/homebrew/etc/mongod.conf --fork
  ```

- To run mongod manually specifying --dbpath and --logpath on the command line, run:

  ```bash
  mongod --dbpath /path/to/dbdir --logpath /path/to/mongodb.log --fork
  ```

- To stop a mongod running, connect to the mongod using mongosh, and issue the `shutdown` command as needed.

- To verify that MongoDB is running:

  ```bash
  ps aux | grep -v grep | grep mongod
  ```

  Log file of mongod process: `/usr/local/var/log/mongodb/mongo.log`.

## Connect and Use MongoDB

To begin using MongoDB, connect mongosh to the running instance. From a new terminal, issue the following:

- monitoring tools:

```bash
mongosh
```

## Configuration file

- To view:

  ```bash
  cat /opt/homebrew/etc/mongod.conf
  ```

  Output:

  ```
  systemLog:
    destination: file
    path: /opt/homebrew/var/log/mongodb/mongo.log
    logAppend: true
  storage:
    dbPath: /opt/homebrew/var/mongodb
  net:
    bindIp: 127.0.0.1, ::1
    ipv6: true
  ```

## References:

- https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/
