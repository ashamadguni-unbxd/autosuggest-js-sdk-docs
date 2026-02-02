---
layout: default
title: API Configuration
parent: Configurations
nav_order: 5
---

## API Configuration

The API configuration controls how Autosuggest communicates with the Unbxd backend. It allows you to define the API endpoint and fine-tune the types and number of suggestions fetched for each autosuggest request. These settings help tailor the autosuggest experience to match business priorities and user behavior.

---

## api
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

The `api` object groups all API-related configuration options. It defines which suggestion categories are enabled, how many results should be returned for each category, and the endpoint used to fetch autosuggestion data from Unbxd.

If not provided, Autosuggest uses default values for all API settings.

### Default Value
```js
api: {
  apiEndpoint: "https://search.unbxd.io",
  inFields: { count: 2 },
  popularProducts: { count: 3 },
  keywordSuggestions: { count: 2 },
  topQueries: { count: 2 },
  promotedSuggestions: { count: 2 }
}
```

---

## api.apiEndpoint
{: .d-inline-block }
String
{: .label }
Optional
{: .label .label-blue }

Specifies the base URL for the Unbxd Search API used to fetch autosuggestion data. In most cases, the default endpoint should be used. This option is primarily useful for advanced setups such as private cloud deployments or custom routing.

### Default Value
```js
apiEndpoint: "https://search.unbxd.io"
```

Example Usage:
```js
const autosuggest = new Autosuggest({
  api: {
    apiEndpoint: "https://search.unbxd.io"
  }
});
```

---

## api.inFields
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Configures **in-field suggestions**, which are keyword suggestions matched against specific indexed fields (such as product name, category, or brand). These suggestions help users refine their search intent as they type.

### api.inFields.count
{: .d-inline-block }
Number
{: .label }
Optional
{: .label .label-blue }

Defines the number of in-field suggestions to fetch per autosuggest request.

### Default Value
```js
count: 2
```

Example Usage:
```js
const autosuggest = new Autosuggest({
  api: {
    inFields: { count: 5 }
  }
});
```


---

## api.popularProducts
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Configures **popular product suggestions**, which surface frequently viewed or searched products relevant to the user’s input. These suggestions help promote trending or high-interest products directly within autosuggest.

### api.popularProducts.count
{: .d-inline-block }
Number
{: .label }
Optional
{: .label .label-blue }

Specifies the number of popular product suggestions to retrieve.

### Default Value
```js
count: 3
```

Example Usage:
```js
const autosuggest = new Autosuggest({
  api: {
    popularProducts: { count: 5 }
  }
});
```


---

## api.keywordSuggestions
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Configures **keyword-based suggestions**, which recommend commonly searched or relevant keywords based on the user’s input. These suggestions are useful for guiding users toward popular or high-conversion queries.

### api.keywordSuggestions.count
{: .d-inline-block }
Number
{: .label }
Optional
{: .label .label-blue }

Defines the number of keyword suggestions to fetch.

### Default Value
```js
count: 2
```

Example Usage:
```js
const autosuggest = new Autosuggest({
  api: {
    keywordSuggestions: { count: 5 }
  }
});
```


---

## api.topQueries
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Configures **top search query suggestions**, which display the most frequently searched queries across the site. These suggestions help users discover popular searches even with minimal input.

### api.topQueries.count
{: .d-inline-block }
Number
{: .label }
Optional
{: .label .label-blue }

Specifies the number of top search queries to include in autosuggest results.

### Default Value
```js
count: 2
```

Example Usage:
```js
const autosuggest = new Autosuggest({
  api: {
    topQueries: { count: 5 }
  }
});
```


---

## api.promotedSuggestions
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Configures **promoted suggestions**, which allow specific keywords or results to be boosted or prioritized based on merchandising rules configured in the Unbxd Console.

### api.promotedSuggestions.count
{: .d-inline-block }
Number
{: .label }
Optional
{: .label .label-blue }

Defines the number of promoted suggestions to fetch.

### Default Value
```js
count: 2
```

Example Usage:
```js
const autosuggest = new Autosuggest({
  api: {
    promotedSuggestions: { count: 5 }
  }
});
```

