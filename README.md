# Complete Angular


### Introduction to Angular
#### What is Angular?
*Angular is a popular open-source framework developed by Google for building dynamic single-page applications (SPAs). It uses TypeScript, a superset of JavaScript, to build scalable web applications with rich user interfaces.*

#### Installation
*To get started, you need to install Angular CLI (Command Line Interface) globally. You can do this using npm:*
```
npm install -g @angular/cli
```

*Create a new Angular project:*

```
ng new my-app
cd my-app
ng serve
```

### TypeScript
*Superset of JS which helps us to add types in JS code and allow not to change the type of it once declared and finally the code is converted to JS.*

### Components
#### What are Components?
*A component is the basic building block of an Angular application. It controls a part of the user interface (UI) through a template. Components consist of:*

- *HTML template for layout.*
- *TypeScript class for business logic.*
- *CSS styles for presentation.*
- *Metadata (decorator) that defines the component.*

#### Creating a Component
```
ng generate component my-component
```

#### Example
```
// my-component.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: '<h1>Hello, Angular!</h1>',
  styles: ['h1 { color: blue; }']
})
export class MyComponent {}
```

### Templates
#### What are Templates?
*Templates are HTML views that define the UI of a component. They can include Angular-specific syntax for data binding and directives.*
#### Data Binding
*Data binding is a technique used to connect a component’s data with the view or template.*

**Angular provides four types of data binding:**
##### Interpolation:
*{{ expression }} to bind data from the component to HTML (template).*
##### Property Binding: 
*[property]="expression" to bind data from component to a HTML element*
##### Event Binding:
*(event)="handler" to bind an event to a method in the component.*
##### Two-way Binding:
*[(ngModel)]="property" to bind data between the view and the component.*

### Modules
#### What are Modules?
*Angular applications are modular. A module is a container that groups related components, directives, pipes, and services. Every Angular application has at least one module, the root module, defined in the AppModule.*
- *Modules help organize an application and enable lazy loading.*

#### Creating a Module
```
ng generate module my-module
```
#### Example
```
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { MyComponent } from './my-component/my-component.component';

@NgModule({
  declarations: [MyComponent],
  imports: [CommonModule],
  exports: [MyComponent]
})
export class MyModule {}
```

### Dependency Injection(DI)
*Dependency Injection (DI) is a design pattern in which components receive their dependencies (e.g., services) from external sources rather than creating them themselves.*
*Angular’s DI system allows you to:*
- *Inject services into components, pipes, directives, and other services.*

#### Example
```
import { Component } from '@angular/core';
import { MyService } from './my-service.service';

@Component({
  selector: 'app-my-component',
  template: '{{ data | json }}'
})
export class MyComponent {
  data: any;

  constructor(private myService: MyService) {
    this.data = this.myService.getData();
  }
}
```

### Services
*A service in Angular is a class that contains business logic or reusable data that can be shared across components.*
*Services are typically injected into components using DI.*
- Services help achieve separation of concerns and are generally used to handle HTTP requests, logging, or data management.

#### Examples
```
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class MyService {
  getData() {
    return ['Data1', 'Data2', 'Data3'];
  }
}
```

### Routing
#### What is Routing?
*Angular Router enables navigation from one view to the next as users perform application tasks.*
*Angular uses a router to navigate between different views or pages within an application.*
*The router maps URL paths to components:*
- *```RouterModule``` enables routing.*
- *Routing is defined in the app's module with route configurations.*
- ```RouterLink``` and ```router-outlet``` are used to handle navigation in templates.
#### Setting Up Routing
*Add the RouterModule to your application:*
```
import { RouterModule, Routes } from '@angular/router';

const routes: Routes = [
  { path: 'home', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: '', redirectTo: '/home', pathMatch: 'full' }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```

### Directives
#### What are Directives?
*Directives are instructions in the DOM (Document Object Model) that tell Angular how to render or alter the element and its children.*
#### Types of Directives
- **Structural Directives:** *Change the DOM layout by adding or removing elements (e.g., ```*ngIf```, ```*ngFor```).*
#### Example
```
<div *ngIf="isVisible">Visible</div>
```
- **Attribute Directives:** *Change the appearance or behavior of an existing element (e.g., ```*ngClass```, ```*ngStyle```).*
#### Example
```
<td [ngClass]="val > 10 ? 'red' : 'green'">{{ val }}</td>
<input type="text" [ngClass]="{ error: control.isInvalid }" />
```

### Pipes
#### What are Pipes?
*Pipes are a way to transform data for display in templates Angular comes with several built-in pipes (e.g., ```date```,```uppercase```,```currency```), and custom pipes can be created to handle specific transformations.*
- ```Syntax: {{ data | pipeName }}.```
#### Using Built-in Pipes
```
<p>{{ birthday | date }}</p>
```
#### Creating a Custom Pipe
```
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'customPipe'
})
export class CustomPipe implements PipeTransform {
  transform(value: string): string {
    return value.toUpperCase();
  }
}
```

### Forms
*Angular provides two approaches for managing forms:*
- ***Template-driven Forms:*** *Forms created using template-driven syntax in the HTML template. Ideal for simple forms.*
#### Example
```
<form #myForm="ngForm" (ngSubmit)="onSubmit(myForm)">
  <input name="name" ngModel required />
  <button type="submit">Submit</button>
</form>
```
- ***Reactive Forms:*** *Forms managed via code in the component class using FormControl, FormGroup, and FormArray. Ideal for complex, dynamic forms.*
#### Example
```
import { FormGroup, FormBuilder } from '@angular/forms';

export class MyComponent {
  form: FormGroup;

  constructor(private fb: FormBuilder) {
    this.form = this.fb.group({
      name: [''],
      age: ['']
    });
  }
}
<form [formGroup]="myForm" (ngSubmit)="onSubmit()">
      <input type="text" id="name" formControlName="name" />
</form>
```

### HTTP Client
*Making HTTP Requests Angular provides an HTTP client for making API requests.*
#### Example
```
import { HttpClient } from '@angular/common/http';
import { Component, OnInit } from '@angular/core';

export class MyComponent implements OnInit {
  data: any;

  constructor(private http: HttpClient) {}

  ngOnInit() {
    this.http.get('https://api.example.com/data').subscribe(response => {
      this.data = response;
    });
  }
}
```
### Routing Guards
#### What are Routing Guards?
*Guards can control whether a route can be activated or deactivated. Guards are used to control access to routes based on certain conditions:*
- ***CanActivate***: *Determines if a route can be activated.*
- ***CanDeactivate***: *Determines if a user can leave a route.*
- ***Resolve***: *Fetches data before route activation.*
- ***CanLoad***: *Determines if a module can be loaded.*
#### Example
```
import { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot } from '@angular/router';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): boolean {
    // Logic to determine if the route can be activated
    return true; // or false based on authentication
  }
}
```

### Observables and RxJS
#### What are Observables?
*Observables are a way to manage asynchronous data streams. Angular uses RxJS Observables for handling asynchronous data streams, such as HTTP requests or user input events. Observables are a powerful way to work with asynchronous data, and they can be subscribed to, transformed, and combined.*
- Common operators: ```map()```, ```filter()```, ```mergeMap()```, ```switchMap()```.
#### Example
```
import { Component } from '@angular/core';
import { Observable, of } from 'rxjs';

export class MyComponent {
  data$: Observable<string[]> = of(['Item1', 'Item2', 'Item3']);
}
```
### Change Detection
#### What is Change Detection?
*Change detection in Angular checks for changes in component data and updates the view accordingly. Angular uses two strategies:*
- ***Default:*** *Angular checks every component's bindings on every event.*
- ***OnPush***: *Angular checks only when the component’s input properties change or an event is triggered.*
#### Example
```
import { ChangeDetectorRef } from '@angular/core';

export class MyComponent {
  constructor(private cdr: ChangeDetectorRef) {}

  updateData() {
    // Change data
    this.cdr.detectChanges(); // Trigger change detection manually if needed
  }
}
```

### Angular Universal
#### What is Angular Universal?
*Angular Universal is a server-side rendering (SSR) solution for Angular. It renders Angular applications on the server, improving SEO and reducing initial load times by delivering pre-rendered pages to the client.*
#### Example
*You can set up Angular Universal in your project to enable server-side rendering:*
```
ng add @nguniversal/express-engine
```

### State Management
#### Using NgRx for State Management
*NgRx is a popular library for managing global state in Angular applications.*
#### Example
```
ng add @ngrx/store
```
*Set up a store with actions and reducers to manage state.*

### Testing
*Unit Testing Components and Services Angular provides testing utilities with Jasmine and Karma for unit testing components and services.*
#### Example
```
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { MyComponent } from './my-component.component';

describe('MyComponent', () => {
  let component: MyComponent;
  let fixture: ComponentFixture<MyComponent>;

  beforeEach(() => {
    TestBed.configureTestingModule({ declarations: [MyComponent] });
    fixture = TestBed.createComponent(MyComponent);
    component = fixture.componentInstance;
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });
});
```

### Lifecycle of Component
*Angular components have a defined lifecycle managed by Angular. This lifecycle includes a set of methods or hooks:*
- ***ngOnInit()*** – *Called after the component is initialized/mounted.*
- ***ngOnChanges()*** – *Called when input properties change.*
- ***ngOnDestroy()*** – *Called just before the component is destroyed.*
- ***ngDoCheck*** – *Called when changes detected in input properties or any other states.*
- ***ngAfterViewInit*** – *Called when components and it's views are initialized.*

### Lazy Loading
*Lazy loading allows you to load feature modules only when needed. This improves application performance by splitting the application into chunks and loading them on demand.*
- *Lazy-loaded modules are loaded through Angular's Router.*

### Ahead-of-Time (AOT) Compilation
*AOT compilation is the process of compiling Angular templates and TypeScript code during the build process rather than at runtime. This reduces the size of the JavaScript files, improves performance, and catches errors early.*

### Angular Material
*Angular Material is a UI component library that implements Material Design. It provides a wide range of reusable and accessible components like buttons, dialogs, forms, and more.*

### Ivy in Angular
*Ivy is Angular’s next-generation rendering engine. Introduced in Angular 9, it improves build performance, makes smaller bundles, and enables advanced features like lazy loading of components and faster change detection.*

### NgModule
*```NgModule``` is a decorator that defines an Angular module. It declares which components, directives, pipes, and services belong to the module and specifies the imports and exports. Every application has at least one root module, typically named ```AppModule```.*


### Decorators
*In Angular, decorators are functions that are used to modify the behavior of classes and their members. They provide a way to add metadata or apply transformations to code elements. In Angular, decorators are extensively used to define components, services, directives, pipes, modules, and more.*

#### Types of Decorators
##### 1. Component Decorator
*The ```@Component``` decorator is used to define a component. It includes metadata such as the component's selector, template, and styles.*
##### Example
```
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello-world',
  template: `<h1>Hello World!</h1>`,
  styles: [`h1 { color: blue; }`]
})
export class HelloWorldComponent {}
```
##### 2. Directive Decorator
*The ```@Directive``` decorator is used to define a directive, which is a class that can modify the behavior or appearance of elements in the DOM.*
##### Example
```
import { Directive, ElementRef, Renderer2 } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(el: ElementRef, renderer: Renderer2) {
    renderer.setStyle(el.nativeElement, 'backgroundColor', 'yellow');
  }
}
```

##### 3. Injectable Decorator
*The ```@Injectable``` decorator is used to define a service that can be injected into components or other services.*
##### Example
```
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  getData() {
    return ['Data 1', 'Data 2', 'Data 3'];
  }
}
```

##### 4. NgModule Decorator
*The ```@NgModule``` decorator defines an Angular module, which is a container for a cohesive block of code dedicated to an application domain, workflow, or closely related set of capabilities.*
##### Example
```
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

##### 5. Input Decorator
*```@Input()``` allows a parent component to pass data to a child component.*
##### Example
```
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>{{ childData }}</p>`
})
export class ChildComponent {
  @Input() childData!: string;
}
```

##### 6. Output Decorator
*```@Output()``` allows a child component to emit events to the parent component.*
##### Example
```
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="notifyParent()">Notify</button>`
})
export class ChildComponent {
  @Output() notify: EventEmitter<string> = new EventEmitter();

  notifyParent() {
    this.notify.emit('Hello from Child!');
  }
}
```