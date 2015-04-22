# Sprinkler-js

##What:
Sprinkler is a simple JavaScript library used to inject (or sprinkle) JSON data into the dom.  

##Advantages:
<ul>
<li>Newbee friendly - No need to know anything other then HTML</li>
<li>Easy - The entire library can be learned in about a half hour.  </li>
<li>Free - MIT license</li>
<li>Light Weight</li>
<li>Zero dependencies</li>
</ul>

##Problem:
There's large skills gap between building static html websites and websites containing dynamic data.  Sprinkler is a tool to help bridge that gap.   

##Usage:
### {{text}}
##### js:
```javascript
Sprinkler({"Name":"Apple Inc","Symbol":"AAPL","LastPrice":126.45});
```
##### html:
```html
<p>The value of {{Name}} is {{LastPrice}}.</p>
```
##### output:
<p>The value of Apple Inc is 126.45.</P>

JSON is a collection of name value pairs.  Placing the name inside  the double curly-brace will get replaced with the value.  If a name inside does not match the passed in value, the text command will be removed.  You can access nested data separating the parent child values with /.

##### js:
```javascript
Sprinkler({AAPL: {"Name":"Apple Inc","LastPrice":126.45}});
```
##### html:
```html
<p>The value of {{AAPL/Name}} is {{AAPL/LastPrice}}.{{NoKey}}</p>
```
##### html:
<p>The value of Apple Inc is 126.45.</P>

### {{#if node}} {{#ifnot node}}
##### js:
```javascript
Sprinkler({"Name":"Bust coin","LastPrice": 0}});
```
##### html:
```html
<p>
{{Name}} 
{{#if LastPrice}}
<span>is worth {{LastPrice}}</span> <!-- this node will not show if LastPrice is truthy -->
{{#ifnot LastPrice}}
<span>is worthless</span> <!-- this node will not show if LastPrice is falsy -->
</p>
```
##### output:
<p> Bust coin is worthless </p>
Inside the double curly-brace, you can precede the name with the #if or #ifnot command.  If the #if value is evaluated to <a href="http://www.sitepoint.com/javascript-truthy-falsy/" target="window">truthy</a>, the next HTML node will be removed.   If #ifnot name value is evaluated to <a href="http://www.sitepoint.com/javascript-truthy-falsy/" target="window">falsy</a>, the next HTML node will be removed.  

### {{#foreach node}}
##### js:
```javascript
Sprinkler({stocks: [{"Name":"Apple Inc","LastPrice":126.45}, {"Name":"General Electric","LastPrice":26.62}]});
```
##### html:
```html
<ul>
{{#foreach stocks}}
<li>{{Name}}- {{LastPrice}}</li><!-- this node will be duplicated --> 
</ul>
```
##### output:
<ul>
<li>Apple Inc- 126.45</li>
<li>General Electric- 26.62</li>
</ul>
Inside the double curly-brace, you can precede the name with the #foreach command.  If the named value is an object or array, the next HTML node will be duplicated once for each item in the array or object.  If the next HTML node contains double curly-braces, they will be evaluated with each array entry. 
