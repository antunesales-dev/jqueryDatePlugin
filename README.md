# rolldate [![npm](https://img.shields.io/npm/v/rolldate.svg)](https://www.npmjs.com/package/rolldate) [![npm](https://img.shields.io/npm/dm/rolldate.svg)](https://www.npmjs.com/package/rolldate)

This plugin is [jquery-date](https://github.com/weijhfly/jqueryDatePlugin "jquery-date") the new version of , mainly to solve the problems of the old version's unreasonable parameter design, low sliding efficiency, dependence on jquery, and no optional theme style, etc., and added a callback function to make the plugin more flexible.

## 2019/05/24 Version 3.0 update

The previous version was 2.1.5,Changes in new versions (from 3.0.0)：

1. The usage method is changed from new rolldate.Date to new Rolldate;
2. Callback function adjustment: tapBefore was renamed init, confirmBefore was renamed confirm, confirmEnd was canceled, and cancel was added;
3. The date format (format) is adjusted to unlimited, and can be freely combined according to the rules;

## 2019/02/03 important version update

The previous version was 1.5.1, the difference between the new version (starting from 2.0.0) and the previous version:

1. Replaced the sliding plugin from iscroll to better-scroll to improve compatibility;
2. Changed the interface style, making the operation more convenient;
3. Cancel the rolldate.css file, just import js;
4. Removed the sliding time settings for theme style and date initialization；  

Note that versions before 2.0.0 will no longer be maintained, if necessary, please visit: [Old rolldate](https://weijhfly.github.io/rolldate-index2.html "rolldate")

## Demo

[rolldate](https://weijhfly.github.io/rolldate-index.html "rolldate") (scan the code directly below to experience)

![rolldate](https://weijhfly.github.io/images/rolldate-demo.jpg)

## How to use

### es6

```js
import Rolldate from 'rolldate'
new Rolldate({
  el:'#date'
})

```

### commonJS

```js
var Rolldate = require('rolldate');
new Rolldate({
  el:'#date'
})

```

### amd

```js
require(['rolldate'],function(Rolldate){
  new Rolldate({
    el:'#date'
  })
})
```

### cmd

```js

seajs.use('rolldate',function(undefined){
    //The plugin does not follow the cmd specification, the Rolldate here is global
    new Rolldate({
      el:'#date'
    })
});
```

## Parameters, method description

Name|Required|Default|Description
---|:-:|:-:|---
el|No|None|Bind the dom element of the plug-in, the plug-in uses document.querySelector inside,<br>You can also pass the dom element object directly, only supports a single
format|no|'YYYY-MM-DD'|date format, unlimited. Rules: year-YYYY month-MM day-DD hour-hh minute-mm second-ss separated by one of /, -, space, : and can be combined at will
beginYear|No|2000|Date start year
endYear|No|2100|Date end year
value|no|none|the default value for date initialization, such as '2018-03-18'
lang|No|Year, month, day...|Configure plugin language, default: title:'select date',cancel:'cancel',confirm:'confirm',<br>year:'year',month:' month',day:'day',hour:'hour',min:'minute',sec:'second'
minStep|no|1|minutes separated by specified number
init|no|null|The callback function before the plug-in is triggered, return false can prevent the plug-in from executing
moveEnd|No|null|The callback function after the plugin scrolls, the function returns a parameter (better-scroll instance)
confirm|No|null|The callback function before the confirmation button is triggered, return false can prevent the plug-in from executing, <br> return other values can modify the date, the function returns a parameter (the selected date)
cancel|No|null|The callback function triggered when the plugin is canceled
trigger|No|'tap'|By default, tap is used to solve the 300ms delay of the click event on the mobile terminal, and click can be used to replace tap. Note that using tap will prevent other bound click events from firing
show|no|none|Active trigger plug-in, when the trigger is tap, active trigger plug-in should use this method
hide|No|None|Actively hide plugins
theme|No|selectedBackground: lightgrey, <br> fontColor: black|Sets the background and font color of the current selected date
monthNameLength|No|Number|Sets the month format. Use 'full' to display full month, 'short' to display month abreviated, and let it empty to show number
showZeroBefore|No|date: true, <br> time: true|Defines if the 0 show before the number for time and date

```js
//Complete parameters, method examples
var rd = new Rolldate({
    el: '#date',
    format: 'YYYY-MM-DD',
    beginYear: 2000,
    endYear: 2100,
    minStep:1,
    lang:{title:'custom title'},
    trigger:'tap',
    theme: {
      selectedBackground: 'lightgrey',
      fontColor: 'black'
    },
    monthNameLength: '', //short (Jan), full (January), empty (01)
    showZeroBefore: {
      date: true,
      time: true
    },
    init: function() {
      console.log('The plugin starts triggering');
    },
    moveEnd: function(scroll) {
      console.log('end of scrolling');
    },
    confirm: function(date) {
      console.log('OK button fires');
    },
    cancel: function() {
      console.log('Plugin run canceled');
    }
})
rd.show();
rd.hide();

```
