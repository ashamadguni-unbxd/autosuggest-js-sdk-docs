---
layout: default
title: Getting Started – Autosuggest SDK
nav_order: 3
---

# Getting Started – Autosuggest SDK

## Table of Contents
- Prerequisite
- Integration Instructions
- Complete Example
- Default Configuration
- Notes & Best Practices
- API Response Structure
- FAQs

---

## Prerequisite

Before integrating the Autosuggest SDK, ensure the following:

- You have completed the **self-serve FTU flow**
- Your feed is successfully uploaded and indexed
- Required fields such as **title, imageUrl, price, categoryPath** are mapped correctly

> **Note:**  
> The configuration attributes shown in this document are based on a **sample apparel feed**.  
> These attributes **will vary depending on the site and feed schema** being used.

---

## Integration Instructions

Follow these steps to integrate Autosuggest into your site.

### 1. Configure Site Credentials

Update the `siteKey` and `apiKey` with values specific to your account.

```js
siteKey: "<<site key>>",
apiKey: "<<api key>>"
```

### 2. Attach Autosuggest to Search Input

Provide a valid CSS selector or DOM element for the search input field.

```
searchInput: ".search-input"
```
This is mandatory for Autosuggest to initialize.

### 3. Customize API Configuration

Control what type of suggestions appear and how many results are fetched.

* In-field suggestions

* Popular products

* Keyword suggestions

* Top queries

* Promoted suggestions

These should be adjusted based on UI space and performance needs.
