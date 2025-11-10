# React js framework 
## in simple language .not exact 
i understand that when we write const [materialName, setMaterialName] = useState(""); we are creating a variable called materialName which is a pointer..it has address of some storage location.. and that address cannot be changed that is why it is declared const.. but the value in that address can change.. the inital value is set by usestate("") which is setting it to empty string.. and setMaterialName is the method that will have the authority to chagne the value in that address.. and the power of this syntax is whenever the setMaterialName changes the value in the location whose address is in materialName, all UI elements will show the new value in that location pointed by that adddress.. ..

Rendering means React executing your component to produce a tree of elements that describes the UI.That description is compared with the previous one, and only the changed parts are updated on the page.

Code calls setting on a variable > react schedules a render > calls component again > diff done between new result and old result > changes are made in DOM and committed > Browser repaints the UI.

```
When a render happens
Initial mount: The very first time your app or component appears.
State updates: Calling a setter like setMaterialName(...).
Prop changes: A parent passes different data down.
Context changes: Values from React context update.

What happens during render
Render phase: React calls your components to compute the next UI description (elements/virtual tree).
Diffing: React compares the new description with the previous one to figure out what changed.
Commit phase: React applies those changes to the real DOM; the browser then paints the screen.

Is React a compiler or interpreter?
React itself is a runtime UI library that schedules and reconciles updates in JavaScript; it’s not a compiler or interpreter.
JSX you write is typically compiled by build tools (e.g., Babel/TypeScript + bundler) into plain JavaScript before it runs in the browser.
During development, a dev server may “watch” files and hot-reload, but React’s update loop is event-driven (state/props changes), not a source-code interpreter.
```

What is a primitive?
In JavaScript, primitives are: string, number, boolean, bigint, symbol, undefined, and null.
Primitives are immutable and copied by value; objects and arrays are reference types and are copied by reference.
This is why updating object/array state should create a new object/array rather than mutating in place.?????

## more accurate way of thinking
Mostly correct, but two important fixes: JavaScript doesn’t expose “addresses,” and the const variable isn’t a persistent pointer; instead, React stores the state internally and gives your component the latest value on each render.

### What you got right
- Initial value: useState("") sets the first state value to an empty string.  
- Updates: setMaterialName(...) is the supported way to change the state.  
- UI refresh: Calling the setter updates state and triggers a re-render, so the UI shows the new value.

### What’s not quite right
- No raw pointers: JavaScript doesn’t give access to memory addresses, so materialName isn’t a pointer you mutate in place.  
- Const nuance: const means the variable binding in that render can’t be reassigned, but React will call your component again with a fresh binding holding the updated value on the next render.

### How it actually works
- React keeps state in its own internal memory, keyed by the order of hooks in the component.  
- On each render, useState returns a pair: [currentValue, setter]. Your const binding receives that currentValue for this render.  
- When you call the setter, React stores the new value internally and re-renders; on the next render, materialName equals the new value.

### Quick mental model
- Think: “React stores my state; each render gives me the latest snapshot (materialName) and a button to change it (setMaterialName).”  
- For primitives (string/number/boolean), React replaces the old value.  
- For objects/arrays, avoid in-place mutation; create a new object/array and pass it to the setter.

