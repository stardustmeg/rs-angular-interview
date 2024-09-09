# Angular interview questions

## General:

<details>
<summary>1. What is Angular and what is it used for?</summary>

[Angular](https://angular.dev/overview) is a web framework that empowers developers to build fast, reliable applications.
Maintained by a dedicated team at Google, Angular provides a broad suite of tools, APIs, and libraries to simplify and streamline your development workflow. Angular gives you a solid platform on which to build fast, reliable applications that scale with both the size of your team and the size of your codebase.

#### Key Features of Angular:

- Component-Based Architecture:

Applications are built using reusable components, each encapsulating its own logic and view, which promotes modularity and maintainability.

- Two-Way Data Binding:

Synchronizes data between the model and the view, ensuring that changes in the model are automatically reflected in the view and vice versa.

- Dependency Injection:

Angular's dependency injection system helps manage the dependencies of components and services, making the code more modular, testable, and maintainable.

- Directives:

Extend HTML's capabilities by creating custom HTML tags and attributes, which can manipulate the DOM and add behavior to elements.

- Services:

Reusable business logic can be encapsulated in services, which can then be injected into components or other services, promoting code reuse and separation of concerns.

- Signals:

Angular provides a powerful signal system, which allows components to communicate with each other in a loosely coupled manner.

- Change Detection:

Angular provides a change detection mechanism, which allows components to detect changes in their data and update their view accordingly.

- Pipes:

Angular provides a powerful pipe system, which allows you to transform data within your application.

- Routing:

Angular's powerful router enables the creation of SPAs with multiple views, allowing for navigation between different parts of the application without a full page reload.

- Forms:

Angular provides robust support for handling user input through both template-driven and reactive forms, with built-in validation.

- HTTP Client:

Built-in services for making HTTP requests to interact with backend APIs, making it easier to handle asynchronous operations.

- Animation:

Angular includes a module for creating complex animations to enhance the user experience.

- Internationalization (i18n):

Built-in support for internationalizing applications, making it easier to translate the app into different languages.

- Testing:

Angular is designed with testing in mind, offering tools and best practices for unit testing (using Jasmine and Karma) and end-to-end testing (using Protractor).

#### Example Use Cases:

- Single-Page Applications (SPAs):

Applications that load a single HTML page and dynamically update the content as the user interacts with the app, providing a smooth user experience.

- Enterprise Web Applications:

Large-scale applications that require maintainability, scalability, and robust architecture, such as CRM systems, content management systems, and e-commerce platforms.

- Progressive Web Apps (PWAs):

Web applications that provide a native app-like experience, including offline capabilities, push notifications, and faster load times.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello-world',
  template: `<h1>Hello, {{ name }}!</h1>`,
  styles: [
    `
      h1 {
        font-family: Lato;
      }
    `,
  ],
})
export class HelloWorldComponent {
  name = 'Angular';
}
```

</details>

<details>
<summary>2. What is Angular CLI and what are its main features?</summary>

[The Angular CLI](https://angular.dev/tools/cli) is a command-line interface tool which allows you to scaffold, develop, test, deploy, and maintain Angular applications directly from a command shell.
Angular CLI is published on npm as the @angular/cli package and includes a binary named ng. Commands invoking ng are using the Angular CLI.

#### Main Features of Angular CLI:

- Project Initialization: `ng new`.
- Scaffolding: generate components, services, modules, and other Angular constructs using `ng generate` (or `ng g`) command.
- Development Server: local development server with live reloading using `ng serve`.
- Build Automation: `ng build`.
- Testing:
  - unit tests with Karma using `ng test`.
  - end-to-end tests with Protractor using `ng e2e`.
- Linting: `ng lint`.
- Code Updates: update your Angular application and its dependencies using `ng update`.
- Deployment: deploy your application to platforms like Firebase using third-party deployment tools.
- Configuration: manage different environments and configurations for your application (e.g., development, production).
- Internationalization: support for creating and managing localized versions of your application.

</details>

<details>
<summary>3. What is a module in Angular, and what is its role in an application?</summary>

In Angular, a module is a cohesive block of code dedicated to an application domain, a workflow, or a closely related set of capabilities. An Angular module is defined using the `@NgModule` decorator, which provides metadata that tells Angular how to compile and launch the application.

#### Role of a Module in an Angular Application:

- Organization:

Modules help organize an application into cohesive blocks of functionality, making the application easier to manage and scale.

- Separation of Concerns:

They promote separation of concerns by encapsulating related components, services, directives, and pipes, which enhances maintainability.

- Dependency Management:

Modules manage dependencies by specifying which components, directives, and pipes they use, and which services they require.

- Lazy Loading:

Angular modules support lazy loading, which can improve application performance by loading parts of the application only when they are needed.

- Scalability:

They enable the development of large applications by breaking down the application into smaller, more manageable pieces.

#### Key Properties of `@NgModule`:

- declarations:

Specifies the components, directives, and pipes that belong to the module.

- imports:

Lists other modules whose exported components, directives, or pipes are needed by the components in this module.

- providers:

Specifies the services available to the module.

- bootstrap:

Lists the root component(s) that Angular should bootstrap when the application starts.

#### Core Module:

The root module, often called AppModule, is the entry point of an Angular application:

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { HelloWorldComponent } from './hello-world/hello-world.component';

@NgModule({
  declarations: [AppComponent, HelloWorldComponent],
  imports: [BrowserModule],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

#### Feature Modules:

In addition to the root module, an Angular application can have multiple feature modules. A feature module is dedicated to a specific application feature or functionality. This helps in organizing the code better and enables lazy loading.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FeatureComponent } from './feature/feature.component';

@NgModule({
  declarations: [FeatureComponent],
  imports: [CommonModule],
  exports: [FeatureComponent],
})
export class FeatureModule {}
```

#### Summary:

Modules are (were!) fundamental building blocks in Angular applications. They help in organizing the application into cohesive blocks, managing dependencies, enabling lazy loading, and improving maintainability and scalability. By dividing an application into modules, developers can build and maintain large-scale applications more efficiently.

</details>

<details>
<summary>4. What is inter-component communication in Angular? Describe different ways of sharing data between components (e.g., @Input/@Output, services with Observables, etc.).</summary>

Inter-component communication in Angular refers to the methods and techniques used to share data and interact between different components within an application. Angular provides several ways to facilitate this communication:

#### 1. `@Input` and `@Output` Decorators:

These decorators are used for parent-child communication, where a parent component passes data to a child component and vice versa.

`@Input`: Allows a parent component to pass data to a child component.

```ts
// Parent Component Template
<app-child [childInput]="parentData"></app-child>

// Child Component
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>{{ childInput }}</p>`
})
export class ChildComponent {
  @Input() childInput: string;
}
```

`@Output`: Allows a child component to send data to a parent component using an event.

```ts
// Child Component
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="sendData()">Send Data</button>`
})
export class ChildComponent {
  @Output() dataEmitter = new EventEmitter<string>();

  sendData() {
    this.dataEmitter.emit('Data from Child');
  }
}

// Parent Component Template
<app-child (dataEmitter)="receiveData($event)"></app-child>

// Parent Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `<app-child (dataEmitter)="receiveData($event)"></app-child>`
})
export class ParentComponent {
  receiveData(data: string) {
    console.log(data);
  }
}
```

#### 2. Services with Observables:

Services can be used as a central place to share data between components, especially when the components are not directly related.

Service: Create a service that uses an `Observable` to share data.

```ts
import { Injectable } from '@angular/core';
import { BehaviorSubject, Observable } from 'rxjs';

@Injectable({
  providedIn: 'root',
})
export class DataService {
  private dataSubject = new BehaviorSubject<string>('Initial Data');
  data$: Observable<string> = this.dataSubject.asObservable();

  updateData(newData: string) {
    this.dataSubject.next(newData);
  }
}
```

Components: Inject the service and subscribe to the `Observable`.

```ts
// Component A (Sender)
import { Component } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-component-a',
  template: `<button (click)="updateData()">Update Data</button>`,
})
export class ComponentA {
  constructor(private dataService: DataService) {}

  updateData() {
    this.dataService.updateData('Updated Data from Component A');
  }
}

// Component B (Receiver)
import { Component, OnInit } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-component-b',
  template: `<p>{{ data }}</p>`,
})
export class ComponentB implements OnInit {
  data: string;

  constructor(private dataService: DataService) {}

  ngOnInit() {
    this.dataService.data$.subscribe((data) => (this.data = data));
  }
}
```

#### 3. ViewChild and ContentChild Decorators:

These decorators allow a parent component to access a child component's properties and methods directly.

`@ViewChild`: Used to access a child component declared in the parent component's template.

```ts
// Child Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>Child Component</p>`,
})
export class ChildComponent {
  childMethod() {
    console.log('Child Method Called');
  }
}

// Parent Component
import { Component, ViewChild, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `<app-child></app-child>`,
})
export class ParentComponent implements AfterViewInit {
  @ViewChild(ChildComponent) childComponent: ChildComponent;

  ngAfterViewInit() {
    this.childComponent.childMethod();
  }
}
```

`@ContentChild`: Used to access a child component projected into the parent component using content projection.

```ts
// Child Component (Projected)
import { Component } from '@angular/core';

@Component({
  selector: 'app-projected-child',
  template: `<p>Projected Child Component</p>`,
})
export class ProjectedChildComponent {}

// Parent Component
import { Component, ContentChild, AfterContentInit } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `<ng-content></ng-content>`,
})
export class ParentComponent implements AfterContentInit {
  @ContentChild(ProjectedChildComponent) projectedChild: ProjectedChildComponent;

  ngAfterContentInit() {
    console.log(this.projectedChild);
  }
}
```

#### 4. RxJS Subjects:

Subjects are a type of `Observable` that can multicast to multiple observers. They can be used for broadcasting data to multiple components.

```ts
import { Component } from '@angular/core';
import { Subject } from 'rxjs';

// Service
@Injectable({
  providedIn: 'root',
})
export class DataService {
  private dataSubject = new Subject<string>();
  data$ = this.dataSubject.asObservable();

  sendData(data: string) {
    this.dataSubject.next(data);
  }
}

// Component A (Sender)
@Component({
  selector: 'app-component-a',
  template: `<button (click)="sendData()">Send Data</button>`,
})
export class ComponentA {
  constructor(private dataService: DataService) {}

  sendData() {
    this.dataService.sendData('Data from Component A');
  }
}

// Component B (Receiver)
@Component({
  selector: 'app-component-b',
  template: `<p>{{ data }}</p>`,
})
export class ComponentB implements OnInit {
  data: string;

  constructor(private dataService: DataService) {}

  ngOnInit() {
    this.dataService.data$.subscribe((data) => (this.data = data));
  }
}
```

#### 5. Signals:

Signals in Angular can be used to create reactive state objects that emit new values when the state changes. This can be very useful for sharing data between components.

Create a `Signal`: First, create a Signal that will be shared across components. This is typically done in a service.

```ts
import { Injectable, Signal } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class SignalService {
  private signal = new Signal<string>('Initial Data');

  get dataSignal() {
    return this.signal;
  }

  updateData(newData: string) {
    this.signal.emit(newData);
  }
}
```

Use the `Signal` in Components: Inject the service in your components and subscribe to the signal to get updates.

_Component A (Sender):_

```ts
import { Component } from '@angular/core';
import { SignalService } from './signal.service';

@Component({
  selector: 'app-component-a',
  template: `<button (click)="updateData()">Update Data</button>`,
})
export class ComponentA {
  constructor(private signalService: SignalService) {}

  updateData() {
    this.signalService.updateData('Updated Data from Component A');
  }
}
```

_Component B (Receiver):_

```ts
import { Component, OnInit } from '@angular/core';
import { SignalService } from './signal.service';

@Component({
  selector: 'app-component-b',
  template: `<p>{{ data }}</p>`,
})
export class ComponentB implements OnInit {
  data: string;

  constructor(private signalService: SignalService) {}

  ngOnInit() {
    this.signalService.dataSignal.subscribe((data) => (this.data = data));
  }
}
```

</details>

## Components:

<details>
<summary>1. What are `Components` in Angular, and how are they the foundation of an application structure?</summary>

</details>

<details>
<summary>2. How do you configure a component's selector, template, and style using the `@Component` decorator?</summary>

</details>

<details>
<summary>3. How would you explain the component lifecycle and its main methods (e.g., ngOnInit, ngOnChanges, ngOnDestroy)?</summary>

</details>

<details>
<summary>4. How does two-way data binding work in Angular, and how does it differ from one-way data binding?</summary>

</details>

<details>
<summary>5. Standalone components.</summary>

</details>

<details>
<summary>6. What are ViewChild and ViewChildren?</summary>

</details>

<details>
<summary>7. What is the difference between ElementRef and Renderer2?</summary>

</details>

<details>
<summary>8. How do HostBinding and HostListener decorators work?</summary>

</details>

<details>
<summary>9. What is the change detection mechanism in Angular, and how do the Default and OnPush strategies differ? When is it better to use each one?</summary>

</details>

<details>
<summary>10. How do you handle dynamic components?</summary>

</details>

## Directives:

<details>
<summary>1. What are `Directives` in Angular, and what are they used for?</summary>

</details>

<details>
<summary>2. What is the difference between structural and attribute directives? Please provide examples.</summary>

</details>

<details>
<summary>3. How do you create and use a custom directive? Explain the use of the `@Directive` decorator.</summary>

</details>

<details>
<summary>4. Explain **ngIf** and **ngFor** and their usage.</summary>

</details>

<details>
<summary>5. What is the difference between **\*ngIf** and **[hidden]**?</summary>

</details>

<details>
<summary>6. What is the purpose of **ngSwitch**, **ngSwitchCase**, and **ngSwitchDefault**, and how do you use them?</summary>

</details>

<details>
<summary>7. What is the difference between **ngStyle** and **ngClass**?</summary>

</details>

<details>
<summary>8. What is **ngContainer** and what is it used for? Provide an example.</summary>

</details>

<details>
<summary>9. How do you create custom structural directives using **ng-template**?</summary>

</details>

## Pipe:

<details>
<summary>1. What is a `Pipe`, and what is its purpose in Angular?</summary>

</details>

<details>
<summary>2. Can you provide examples of some built-in pipes (e.g., **date**, **uppercase**, **lowercase**)?</summary>

</details>

<details>
<summary>3. What is the difference between 'pure' and 'impure' pipes. How do they affect performance?</summary>

</details>

<details>
<summary>4. How do you use multiple pipes simultaneously?</summary>

</details>

<details>
<summary>5. How do you pass parameters to a `Pipe` to change behavior or format data?</summary>

</details>

<details>
<summary>6. What are the advantages of using `Async pipes`. How do you apply them with Observable or Promise?</summary>

</details>

<details>
<summary>7. How does the process of registering a custom pipe in a module occur?</summary>

</details>

<details>
<summary>8. How do you handle complex transformations in pipes?</summary>

</details>

## Routing:

<details>
<summary>1. What is `Routing` in Angular, and what is it used for?</summary>

</details>

<details>
<summary>2. How do you configure a basic routing system using **RouterModule** and **router-outlet**?</summary>

</details>

<details>
<summary>3. How do you use route parameters and queryParams to pass and retrieve data in routes?</summary>

</details>

<details>
<summary>4. Can you provide an example of using child routes?</summary>

</details>

<details>
<summary>5. What are the preloading strategies, and how do you use them?</summary>

</details>

<details>
<summary>6. How do you use **Route Guards** (e.g., **CanActivate** and **CanDeactivate**) to protect routes?</summary>

</details>

<details>
<summary>7. What is **ActivatedRoute**, and how do you apply it to get information about the current route?</summary>

</details>

<details>
<summary>8. How do you handle lazy loading in routing?</summary>

</details>

## RxJS:

<details>
<summary>1. Define the concept of `RxJS` and its usage in Angular.</summary>

</details>

<details>
<summary>2. What are _Observable_, Observer, and Subscriptions?</summary>

</details>

<details>
<summary>3. What is the difference between Observable and Promise?</summary>

</details>

<details>
<summary>4. Can you provide examples of basic RxJS operators in Angular (e.g., map, filter, catchError, switchMap)?</summary>

</details>

<details>
<summary>5. How do you create a Custom Observable using the new Observable method and manage the data passed into the stream?</summary>

</details>

<details>
<summary>6. What are Subject and BehaviorSubject, and how are they used in Angular?</summary>

</details>

<details>
<summary>7. How would you explain the concepts of **_Hot_** and **_Cold_** Observables?</summary>

</details>

<details>
<summary>8. How do you properly unsubscribe from an Observable?</summary>

</details>

<details>
<summary>9. What are the different approaches to state management in Angular? What are the benefits of using service-based methods versus NgRx or other state management libraries?</summary>

</details>

<details>
<summary>10. How do you handle error handling and retry logic with RxJS?</summary>

</details>

## Dependency Injection:

<details>
<summary>1. What is `Dependency Injection`, and what are its objectives in Angular?</summary>

</details>

<details>
<summary>2. How do you create a service and use it in components for dependency injection?</summary>

</details>

<details>
<summary>3. What is the difference between _providedIn: 'root'_, _providedIn: 'any'_, and registering a provider in the "providers" section of NgModule?</summary>

</details>

<details>
<summary>4. What are **useClass**, **useValue**, and **useFactory**? How are they used when creating providers?</summary>

</details>

<details>
<summary>5. Explain the concept of Injector and provider hierarchy.</summary>

</details>

<details>
<summary>6. What is a DI token, and how do you use it for dependency injection?</summary>

</details>

<details>
<summary>7. How do you use **@Optional**, **@Self**, and **@SkipSelf** decorators to control dependency injection and their handling?</summary>

</details>

<details>
<summary>8. How do you inject dependencies based on conditions or by different provided implementations?</summary>

</details>

<details>
<summary>9. What is a multi-provider and how do you configure it?</summary>

</details>

<details>
<summary>10. How do you implement dependency injection for standalone components?</summary>

</details>

<details>
<summary>11. How can you reuse standalone components across different parts of your Angular application?</summary>

</details>

## Forms:

<details>
<summary>1. What is the difference between `Template-driven Forms` and `Reactive Forms`?</summary>

</details>

<details>
<summary>2. What are **FormControl**, **FormGroup**, and **FormArray** in the context of Reactive Forms?</summary>

</details>

<details>
<summary>3. What are the differences in working with validation for Template-driven Forms and Reactive Forms?</summary>

</details>

<details>
<summary>4. How do you implement custom validators for forms?</summary>

</details>

<details>
<summary>5. How can you retrieve and process data from forms after submission?</summary>

</details>

<details>
<summary>6. What is two-way data binding in the context of Template-driven Forms?</summary>

</details>

<details>
<summary>7. How do you use FormBuilder to create reactive forms using convenient and shorter syntax notation?</summary>

</details>

<details>
<summary>8. How do you track the change state of forms or form controls (e.g., _touched_, _dirty_)?</summary>

</details>

<details>
<summary>9. How do you handle asynchronous validation?</summary>

</details>

## Lazy Loading:

<details>
<summary>1. What is `Lazy loading`, and what is its purpose in Angular applications?</summary>

</details>

<details>
<summary>2. How do you configure lazy loading for a specific module?</summary>

</details>

<details>
<summary>3. What changes to the routing system are necessary to support lazy loading?</summary>

</details>

<details>
<summary>4. What are the advantages of using lazy loading in your application?</summary>

</details>

<details>
<summary>5. What is Preload strategy, and what are the main strategies used for preloading modules (**NoPreloading** or **PreloadAllModules**)?</summary>

</details>

<details>
<summary>6. How do you use PreloadingStrategy with Angular Router to organize preloading of data?</summary>

</details>

<details>
<summary>7. What are the disadvantages of lazy loading?</summary>

</details>

<details>
<summary>8. How do you debug lazy loading issues?</summary>

</details>

## Modules:

<details>
<summary>1. What is a `Module` in Angular, and what role does it play in an application?</summary>

</details>

<details>
<summary>2. Can you explain the structure of a module and its metadata?</summary>

</details>

<details>
<summary>3. How can you separate functionality into different modules and connect them to the main application module?</summary>

</details>

## HTTP:

<details>
<summary>1. What is `HttpClientModule`, and why is it important in Angular applications?</summary>

</details>

<details>
<summary>2. How can you make HTTP requests using Angular's **HttpClient**?</summary>

</details>

<details>
<summary>3. Can you explain the difference between Observables and Promises in handling HTTP responses?</summary>

</details>

<details>
<summary>4. How can you handle errors during HTTP requests in Angular?</summary>

</details>

<details>
<summary>5. What are some techniques to optimize HTTP requests and handle caching considerations for Angular applications?</summary>

</details>

<details>
<summary>6. What is the purpose of **HttpInterceptor** in Angular, and how does it work?</summary>

</details>

<details>
<summary>7. In which scenarios would you consider using an interceptor for error handling in an Angular application?</summary>

</details>

<details>
<summary>8. How do you handle authentication and authorization with HTTP interceptors?</summary>

</details>

## Tests (Testing):

<details>
<summary>1. What types of `Testing` does Angular support (e.g., unit tests, integration tests, e2e tests)?</summary>

</details>

<details>
<summary>2. What are the main tools and libraries used by Angular for testing (**Jasmine**, **Karma**, and **Protractor**)?</summary>

</details>

<details>
<summary>3. What is **TestBed**, and how is it used to set up a testing environment?</summary>

</details>

<details>
<summary>4. How do you test Angular components using **ComponentFixture** and **DebugElement**?</summary>

</details>

<details>
<summary>5. How do you test directives and pipes in Angular?</summary>

</details>

<details>
<summary>6. How do you mock (mock) and stub (stub) dependencies in tests for services?</summary>

</details>

<details>
<summary>7. How do you test forms based on templates and reactive forms?</summary>

</details>

<details>
<summary>8. What are async, **fakeAsync**, and **tick**, and how are they used when testing asynchronous code?</summary>

</details>

<details>
<summary>9. How do you ensure your tests are isolated and do not interfere with each other?</summary>

</details>

## Signals:

<details>
<summary>1. What are Signals?</summary>

</details>

<details>
<summary>2. How to read and modify the value of a signal?</summary>

</details>

<details>
<summary>3. What is the main advantage of using signals instead of primitive values?</summary>

</details>

<details>
<summary>4. What is the advantage of using Signal Inputs?</summary>

</details>

<details>
<summary>5. How do we subscribe to a signal?</summary>

</details>

<details>
<summary>6. Can we read the value of a signal from a computed signal without creating a dependency?</summary>

</details>

<details>
<summary>7. Detecting signal changes with the effect() API</summary>

</details>

<details>
<summary>8. What is the relation between Signals and change detection?</summary>

</details>

<details>
<summary>9. How do you handle signal debugging?</summary>

</details>

## Angular 16, 17, 18 features:

<details>
<summary>1. What's new in Angular 16, 17, and 18 versions?</summary>

</details>

<details>
<summary>2. Describe the new features **@if**, **@for**, **@switch**, **@defer**.</summary>

</details>

<details>
<summary>3. Can you explain the benefits of using the new Angular Ivy renderer introduced in Angular 18?</summary>

</details>

<details>
<summary>4. How does Angular 18 improve performance and bundle size optimization compared to previous versions?</summary>

</details>

<details>
<summary>5. What enhancements or additions have been made to Angular Material in the recent versions?</summary>

</details>

<details>
<summary>6. How does Angular 18 support server-side rendering (SSR) and what improvements does it offer in this area?</summary>

</details>

<details>
<summary>7. Discuss any updates or improvements made to Angular CLI and its features in the latest releases.</summary>

</details>
