================================================================================
                    AUTOSUGGEST JS SDK - CONFIGURATION DOCUMENTATION
================================================================================

OVERVIEW
--------
The Autosuggest class is initialized with a configuration object that controls
the behavior, appearance, and API interactions of the autosuggestion feature.
All configuration options are optional and will fall back to default values
if not provided.

================================================================================
                            CONFIGURATION OPTIONS
================================================================================

1. BASIC CONFIGURATION
---------------------

1.1 siteKey (String, Required)
    Description: Your Unbxd site key for API authentication
    Default: ""
    Example: "ss-unbxd-aus-demo-fashion831421736321881"
    
    Usage:
        const autosuggest = new Autosuggest({
            siteKey: "your-site-key-here"
        });


1.2 apiKey (String, Required)
    Description: Your Unbxd API key for authentication
    Default: ""
    Example: "1ccbb7fcb0faf770d1c228be80ba16d9"
    
    Usage:
        const autosuggest = new Autosuggest({
            apiKey: "your-api-key-here"
        });


1.3 searchInput (String | null, Required)
    Description: CSS selector for the search input element
    Default: null
    Example: ".search-input" or "#search-box"
    
    Usage:
        const autosuggest = new Autosuggest({
            searchInput: ".search-input"
        });
    
    Note: The SDK will query the DOM using this selector to find the input
          element where autosuggestions will be attached.


1.4 containerTag (String, Optional)
    Description: HTML tag name for the autosuggestion container element
    Default: "div"
    Example: "div", "section", "ul"
    
    Usage:
        const autosuggest = new Autosuggest({
            containerTag: "section"
        });


1.5 attributes (Object, Optional)
    Description: HTML attributes to apply to the autosuggestion container
    Default: {}
    Example: { "class": ["search-input", "unbxd-autosuggest-box"], 
               "data-testid": "search-input", 
               "id": "search-id" }
    
    Usage:
        const autosuggest = new Autosuggest({
            attributes: {
                "class": ["search-input", "unbxd-autosuggest-box"],
                "data-testid": "search-input",
                "id": "search-id"
            }
        });
    
    Note: Array values (like class) will be handled appropriately by the SDK.


1.6 debounceDelay (Number, Optional)
    Description: Delay in milliseconds before triggering autosuggest API call
                 after user stops typing
    Default: 0
    Example: 300, 500, 1000
    
    Usage:
        const autosuggest = new Autosuggest({
            debounceDelay: 500
        });
    
    Note: A value of 0 means no debouncing - API will be called on every
          input change (after minChars threshold is met).


1.7 minChars (Number, Optional)
    Description: Minimum number of characters required before triggering
                 autosuggest API call
    Default: 3
    Example: 2, 3, 5
    
    Usage:
        const autosuggest = new Autosuggest({
            minChars: 2
        });
    
    Note: The autosuggest API will only be called when the input length
          is greater than or equal to this value.


1.8 template (Function, Optional)
    Description: Custom template function for rendering the autosuggestion box
    Default: AutosuggestionBoxTemplate (default template)
    Example: Custom function that returns HTML string
    
    Usage:
        function CustomTemplate(props) {
            const { POPULAR_PRODUCTS, IN_FIELD, KEYWORD_SUGGESTION, 
                    PROMOTED_SUGGESTION, TOP_SEARCH_QUERIES } = props;
            return `<div>Custom HTML here</div>`;
        }
        
        const autosuggest = new Autosuggest({
            template: CustomTemplate
        });
    
    Template Props:
        - POPULAR_PRODUCTS: Array of popular product suggestions
        - IN_FIELD: Array of in-field suggestions
        - KEYWORD_SUGGESTION: Array of keyword suggestions
        - PROMOTED_SUGGESTION: Array of promoted suggestions
        - TOP_SEARCH_QUERIES: Array of top search queries


================================================================================
2. API CONFIGURATION
-------------------

2.1 api (Object, Optional)
    Description: Configuration object for API-related settings
    Default: See individual api.* properties below
    
    Usage:
        const autosuggest = new Autosuggest({
            api: {
                apiEndpoint: "https://search.unbxd.io",
                inFields: { count: 2 },
                popularProducts: { count: 3 },
                keywordSuggestions: { count: 2 },
                topQueries: { count: 2 },
                promotedSuggestions: { count: 2 }
            }
        });


2.2 api.apiEndpoint (String, Optional)
    Description: Base URL for the Unbxd search API
    Default: "https://search.unbxd.io"
    Example: "https://search.unbxd.io" or custom endpoint
    
    Usage:
        const autosuggest = new Autosuggest({
            api: {
                apiEndpoint: "https://search.unbxd.io"
            }
        });


2.3 api.inFields (Object, Optional)
    Description: Configuration for in-field suggestions
    Default: { count: 2 }
    
    2.3.1 api.inFields.count (Number, Optional)
          Description: Number of in-field suggestions to fetch
          Default: 2
          Example: 1, 2, 5, 10
          
          Usage:
              const autosuggest = new Autosuggest({
                  api: {
                      inFields: { count: 5 }
                  }
              });


2.4 api.popularProducts (Object, Optional)
    Description: Configuration for popular product suggestions
    Default: { count: 3 }
    
    2.4.1 api.popularProducts.count (Number, Optional)
          Description: Number of popular product suggestions to fetch
          Default: 3
          Example: 1, 3, 5, 10
          
          Usage:
              const autosuggest = new Autosuggest({
                  api: {
                      popularProducts: { count: 5 }
                  }
              });
    
    Note: There is a commented-out fields option for popularProducts that
          may be available in future versions:
          // fields: {
          //     popularProducts: []
          // }


2.5 api.keywordSuggestions (Object, Optional)
    Description: Configuration for keyword suggestions
    Default: { count: 2 }
    
    2.5.1 api.keywordSuggestions.count (Number, Optional)
          Description: Number of keyword suggestions to fetch
          Default: 2
          Example: 1, 2, 5, 10
          
          Usage:
              const autosuggest = new Autosuggest({
                  api: {
                      keywordSuggestions: { count: 5 }
                  }
              });


2.6 api.topQueries (Object, Optional)
    Description: Configuration for top search queries
    Default: { count: 2 }
    
    2.6.1 api.topQueries.count (Number, Optional)
          Description: Number of top search queries to fetch
          Default: 2
          Example: 1, 2, 5, 10
          
          Usage:
              const autosuggest = new Autosuggest({
                  api: {
                      topQueries: { count: 5 }
                  }
              });


2.7 api.promotedSuggestions (Object, Optional)
    Description: Configuration for promoted suggestions
    Default: { count: 2 }
    
    2.7.1 api.promotedSuggestions.count (Number, Optional)
          Description: Number of promoted suggestions to fetch
          Default: 2
          Example: 1, 2, 5, 10
          
          Usage:
              const autosuggest = new Autosuggest({
                  api: {
                      promotedSuggestions: { count: 5 }
                  }
              });


================================================================================
3. CALLBACKS CONFIGURATION
-------------------------

3.1 callbacks (Object, Optional)
    Description: Configuration object for event callbacks
    Default: { onError: null }
    
    Usage:
        const autosuggest = new Autosuggest({
            callbacks: {
                onError: (error) => {
                    console.error("Autosuggest error:", error);
                }
            }
        });


3.2 callbacks.onError (Function | null, Optional)
    Description: Callback function called when an error occurs
    Default: null
    Example: (error) => { console.error(error); }
    
    Usage:
        const autosuggest = new Autosuggest({
            callbacks: {
                onError: (error) => {
                    // Handle error
                    console.error("Autosuggest error:", error);
                    // You can also send to error tracking service
                }
            }
        });
    
    Parameters:
        - error: Error object or error message


================================================================================
                            COMPLETE EXAMPLE
================================================================================

const autosuggest = new Autosuggest({
    // Basic Configuration
    siteKey: "ss-unbxd-aus-demo-fashion831421736321881",
    apiKey: "1ccbb7fcb0faf770d1c228be80ba16d9",
    searchInput: ".search-input",
    containerTag: "div",
    attributes: {
        "class": ["search-input", "unbxd-autosuggest-box"],
        "data-testid": "search-input",
        "id": "search-id"
    },
    debounceDelay: 500,
    minChars: 3,
    template: AutosuggestionBoxTemplate, // or custom template function
    
    // API Configuration
    api: {
        apiEndpoint: "https://search.unbxd.io",
        inFields: {
            count: 2
        },
        popularProducts: {
            count: 3
        },
        keywordSuggestions: {
            count: 2
        },
        topQueries: {
            count: 2
        },
        promotedSuggestions: {
            count: 2
        }
    },
    
    // Callbacks
    callbacks: {
        onError: (error) => {
            console.error("Autosuggest error:", error);
        }
    }
});


================================================================================
                            DEFAULT CONFIGURATION
================================================================================

If no configuration is provided, the SDK uses these defaults:

{
    siteKey: "",
    apiKey: "",
    searchInput: null,
    containerTag: "div",
    attributes: {},
    debounceDelay: 0,
    minChars: 3,
    template: AutosuggestionBoxTemplate,
    api: {
        apiEndpoint: "https://search.unbxd.io",
        inFields: { count: 2 },
        popularProducts: { count: 3 },
        keywordSuggestions: { count: 2 },
        topQueries: { count: 2 },
        promotedSuggestions: { count: 2 }
    },
    callbacks: {
        onError: null
    }
}


================================================================================
                            NOTES & BEST PRACTICES
================================================================================

1. REQUIRED FIELDS
   - siteKey: Must be provided for API authentication
   - apiKey: Must be provided for API authentication
   - searchInput: Must be provided to attach autosuggest to an input element

2. DEBOUNCING
   - Set debounceDelay to 300-500ms for better performance and reduced API calls
   - A value of 0 means no debouncing (not recommended for production)

3. MINIMUM CHARACTERS
   - minChars of 2-3 is recommended for good user experience
   - Lower values may result in too many API calls
   - Higher values may delay suggestions

4. SUGGESTION COUNTS
   - Adjust counts based on your UI design and available space
   - Higher counts may impact API response time
   - Balance between user experience and performance

5. TEMPLATE CUSTOMIZATION
   - Use custom templates to match your site's design
   - Template function receives props with all suggestion types
   - Return valid HTML string from template function

6. ERROR HANDLING
   - Always provide an onError callback for production applications
   - Log errors appropriately for debugging
   - Consider integrating with error tracking services

7. API ENDPOINT
   - Use default endpoint unless you have a custom setup
   - Ensure endpoint is accessible from your domain

8. ATTRIBUTES
   - Use attributes to add CSS classes, data attributes, or IDs
   - Useful for styling and testing purposes
   - Array values for class attribute are supported


================================================================================
                            API RESPONSE STRUCTURE
================================================================================

The autosuggest API returns data in the following structure:

{
    response: {
        products: [...],           // All products
        // Processed and categorized into:
        popularProducts: [...],    // Popular product suggestions
        inFields: [...],           // In-field suggestions
        keywordSuggestions: [...], // Keyword suggestions
        promotedSuggestions: [...],// Promoted suggestions
        topSearchQueries: [...],   // Top search queries
        trendingSearches: [...]    // Trending searches (from separate API)
    }
}

These are passed to your template function as props:
- POPULAR_PRODUCTS
- IN_FIELD
- KEYWORD_SUGGESTION
- PROMOTED_SUGGESTION
- TOP_SEARCH_QUERIES


================================================================================
                            VERSION INFORMATION
================================================================================

Documentation generated based on:
- Autosuggest class: src/core/Autosuggest.js
- Default options: src/constants/options.js
- ConfigManager: src/managers/ConfigManager.js
- DOMService: src/services/DOMService.js
- APIService: src/services/APIService.js


================================================================================
                            END OF DOCUMENTATION
================================================================================
