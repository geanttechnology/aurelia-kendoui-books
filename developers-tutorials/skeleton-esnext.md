# 4.2 skeleton-esnext

### Introduction

This tutorial (like all others in this `App developers tutorials` section) is organized as "two separate chapters", residing in the same file. The first chapter explains how to use open source version of Telerik's KendoUI, known as **[kendo-core](https://github.com/telerik/kendo-ui-core)**, while the second chapter assumes the use of Telerik's **[KendoUI PRO](http://www.telerik.com/kendo-ui)** version.
<br><br>

#### [Go to pro tutorial](#pro-anchor)
<br>


***
<!-- make the reference to this anchor from setup.md page -->

<a id="core-anchor"></a>
### 2.1 Using KendoUI-core

This chapter explains the steps that need to be taken to ___add several KendoUI components to the standard___ **[skeleton-esnext](https://github.com/aurelia/skeleton-navigation/tree/master/skeleton-esnext)** application, using the **[KendoUI Core](https://aurelia-ui-toolkits.gitbooks.io/kendoui-sdk-installation/content/jspm_based-installation/kendoui_core.html)** package:
<br><br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13726972/e3414ec4-e8ac-11e5-95b9-409ddd1df6aa.png"></img>
<br><br>
  Image 2.1 - 1
</p>


___into this "extended version"___ that implements Aurelia `autocomplete` and `button` components using Aurelia Kendoui bridge.
<br><br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13731170/44c8f192-e939-11e5-8f39-baad56f590b9.png"></img>
 <br><br>
 Image 2.1 - 2
</p>


***

#### Step 2.1.1

**Add tutorial specific welcome greeting**
<br><br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13729225/86c184d4-e906-11e5-8b00-0d89047d0a21.png"></img>
 <br><br>
 Image 2.1 - 3
</p>

***

#### Step 2.1.2

**Add `KendoUI autcomplete` and  `KendoUI button` menu items**
<br><br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13729454/d5aaa5ee-e90b-11e5-9844-a1c05a9d8d2a.png"></img>
 <br><br>
 Image 2.1 - 4
</p>

***

#### Step 2.1.3

**Add `KendoUI autcomplete` and  `KendoUI button` components implementation**

KendoUI bridge implements the API which allows treating KendoUI native "plugins" as Aurelia components. In order to "isolate" our added code from the original **[skeleton-es2016](https://github.com/aurelia/skeleton-navigation/tree/master/skeleton-es2016)** application we added the `kendoui` folder which contains the code that implements `autocomplete` and `button` Aurelia components;
<br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13730834/2f285ed4-e931-11e5-931e-92e661af2e4c.png"></img>
 <br><br>
 Image 2.1 - 5
</p>


**autocomplete.html**

```html
<template>
  <section>
        <br>
        <h3>Basic KendoUI Autocomplete sample</h3>

        <a href="https://github.com/aurelia-ui-toolkits/aurelia-kendoui-plugin/tree/master/sample/src/samples/autocomplete">See KendoUI Bridge autocomplete folder for more details</a>
        <br>
        <br>

       <p><strong>People:</strong></p>
        <ak-autocomplete k-data-source.bind="items">
        <input style="width: 100%;">
        </ak-autocomplete>
        <br>
        <br>
        <br>
        <p class="demo-hint" style="word-break: break-all">Type a name, available values in the list are: ${ items } </p>
  </section>
</template>
```
<br>

**autocomplete.js**
<br>
```javascript
export class BasicUse {
  items = [
    'Charles',
    'Jedd',
    'Nikolaj',
    'Jeroen',
    'David',
    'Rob',
    'Matt',
    'Patrick',
    'Jason',
    'Martin',
    'Fredrick',
    'Alex'
  ]
}

```
<br>

**button.html**
```html
<template>
    <require from="./button.css"></require>
    <section>
        <br>
        <h3>Basic KendoUI Button API sample</h3>

        <a href="https://github.com/aurelia-ui-toolkits/aurelia-kendoui-plugin/tree/master/sample/src/samples/button">See KendoUI Bridge button folder for more details</a>
        <br>
        <br>

        &nbsp;&nbsp;<button ak-button="k-icon: ungroup; k-widget.bind: button" k-on-click.delegate="test()">Kendo UI Button</button>
        <br>
        <br>
        <button ak-button click.delegate="button.enable(false)">Disable</button>
        &nbsp;&nbsp;
        <button ak-button click.delegate="button.enable(true)">Enable</button>

    </section>
</template>
```
<br>

**button.js**
```javascript
export class Button {
    test() {
      alert('You clicked me');
    }
}

```
<br>

**button.css**
```
#button .demo-section {
    text-align: center;
}
#button .box .k-textbox {
    margin: 0;
    width: 80px;
}
```

<br><br>


#### Step 2.1.4

**Add Aurelia KendoUI bridge plugin**
<br><br>

```
jspm install aurelia-kendoui-bridge
...
ok   Installed aurelia-kendoui-bridge as npm:aurelia-kendoui-bridge@^0.6.0 (0.6.0)
...
ok   Install complete.
```
<br><br>

#### Step 2.1.5

**Add the kendo-core modules** - as described on Installation - New from GitHub: Kendo Core
<br>

Run:
```
jspm install kendo-ui
```
<br>

Verify that the open source version of Telerik's KendoUI is properly installed - as shown on Image 2.1 - 6 below
<br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13731061/ed14ee9e-e936-11e5-8de0-476fde9b9bb1.png"></img>
 <br><br>
 Image 2.1 - 6
</p>


***

#### Step 2.1.6

**Verify the mapping needed to access kendo-core plugins**

File **config.js**

```
  ...
  paths: {
    "*": "dist/*",
    "github:*": "jspm_packages/github/*",
    "npm:*": "jspm_packages/npm/*",
    "kendo.*": "jspm_packages/github/kendo-labs/bower-kendo-ui@2016.1.217/js/kendo.*.js"  <------
  },
  ...
```
<br>

***

#### Step 2.1.7

**Activate Aurelia KendoUI bridge plugin**
<br><br>

Add `plugin('aurelia-kendoui-bridge', (kendo) => kendo.core())` instruction to the list of Aurelia plugins
<br>

File: **main.js**

```
import 'bootstrap';

export function configure(aurelia) {
  aurelia.use
    .standardConfiguration()
    .developmentLogging()
    .plugin('aurelia-kendoui-bridge', (kendo) => kendo.core());

  aurelia.start().then(() => aurelia.setRoot());
}
```

***

#### Step 2.1.8

**Run the application**
<br>

```
gulp watch
```


***
***

<a id="pro-anchor"></a>
### 2.2 Using KendoUI-pro

#### [Go to core tutorial](#core-anchor)
<br>
The goal of this chapter is to demonstrate all steps that need to be taken to ___transform the original___ **[skeleton-es2016](https://github.com/aurelia/skeleton-navigation/tree/master/skeleton-es2016)** application, using the KendoUI PRO version:
<br><br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13726972/e3414ec4-e8ac-11e5-95b9-409ddd1df6aa.png"></img>
 <br><br>
  Image 2.2 - 1
</p>
<br>

___into this "extended version"___ that implements Aurelia `chart` and `grid` components using Aurelia Kendoui bridge.
<br><br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13733770/548b37fa-e96d-11e5-9f57-523918d279a9.png"></img>
 <br><br>
 Image 2.2 - 2
</p>
<br><br>

<!--  __________________________________________________________________________________________________________ -->


#### Step 2.2.1

**Add tutorial specific welcome greeting**
<br><br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13733889/a55db3a0-e96e-11e5-9ff5-7f3bc4b195e3.png"></img>
 <br><br>
 Image 2.2 - 3
</p>

***

#### Step 2.2.2

**Add `KendoUI chart` and  `KendoUI grid` menu items**
<br><br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13732057/d1dd9d1a-e94f-11e5-8f0a-eff11209851b.png"></img>
 <br><br>
 Image 2.2 - 4
</p>

***

#### Step 2.2.3

**Add `KendoUI chart` and  `KendoUI grid` components implementation**

KendoUI bridge implements the API which allows treating KendoUI native "plugins" as Aurelia components. In order to "isolate" our added code from the original **[skeleton-es2016](https://github.com/aurelia/skeleton-navigation/tree/master/skeleton-es2016)** application we added the `kendoui` folder which contains the code that implements `chart` and `grid` Aurelia components;
<br>

<p align=center>
  <img src=""></img>
 <br><br>
 Image 2.2 - 5
</p>


**chart**

```html
<template>
    <section>
        <br>
        <h3>Basic KendoUI Chart sample</h3>

        <a href="https://github.com/aurelia-ui-toolkits/aurelia-kendoui-plugin/tree/master/sample/src/samples/chart">See KendoUI Bridge chart folder for more details</a>
        <br>
        <br>

        <ak-chart    k-title.bind="{text: 'Gross Domestic product growth \n /GDP annual %/'}"
                    k-legend.bind="{position: 'bottom'}"
                    k-series-defaults.bind="seriesDefaults"
                    k-series.bind="series"
                    k-value-axis.bind="valueAxis"
                    k-category-axis.bind="categoryAxis"
                    k-tooltip.bind="tooltip">
        </ak-chart>
    </section>
</template>
```
<br>

**chart.js**
<br>
```javascript
export class BasicUse {

  seriesDefaults = {
    type: 'line',
    line: {
      line: {
        style: 'smooth'
      }
    }
  };

  series = [{
    name: 'India',
    data: [3.907, 7.943, 7.848, 9.284, 9.263, 9.801, 3.890, 8.238, 9.552, 6.855]
  }, {
    name: 'World',
    data: [1.988, 2.733, 3.994, 3.464, 4.001, 3.939, 1.333, -2.245, 4.339, 2.727]
  }, {
    name: 'Haiti',
    data: [-0.253, 0.362, -3.519, 1.799, 2.252, 3.343, 0.843, 2.877, -5.416, 5.590]
  }];

  valueAxis = {
    labels: {
      format: '{0}%'
    },
    line: {
      visible: false
    },
    axisCrossingValue: -10
  };

  categoryAxis = {
    categories: [2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011],
    majorGridLines: {
      visible: false
    },
    labels: {
      rotation: 'auto'
    }
  };

  tooltip = {
    visible: true,
    format: '{0}%',
    template: '${series.name} ${value}'
  }
}
```
<br>

**grid.html**
```html
    <template>
    <require from="./grid.css"></require>
    <section>
        <br>
        <h3>Basic KendoUI Grid sample</h3>

        <a href="https://github.com/aurelia-ui-toolkits/aurelia-kendoui-plugin/tree/master/sample/src/samples/grid">See KendoUI Bridge grid folder for more details</a>
        <br>
        <br>
         <ak-grid k-data-source.bind="datasource" k-pageable.bind="pageable" k-sortable.bind="true">
            <ak-col k-title="Contact Name" k-field="ContactName">
            <ak-template>
              <div class='customer-photo' style="background-image: url(http://demos.telerik.com/kendo-ui/content/web/Customers/${CustomerID}.jpg);"></div>
              <div class='customer-name'>${ContactName}</div>
            </ak-template>
            </ak-col>
            <ak-col k-title="Contact Name" k-field="ContactName"></ak-col>
            <ak-col k-title="Contact Title" k-field="ContactTitle"></ak-col>
            <ak-col k-title="Company Name" k-field="CompanyName"></ak-col>
            <ak-col k-field="Country"></ak-col>
        </ak-grid>
    </section>
    </template>
```
<br>

**grid.js**
```javascript
export class BasicUse {

  pageable = {
    refresh: true,
    pageSizes: true,
    buttonCount: 10
  };

  constructor() {
    this.datasource = {
      type: 'odata',
      transport: {
        read: '//demos.telerik.com/kendo-ui/service/Northwind.svc/Customers'
      },
      pageSize: 10
    };
  }
}

```
<br>

**grid.css**
```
.customer-photo {
    display: inline-block;
    width: 32px;
    height: 32px;
    border-radius: 50%;
    background-size: 32px 35px;
    background-position: center center;
    vertical-align: middle;
    line-height: 32px;
    box-shadow: inset 0 0 1px #999, inset 0 0 10px rgba(0,0,0,.2);
    margin-left: 5px;
}

.customer-name {
    display: inline-block;
    vertical-align: middle;
    line-height: 32px;
    padding-left: 3px;
}
```

<br><br>


#### Step 2.2.4

**Add Aurelia KendoUI bridge plugin**
<br><br>

```
jspm install aurelia-kendoui-bridge
...
ok   Installed aurelia-kendoui-bridge as npm:aurelia-kendoui-bridge@^0.6.0 (0.6.0)
...
ok   Install complete.
```
<br><br>

#### Step 2.2.5

**Add the kendo-pro modules** - as described on Installation - Having KendoUI already: Vendors
<br>

If you do not have the KendoUI PRO license download the **[trial version](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwirtNrBmL_LAhVHQCYKHUKmDTcQFggcMAA&url=https%3A%2F%2Fwww.telerik.com%2Fdownload-trial-file%2Fv2%2Fkendo-ui&usg=AFQjCNHJfpB2d55TpjuAyLF3LH9ZnO4MAw&sig2=F9ATtlSr-_7dJPPAjO-xkw)**

Now, having either trial or regular version of KendoUI PRO, create the `vendors` folder at the **root of this application** and copy the two folders (`js` and `styles` from KendoUI (trial or PRO) distribution:
<br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13734099/cc4eb2aa-e970-11e5-98a6-22630f2f2a36.png"></img>
 <br><br>
  Image 2.2 - 6
</p>



<br>

At this point your project should look as shown on Image 2.2 - 7 below
<br><br>

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/13734150/599a9782-e971-11e5-8d4d-271d3991e4d0.png"></img>
 <br><br>
 Image 2.2 - 7
</p>


***

#### Step 2.2.6

**Verify the mapping needed to access kendo-pro plugins**

File **config.js**

```
  ...
  paths: {
    "*": "dist/*",
    "github:*": "jspm_packages/github/*",
    "npm:*": "jspm_packages/npm/*",
    "kendo-ui/*": "vendors/*",
    "kendo.*": "vendors/js/kendo.*.js"
  },
  ...
```
<br>

***

#### Step 2.2.7

**Activate Aurelia KendoUI bridge plugin**
<br><br>

Add `plugin('aurelia-kendoui-bridge', (kendo) => kendo.pro())` instruction to the list of Aurelia plugins
<br>

File: **main.js**

```
import 'bootstrap';

export function configure(aurelia) {
  aurelia.use
    .standardConfiguration()
    .developmentLogging()
    .plugin('aurelia-kendoui-bridge', (kendo) => kendo.pro());

    aurelia.start().then(() => aurelia.setRoot());
}

```

***

#### Step 2.2.8

**Run the application**
<br>

```
gulp watch
```
<br>


#### [back to the top](#top-anchor)





