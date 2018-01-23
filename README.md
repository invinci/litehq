# About
Single mono-repo containing all of Lite HQ code.

# Tech Stack
- react native
- couchbase server
- couchbase sync gateway
- couchbase lite
- redux

# Setup

Please read and follow the instruction [here](docs/setup.md)

# Lint

- `yarn run lint` Lint all modified JS files
- `yarn run lint:all` Lint all JS files under src directory

# Tests

- `yarn global add jest-cli` or `npm i jest-cli -g`
- execute command `jest` to run specs

# Backend User interfaces

Provided you have the backend up and running locally using `docker-compose up` you can access backend interfaces:

- `http://localhost:8091` Couchbase DB
- `http://localhost:4985/_admin/` Couchbase sync gateway admin

# Debugging Hints

- Authentication requires running a tunnel (see `tunnel.sh`). For development you will need to be setup in auth0.

# Auth0

View auth0 logs `wt logs -p "lite-au-logs"`

# Changing Sync Function

If the sync function requires changes, documents stored need to be reindexed. Reindexing is not done automatically and can be performed by taking db off, resyncing, bringing db back online again. More info can be found in the links below:

- http://developer.couchbase.com/documentation/mobile/1.2/develop/references/sync-gateway/admin-rest-api/database-admin/post-db-offline/index.html
- http://developer.couchbase.com/documentation/mobile/1.2/develop/references/sync-gateway/admin-rest-api/database-admin/post-db-resync/index.html
- http://developer.couchbase.com/documentation/mobile/1.2/develop/references/sync-gateway/admin-rest-api/database-admin/post-db-online/index.html

```bash
http POST <couchbase-sync-admin-api>/litehq/_offline && \
  http POST <couchbase-sync-admin-api>/litehq/_resync && \
  http POST <couchbase-sync-admin-api>/litehq/_online
```

# Releasing the app

Ensure that the correct config is not commented out in config.js.

# Hockeyapp

## Adding user to provisioning profile
- Add user to Hockeyapp
- Once user has registered, add their device UUID to apple developer portal
- Regenerate provisioning profile `sigh --adhoc -u dev@getlitenow.com -a me.litehq.LiteHQMobile -n "LiteHQ UAT" --force`
- Release a new version of the app to hockeyapp

## Releasing
- Connect iphone to mac
- In xcode - `Product -> Build` then `Product -> Archive`
- Hockey app should launch and you can click upload

# App store
- `gym`
- `deliver --ipa build/LiteHQMobile.ipa`

# Code push

Install code push cli: `yarn global add code-push-cli`

Any updates made through code push should not contain native code updates. It's best to limit lib updates as much as possible just in case and changes should only be made to javascript files. To run execute the command:

`code-push release-react litehq ios --entryFile index.ios.js -d Staging`

# Libraries to explore
- https://github.com/morcmarc/react-native-cognito
- https://github.com/exponentjs/react-native-loading-container
- https://github.com/Enrise/react-native-nmrangeslider-ios

# look into
- https://dzone.com/articles/couchbase-cluster-using-docker-compose

# Helpful
- https://github.com/couchbaselabs/mini-hacks
- https://github.com/vladoatanasov/docker-cbsg
- https://github.com/reindexio/reindex-examples/tree/master/react-native-gallery
