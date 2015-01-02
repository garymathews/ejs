# EJS

Embedded JavaScript templates

## Installation

```bash
$ npm install ejs
```

## Features

  * Control flow with `<% %>`
  * Escaped output with `<%= %>`
  * Unescaped raw output with `<%- %>`
  * Trim-mode ('newline slurping') with `-%>` ending tag
  * Custom delimiters (e.g., use '?' instead of '%')
  * Includes
  * Client-side support
  * Static caching of intermediate JavaScript
  * Static caching of templates
  * Complies with the [Express](http://expressjs.com) view system

## Example

```html
<% if (user) { %>
  <h2><%= user.name %></h2>
<% } %>
```

## Usage

```javascript
var template = ejs.compile(str, options);
template(data);
// => Renderded HTML string

ejs.render(str, data, options);
// => Renderded HTML string
```

## Options

  - `cache`           Compiled functions are cached, requires `filename`
  - `filename`        Used by `cache` to key caches, and for includes
  - `context`         Function execution context
  - `compileDebug`    When `false` no debug instrumentation is compiled
  - `client`          Returns standalone compiled function
  - `delimiter`       Character to use with angle brackets for open/close

## Tags

  - `<%`              'Scriptlet' tag, for control-flow, no output
  - `<%=`             Outputs the value into the template (HTML escaped)
  - `<%-`             Outputs the unescaped value into the template
  - `<%#`             Comment tag, no execution, no output
  - `<%%`             Outputs a literal '<%'
  - `%>`              Plain ending tag
  - `-%>`             Trim-mode ('newline slurp') tag, trims following newline

## Includes

Includes are relative to the template with the `include` statement. (This
requires the 'filename' option.) For example if you have "./views/users.ejs" and
"./views/user/show.ejs" you would use `<%- include('user/show'); %>`.

You'll likely want to use the raw output tag (`<%-`) with your include to avoid
double-escaping the HTML output.

```javascript
<ul>
  <% users.forEach(function(user){ %>
    <%- include('user/show'); %>
  <% }); %>
</ul>
```

Includes are inserted at runtime, so you can use variables for the path in the
`include` call (for example `<%- include(somePath); %>`). Local variables are
available to all your includes.

NOTE: Include preprocessor directives (`<% include user/show  %>`) are
transparently converted to `include` function calls.

## Custom delimiters

Custom delimiters can be applied on a per-template basis, or globally:

```javascript
var ejs = require('ejs'),
    users = ['geddy', 'neil', 'alex'];

// Just one template
ejs.render('<?= users.join(' + '); ?>, {users: users}, {delimiter: '?'});
// => 'geddy + neil + alex'

// Or globally
ejs.delimiter = '$';
ejs.render('<$= users.join(' + '); $>, {users: users});
// => 'geddy + neil + alex'
```

## Layouts

EJS does not specifically support blocks, but layouts can be implemented by
including headers and footers, like so:


```html
<%- include('header'); -%>
<h1>Title</h1>
<p>My page</p>
<%- include('footer'); -%>
```

## Client-side support

Include `./ejs.js` or `./ejs.min.js` and `ejs.render(str)`.

## Related projects

There are a number of implementations of EJS:

 * TJ's implementation, the v1 of this library: https://github.com/tj/ejs
 * Jupiter Consulting's EJS: http://www.embeddedjs.com/
 * EJS Embedded JavaScript Framework on Google Code: https://code.google.com/p/embeddedjavascript/
 * Sam Stephenson's Ruby implementation: https://rubygems.org/gems/ejs

## License

Licensed under the Apache License, Version 2.0
(<http://www.apache.org/licenses/LICENSE-2.0>)

- - -
EJS Embedded JavaScript templates copyright 2112
mde@fleegix.org.


