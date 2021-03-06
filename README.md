## <img src="https://camo.githubusercontent.com/6ce15b81c1f06d716d753a61f5db22375fa684da/68747470733a2f2f67612d646173682e73332e616d617a6f6e6177732e636f6d2f70726f64756374696f6e2f6173736574732f6c6f676f2d39663838616536633963333837313639306533333238306663663535376633332e706e67"> Our Example Dentist Website

### What are the objectives?
<!-- specific/measurable goal for students to achieve -->
*After this workshop, developers will be able to:*

* **Introduce** React Router into a project
* **Describe** how routing in React works
* **Build** some routes in a React app

We'll make an example Dentist website that has a `Home` page, a page that lists
available `Procedures` and a page displaying `Contact` information. Each off
these pages of content will be built into their own regular **React** component;
then we'll create a unique URL route that leads to each component.

Here's how we'll route our Single Page Application.

| **URL Route**  | **Component**  | **Content Description**                          |
|----------------|----------------|--------------------------------------------------|
| /              | `<Home>`       | A homepage with welcome text.                    |
| /procedures    | `<Procedures>` | A list of all dentist procedures.                |
| /contact       | `<Contact>`    | A page with an address, phone number, and email. |

Remember, the URL routes are paths off our main website. We could put our
website at any domain, like `www.ourdentistwebsite.com` or
`www.premiumdental.com`, and the URL route paths would behave the same. Paths
only care about what comes after the domain name.

Our routes say that if someone goes to `ourdomain.com/` they will see our
homepage with welcome text. The content of this page will all be defined in its
own component in a file called `home.js`. If someone navigates to the URL
`ourdomain.com/contact` then they'll see content with the business address,
a phone number and an email. All of this content will be defined in a component
called `Contact` in a file called `contact.js`.

You can see all of the final code and a live working copy of the site here:

Full Repo: <https://github.com/geluso/react-router-simple-dentist-site>

Live Site: <https://react-router-dentist.herokuapp.com/>

## In Your Terminal

> Remember to stop the React project you currently have running!

Now let's make the dentist project. In your terminal, type:

```
$ create-react-app dentist-website
$ cd dentist-website
$ npm start
```

Your browser should open to <http://localhost:3000/> and you'll see the standard
"Welcome to React" message with a fancy rotating atomic icon. `create-react-app`
creates several files for us in a directory called `src`. Open the `App.js`
file in your editor.

`App.js` contains our main application. You should see the basic HTML structure
of the standard React starter page. Make sure the file is the same thing you're
looking at in the browser by finding the text `Welcome to React` inside an
`<h2>` element.

Change the text to say `My First React Router App`, save the file and make sure
you see the changes automatically appear in your browser.

> If it doesn't automatically refresh, then try to manually
  refresh the page. If you still don't see changes after a manual refresh then  something could be wrong. Make sure you're editing the right file.

**Pro tip:**

It's a good idea to make simple, verifiable changes like this when
    you're first starting to make changes to a project. It's like a sanity check.

Make sure you can do simple things first. Don't start with complex things; many things can go wrong when you make complex changes. Prove to yourself the small changes work, and you'll save yourself headaches debugging large
    complex changes.


# Installing React Router
Let's install **React Router**.

Hit `ctrl-c` to stop the running app, so that we can use the terminal!

Since React Router is a third-party library, we'll need to use to download React Router and save it as
a dependency in our project.

In your Terminal, enter:

```bash
$ npm install react-router-dom
```

<!-- hand off to devs -->

# Create Custom Homepage

Let's start the app again. Put the command `npm start` in your terminal.

Let's get rid of the standard "Welcome to React" page and replace it with our
own Dentist Website Homepage. Continue editing `App.js`. Gut most of the HTML
contents, and delete the import statement for the `logo.svg` which we won't use.

The `App.js` file contains one component that our whole App will live inside
of. Remember that React components have a `render(){ ... }` function that
defines what the component will look like when it is rendered on the webpage.

> Reminder! The render function alway has to return *at most* one top-level element. It's common to wrap everything in your component in a `div``to make sure you
  satisfy this constraint.

**So...**

I added one `<h1>` that says `Dentist Website` and added a paragraph with some
short welcome text. My `App.js` file now looks like this. Save the file and go
to your browser to make sure these changes show up.

**App.js**

```javascript
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div>
        <h1>Dentist Website</h1>
        <p>
          Welcome to my dentist website.
        </p>
      </div>
    );
  }
}

export default App;
```

Good. Now we have a simple homepage set up. Let's move on to getting the rest
of the content for our site set up.

<!-- hand off to devs -->

# Creating Our Homepage Component
We've been editing `App.js`, which defines one component for our entire
application. So far our app manually shows just the homepage. Let's refactor
this so the content of the homepage is moved into its own component called
`Home`.

1. Create a new file called `Home.js`.
2. Copy and paste everything inside `App.js` into `Home.js` to use as a
  template for how to create a React component.
3. Delete the import statement for `./App.css`.
4. Find everywhere the file says `App` and rename it to `Home`. This code used
  to create a component called `App`. Now we're rewriting it to instead create a
  component called `Home`.
5. Look at the `render() { ... }` function and verify that it's returning
  content that represents our homepage. It should just be the one top-level
  `<div>`, the `<h1>` and a `<p>` paragraph element (if you used the same
  content as we did). Great. We actually don't need to make any changes here! Now you have your `Home` component.
6. Go back to the `App.js` file and delete the `<h1>` and `<p>` tags where we used to
  have content written directly inside our `App` component. We don't
  need that written inside `App` any longer, because we just moved it all to the
  new `Home` component.
7. Instead, we need to call our new component. Put `<Home></Home>` inside the `<div>` in the `App` component. This tells the
  `App` component to render the `Home` component right there inside the div.
  > Note: We have been using `<Home />` to call components. `<Home></Home>` is just a different syntax we're showing you so that if you see it elsewhere, you're familiar with it.
8. Let's try it out! Look at the browser and see if the homepage appears. Unfortunately, if you've been following along, it won't. You'll see an
  error, which should look like this:

<img width="360" alt="home-not-defined-error" src="https://user-images.githubusercontent.com/4304660/27137933-d2d1b9ec-50e4-11e7-820e-c734eb921d3e.png">

It's not enough to simply create the `Home.js` file and create the `Home`
component. We must also remember to import the component into the `App.js` file. Any components you want to use in a file need to first be imported into that file.

Your `App.js` and `Home.js` files should look like this after you've properly
created and imported the `Home` component.

<!-- hand off to devs -->

**App.js**

```javascript
import React, { Component } from 'react';
import './App.css';
import Home from './Home';

class App extends Component {
  render() {
    return (
      <div>
        <Home></Home>
      </div>
    );
  }
}
export default App;
```

**Home.js**

```javascript
import React, { Component } from 'react';

class Home extends Component {
  render() {
    return (
      <div>
        <h1>Dentist Website</h1>
        <p>
          Welcome to my dentist website.
        </p>
      </div>
    );
  }
}

export default Home;
```

# Create Components for Procedures and Contact
The purpose of our site is to create several components that we can swap out
as the main content of the main page of our application in order to create a
modern Single Page Application. We'll create two more components, and then
we'll start routing things up.

1. Create a new file called `Procedures.js`
2. Create a new file called `Contact.js`

The files
were created using the same procedure we used to create the `Home` component
using the `App` component as a template. Basically: create each file, change the
name of the component to its new name, then replace the HTML in the
`render() { ... }` function with custom content. Be sure to import each new
component into `App.js` just like we did with the `Home` component.

You can put your own content to be rendered by each component if you'd like. Refer to these complete files in the finished repo to make sure you got
everything correct:

<https://github.com/geluso/react-router-simple-dentist-site/blob/master/src/procedures.js>
<https://github.com/geluso/react-router-simple-dentist-site/blob/master/src/contact.js>

Now that we have our components made, there's nothing stopping us from importing multiple components into our App.js. So now, we have:

**App.js**

```javascript
import React, { Component } from 'react';
import './App.css';

import Home from './Home';
import Procedures from './Procedures';
import Contact from './Contact';

class App extends Component {
  render() {
    return (
      <div>
        <Home></Home>
        <Procedures></Procedures>
        <Contact></Contact>
      </div>
    );
  }
}

export default App;
```


> Check yourself! You should see all of content for each of the pages all stacked on top of each
other on the homepage. If you don't see content from all three of your
components then something is wrong. You must fix this before continuing. Always:
do simple things before doing complex things!

<!-- turn  over to devs -->

# Displaying Pages Individually

Try manually deleting two of the three components so only one component is left
on the page at a time. You should see your webpage update with just that
component. This is effectively what **React Router** does. We can configure React Router
so that it's aware of which component we want to show on the screen, and React
Router will swap the components out so that only the correct one is shown at a time.

Now that we've proven to ourselves that we're able to show each of the
components on the main page, it's time to hook them up to Router.

## Creating Routes
Here's the general syntax for creating routes. React Router uses some of its own components to define how URLs are routed
to your components and to create links to those routes. You must have one `<Router>`
component that wraps itself around multiple `<Route>` components. Each `<Route>`
component has two pieces:
- `path` - defining the URL path that leads to the component.
- `component` - defining
what component users will see when they navigate to the path.

```js
<Router>
  <div>
    <Route exact path="/" component={Home} />
    <Route path="/procedures" component={Procedures} />
    <Route path="/contact" component={Contact} />
  </div>
</Router>
```

There are three other important things to note here:

- This goes *in place of* your existing component calls of `<Home />` or `<Home></Home>` (depending on which syntax you went for).

- The first route for the homepage at the root URL path `/` uses a
special extra `exact` attribute before defining the path. The `exact` attribute
means the component associated with the route will only be shown if users are
at exactly that URL path. If you forget to include the `exact` keyword then
when someone navigates to `/contact` they will actually see two components,
because `/` is a partial match for `/contact`.

- Notice that all of the `<Route>` components are wrapped inside one `<div>`. Like `render`, the
`<Router>` element requires that it only has one direct child element. If you don't
wrap the routes with a `<div>`, the page will appear blank, and you'll have to
open your JavaScript console to see that there's an error being logged to the
console. Like so -

<img width="719" alt="router-requires-only-one-child" src="https://user-images.githubusercontent.com/4304660/27137977-f6d2e208-50e4-11e7-81af-1e6374a759fe.png">


**Pro tip:** It's a good habit to check the console for errors whenever your
app is not behaving as expected.


## Import Statements
In order to use the React Router components, you'll need to import them. This
import syntax allows us to grab several specific components out of the
`react-router-dom` library at once. So far we've used `Router` and `Route`.

The Router component is actually called `BrowserRouter`
inside the library package, but we'll use the `as` keyword to rename it to
`Router` so it's easier to remember.

While we're here, we'll also import a third component, `Link`, which we'll get to in a minute.

```
import {
  BrowserRouter as Router,
  Route,
  Link
} from 'react-router-dom';
```
<!-- turn  over to devs -->

## Fully Routed
Here's how the imports and all the components look like together for our dentist
website:

**App.js**

```javascript

import React, { Component } from 'react';
import './App.css';

import {
  BrowserRouter as Router,
  Route,
  Link
} from 'react-router-dom';

import Home from './Home';
import Procedures from './Procedures';
import Contact from './Contact';


class App extends Component {
  render() {
    return (
      <Router>
        <div>
          <Route exact path="/" component={Home} />
          <Route path="/procedures" component={Procedures} />
          <Route path="/contact" component={Contact} />
        </div>
      </Router>
    );
  }
}

export default App;
```

# Navigate to the Routes
Now that everything is hooked up you can manually enter different URLs and
see how your page appears. If you go to <http://localhost:3000/>, you should
see just the homepage. If you go to <http://localhost:3000/procedures>, you should
see just the procedures page. If you go to <http://localhost:3000/contact>,
then you should see just the contact page.

> Check it!
> * Make sure that React Router is routing from each URL to the proper component
correctly.
> * Double check to make sure that the home page doesn't display at the
same time as another component. If the homepage is shown while you're at the
path to `/procedures` or `/contact` then you probably did not write the `exact`
keyword when you defined the `/` Home route.

## Debugging Common Errors
Let's intentionally make an error. Delete the `exact` keyword off the Home
route. Navigate to the `/procedures` page and the `/contact` page again and
see how the components are displayed. You should see the content of the
homepage and the content for one of the other pages at the same time, with
the home page on top.

Now add the `exact` keyword back to the home route and notice that the pages
don't double up any more.

Two common errors:
1. If the page appears blank, open the JavaScript console to see if there are
  errors. Chances are you have a typo somewhere or forgot to make sure the
  `<Router>` only has one child element. Remember, wrap all of your `<Route>` components
  in one `<div>`.
2. If multiple components appear on the page at the same time there's
  something with how you've routed URLs. Make sure you use the `exact`
  keyword on the root path `/` and make sure there are no duplicate URL paths
  defined anywhere.

# Adding a Nav Section
Great, now our site is up and running! We can manually type in URLs and see the
different pages.

Although... users never really type URLs, do they? We should probably have links at the top of the page so we can just click on
things. We could build this ourselves, but we don't have to! Remember that `Link` component we imported from React Router?

Just like links in HTML, we can wrap `<Link>` tags around whatever text that we want to display to the user to click on. The pieces of this are:

* `<Link>` - creates `<a>` tags and automatically integrates
  modern HTML5 browser history mechanics for the Single Page Application. It
  has one attribute:
* `to` - what path to navigate to when the user clicks the link

We'll add one `<Link>`
  component that leads to each of our different content pages.

```js
<Link to="/">Go to Home Page</Link>
<Link to="/procedures">See Our Procedures</Link>
<Link to="/contact">Contact Us!</Link>
```

> Did you notice that we don't reference components here? We simply make links for users to click that connect to URLs, and the `Router` section in the code handles the actual component changes.

We can include those links in a `<nav>` element at the top of our page.
It will stay on the page permanently, and the different components will be
swapped between each other below it. There's actually nothing special about
the `<nav>` element. It behaves exactly like a `<div>`. `<nav>` Is just a
semantic element that gives your HTML more meaning when people read it.

So, our web app now looks like the left image - but do you see a difference between the left and the right?


<img width="530" alt="manual-spaces-in-nav" src="https://user-images.githubusercontent.com/4304660/27138270-c1643d78-50e5-11e7-8836-6dd12077159b.png">

There's one slightly annoying thing about React here - React strips out whitespace between elements. If we write `<Link>` components next to each
other, even if they're on new lines, React strips all of the whitespace
(spaces, returns, tabs...) between them and squishes them all together.

We
must insert a space manually by writing `{' '}` in order to get spaces between
our links.

So instead, here's how we'll write the links. Nothing has changed except that we've added the space:

```
<Link to="/">Go to Home Page</Link>{' '}
<Link to="/procedures">See Our Procedures</Link>{' '}
<Link to="/contact">Contact Us!</Link>
```

And now the nav bar will have spaces like it should.


# Final Code
Here's what our final `App.js` looks like:

```js
class App extends Component {
  render() {
    return (
      <Router>
        <div>
          <nav>
            <Link to="/">Go to Home Page</Link>{' '}
            <Link to="/procedures">See Our Procedures</Link>{' '}
            <Link to="/contact">Contact Us!</Link>
          </nav>
          <Route exact path="/" component={Home} />
          <Route path="/procedures" component={Procedures} />
          <Route path="/contact" component={Contact} />
        </div>
      </Router>
    );
  }
}

export default App;
```

> Check it out! Does yours work?

