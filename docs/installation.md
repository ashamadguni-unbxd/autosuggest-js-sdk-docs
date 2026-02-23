---
layout: default
title: Installation
nav_order: 2
---

# Installation
{: .no_toc }

This section describes the steps required to include the New Autosuggest SDK and its default styles in your application.

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Prerequisites

Before installing the New Autosuggest SDK, complete the initial onboarding and configuration of your Unbxd account in the Self Serve Dashboard. Required steps include account registration, site creation, feed upload, and relevancy configuration.

For detailed guidance, see the [Self Serve Dashboard Documentation](https://unbxd.com/docs/site-search/integration-documentation/onboarding-flow/).

---

## SDK Integration

Add the New Autosuggest SDK by including the following script tag in your HTML:

```html
<script src="https://libraries.unbxdapi.com/search-sdk/v<<latest-version>>/autosuggest.min.js"></script>
```

The latest version identifier is available in the [new autosuggest js library](https://www.npmjs.com/package/@unbxd-ui/autosuggest-js-sdk) or the [Changelogs](changelog.html) for this SDK.

To use the default search UI styles, include the following stylesheet:

To apply the default Search UI styles, include the corresponding stylesheet using the following link tag:
```js
    <link rel="stylesheet" type="text/css" href="https://libraries.unbxdapi.com/search-sdk/v<<latest-version>>/vanillaSearch.min.css" />
```
