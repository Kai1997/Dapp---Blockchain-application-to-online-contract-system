# A test project to get familiar with React Router v4


![](./rr4.png)


## create-react-app

We use the [Facebook React Boilerplate](https://github.com/facebookincubator/create-react-app) to get started:

```
create-react-app react-router-4
```

And add some [Bootstrap](https://react-bootstrap.github.io/getting-started.html) for styling:

```
npm install --save react-bootstrap
```

We can now add the Bootsrap CSS inside the head of _./public/index.html_ :

```html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css" integrity="sha384-PsH8R72JQ3SOdhVi3uxftmaW6Vc51MKb0q5P2rRUpPvrszuE4W1povHYgTpBfshb" crossorigin="anonymous">
```

And the Javascript at the end of the body tag:

```html
<script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.3/umd/popper.min.js" integrity="sha384-vFJXuSJphROIrBnz7yo7oB41mKfc8JzQZiCq4NCceLEaO4IHwicKwpJf9c9IpFgh" crossorigin="anonymous"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/js/bootstrap.min.js" integrity="sha384-alpBpkh1PFOepccYVYDB4do5UnbKysX5WZXm3XxPqe5iKTfUKjNkCk9SaVuEZflJ" crossorigin="anonymous"></script>
```

To add a simple Navbar on top, we will now replace the default create-react-app JSX inside _./src/coponents/app.js_ with a Bootstrap Navbar from their [Example list](https://getbootstrap.com/docs/4.0/examples/) (remember to replace all instances of __class__ with __className__!):

```js
return (
  <div className="App">
    <nav className="navbar navbar-expand-md navbar-dark bg-dark fixed-top mb">
      <a className="navbar-brand" href="#">React Router 4</a>
      <button className="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarsExampleDefault" aria-controls="navbarsExampleDefault" aria-expanded="false" aria-label="Toggle navigation">
        <span className="navbar-toggler-icon"></span>
      </button>

      <div className="collapse navbar-collapse" id="navbarsExampleDefault">
        <ul className="navbar-nav mr-auto">
          <li className="nav-item active">
            <a className="nav-link" href="#">Page 1 <span className="sr-only">(current)</span></a>
          </li>
          <li className="nav-item">
            <a className="nav-link" href="#">Page 2</a>
          </li>
        </ul>
      </div>
    </nav>

    <div className="jumbotron mt">
      <div className="col-sm-8 mx-auto mt">
        <h1>This is just a Test</h1>
        <p>
          <a className="btn btn-primary" href="#" role="button">View navbar docs &raquo;</a>
        </p>
      </div>
    </div>

  </div>
);
```

Now start the app with:

```
npm start
```

The Bootstrap Navbar should now show up in our React app on _locallhost:3000_:

We can now use the [basic example](https://reacttraining.com/react-router/web/example/basic) from the reacttraining.com website to add some routing to our app. First install the web based router - which is now called react-router-dom:

```
npm install --save react-router-dom
```

To add links to our navigation, we will need the [\<NaveLink/\> component](https://reacttraining.com/react-router/web/api/NavLink), which is special version of the \<Link/\> that will add styling attributes to the rendered element when it matches the current URL (activeState). Replace all:

```html
<a href="#"></a>
```

with

```html
<NavLink to="#"></NavLink>
```

and import \<NavLink /\> from react-router-dom:

```js
import { NavLink } from 'react-router-dom'
```

We created two links to two components, aptly named _/page-1_ and _/page-2_, that we now have to create inside the _./src/components_ directory. For \<PageOne /\> we want to use an __ES6 Class Component__ to render some JSX:

```js
import React, {Component} from 'react'
import { Link } from 'react-router-dom'
import { Button } from 'react-bootstrap'

class PageOne extends Component {
  render() {
    return (
        <div className="jumbotron mt">
          [...]
        </div>
    );
  }
}

export default PageOne
```

And for \<PageTwo /\> we use a __Stateless Component__:

```js
import React from 'react'
import { Link } from 'react-router-dom'
import { Button } from 'react-bootstrap'


const PageTwo = () => (
    <div className="jumbotron mt">
      [...]
    </div>
)

export default PageTwo
```

Make sure to import all components in _./src/index.js_:

```js
import App from './App';
import PageOne from './PageOne';
import PageTwo from './PageTwo';
```

As well as adding the Router itself:

```js
import {
  BrowserRouter as Router,
  Route,
  Link
} from 'react-router-dom'
```

Now we can copy the navigation (everything inside the \<nav\> tag) from  _./src/components/app.js_ to _./src/index.js_ and replace the \<App /\> component that was placed there by create-react-app. Then wrap the JSX into a \<Router\> tag:

```js
render(
  <Router>
    <div className="container">
      <nav className="navbar navbar-expand-md navbar-dark bg-dark fixed-top mb">
        <NavLink className="navbar-brand" to="/"> <img src={Logo} alt="React Router v4" /> </NavLink>

        <button className="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarsExampleDefault" aria-controls="navbarsExampleDefault" aria-expanded="false" aria-label="Toggle navigation">
          <span className="navbar-toggler-icon"></span>
        </button>

        <div className="collapse navbar-collapse">
          <ul className="navbar-nav mr-auto">
            <li className="nav-item">
              <NavLink className="nav-link" to="/page-1">Page 1</NavLink>
            </li>
            <li className="nav-item">
              <NavLink className="nav-link" to="/page-2">Page 2</NavLink>
            </li>
          </ul>
        </div>
      </nav>

      <Route exact path="/" component={App}/>
      <Route path="/page-1" component={PageOne}/>
      <Route path="/page-2" component={PageTwo}/>
    </div>
  </Router>,

document.getElementById('root'))
```
