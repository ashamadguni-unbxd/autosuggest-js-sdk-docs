---
layout: default
title: Introduction
description: New Autosuggest SDK Documentation
nav_order: 1
has_children: true
permalink: /
---

# New Autosuggest SDK Documentation

A JavaScript SDK for building **fast, real-time autosuggest experiences** powered by Unbxd.
Built with modern JavaScript and designed to work seamlessly **without jQuery or other legacy dependencies**.

<div class="mt-6">
  <a href="/autosuggest-js-sdk/installation.html" class="btn btn-primary mr-2">
    Get started now
  </a>
  <a href="https://github.com/unbxd/autosuggest-js-sdk" class="btn btn-outline" target="_blank">
    View it on GitHub
  </a>
</div>

{: .important }
> ###IMPORTANT
> This documentation is intended for customers using the new version of the Autosuggest JS SDK (V2 integrations).
> If you are using the previous version of the Autosuggest SDK, please refer to the  
> [Legacy Autosuggest SDK Documentation](https://ashamadguni-unbxd.github.io/autosuggest-js-sdk-docs/).
> As part of our upgrade process, the older version will be gradually deprecated.

---

## Introduction

The **New Autosuggest SDK** is a lightweight JavaScript library that enables
real-time search suggestions as users type into a search input. It helps guide
users toward relevant queries and products by dynamically presenting suggestions
based on partial input.

By surfacing meaningful suggestions early in the search journey, the new Autosuggest SDK
reduces typing effort, minimizes zero-result searches, and improves overall
search efficiency. This results in faster discovery, higher engagement, and a
more intuitive search experience for end users.

The SDK is designed to be easy to integrate and flexible to configure. It can be
used with any web application—regardless of framework—and does not require build
tools or additional dependencies. Once initialized, the new Autosuggest SDK listens to user
input events and fetches relevant suggestions from Unbxd in real time.

This documentation provides a complete reference for integrating and using the
New Autosuggest SDK, including setup instructions, configuration options,
available methods, event callbacks, and best practices for implementation.


---

## What is the New Autosuggest SDK?

The **New Autosuggest SDK** is a JavaScript library that enables real-time
suggestions in a search input as users type. It helps guide users toward relevant
queries by dynamically displaying suggestions based on partial input.

The SDK supports multiple suggestion types, allowing applications to present
contextual and relevant options during the search interaction. By surfacing
suggestions early, the new Autosuggest SDK improves search usability and reduces the effort
required to complete a query.

Supported suggestion types include:

- Keyword and query suggestions
- Popular search terms
- In-field suggestions during typing
- Promoted suggestions
- Top search queries

---

## Why use the New Autosuggest SDK?

- **Lightweight** — Designed with a minimal footprint, built **without jQuery or external dependencies**, ensuring fast load times and optimal performance.
- **Simple integration** — Easily integrates with plain JavaScript and does not require a build step or additional tooling.
- **Configurable** — Offers flexible configuration options along with event callbacks to customize behavior and UI interactions.
- **Improves search usability** — Enhances the search experience by helping users refine queries efficiently as they type.
- **Framework-agnostic** — Works seamlessly with any frontend framework or vanilla JavaScript applications.


---

## Quick links

- [Installation](installation.html)
- [Getting Started](getting-started.html)
- [Changelogs](changelog.html)
- [Configurations](configurations.html)
- [Usecases](usecases.html)
- [Best Practices](best-practices.html)
- [FAQs](faqs.html)
