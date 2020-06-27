# React: The Big Picture

These are my notes from a Pluralsight course called  'React: The Big Picture'.

Created by Facebook in 2011 for internal use. Open sourced in 2013. React Native came out in 2015.

It fits HTML into JavaScript, unlike other frameworks that fit JavaScript into HTML (e.g. Angular).

"JS" in HTML example, using custom syntax per framework:

Angular = `<div *ngFor="let user of users">`

Vue = `<div v-for="user in users">`

Ember = `{{#each user in users}}`

"HTML" in JS example:

React = `{users.map(createUser)}`. It just uses the JavaScript's `map` method. You can use all your JavaScript knowledge to get better at React.

## Why React

### Flexibility

It's a library, and less opinionated that frameworks like Angular.

Different renderers can render your React app to web, native mobile apps, and event VR.

You can render on the server with Gatsby (static), and Next.js (Server Side Rendering).

Supports all major browsers.

### Developer Experience

Rapid feedback gives enjoyable experience. Not much React API to learn.

```javascript
import React from 'react';

function HelloWorld(props) {
    return <div>Hello {props.name}</div>
}
```

Import React. Create a function which received an object called `props`.

```javascript
import React from 'react';

class HelloWorld extends React.Components {
    render() {
        return <div>Hello {props.name}</div>
    }
}
```

Above looks like HTML but has JavaScript inside. This is JSX syntax. JSX compiles into JavaScript.

```javascript
<h1 color="red">Heading here</h1>
```

The above JSX compiles into:

```javascript
React.createElement("h1", {color: "red"}, "Heading here")
```

The `React.createElement` methods takes the element you want created, object that sets the attributes you want to set, and the markup you want to sit inside. You can type this JavaScript yourself, but it's recommended to just use JSX.

You can quickly build a new app with `create-react-app nameofyourapp`, which sets up your full environment. `npm start` will serve your app to the browser.

### Corporate investment

Facebook are committed to supporting React for themselves, so the community benefits from their contributions.

### Community

React's popularity has exploded and many contributors.

### Performance

React uses Virtual DOM to minimise calls to the DOM. It avoids performance issues in the browser.

### Testability

React was designed with testing in mind. There's not much setup, and `create-react-app` will set up testing for you. Tests run in memory (via node.js) so you don't need to use a browser.

There's many JS test frameworks, but Jest is made by Facebook and is the most popular with React.

## Tradeoffs with React

### Framework vs. Library

React is a library. It's lean and focused on giving you components to work with.

It is not as opinionated as a framework, so you need to add other libraries for other features you need, e.g. Testing = Jest, HTTP library = Fetch or Axios, Routing = React Router, i18n = react-intl, Animation = react-motion, Form validation = react-forms, CLI tooling = create-react-app. Something like Angular has all of this built in.

### Concise vs. Explicit

In React you spend more time wiring things together.

Other frameworks use two-way binding, e.g. Angular. It requires less coding:

```javascript
let user = 'Mark'

<input
    type="text"
    value="{user}"
/>
```

React is more explicit and uses one-way binding:

```javascript
state = { user: 'Mark' };

function handleChange(event) {
    this.setState({
        user: event.target.value // an explicit change handler
    });
}

<input
    type="text"
    value={this.state.user}
    onChange={this.handleChange}
/>
```

It requires more code to write in React, but you have more control over what happens in the event, e.g. validate input before binding and performance optimisations.

### Template-centric vs. JavaScript centric

Other frameworks makes HTML more powerful by adding custom/unique syntax, whereas React adds HTML into JavaScript.

"JS" in HTML example, using custom syntax per framework:

Angular = `<h1 *ngIf="isAdmin">Hi Admin</h1>`

Vue = `<h1 v-if="isAdmin">Hi Admin</h1>`

Ember = `<h1>{{if isAdmin 'Hi Admin'}}</h1>`

"HTML" in JS example:

React = `{isAdmin && <h1>Hi Admin</h1>}`

One thing to note with React, if you are adding HTML handlers, you need to use camel casing, e.g. `onClick` and not `onclick`, as this is convention for JSX.

```javascript
<button onClick={delete}>Delete</button>
```

React has very little framework-specific syntax, as you mainly write JavaScript.

### Separate Template vs. Single File

Many frameworks use MVC pattern:

* Model = JS
* View = HTML
* Controller = JS

React takes a 'Component' approach; each one being its own concern:

* Component = JS & JSX

Components contain logic and markup in the same file, which seems to violate best practice or separation of concerns. But, Components are split by functionality, which are their own concern.

Component composition works similarly to Russian Dolls, with nested Components.

### Standard vs. Non-standard

Most JS frameworks and libraries are not using the HTML5 Web Component Standard.

HTML5 Web Component Standard:

* Templates (Inert, reusable markup)
* Custom Elements (Define our own elements)
* Shadow DOM (Encapsulated styling)
* Imports (Bundle HTML, JS, and CSS)

Main reason for lack of adoption is the browser support is bad, and using it doesn't provide anything more than what modern JS frameworks/libraries provide. The frameworks/libraries provide newer, innovative features and also have much better support for all major browsers.

### Corporate backing

React is open source, but owned by Facebook. Its development is driven by Facebook's need. However, they do have full-time staff building and supporting React.

## Common complaints about React

These are apparently some common complaints, although they don't seem like show stoppers.

### HTML vs. JSX

Some people complain about the differences between JSX and plain HTML. They are very similar though. You can write plain HTML and JavaScript if you want, but JSX is much easier to read and generally more preferred.

Some differences between HTML and JSX:

HTML | JSX
--- | ---
`for` | `htmlFor`
`class` | `className`
`<style color="blue">` | `<style={{color:'blue'}}>`
`<!-- Comment -->` | `{/* Comment */}`

### Version conflicts

You can't run two different versions of React on the same page. All your components have to use the same run time.

As an alternative, there's no runtime with Standard Web Components, or frameworks like Svelte, so you don't have to worry about this issue. Although you can easily avoid this, and React gives many more benefits.

### Changes are frequent, community guides get out of date

You should always double check the React documents for current features. Many features have been extracted out of React Core and into separate libraries to make React leaner, but some community guides haven't kept up with these changes.

Some current gotchas:

Old style | New style
--- | ---
`import {render} from 'react';` | `import {render} from 'react-dom';`
`React.createClass` | `var crc = require('create-react-class')`
`import {PropTypes} from 'react';` | `import PropTypes from 'prop-types'; // or use TypeScript instead!`
`mixins: [mixinNameHere]` | Use React Hooks to share logic between Components!

### Decision fatigue

React is lightweight and un-opinionated, so it's sometimes hard to chose the right things, but it does mean you have lot of options.

There's 5 major decisions you should decide on early on:

**1. Dev environment**:

* There are many React boilerplates available, but a very common way to start your project is using `create-react-app`. It is maintained by Facebook and handles testing environment, transpiling, bundling assets, linting and automated builds.
* `create-react-app` doesn't include React Router (for routing) or Redux (for state management), but you don't really need these to get started.

**2. Clases or functions**:

Class syntax:

```javascript
class Greeting extends React.Component {
    render() {
        return <h1>Hello</h1>;
    }
}
```

Function syntax:

```javascript
function Greeting() {
    return <h1>Hello<h1>;
}
```

You can accomplish the same thing with both, but it's becoming more common for React developers to use functions. The syntax is more concise.

**3. Whether or not to use Types**:

Three popular ways to implement Types:

PropTypes:

Declare the types of the data passed into the components. Types are only checked at run time and only during development.

```javascript
import React from "react";
import PropTypes from 'prop-types';

function Greeting(props) {
    return (
        <h1>Hello {props.name}</h1>
    )
}

Greeting.propTypes = {
    name: PropTypes.string
};
```

TypeScript:

A superset of JavaScript, that adds strong typing support. Compiles to plain JavaScript.

Types are checked at compile time, so you find out earlier if there are issues.

```typescript
import * as React from "react";

interface Props {
    name: string
}

function Greeting(props : Props) {
    return (
        <h1>Hello {props.name}</h1>
    )
}
```

Flow:

A project from Facebook to check types in JavaScript. You add type annotations to your JavaScript. You need `// @flow` at the top of your file, and you declare the types above the function and in the parameters.  The types are inferred when you run Flow.

```javascript
// @flow
import React from "react";

type Props = {
    name: string
}

function Greeting(props: Props) {
    return (
        <h1>Hello {props.name}</h1>
    )
}
```

PropTypes are easy to get started. TypeScript is good and popular, but you have to learn it; you can create a TypeScript project with `create-react-app`. Flow is rather unpopular.

**4. State**:

State is your app's data. Popular ways to handle state in React:

* Plain React (Component state)
* Flux (Created by Facebook. It adds a centralised state)
* Redux (Very popular. Adds centralised state. Is an immutable data store)
* MobX (lightweight, and uses 'observable state')

React handles state great by itself, so the other libraries are optional.

**5. Styling**:

There are many different ways to implement styling in React, but the best is to just use what you know. Stick to a traditional CSS/Sass/SCSS approach.
