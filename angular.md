# Angular
A small Collection of Angular best practices.

## Use Angular CLI
```bash
# Install Angular CLI

npm install -g @angular/cli

# Check Angular CLI version

ng version
```

## Maintain proper Folder Structure
```
-- app
    |-- modules
    |-- home
        |-- [+] components
        |-- [+] pages
    |-- home-routing.module.ts
    |-- home.module.ts
    |-- core
        |-- [+] authentication
        |-- [+] footer
        |-- [+] guards
        |-- [+] http
        |-- [+] interceptors
        |-- [+] mocks
        |-- [+] services
        |-- [+] header
        |-- core.module.ts

|-- shared
    |-- [+] components
    |-- [+] directives
    |-- [+] pipes
    |-- [+] models

|-- [+] configs
    |-- assets
    |-- scss

|-- [+] partials
    |-- _base.scss
    |-- styles.scss
```

## Follow Consistent (Angular) Coding Styles

Always separate your components into three main files components, template and style.

### Component
- Define small functions

- Have consistent names for all symbols. The recommended pattern is feature.type.ts.

- If the values of the variables are intact, then declare it with ‘const’.

- Use dashes to separate words in the descriptive name and use dots to separate the descriptive name from the type.

- Names of properties and methods should always be in lower camel case.

- Always leave one empty line between imports and modules; such as third party and application imports and third-party modules and custom modules. Starting with Angular Imports, then Third-Party-Imports and last custom modules.

- Use Safe String Declarations
```js
private vehicleType: string;

// We can assign any string to vehicleType.
this.vehicleType = 'four wheeler';
this.vehicleType = 'two wheeler';
this.vehicleType = 'car';
```

```js
private vehicleType: 'four wheeler' | 'two wheeler';
this.vehicleType = 'four wheeler';
this.vehicleType = 'two wheeler';

this.vehicleType = 'car'; // This will give the below error

Type '"car"' is not assignable to type '"four wheeler" | "two wheeler"'
```

- Avoid "any" Type use Safe Strings or Types instead

### Template
- Always structure your HTML like to maintain clarity e.g. 
```html
<div class="wrappaer"
     attribute="value"
     [dynamicAttribute]="dynamicValue"
     (emitter)="onFunctionTriggered"
>
    <div class="content" />
    <div class="content" />
</div>
```
- Use trackBy along with ngFor
```html
<!-- Now, each time the changes occur, the whole DOM tree will be re-rendered. -->
<li *ngFor="let item of itemList;">{{item.id}}</li>
```

```html
<!-- Now, it returns as a unique identifier for each item so only updated items will be re-rendered. -->
<ul>
  <li *ngFor="let item of itemList; trackBy: trackByFn">
    {{item.id}}
  </li>
</ul>
```

```js
trackByFn(index, item) => index; // or item.id
```

- No Logic in Templates, Use Variables in Component in Combination with custom Types

- Use async pipe in templates
```html
<!-- No Async Pipe -->
{{ text }}

<!-- Async Pipe in combination with Observables -->
{{ text | async }}
```

### Style
- Always declare classes according to the usage sequence in template for easy and quick adjustments.

## Typescript
Typescript is a superset of Javascript, which is designed to develop large Javascript applications. You don’t have to convert the entire Javascript code to Typescript at once. Migration from Javascript to Typescript can be done in stages.

- Use Types instead of Enums in order to use Typescript Type Checking and to reduce the amount of files served

## Use ES6 Features
- Arrow Functions

- String interpolation

- Object Literals

- Let and Const

- Destructuring

- Default

## Single Responsibility Principle
Large components are very difficult to debug, manage and test. If the component becomes large, break it down into more reusable smaller components to reduce duplication of the code, so that we can easily manage, maintain and debug with less effort.

## Use Lazy Loading
Try to lazy load the modules in an Angular application whenever possible. Lazy loading will load something only when it is used. This will reduce the size of the application load initial time and improve the application boot time by not loading the unused modules.

```js
// Without Lazy Loading

// app.routing.ts
import { WithoutLazyLoadedComponent } from './without-lazy-loaded.component';

{
path: 'without-lazy-loaded',
component: WithoutLazyLoadedComponent
}
```

```js
//With Lazy Loading

// app.routing.ts
{
path: 'lazy-load',
loadChildren: 'lazy-load.module#LazyLoadModule'
}
```

```js
// lazy-load.module.ts
import { LazyLoadComponent } from './lazy-load.component';
@NgModule({
imports: [
RouterModule.forChild([
{
path: '',
component: LazyLoadComponent
}
])
],
declarations: [
LazyLoadComponent
]
})
export class LazyModule { }
```

## Cache API calls
When making API calls, responses from some of them do not change frequently. In those cases, we can add a caching mechanism and store the value from an API. When another request to the same API is made, we get a response from the check, if there is no value available in the cache then we make an API call and store the result.

## Use environment variables
Angular provides environment configurations to declare variables unique for each environment. The default environments are development and production. We can even add more environments, or add new variables in existing environment files.

| [Start](README.md) |
| ------------------------------------- | --------------------------------- | ------------------ |