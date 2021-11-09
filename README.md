## StateManager.js

`npm i anotherstatemanager`

Simple state manager.

Set key responses to have functions fire when keyed values change. Can be set to run on a timer interval, or only fire when triggered, or you can stack sequential updates to fire per frame (e.g. summing key inputs). Very flexible, dependent on our ObjectListener.js



Example:
```
import {StateManager} from 'anotherstatemanager'

let state = new StateManager();

let sub = state.subscribe('x',(newx) => {console.log(newx);});

state.setState({x:3});


state.setState({...keys:values})

state.subscribe(key,onchange)
state.subscribeTrigger(key,onchange)
state.subsribeSequential(key,onchange)

state.unsubsribe(sub)
state.unsubscribeTrigger(sub)
state.unsubscribeSequential(sub)
//...

```

There are 3 different state systems stacked on top of each other. You can set up the state
manager to only use triggers (by setting defaultKeyEventLoop to false on init) which run exclusively
on setState, avoiding needless timer checks. Individual subscriptions can be set to not run the checkers too, you can get pretty complicated but it's easier to keep different states with different schedules.


The rest of the functions are pretty much internal use only.

You can directly mutate state.data.x etc. which will still update the timer-check data, but will miss triggers.

The crux of this relies on a heavily modified JSON.stringifyFast function which lets you monitor large objects and arrays with a fast, shallow deep-copy system. We hammered it out to deal with giant objects or arrays etc. as lazily as possible, just watch your performance if you're also gonna be that lazy as it has a few catches.



By Joshua Brewster and Garrett Flynn
License: AGPL v3.0

