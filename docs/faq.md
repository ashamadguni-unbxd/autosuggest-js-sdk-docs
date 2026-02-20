---
layout: default
title: FAQs
nav_order: 6
permalink: /faqs.html
---

# FAQs
{: .no_toc}

This page answers common questions about the Autosuggest JS SDK, including setup, configuration, behavior, and troubleshooting. For step-by-step integration, see [Getting Started](getting-started.html). For all configuration options, see [Configurations](configurations/configurations.html).

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## General queries

### What is the Autosuggest JS SDK?

The **Autosuggest JS SDK** is a lightweight JavaScript library that enables **real-time search suggestions** as users type into a search input. It helps guide users toward relevant queries and products by dynamically presenting suggestions based on partial input—reducing typing effort, minimizing zero-result searches, and improving overall search efficiency.

The SDK is designed to be easy to integrate and flexible to configure. It can be used with any web application, regardless of framework, and does not require build tools or additional dependencies. Once initialized, Autosuggest listens to user input events and fetches relevant suggestions from Unbxd in real time. By surfacing meaningful suggestions early in the search journey, it results in faster discovery, higher engagement, and a more intuitive search experience for end users.

---

### Do I need a framework to use the Autosuggest SDK?

No. The SDK is **framework-agnostic** and works with:

- **Vanilla JavaScript** — Plain HTML and JS, no build step required.
- **React, Vue, Angular, or other frameworks** — You can initialize the SDK in a lifecycle hook (e.g. `useEffect`, `mounted`) and pass the search input element or selector. Ensure the DOM element exists at the time of initialization.

The library is a single script that attaches to a search input and manages suggestions via the Unbxd API. Your application only needs to include the script, provide configuration (including `siteKey`, `apiKey`, and `searchInput`), and optionally customize templates and callbacks.

---

### What types of suggestions does the SDK support?

The Autosuggest SDK supports multiple suggestion types, each configurable via the [API configuration](configurations/api-configuration.html):

| Suggestion type | Description | Configuration |
|-----------------|-------------|---------------|
| **In-field suggestions** | Keyword suggestions matched against specific indexed fields (e.g. product name, category, brand). | `api.inFields.count` |
| **Popular products** | Frequently viewed or searched products relevant to the user’s input. | `api.popularProducts.count` |
| **Keyword suggestions** | Commonly searched or relevant keywords based on the user’s input. | `api.keywordSuggestions.count` |
| **Top queries** | Most frequently searched queries across the site. | `api.topQueries.count` |
| **Promoted suggestions** | Keywords or results boosted by merchandising rules in the Unbxd Console. | `api.promotedSuggestions.count` |

You can enable or disable categories and set how many results to fetch per category. Adjust these counts based on your UI space and performance needs; see [Best Practices](best-practices.html) for guidance on suggestion counts.

---

## Integration related queries

### How do I get an API key and Site key to use with the SDK?

To use the Autosuggest SDK, you need a valid **siteKey** and **apiKey** from your Unbxd account.

1. **Sign up or log in** at [Unbxd](https://unbxd.com/).
2. **Complete the self-serve FTU (First Time User) flow** — This includes account setup, site creation, feed upload, and relevancy configuration. Detailed guidance is available in the [Self Serve Dashboard Documentation](https://unbxd.com/docs/site-search/integration-documentation/onboarding-flow/).
3. **Obtain your keys** — Once your project and site are set up, locate the **API key** and **Site key** in the project dashboard (often displayed as long strings). Copy these and use them in your SDK configuration.
4. **Keep keys secure** — Treat these keys like any other sensitive credentials. Do not share them publicly or commit them in a way that violates your agreement. Use environment variables or secure config in production where appropriate.

The exact steps may vary depending on your plan and Unbxd’s current offerings. If you need help, refer to the Unbxd dashboard or contact Unbxd support. For integration steps using these keys, see [Getting Started](getting-started.html).

---

### How do I configure the SDK on my website?

Configuring the Autosuggest SDK involves **including the script** and **initializing the SDK** with the required and optional settings.

**1. Include the script (and optional styles)**

Add the Autosuggest script to your HTML, as described in [Installation](installation.html):

```html
<script src="https://libraries.unbxdapi.com/search-sdk/v1/autosuggest.min.js"></script>
```

To use the default Search UI styles, include the stylesheet:

```html
<link rel="stylesheet" type="text/css" href="https://libraries.unbxdapi.com/search-sdk/v<<latest-version>>/vanillaSearch.min.css" />
```

You can use the CDN (as above) or host the script and CSS yourself. The latest version can be identified from the npm repository or the official changelog.

**2. Initialize with at least the required fields**

You must provide:

- **siteKey** — Your Unbxd site key.
- **apiKey** — Your Unbxd API key.
- **searchInput** — A valid CSS selector (e.g. `".search-input"`) or DOM element for the search input to which Autosuggest will attach.

Example minimal configuration:

```js
const autosuggest = new Autosuggest({
  siteKey: "<<site key>>",
  apiKey: "<<api key>>",
  searchInput: ".search-input"
});
```

**3. Add optional configuration**

You can then customize behavior, API, DOM, and callbacks. For example:

- **Behavior** — `debounceDelay`, `minChars` (see [Behavior & Performance Configuration](configurations/behavior-configuration.html)).
- **API** — Suggestion types and counts (see [API Configuration](configurations/api-configuration.html)).
- **DOM** — `containerTag`, `attributes` (see [DOM Configuration](configurations/dom-configuration.html)).
- **Callbacks** — `onError`, and other lifecycle hooks (see [Callbacks Configuration](configurations/callback-configuration.html)).
- **Templates** — Custom UI (see [Customization](configurations/customization.html)).

A full example is available in [Getting Started](getting-started.html). For a complete list of options, see [Configurations](configurations/configurations.html).

---

### How can I test the SDK before deploying to production?

You can test the Autosuggest SDK safely by using a **sandbox or test environment** that is isolated from production.

- **Use separate credentials** — Create or use a test project in the Unbxd dashboard with its own **API key**, **site key**, and **index**. This keeps test traffic and configuration separate from your live site.
- **Use a test feed** — Upload and index a test feed (or a subset of data) so you can verify suggestion behavior without affecting production data.
- **Verify prerequisites** — Ensure your test site has completed the FTU flow and that required fields (e.g. title, imageUrl, price, categoryPath) are mapped correctly for the test feed.
- **Test on a staging URL** — Deploy the integration to a staging or development URL and verify initialization, suggestion display, and callbacks (e.g. `onSelect`, `onError`) before going live.

This approach lets you experiment with configuration, templates, and styling without impacting real users or production analytics.

---

### Can I use my own styles instead of the default SDK styles?

Yes. The default styles are **optional**. You can fully style the suggestion UI with your own CSS.

- If you **omit** the default stylesheet (`vanillaSearch.min.css`), the SDK still renders the suggestion box; you are responsible for all styling so that it matches your site.
- You can use the **attributes** configuration (e.g. `attributes: { class: ["my-autosuggest-box"] }`) to attach your own classes to the container for targeting with CSS.
- For full control over structure and markup, use a **custom template** (see [Customization](configurations/customization.html)). The template function receives suggestion data and returns an HTML string, which you can style entirely with your own classes and design system.

This makes it possible to align the autosuggest experience with your brand and layout without relying on the default theme.

---

## Behavior and usage

### When do suggestions appear, and how often are API calls made?

Suggestions are requested based on two main settings: **minChars** and **debounceDelay**.

- **minChars** — The minimum number of characters the user must type before an Autosuggest API call is triggered. The default is `3`. For example, with `minChars: 3`, typing "sh" will not trigger a request; "sho" will. This prevents too many requests for very short queries and can be set to `2` or `3` for a balanced experience (see [Best Practices](best-practices.html)).
- **debounceDelay** — The delay in **milliseconds** after the user stops typing before the API call is sent. For example, with `debounceDelay: 500`, rapid typing of "shoes" will result in one request 500 ms after the last keystroke, rather than a request on every character. This reduces the number of API calls and improves performance. A value of `0` disables debouncing (not recommended in production).

Both options are documented in [Behavior & Performance Configuration](configurations/behavior-configuration.html). Tuning them helps balance responsiveness with server load and rate limits.

---

### How do I handle suggestion clicks (when the user selects a suggestion)?

You can handle suggestion selection by using the appropriate **callback** provided by the SDK (e.g. **onSelect**, or the equivalent in your version). When the user clicks or selects a suggestion, this callback is invoked so you can run custom logic.

Common use cases include:

- **Navigating to a search results page** — Use the selected suggestion text (or associated data) to build the URL and redirect the user (e.g. `/search?q=selected-query`).
- **Updating the search input** — Set the input value to the selected suggestion and optionally submit the form or trigger a search.
- **Analytics and tracking** — Record the suggestion click for conversion or engagement analytics.

The exact callback name and parameters may vary by SDK version; refer to [Callbacks Configuration](configurations/callback-configuration.html) and the SDK reference for the current API. Implement this callback during initialization so that every selection is handled consistently.

---

### Does the Autosuggest SDK work on mobile and touch devices?

Yes. The SDK works on **mobile and touch devices**. It does not rely on mouse-only events; suggestions can be opened, scrolled, and selected via touch.

You can further optimize for small screens by:

- **Adjusting suggestion counts** — Request fewer suggestions per category on mobile to keep the dropdown compact and fast (see [API Configuration](configurations/api-configuration.html)).
- **Using responsive CSS** — Style the suggestion container and items with media queries so layout, font size, and spacing work well on narrow viewports.
- **Tuning behavior** — Consider slightly higher `minChars` or `debounceDelay` on mobile if you observe performance or UX issues, though the same configuration often works across devices.

No separate “mobile build” is required; a single integration works across desktop and mobile.

---

## Troubleshooting

### Suggestions are not showing. What should I check?

If suggestions do not appear, work through the following:

1. **Required configuration**  
   Ensure **siteKey**, **apiKey**, and **searchInput** are set correctly. Missing or wrong values can prevent the SDK from authenticating or attaching to the input. See [Getting Started](getting-started.html) and [Best Practices](best-practices.html).

2. **Search input element**  
   The element matching `searchInput` (selector or DOM reference) must **exist in the DOM** when the SDK is initialized. If you use a framework, initialize after the component has mounted and the input is rendered.

3. **Feed and index**  
   Your Unbxd feed must be **uploaded and indexed**, and the FTU flow completed. Required fields (e.g. title, imageUrl, price, categoryPath) should be mapped. Configuration attributes in the docs are based on sample feeds; your schema may differ.

4. **Browser console and network**  
   Open the browser’s developer tools:  
   - **Console** — Look for JavaScript errors (e.g. invalid config, missing element).  
   - **Network** — Check whether Autosuggest API requests are sent, and whether they return 200 with valid JSON. Failed or blocked requests (e.g. CORS, wrong endpoint) will prevent suggestions from appearing.

5. **Error callback**  
   Configure the **onError** callback (see [Callbacks Configuration](configurations/callback-configuration.html)) to log or report errors. This helps capture API failures, network issues, or invalid responses in production.

Addressing these areas usually resolves missing suggestions. If the issue persists, verify your Unbxd dashboard and account status and contact Unbxd support if needed.

---

### I am seeing too many API requests. How do I reduce them?

Too many requests are usually due to **no or low debouncing** or **low minChars**. Use the following to reduce load:

- **Enable debouncing** — Set **debounceDelay** to a value such as **300–500 ms**. This waits until the user pauses typing before sending a request, so rapid typing generates fewer calls. A value of **0** disables debouncing and is **not recommended in production** (see [Best Practices](best-practices.html)).
- **Increase minChars** — Use at least **2 or 3** characters (e.g. `minChars: 3`) so that very short partial queries do not trigger requests.
- **Review suggestion counts** — Lower `count` for each suggestion type in [API Configuration](configurations/api-configuration.html) if you do not need many results; this can also reduce response size and processing time.

These settings are documented in [Behavior & Performance Configuration](configurations/behavior-configuration.html). Balancing **debounceDelay** and **minChars** will significantly reduce the number of API calls while keeping the experience responsive.

---

For more detail, see [Getting Started](getting-started.html), [Configurations](configurations/configurations.html), and [Best Practices](best-practices.html).
