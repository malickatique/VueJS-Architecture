
## Vue Js

### Vue as a flavour

- Add Vue Js library in main HTML document
- Create a vue element 
```js
    Vue.createApp({
        // 1. A data function that returns an object.
        data() 
        {
            return {
                tasks: [],
                enteredTask: "",
            };
        },
        // 2. A Methods / Functions Object or Key-Value pair
        methods: {
            addTask() {
                this.tasks.push(this.enteredTask);
            }
        }
    });
```
- Bind the Vue object with a HTML element
```js
    Vue.createApp({
        // Data, Methods, Hooks ...
    })
    // Vue element id
    .mount("#app");

    // OR
    const app =Vue.createApp({
        // Data, Methods, Hooks ...
    });
    app.mount("#app");

```
- Vue Js can have or run multiple apps concurrently

### Virtual DOM

- Vue Instance (JS) -> Virtual DOM (JS memory) -> Vue Template Rendering -> Browser DOM
- Vue removes its own syntax/instructions when rendering template to Browser DOM
- Vue does not rerender everything upon changes BUT only the parts that did change.
- Vue compares Browser DOM and Virtual DOM and only differences are then rendered onto browser.
- Behind the scenes Vue does not take entire copies of DOM as Virtual but does some optimisations before.

### Vue Instance Lifecycle

```js
// Step1. Create and Bind Vue App
createApp({...});
mount("#app")

// ==== Life Cycle Hooks ==== //

// Run before the app has fully initialized
beforeCreate()

// After the app has been creted/initialized
// Aware of data and other general app configurations
created()

// :
// :    Template Compilation
// v
beforeMount()

// Upuntil now, nothing appears on the screen
// Browser rendered Vue tempalte/component on the screen
mounted()

// /Mounted Vue Instance/

// === Reverse Cycle Starts

// /Data Changes/ Vue UnMounted/

// Before the update has processed
beforeUpdate()

// After processing update
// Templete does not unmount in this cycle
// Rerendering template's updated part and showing it on browser
updated()

// After mounted() an app can also me unmounted
// Unmounted = All vue content wiped out
// Trigger following by
app.unmount()

// Things to save - check for any pending tasks
beforeUnmount()

// Cleanup code
unmounted()

// Imp: All the methods will be used in Vue instance's methods, data hierarchy.
```

### 'this' keyword
- Refer to Vue object and Vue also merge data attributes/values with 'this' keyword

### Essentials

- To output / render any Javascript expression {{ variable Or if(a==b) ? a : b }}
- v-html directive is use to render a string as HTML. Avoid it to prevent XSS.
- v-bind:attributeName For setting value of an attribute. i.e; v-bind:href="url" OR :href="url"
- v-model="propertyName" Two way binding. Shortcut for v-bind.
- methodName($event, arg1)

```js
    // Push items at the end of array
    this.tasks.push({task});    // It can be object, string or any other data type

    // Push items at the start of array
    this.tasks.unshift({task});    // It can be object, string or any other data type

    // Remove item in an array
    // Remove 1 element at 'index'
    this.tasks.splice(index , 1);
```

#### Conditional Rendering

```html
    <!-- Pro Tip: -->
    <!-- v-show only makes element hidden "display: none" -->
    <!-- Use this only for visibility purposes -->
    <p v-show="test.length === 0"> Test is empty. </p>

    <!-- Or if-else -->
    <!-- This will not render the element in first place -->
    <p v-if="test.length === 0"> Test is empty. </p>
    <p v-else-if="test.length === 1"> Test has something. </p>
    <p v-else="test.length === 0"> Test is not empty. </p>
```

#### Rendereing List

```html
    <ul>
        <li v-for="task in tasks"> {{ task.name }} </li>

        <!-- Get index or key of an item -->
        <!-- key is a unique identification of each item it's default in HTML not native for Vue Js -->
        <li v-for="(task, index) in tasks" :key="index"> {{ task.name }} </li>

        <!-- Loog through a range of number. 1 to 10 -->
        <li v-for="num in 10"> {{ num }} </li>
    </li>
```

#### Styling

- Inline Styling
```html
    <p v-bind:style="border-color: red;" ></p>
    
    <!-- OR -->
    <p :style="border-color: red;" ></p>
    
    <!-- Conditional Style -->
    <p :style="{ borderColor: isSelected ? 'red' : '' }" ></p>

```

- Class Styling
```html
    <p v-bind:class="isSelected ? 'active' : '' "></p>

    <!-- class 'contentA' added by default then 'active' will be added when isSelected becomes true -->
    <p v-bind:class="{ contentA:true, active: isSelected }"></p>
```

#### Events
- v-on shorthand is @
- v-on:eventName; eventName inclue all the events for HTML elements
- v-on:click or @click
- v-on:input => Method(evt) => event.taget.value => To get input value.
- v-on:submit.prevent
- v-on:keyup.enter == When enter key pressed.
- We can add multiple events inside a single HTML element.

<!-- Pro -->
- @click.stop  This will stop propagation of event and only remains there.

#### Computed Properties
- Are just like methods, but they only invocked when their dependency change.
```js
// Define in the same hierarchy as of 'data' or 'methods'
computed: {
    // Mostly it's methods used as data properties to return some content
    // This method will invoke whenever 'firstName' or 'lastName' changes AND once initially
    // It will watch all properties used or referenced within this method
    fullName() {
        return this.firstName + " " + this.lastName; 
    }
}

// To use computed properties we can not add () after
{{ fullName }}
```

#### Watchers
- 
```js
    data: {
        name: "",
    },
    watch: {
        // It can watch only one attribute at a time
        // It's method has same name as it has in data
        // We don't use to to return a modified value instead here we write any logical code.
        name(latestedValue) {
            this.fullName = "Dr. "+value;
        }
    }
```


#### Vue Js $ref
```js
    <p ref="test1"></p>
    this.$ref // contains global variables key value paris
    this.$ref.test1 // Will get the entire element with JS attributes
```

#### Vue Js separate template

```js
    const app =Vue.createApp({
        template: `
            HTML, JSX here
        `,
        data() {

        }
        // Data, Methods, Hooks ...
    });

    // Render the template in app in id="app"
    app.mount("#app");

```

### Vue CLI
- It helps us create project and a gives us a starting point boilerplate.
- Add Vetur extension in VS Code

#### Installations

```shell
    # 1. Install Node - check 
    node -v

    # 2.Install Vue CLI globally
    npm install -g @vue/cli
    
    # 3. Install Vue
	clear		 # this "vue" we get via Vue CLI
    
    # 4. Install dependencies: 
    npm install
    
    # 5. Run: 
    npm run serve
```

### Basics
- We will import the things we need from "Vue" library then use it like;
i. import { createApp } from 'vue'		// grabs 'createApp' function from 'vue' lib in node_modules
ii. import App from './App.vue' 	// import main "Vue" component and mount it to root id "#app" - Root Component for SPAs
iii. main.js is the starter point for Vue app


### Vue Components

- Components are reusable, maintainable, loosely connected Vue Js sub-app or nested app
- Components can split to chunks big applications
- Components are mini-apps of Vue Js
- Components contains their own HTML-templates
- Every Vue component contains; 1.Template (mand), 2.Script(optional), 3.Style(optional)

#### Creating a Component

* Component without CLI
```js
// 1. Create Vue Component
// arg1: Component name HTML tags-like
// arg2: contains Vue App Configurations like data, methods and importantly `template`
app.component("html-content", { VueComponent });

// Example
app.component("contact", {
    template: `<p>Contact</p>`,
    data() {},
    methods: {}
});

// 2. Use Component
<contact></contact>
```

1. A Vue Component `PascalCase.vue`
```js
// Template for this component
<template>
    // HTML
</template>

// Vue App for this component
<script>
    export default {
        data() {},
        methods: {},
        mounted(),
    }
</script>

// Styles for this component
<style></style>
```

#### Component Registration

1. Registering globally

```js
import Task from "./components/Task.vue";
app.component("task", Task);

// Now we can use Task component anywhere in Vue app 
<task></task>
```
2. Registering locally or for a component only

```js
<template>
    <task-comp></task-comp>
</template>

<script>
    import Task from "./components/Task.vue";
    export default {
        components: {
            "task-comp": Task
        }
    }
</script>
```

#### Component Styling

0. Add stylesheets in index.html
```html
    <!-- 
        Only add stylesheets here that will be used throughout the application
        Otherwise add component based stylesheets in components
    -->
```

1. Use styling in Task.vue component
- Global Styling
```js
    <template></template>
    <script></script>

    // It will always be treated as global styling and will affect entire app
    <style>
        // Your stylesheet
    </style>
```

- Pro! Scoped or component-only styling
```js
    <template></template>
    <script></script>

    // It will applied to only this Vue component
    // This will affect the template in this component
    <style scoped>
        // Your stylesheet
    </style>
```

#### Component Communication

1. Props (Parent to Chil Communication)
- Pro! Props should not be mutated. Here data is uni-directional and can not be changed in Child Component it can only be changed in parent compoennt.

```js
// 1. Send Props from parent component
<contact
    name="malik atique"
    phone-number="+92 (304) 8486 653"
></contact>

// 2. Receive Props in Child Component
<template>
    // To avoid conflicts don't use same props names as of in data
    {{ phoneNumber }}
</template>
<script>
    export default {
        props: [
            "name",
            "phoneNumber"   // Remember no - in here
        ],
        // Vue automatically inject the props in `this` like it does with `data` object
        mounted() {
            this.phoneNumber;   // +92 (304) 8486 653
            this.phone-number;   // Invalid
        } 
    }
</script>
```

- Validating Props
```js
export default {
    props: {
        // If received name type is not string it will throw error
        name: String,

        // More validation
        phone: {
            type: String,
            required: true,
            default: "+920000000000",   // Here ir can also be a function getDefault(){}
            // Add Validation Logic
            validator: function (value){ return true; }
        }
    }
}
```

2. Emitting Custom Events (Child to Parent Communication)

- Emit a custom event from Child Component
```js
    // Click on a button, value changed or some other event happened
	// Child Component Event Emit
	closeModel()
    {
		this.$emit('close-it-now')

		// Pass data to events
		this.$emit('close-it-now', [12.51])
		this.$emit('close-it-now', 75)
	}
```

- Receive or handle event in parent component
```js
	// Parent Component Event Listening
    // Listen that where you use/insert the component
	<Modal
        // Props
        title="Some Title" 
        v-on:close-it-now="closeMyModal"
        // @close-it-now="closeMyModal"   // OR shorthand
        >
    </Model>

	closeMyModal(modelId) {
		// code `modelId`
	}
```

- Validating Custom Events from where they will emit or triggered
- This is used mostly to document code or to let other developers know what to handle
- It also helps in dev process to handle bugs
```js
    export default {
        props: [],

        // emits: ["close-it-now"],     // Basic way of telling
        emits: {
            "close-it-now": function (params) { return true; Perform event data validation }
        }
    }
```

- Event emitting passing tunnel
```js
// Parent Component
<a-component
    @select-topic="selectTopic"
></a-component>

// a-component has
<b-component
    @select-topic="$emit('selectTopic', $event)"
></b-component>

// b-component
<button @click="$emit('selectTopic', 12)">Topic12</button>

// The above will forward event from Child to It's parent then from parent to paret's parent.
// The event has no use in a-component as it is just passing
// Vue has an alternative to that called Injecting
```

3. Pro! Provide and Inject Pattern of component communication
- It is a parent to it's sub child components communication
- It avoid data passing through components
- It can be use to pass data and custom events (passing method)

- 1. Provide will declare data to share in the parent component
```js
    export default {
        data(){},
        provide: {
            // data goes here
        }
    }
```

- 2. Inject will receive data in any nested child component and use it there
```js
    export default {
        data(){},
        inject: ['dataA'],  // where `dataA` is a key from `provide` object
    }

    // Then use it just like props
```

- Important!
- Pro! To make sure the `provide` and `data` data is consistent when they're using the same data. `provide` will create a separate brand new data object. Thus not connected with `data`.

```js
    export default {
        data(){},
        provide() {
            return {
                // Here provide uses data from data of component.
                // Thus makes it consistent
                topics: this.topics
            }
        }
    }
```


<!-- OLD Documentation -->

#### Vue Slots

##### Simple Slots

- They allow to receive HTML content and place it within reusable HTML components
- Pro! Styling in main component does not affect or applied to the slots in another component/slot

1. Create a slot
```js
<template>
    <div class="card box-shadow">
        <slot></slot>
    </div>
</template>

<script>
    export default {}
</script>

<style scoped>
</style>
```

2. Regsiter the slot just like a components
```js
import Card from "./slots/card.vue";
app.component("card", Card);

```

3. Use the slot
```js
    <card>
        <h2>Title</h2>
    </card>
```


##### Named Slots
1. Create Slot
```js
<template>
    <div class="card box-shadow">
        <header>
            <slot name="header">
                // Pro! We can also add default content here!!
            </slot>
        </header>
        <body>
            // Only one can also be default or unnamed slot
            <slot></slot>
        </body>
    </div>
</template>

<script>
    export default {}
</script>

<style scoped>
</style>
```
2. Use Slot
```js
    <card>
        // Will go to the header slot
        <h2 v-slot:header>Title</h2>

        // Will go to the default or un-named slot
        <div v-slot:deafult>
            <p> Description </p>
        </div>
    </card>
```

##### Advanced on slots
- `this.$slots` to access all slots within a slot component
- `this.$slots.header` to access a specific slot. Wether provided or not.
- v-slot:slot-name === #slot-name  A shorthand.
- Scoped Slots : learn more about it...

#### Dynamic Components
- the <component> tag is provided by Vue
```js
    // this will render only the component that is active
    <component v-bind:is="selectedComponent">
    </component>

    // The component will not be unmounted entirely; their state will be preserved
    <keep-alive>
        <component v-bind:is="selectedComponent">
        </component>
    </keep-alive>
```

#### Teleporting Elements
- Is used to transfer an element to anywhere in the DOM structure.
- Vue provides <teleport to=""> tag and a prop to achieve that
- In `to` prop we can select any CSS selector

```js
    // This will render Model in <body>
    <teleport to="body">	// .modals class
      <Modal>
        <!-- code -->
      </Modal>
    </teleport>
```

### Vue Forms

```js
    <input type="number" v-model.number="age">
```

- we can use components to as a form field to get form data.
1. Vue component as an form Input
```js
    // v-model for a component
    // It will send a prop
    // this `rating` is an initial value for this component input
    <comp
        v-model="rating" ref="ratingInput" 
    >
    </comp>
```

2. Vue Component itself as Input
```js
export default {
    props: ["modelValue"],
    emits: ["update:modelValue"],
    methods: {
        getRating(value) {
            this.$emit("update:modelValue", value);
        }
    }
}
```

### Vue HTTP Requests

#### `fetch` the default function of JS

##### POST request
```js
    fetch("https://www.google.com/add-profile", {
        method: "POST", // GET, DELETE, PATCH etc.
        headers: {
            "Content-Type": "application/json",
        },

        // Data as object
        body: {
            name: "Malik Atique",
            whatsapp: "+92 (304) 8486 653"
        }
        
        // OR use data as json
        body: JSON.stringify({
            name: "Malik Atique", 
            whatsapp: "+92 (304) 8486 653"
        })  
    });

```

##### GET Request
```js
    fetch("https://www.google.com/view-profile", {
        method: "GET", // Or don't specify coz default is GET
    });

    // OR
    fetch("https://www.google.com/view-profile")
    .then(function(response) {
        if(response.ok) // default ok property to check request status
        {
            // Parse data if it is in JSON format
            // It's another promise
            return response.json()

            // If data comes as object/array
            response.data
        }
    })
    .then( (data) => {  // Use arrow function to access vue `this` keyword
        console.log(data);
    })
    // Handle Errors
    .catch( () => {

    });
```

##### Handling Erros

```js
    fetch("https://www.google.com/view-profile")
    .then( (response) => {
        // Can alo handle here
        if(response.ok) {
            // OK
        } else {
            // This throw will be caught in catch()
            throw new Error("Could not save data!");
        }
    })
    // Handle Errors
    .catch( (error) => {
        console.log(error.message); // Output: Could not save data!
    });
```

#### `axios` library to make HTTP requests

## Vue Router

- Vue intercepts the request and check URL and inject compnents according to routes. 
- install vue router: select Router when installing vue project
