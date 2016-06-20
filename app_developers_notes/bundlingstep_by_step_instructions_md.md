# Bundling step by step instructions
This set of instructions will guide you through setting up bundling in an Aurelia application where Kendo is used. Since there are multiple skeleton-navigation flavors out there, this tutorial will use the [skeleton-esnext](https://github.com/aurelia/skeleton-navigation/tree/master/skeleton-esnext) flavor. So if you want to follow this tutorial, download skeleton-esnext and follow [these instructions](https://aurelia-ui-toolkits.gitbooks.io/kendoui-sdk-installation/content/jspm_based-installation/kendoui_pro/using_%60vendors%60_folder.html) to install Kendo and the aurelia-kendoui-bridge into the application.

1. Open `build/bundles.js`
2. Add the following bundle configuration:
  ```
  "dist/kendo-build": {
      "includes": ["kendo-ui/js/*.min.js"],
      "excludes": [
        "[kendo-ui/js/angular.min.js]",
        "[kendo-ui/js/jquery.min.js]",
        "[kendo-ui/js/kendo.angular.min.js]",
        "[kendo-ui/js/kendo.angular2.min.js]",
        "[kendo-ui/js/kendo.spreadsheet.min.js]",
        "[kendo-ui/js/kendo.all.min.js]",
        "[kendo-ui/js/kendo.web.min.js]",
        "[kendo-ui/js/kendo.dataviz.min.js]",
        "[kendo-ui/js/kendo.dataviz.mobile.min.js]",
        "[kendo-ui/js/kendo.mobile.min.js]"
      ],
      "options": {
        "inject": true,
        "minify": true,
        "rev": true
      }
    }
    ```



