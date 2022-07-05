# RSS.app Node.js Library

[![Version](https://img.shields.io/npm/v/rss-generator-api.svg)](https://www.npmjs.org/package/rss-generator-api)
[![Try on RunKit](https://badge.runkitcdn.com/rss-generator-api.svg)](https://npm.runkit.com/rss-generator-api)

The rss-generator-api library provides convenient access to the RSS.app API from
applications written in JavaScript.

## Documentation

See the [ API docs](https://rss.app/docs/api) for Node.js.

## Requirements

Node 8 or higher.

## Installation

Install the package with:

```sh
npm install rss-generator-api --save
# or
yarn add rss-generator-api
```

## Usage

The package needs to be configured with your account's api and secret key, which is
available in the [RSS.app Dashboard](https://rss.app/docs/api/authentication). Require it with the key's
value:

<!-- prettier-ignore -->
```js
const RssApp = require('rss-generator-api');

const rssApp = new RssApp({ apiKey:  'c_...', apiSecret:  's_...' });

rssApp.feed
  .create({ url:  'https://bbc.com' })
  .then((feed) => {
     console.log('Success', feed);
  })
  .catch((err) => {
    console.log('Error', err);
  });
```

Or using ES modules and `async`/`await`:

```js
import RssApp from 'rss-generator-api';
const rssApp = new RssApp({ apiKey: 'c_...', apiSecret: 's_...' });

(async () => {
  const feed = await rssApp.feed.create({ url: 'https://bbc.com' });

  console.log(feed.id);
})();
```

### Usage with TypeScript

RSS.app maintains types.

```ts
import RssApp, { RssAppFeed } from 'rss-generator-api';
const rssApp = new RssApp({ apiKey: 'c_...', apiSecret: 's_...' });

const createFeed = async () => {
  const feed: RssAppFeed = await rssApp.feed.create({ url: 'https://bbc.com' });

  console.log(feed.id);
};
createFeed();
```

### Using Promises

Every method returns a chainable promise which can be used instead of a regular
callback:

```js
// Create a new feed and then list all feeds in account:
rssApp.feed
  .create({
    url: 'https://bbc.com',
  })
  .then((feed) => {
    return rssApp.feed
      .list({
        limit: 10,
        offset: 0,
      })
      .then((res) => {
        console.log(res.data);
      })
      .catch((err) => {
        // Deal with an error
      });
  });
```

## More Information

- [Error Handling](https://rss.app/docs/api/errors)
- [Pagination](https://rss.app/docs/api/pagination)
