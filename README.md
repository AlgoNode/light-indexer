# Algorand light-indexer

## Ingridients

* Postgres compatible CockroachDB
* Custom DB schema with extra indexes
* Custom conduit import plugin
  * Sources blocks and deltas from Nodely.io instant follower service
  * https://github.com/AlgoNode/conduit-cockroachdb
  * https://github.com/AlgoNode/blocksrv
* Custom conduit export plugin
  * Writes to custom DB schema
  * Prunes txn, txn_participation, block_headers to keep last 20k blocks
  * https://github.com/AlgoNode/conduit-cockroachdb
* Custom indexer-api
  * Custom DB schema
  * Indexed Note prefix search
  * Faster pagination
  * Faster everything ;)
  * https://github.com/AlgoNode/indexer-api-cdb
* Cloudflare hosted hourly DB snapshots for fast catchup

## Requirements

* Intel/AMD arch (sorry)
* docker-compose
* jq
* bash

## Quickstart


```bash
git clone https://github.com/AlgoNode/light-indexer.git
#make sure you have 20GB in the current dir 

cd light-indexer
./bin/init

#enjoy mainnet indexer in under 20 minutes
```
