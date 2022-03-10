# apollo-link-prismic

## Purpose

An Apollo Link that allow you query Prismic's GraphQL API with [apollo-client](https://www.apollographql.com/client/).

## Installation

```
npm install apollo-link-prismic
```

## Usage

```typescript
import { ApolloClient, InMemoryCache } from "@apollo/client";
import { createPrismicLink } from "apollo-link-prismic";

const apolloClient = new ApolloClient({
	link: createPrismicLink({
		repositoryName: "YOUR_REPOSITORY_NAME",
		// Provide your access token if your repository is secured.
		accessToken: "YOUR_ACCESS_TOKEN",
	}),
	cache: new InMemoryCache(),
});
```

### Providing a `fetch` function

If you are using this link in an environment where a global `fetch` function does not exist, such as Node.js, you must provide one using the `fetch` option.

Environments like the browser, [Next.js](https://nextjs.org/), [Cloudflare Workers](https://workers.cloudflare.com/), and [Remix](https://remix.run/) provide a global `fetch` function and do not require passing your own.

There are many libraries that can provide this function. The most common is [`node-fetch`](https://www.npmjs.com/package/node-fetch), which you would configure like this:

```typescript
import { ApolloClient, InMemoryCache } from "@apollo/client";
import { createPrismicLink } from "apollo-link-prismic";
import fetch from "node-fetch";

const apolloClient = new ApolloClient({
	link: createPrismicLink({
		repositoryName: "YOUR_REPOSITORY_NAME",
		// Provide your access token if your repository is secured.
		accessToken: "YOUR_ACCESS_TOKEN",
		fetch,
	}),
	cache: new InMemoryCache(),
});
```

### Installation with React Native

Using `apollo-link-prismic` in React Native applications requires additional setup.

After installing `apollo-link-prismic`, install the following [URL Web API](https://developer.mozilla.org/en-US/docs/Web/API/URL_API) polyfill:

```sh
npm install react-native-url-polyfill
```

Next, import the polyfill in your app’s entry file (typically this is App.js or index.js).

```javascript
// App.js or index.js

import "react-native-url-polyfill/auto";
```

`apollo-link-prismic` can now be used throughout your app.

**Note**: If the polyfill does not work after importing in your app's entry file, try the alternative ["Flexible" set up method described in `react-native-url-polyfill`'s documentation](https://github.com/charpeni/react-native-url-polyfill#option-2-flexible).
