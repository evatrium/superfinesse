# superfinesse

> inspired by [superfine](https://github.com/jorgebucaran/superfine) with a little extra finesse.

- Capable of renderng into shadowRoot
- Support for Fragments and root level Fragments
- upgraded preact-inspired props diffing (style objects and more...)

### Installation

```sh
npm i superfiness
```

### Usage

```js
import {h, render, mount} from 'superfinesse';

let state = {count: 0};

const Button = ({children, ...rest}) => {

    return (
        <button style={{
            background: 'red',
            height: 40 /*pixels/dimensional units inferred*/
        }} {...rest}>
            {children}
        </button>
    )
};

const App = () => {

    let {count} = state;

    return (
        <Fragment>
            
            <h1>count: {count}</h1>

            <Button onClick={() => update({count: count++})}>
                click me
            </Button>
            
            <div dangerouslySetInnerHTML={{__html:`
                <h2>just like preact, diffing children will be skipped here</h2>
            `}}/>       
            
        </Fragment>
    )
}


const root = document.createElement("div");
document.body.appendChild(root);


const update = (newState) => {
    state = {...state, ...newState};
    render(<App/>, root);
}

update();

```
