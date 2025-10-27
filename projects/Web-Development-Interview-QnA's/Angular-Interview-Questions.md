# 50 Angular Interview Questions and Answers for Software Engineering Jobs

This Markdown file contains 50 common Angular interview questions and answers, covering basics to advanced topics. Angular is a TypeScript-based frontend framework by Google, used for building single-page applications (SPAs). Questions are categorized for ease. Answers include brief explanations. Practice for interviews at companies like Google, Microsoft, or startups.

## Basics (Questions 1-10)

### 1. What is Angular?
**Answer:** Angular is an open-source, TypeScript-based web application framework developed by Google for building dynamic SPAs.  
**Explanation:** It uses components, modules, and services for structured development.

### 2. Difference between AngularJS and Angular?
**Answer:** AngularJS (1.x) is JavaScript-based with MVC; Angular (2+) is TypeScript-based with components and improved performance.  
**Explanation:** Angular is a complete rewrite, not backward-compatible with AngularJS.

### 3. What are the key features of Angular?
**Answer:** Components, Modules, Templates, Dependency Injection, Routing, Forms, HTTP Client, RxJS integration.  
**Explanation:** Enables modular, testable, and scalable apps.

### 4. What is TypeScript and why use it in Angular?
**Answer:** TypeScript is a superset of JavaScript with static typing.  
**Explanation:** Angular uses it for better tooling, error detection, and maintainability.

### 5. What is an Angular Module?
**Answer:** A class with @NgModule decorator that organizes components, services, etc.  
**Explanation:** AppModule is the root module bootstrapped in main.ts.

### 6. How do you create a new Angular project?
**Answer:** Use `ng new project-name` with Angular CLI.  
**Explanation:** CLI scaffolds the app with necessary files.

### 7. What is the Angular CLI?
**Answer:** Command Line Interface for generating components, services, etc.  
**Explanation:** Commands like `ng generate component my-comp`.

### 8. What is bootstrapping in Angular?
**Answer:** Process of starting the app by loading the root module.  
**Explanation:** Done in main.ts with platformBrowserDynamic().bootstrapModule(AppModule).

### 9. What are decorators in Angular?
**Answer:** Functions that modify classes, e.g., @Component, @Injectable.  
**Explanation:** Provide metadata for Angular to process.

### 10. What is the purpose of index.html in Angular?
**Answer:** Entry point HTML file where the app root component is inserted.  
**Explanation:** Contains <app-root> tag.

## Components and Templates (Questions 11-20)

### 11. What is a Component in Angular?
**Answer:** Building block with @Component decorator, template, and logic.  
**Explanation:** Encapsulates UI and behavior.

### 12. How to create a Component?
**Answer:** `ng generate component my-comp` or manually with @Component.  
**Explanation:** Includes selector, templateUrl, styleUrls.

### 13. What is template binding in Angular?
**Answer:** Using {{ }} for interpolation, [ ] for property binding.  
**Explanation:** Binds data from component to template.

### 14. Difference between template and templateUrl?
**Answer:** template: inline HTML; templateUrl: external file.  
**Explanation:** Use templateUrl for larger templates.

### 15. What is View Encapsulation?
**Answer:** Controls CSS scoping: Emulated (default), ShadowDom, None.  
**Explanation:** Prevents style leaks between components.

### 16. What are lifecycle hooks in Angular?
**Answer:** Methods like ngOnInit, ngOnDestroy called at specific points.  
**Explanation:** ngOnInit for initialization after constructor.

### 17. Explain ngOnChanges.
**Answer:** Hook called when input properties change.  
**Explanation:** Receives SimpleChanges object.

### 18. What is a Directive?
**Answer:** Classes that add behavior to elements: Component, Attribute, Structural.  
**Explanation:** E.g., *ngIf is structural.

### 19. Difference between Component and Directive?
**Answer:** Component has template; Directive modifies existing elements.  
**Explanation:** Components are directives with views.

### 20. How to pass data to a child component?
**Answer:** Use @Input() decorator in child.  
**Explanation:** Parent binds via [inputProp]="value".

## Data Binding and Pipes (Questions 21-30)

### 21. Types of data binding in Angular?
**Answer:** Interpolation {{}}, Property [ ], Event ( ), Two-way [( )].  
**Explanation:** Enables dynamic UI updates.

### 22. What is event binding?
**Answer:** (event)="handler()" for DOM events.  
**Explanation:** E.g., (click)="onClick()".

### 23. What is two-way binding?
**Answer:** [(ngModel)] for forms.  
**Explanation:** Requires FormsModule; syncs view and model.

### 24. What are Pipes in Angular?
**Answer:** Transform data in templates, e.g., {{ value | uppercase }}.  
**Explanation:** Built-in like date, currency; custom pipes possible.

### 25. How to create a custom Pipe?
**Answer:** @Pipe({name: 'myPipe'}), implement PipeTransform.  
**Explanation:** Use in template with | myPipe.

### 26. What is the difference between pure and impure pipes?
**Answer:** Pure: recalculates on input change (default); Impure: on every change detection.  
**Explanation:** Impure for complex data like arrays.

### 27. Explain property binding vs interpolation.
**Answer:** [property]="value" vs {{value}}; both one-way, but property for attributes.  
**Explanation:** Interpolation converts to string; property binding preserves type.

### 28. What is $event in event binding?
**Answer:** Object passed to handler with event details.  
**Explanation:** E.g., (keyup)="onKey($event)".

### 29. How does change detection work in Angular?
**Answer:** Zone.js tracks async operations; Angular checks component tree.  
**Explanation:** Default strategy; OnPush for optimization.

### 30. What is @Output() in Angular?
**Answer:** Decorator for emitting events from child to parent.  
**Explanation:** With EventEmitter: @Output() myEvent = new EventEmitter().

## Services and Dependency Injection (Questions 31-35)

### 31. What is a Service in Angular?
**Answer:** Class for shared logic, data, e.g., HTTP calls.  
**Explanation:** Singleton via DI.

### 32. What is Dependency Injection (DI)?
**Answer:** Pattern to provide dependencies via constructors.  
**Explanation:** Angular's injector manages instances.

### 33. How to create a Service?
**Answer:** `ng generate service my-service`; @Injectable({providedIn: 'root'}).  
**Explanation:** Root for app-wide singleton.

### 34. What is providedIn in @Injectable?
**Answer:** Specifies provider scope: 'root', 'platform', 'any', or module.  
**Explanation:** 'root' for tree-shakable singletons.

### 35. How to inject a Service?
**Answer:** Constructor parameter: constructor(private myService: MyService) {}.  
**Explanation:** Angular resolves via injector.

## Routing and Navigation (Questions 36-40)

### 36. What is Angular Routing?
**Answer:** Module for navigating between views without reload.  
**Explanation:** Uses RouterModule and Routes array.

### 37. How to set up routes?
**Answer:** In AppRoutingModule: const routes: Routes = [{path: 'home', component: HomeComponent}].  
**Explanation:** Use <router-outlet> in template.

### 38. What are route parameters?
**Answer:** Dynamic parts in URL, e.g., /user/:id.  
**Explanation:** Access via ActivatedRoute: this.route.snapshot.paramMap.get('id').

### 39. What is lazy loading in routing?
**Answer:** Load modules on demand: {path: 'lazy', loadChildren: () => import('./lazy.module').then(m => m.LazyModule)}.  
**Explanation:** Improves initial load time.

### 40. What is RouterLink?
**Answer:** Directive for navigation: <a routerLink="/path">Link</a>.  
**Explanation:** Prevents full page reload.

## Forms and Validation (Questions 41-45)

### 41. Types of forms in Angular?
**Answer:** Template-driven (ngModel) and Reactive (FormGroup).  
**Explanation:** Reactive for complex, dynamic forms.

### 42. What is Reactive Forms?
**Answer:** Model-driven with FormBuilder, FormGroup, FormControl.  
**Explanation:** Imported from @angular/forms.

### 43. How to add validation?
**Answer:** Validators.required, etc., in FormControl.  
**Explanation:** Display errors with *ngIf on formControl.errors.

### 44. What is ngSubmit?
**Answer:** Event for form submission: (ngSubmit)="onSubmit()".  
**Explanation:** Prevents default submit.

### 45. Difference between template-driven and reactive forms?
**Answer:** Template: directive-based, simple; Reactive: code-based, testable, dynamic.  
**Explanation:** Reactive uses observables for async validation.

## Advanced Topics (Questions 46-50)

### 46. What is RxJS in Angular?
**Answer:** Library for reactive programming with Observables.  
**Explanation:** Used in HTTPClient for async operations.

### 47. What is HttpClient?
**Answer:** Service for HTTP requests: this.http.get(url).subscribe().  
**Explanation:** Returns Observable; interceptors for headers/auth.

### 48. What is NgRx?
**Answer:** State management library inspired by Redux.  
**Explanation:** Uses Store, Actions, Reducers, Effects.

### 49. How to optimize Angular performance?
**Answer:** OnPush change detection, lazy loading, trackBy in ngFor, AOT compilation.  
**Explanation:** Reduces unnecessary checks.

### 50. What is Ivy in Angular?
**Answer:** Rendering engine introduced in Angular 9 for faster builds and smaller bundles.  
**Explanation:** Default since Angular 9; enables tree-shaking.

## Notes
These questions cover Angular up to version 18 (as of 2025). For hands-on practice, use Angular docs or StackBlitz. Refer to official Angular site for updates. Good luck with your interviews!