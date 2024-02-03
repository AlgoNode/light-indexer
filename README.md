# Algorand Light Indexer

Host you own Algorand indexer API in under 15 minutes:
* 100% compatible with upstream Indexer API
* Even faster than Nodely.io cloud service
* Requires <25GB of SSD 
* *[optionally]* Go fully independent by adding a follower node

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
* Cloudflare hosted  DB snapshots (up to 3 hrs old) for fast catchup

## TODO
* ARM images (sorry)
* Auto update container
* Documentation
* Testnet 

## Requirements

* 25GB of free SSD space 
* docker-compose
* jq
* bash

# Quickstart

```bash
git clone https://github.com/AlgoNode/light-indexer.git
#make sure you have 20GB in the current dir 

cd light-indexer
./bin/init

#enjoy mainnet indexer in under 20 minutes
```

# Security

* Database and Indexer API endpoints are exposed, by default, on localhost only.
* CockroachDB runs in insecure mode (no authentication)

If you want to expose Indexer API to the World you can use:
* Development
  * [cloudflare tunnels](https://developers.cloudflare.com/pages/how-to/preview-with-cloudflare-tunnel/)
  * [ngrok tunnels](https://ngrok.com/product/secure-tunnels)
  * Caddy proxy
* Production
  * ...


# Scripts

## Diagnostic scripts 
| Script  | Description |
| ------------- | ------------- | 
| `bin/help`  | Show your API endpoint address & token |
| `bin/logs`  | Tail logs from all services |
| `bin/status`  | Show if your indexer is lagging |

## Safe scripts (should not break stuff)

| Script  | Description | Example |
| ------------- | ------------- | ------------- |
| `bin/down`  | Shutdown whole bundle |
| `bin/down ...`  | Shutdown a service | `/bin/down conduit`
| `bin/up`  | Start whole bundle |
| `bin/up ...`  | Start a service | `/bin/up api`
| `bin/restart ...`  | Start a service | `/bin/restart api`
| `bin/update`  | Download new images and restart services |

## Dangerous scripts (might break stuff)

| Script  | Description |
| ------------- | ------------- | 
| `bin/catchup`  | Destroy and download fresh database |
| `bin/gencfg`  | Regenerate configs  | 
| `bin/upgrade`  | Major upgrade |
