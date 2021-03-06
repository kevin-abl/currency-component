### ABL Currency Component Filter 

#### Generating a new module:
1. npm i
2. gulp generate --name abl-module-name

This will regenerate new module source code, package.json, and file names with the name argument you specify, in this example *abl-module-name*

#### Development with hot-reloading Webpack development server:
1. npm run start
2. http://localhost:9999 in your browser.
3. Packed module is output to *./dst* folder.

The sample Angular Material application to test your module during development is located in the *./samples* folder.

#### Build packaged distributable files (/dst):
1. npm run build

![screenshot](screen.png?raw=true)

#### Adding the module to your app:
1. Include the webpacked .js file: *./dst/currency-component.js*
3. Include the module in your app dependencies:
```javascript
angular
.module('app', [
  'currency-component'
]);
```
4. Using the filter:
```html
<span flex>{{ $ctrl.price | ablCurrency: 'eur' }}</span>
```

#### Component setup
```javascript
app.run(function($ablCurrencyComponentProvider) {
  //this will be used if no currencyFilter is defined
  $ablCurrencyComponentProvider.defaultCurrency = 'usd';
  //if this is true the filter will use 'defaultCurrency' in the whole app. Default: false
  $ablCurrencyComponentProvider.uniqueCurrency = false;
  //Add an array with extra currencies. 
  //Example: {name:'abc', symbol:'#', symbolSeparation:' ', position:'append'} => 12345 #
  $ablCurrencyComponentProvider.currencies = [{ name: 'cl', symbol: '#', symbolSeparation: '', position: 'prepend' }];
})
```

#### Filter Attributes

##### price (Integer)
```javascript
vm.price = 1234567890;
```
```html
<span flex>{{ $ctrl.price | ablCurrency: 'eur' }}</span>
```

##### currencyFilter (String)
```javascript
vm.price = 1234567890;
vm.currencyFilter = 'usd';
```
```html
<span flex>{{ $ctrl.price | ablCurrency: $ctrl.currencyFilter }}</span>
```


##### html (String)
```javascript
vm.price = 1234567890;
vm.currencyFilter = 'usd';
vm.html = 'html';
```
```html
<span flex>{{ $ctrl.price | ablCurrency: $ctrl.currencyFilter : $ctrl.html }}</span>
```

