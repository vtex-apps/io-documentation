---
title: Improving filter navigator experience
description: "Learn how to improve the filter navigator experience and increase your store's conversion"
date: "2020-04-08"
tags: ["filter", "navigator", "search"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/templates/improving-filter-navigator-experience.md"
---

# Improving filter navigator experience

The filter navigator is one of the most important components on the search page. This recipe will show you how to set the filter navigator component in a way that has been proven to improve the conversion of your store.

## Step by step

1. Ensure that you have the `vtex.search-result@3.x` as a dependency of your `manifest.json`:

```diff
{
  "dependencies": [
      // other dependencies
+     "vtex.search-result": "3.x"
    }
  ]
}
```

2. Add the following props to the `search-result-layout.desktop` and the `search-result-layout.mobile`.

```diff
"search-result-layout.desktop": {
    "children": [
        // children
    ],
    "props": {
        // props
+       "preventRouteChange": true,
+       "thresholdForFacetSearch": 10,
+       "showProductsCount": true,
+       "showFacetQuantity": true
    }
}
```

```diff
"search-result-layout.mobile": {
    "children": [
        // children
    ],
    "props": {
        // props
+       "preventRouteChange": true,
+       "thresholdForFacetSearch": 10,
+       "showProductsCount": true,
+       "showFacetQuantity": true
    }
}
```

3. Declare the `filter-navigator.v3` block with the following props

```diff
+ "filter-navigator.v3": {
+     "blocks": ["sidebar-close-button"],
+     "props": {
+         "initiallyCollapsed" :true,
+         "truncateFilters": true,
+         "showClearByFilter": true,
+         "fullWidthOnMobile": true,
+         "navigationTypeOnMobile": "collapsible",
+         "appliedFiltersOverview": "show",
+         "totalProductsOnMobile": "show",
+         "updateOnFilterSelectionOnMobile": true,
+         "priceRangeLayout": "inputAndSlider"
+     }
+ },
```

4. Your filter-navigator should look like this

![filter-navigator demo](https://user-images.githubusercontent.com/40380674/114074357-abc24600-987a-11eb-86ed-35aa05c4b1e8.gif)
