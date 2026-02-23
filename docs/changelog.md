---
layout: default
title: Changelogs
nav_order: 3
permalink: /changelog.html
---

# Changelogs

{: .important }
> **Important**
>
> This document is for the **New Autosuggest SDK** (vanilla JavaScript, no jQuery). If you are on the legacy Autosuggest JS SDK, refer to the [Legacy Autosuggest SDK Documentation](https://ashamadguni-unbxd.github.io/autosuggest-js-sdk-docs/). We recommend integrating and staying on the latest version of the New Autosuggest SDK.

---

## v1.0.0

- **Release date:** Initial release
- **Core SDK Version:** v1.0.0
- **CDN Link:** <https://libraries.unbxdapi.com/search-sdk/v1/autosuggest.min.js>
- **CSS Link:** <https://libraries.unbxdapi.com/search-sdk/v1/vanillaSearch.min.css>

### Features

- Real-time autosuggest as users type in a search input.
- No jQuery or external library dependencies; vanilla JavaScript only.
- Configurable suggestion types: in-field, keyword suggestions, top queries, promoted suggestions, popular products, trending searches.
- Custom template support for full control over suggestion UI markup and styling.
- Lifecycle event callback (`onEvent`) for analytics, error handling, and integration.
- Configurable debounce and minimum character threshold for API requests.
- Framework-agnostic; works with any frontend or plain HTML/JS.
