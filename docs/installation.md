---
layout: default
title: Installation
nav_order: 2
---

# Installation
{: .no_toc }

This section describes the steps required to include the Autosuggest JS SDK and its default styles in your application.

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Prerequisite

Before proceeding with the installation of the Autosuggest JS SDK, you must complete the initial onboarding and configuration of your Unbxd account through the Self Serve Dashboard. This setup includes account registration, site creation, feed upload, and relevancy configuration, which are required for the SDK to function correctly.

Detailed guidance on completing the onboarding process is available in the Self Serve Dashboard documentation:
[Self Serve Dashboard Documentation](https://unbxd.com/docs/site-search/integration-documentation/onboarding-flow/)


---

## SDK Integration

Include the Vanilla JavaScript Search library by adding the following script tag to your HTML file:

```js
    <script src="https://libraries.unbxdapi.com/search-sdk/v1/autosuggest.min.js"></script>
```

  The latest available version of the library can be identified from the npm repository for the Search JS library or from the official ChangeLog.

To apply the default Search UI styles, include the corresponding stylesheet using the following link tag:
```js
    <link rel="stylesheet" type="text/css" href="https://libraries.unbxdapi.com/search-sdk/v<<latest-version>>/vanillaSearch.min.css" />
```
