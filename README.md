# 100+ Angular 2, 4 and 5 Interview Questions And Answers

This is a collection of Angular 2 interview questions I've found online, along with (hopefully) correct answers for most of them. Feel free to contribute / send corrections.
I'm adding in some Angular 4 and 5 questions now.

Note: "PA" stands for Possible Answer (one of many valid ones).

## Template Syntax Questions

**What is a template reference variable, and how would you use it?**

A: A variable (defined using a #) in a component template, which can be referenced in other parts of the template. For example, a template variable for a form can then be referenced by other elements of the form.

**What are the possible ways to bind component properties to an associated template?**

A: Interpolation binding, one way binding, two way binding.

**What's the difference between binding a value with or without square brackets, i.e.: `<input attr="something" />` vs `<input [attr]="something" />`?**

A: The square brackets will cause "something" to be evaluated as an expression, as opposed to just be passed in as a literal string.

**What does the ngFor template syntax look like?**

A: example:`<ul><li *ngFor="let val of values">{{val}}</li></ul>`

**What does the pipe syntax look like in Angular templates?**

A: example: `<div>{{ value | my-pipe : option }}</div>`

**What does an interpolated string look like in a template?**

A: example: `<div title="Hello {{username}}">...</div>`

**What is `<ng-container>`?**

A: A grouping element that does not interfere with styles or layout (it's analogous to curly braces in JavaScript).


**What is `<ng-template>`?**

A: It's an Angular element for rendering HTML when using structural directives. The ng-template itself does not render to anything but a comment directly.


## Component/Directive Questions

**What is the minimum definition of a component?**

A: A class with a Component decorator specifying a template.

**What is the difference between a component and a template?**

A: A component is a directive with a template (representing a view).

**What are different kinds of directives supported in Angular 2?**

A: Structural, component, and attribute directives.

**How do components communicate with each other?**

A: Various ways - for example: Input/Output properties, services, ViewChild/ViewContent.

**How do you create two way data binding in Angular 2.0?**

A: By using the two-way binding syntax [()] (along with ngModel, if you're doing this in the context of a form control element).

**How would you create a component to display error messages throughout your application?**

A: Implement your own ErrorHandler and configure it in the list of providers for the modules you want it used in. 

**How would you support logging in your Angular app?**

PA: One way would be to use angular2-logger, which is a package inspired by log4j. 

**How would you use the ngClass directive?**

A: For example: `<div [ngClass]="{firstCondition: 'class1', secondCondition: 'class2'}">...</div>`

**How do you resolve a template URL relative to a Component class?**

A: By specifying the moduleId to be module.id in the Component decorator. (Note: while this is still needed when using SystemJS, it is not necessary anymore when using Webpack module bundler for Angular 2 projects.)

**What are dynamic components?**

A: Components that are added at runtime (i.e. not fixed). For example, an ad banner component that is determined at runtime.

**What is ComponentFactoryResolver used for?**

A: A class that is used to create dynamic components - it produces a ComponentFactory for a particular component which can then be loaded into view via a createComponent on ViewContainerRef.


## NgModules Questions:

**What is the purpose of NgModule?**

A: It's to give Angular information on a particular module’s contents, through decorator properties like: declarations, imports, exports, providers, etc.

**How do you decide to create a new NgModule?**

A: Typically for a nontrivial feature in an application, that will involve a collection of related components and services.

**What are the attributes that you can define in an NgModule annotation?**

A: Declarations, imports, exports, providers, bootstrap

**What is the difference between a module's forRoot() and forChild() methods and why do you need it?**

A: forRoot and forChild are conventional names for methods that deliver different import values to root and feature modules.

**What would you have in a shared module?**

A: Common components, directives, and pipes used in other modules in your application.

**What would you not put shared module?**

A: Services that should not have multiple instances created for the application.

**What module would you put a singleton service whose instance will be shared throughout the application (e.g. ExceptionService andLoggerService)?**

A: Root Module

**What is the purpose of exports in an NgModule?**

A: Provide components, directives, pipes to other modules for their usage.

**Why is it (potentially) bad if SharedModule provides a service to a lazy loaded module?**

A: You will have two instances of the service in your application, which is often not what you want.

**Can we import a module twice?**

A: Yes, and the latest import will be what is used.

**Can you re-export classes and modules?**

A: Yes.

**What kind of classes can you import in an angular module?**

A: Components, pipes, directives

**What is the providers property used for in a module's NgModule metadata?**

A: To provide a list of service cerators that this module contributes to the global collection of services.

**What is bootstrapping in Angular?**

A: The mechanism that launches the application in Angular, loading the root module (typically called AppModule) which loads one or more bootstrapped components into the application's DOM.

## Services Questions:

**What is the use case of services?**

A: One very common use case is providing data to components, often by fetching it from a server. Though there’s no real definition of service from Angular point of view – it could do almost anything (e.g., logging is another common use case, among many).

**How are the services injected to your application?**

A: Via Angular’s DI (Dependency Injection) mechanism

**Why is it a bad idea to create a new service in a component like the one below?**

`let service = new DataService();`

A: The object may not be created with its needed dependencies.

**How to make sure that a single instance of a service will be used in an entire application?**

A: Provide it in the root module.

**Why do we need provider aliases? And how do you create one?**

A: To substitute an alternative implementation for a provider.  Can create like so: `{ provide: LoggerService, useClass: DateLoggerService }`


## Lifecycle Hooks Questions:

**What is the possible order of lifecycle hooks in Angular?**

A: ngOnChanges, ngOnInit, ngDoCheck, ngAfterContentInit, ngAfterContentChecked, ngAfterViewInit, ngAfterViewChecked, ngOnDestroy.

**When will ngOnInit be called?**

A: Called once, after the first ngOnChanges.

**How would you make use of onNgInit()?**

PA: Fetch initial component data (e.g. from server).

**What would you consider a thing you should be careful doing on onNgInit()?**

A: You cannot expect the component's children's data-bound properties to have been checked at this point.

**What is the difference between onNgInit() and constructor() of a component?**

A: A directive’s data-bound input properties are not set until after construction, so that’s one difference.

## Pipes Questions:

**What is a pure pipe?**

A: A pipe that is only executed when Angular detects a pure change to the input value (e.g. new primitive object or new object reference).

**What is an impure pipe?**

A: A pipe that is executed during every component change detection cycle (i.e., often – every keystroke, mouse move).

**What is an async pipe?**

A: An impure pipe that accepts a promise or observable as input and eventually returns emitted values.

**What kind of data can be used with async pipe?**

A: Stateful, asynchronous

**What types of pipes are supported in Angular 2?**

A: Pure and impure pipes (async pipes are a kind of impure pipe).

## Routing Questions:

**What is the difference between RouterModule.forRoot() vs RouterModule.forChild()? Why is it important?**

A: forRoot is a convention for configuring app-wide Router service with routes, whereas forChild is for configuring the routes of lazy-loaded modules.

**How does loadChildren property work?**

A: The Router calls it to dynamically load lazy loaded modules for particular routes.

**When does a lazy loaded module get loaded?**

A: When its related route is first requested.

**How would you use a Route Guard?**

A: You would implement CanActivate or CanDeactivate and specify that guard class in the route path you’re guarding. 

**What are some different types of RouteGuards?**

A: CanActivate, CanDeactivate, CanLoad, Resolve, etc.

**How would you intercept 404 errors in Angular 2?**

A: Can provide a final wildcard path like so: { path: ‘**’, component: PageNotFoundComponent }

**This link doesn't work. Why? How do I fix it?**
`<div routerLink='product.id'></div>`

A: `<a [routerLink]=”[’product.id’]”>{{product.id}}</a>`


**What do route guards return?**

A: boolean or a Promise/Observable resolving to boolean value.

**What is `<router-outlet>` for?**

A: Specifies the place where routes are mounted in the application.


## Styling Questions:

**How would you select a custom component to style it?**

A: Using the `:host` pseudo-class selector in your component's styles.

**How do you reference the host of a component?**

A: Let DI inject an ElementRef into the constructor of your component.

**What pseudo-class selector targets styles in the element that hosts the component?**

A: The :host pseudo class selector.

**How would you select all the child components' elements?**

A: With the @ViewChildren decorator, like for example:

`@ViewChildren(ChildDirective) viewChildren: QueryList<ChildDirective>;`

**How would you select a css class in any ancestor of the component host element, all the way up to the document root?**

A: Using the :host-context() pseudo-class selector.

**What selector force a style down through the child component tree into all the child component views?**

A: Use the /deep/ selector along with :host pseudo-class selector.

**What does :host-context() pseudo-class selector target?**

A: The :host-context() selector looks for a CSS class in any ancestor of the component host element, up to the document root.

**What does the following css do?**
`:host-context(.theme-light) h2 {
  background-color: red;
}`

A: Will change this component’s background-color to red if the context of the host has the .theme-light class applied.


## Forms Questions:

**When do you use template driven vs model driven forms? Why?**

A: Template driven forms make more sense for simpler forms, at least in terms of validation. Model driven or Reactive forms lend themselves to easier testing of the validation logic, so if that’s complex, Reactive forms make more sense. There’s also the issue of asynchronous (template driven forms) vs. synchronous (model driven).

**How do you submit a form?**

PA: use the ngSubmit event binding like so: `<form (ngSubmit)="onSubmit()" …>`

**What's the difference between NgForm, FormGroup, and FormControl? How do they work together?**

A: FormGroup tracks the value and validity state of a group of AbstractControl instances. FormControl does the same for an individual control. NgForm is a directive that Angular automatically attaches to each `<form>` tag. It has its own ‘valid’ property which is true only if every contained control is valid.

**What's the advantage of using FormBuilder?**

A: Reduces repetition and clutter by handling details of control creation for you.

**How do you add form validation to a form built with FormBuilder?**

A: pass in Validator objects along with the FormControl objects...

**What's the difference between dirty, touched, and pristine on a form element?**

A: Dirty means it contains user data, touched means the user has at least done something with a particular control (perhaps just literally ‘touched’ it by giving it focus?), and pristine means the control has not been touched at all by the user.

**How can you access validation errors in the template to display error messages?**

PA: Use formErrors

**What is async validation and how is it done?**

A: Verifying some field using some asynchronous call (perhaps a server call)… return a `Promise<ValidationResult>` from your validator. When creating a FormControl object, you can pass an asynchronous validator into the constructor (e.g. `new FormControl(‘value’, syncValidator, asyncValidator)`).


**What is patchValue used for?**

A: Setting a form value (one or more fields with an object) bypassing validation.

## Observables Questions

**What are observables?**

A: They provide a declarative way of message passing between publishers and subscribers in an application. They typically produce one or more values over time, which are subscribed to by observers. They provide some advantages over promises.

**What is RxJS?**

A: RxJS stands for Reactive Extensions for JavaScript, and is a reactive programming library centered around observables and operators making it easier to write complex asynchronous code.

**How do observables differ from promises?**

A: Observables are declarative; promises execute immediately upon creation. Observables can provide many values, whereas promises provide one value. Observables are cancellable, whereas promiess aren't. Error handling also differs between them.

**What are some advantages to using observables?**

A: Observables are cancellable; they come with powerful transformative functions (especially when using RxJS) to make asynchronous coding easier.

**Does an observable compute anything if it has no calls to subscribe?**

A: No, it will not.

## Animations Questions

**How do you define transition between two states?**

PA: Using the transition and animate function in an animations block like so: `animations: [transition('inactive => active'), animate('100 ms ease-in')]` 

**How do you define a wildcare state?**

A: Using the asterisk - example: `transition('* => active'), animate('100ms ease-in'))`

## Architecture / Framework Questions:

**What are some of the top level building blocks of the Angular framework?**

A: Services, Templates, Modules, Components, Providers, etc.

**What is AOT?**

A: Ahead of time compilation.

**What is Reactive programming and how does it relate to Angular?**

A: It's an "asynchronous programming paradigm concerned with data streams and the propagation of change."

**What are some differences between Angular 2 and 4?**

A: Improvements in AOT, allowing the "else" clause in ngIf, support for TypeScript 2.1, breaking out the animations package...

**What are some security related features built in to the Angular framework?**

A: Sanitation, to prevent cross site scripting. Built-in support in the HttpClient to prevent cross-site request forgery.

**How can you bypass sanitation in Angular and why would you do so?**

A: To inject known safe code, you can bypass sanitation (e.g. to embed an iframe).

**What is a good use case for ngrx/store?**

A: Complex application state management requirements, involving asynchronous requests to update state.

**What is Redux and how does it relate to an Angular app?**

A: It's a way to manage application state and improve maintainability of asynchronicity in your application by providing a single source of truth for the application state, and a unidirectional flow of data change in the application. ngrx/store is one implementation of Redux principles.

**What would be a good use case for having your own routing module?**

A: An application whose requirements imply having many routes, and potentially route guards, and child routes.

**Where would you configure TypeScript specific compiler options for your project?**

A: In the tsconfig.json file.A

**What is the tslint.json file used for?**

A: Linting the TypeScript code (making sure it conforms to certain standards / conventions).

**What are some changes introduced in Angular 4?**

A: Introduction of the else clause in ngIf; splitting out of animation package; support for TypeScript 2.1; improvements around AOT.

**What are some changes introduced in Angular 5?**

A: New version of HttpClient; build optimizer; Universal State Transfer API (allows sharing state of app between server and client easily); support for TypeScript 2.3.

## API Questions:

**What does this line do?**
  `@HostBinding('[class.valid]') isValid;`

A: Applies the css class ‘valid’ to whatever is using this directive conditionally based on the value of isValid.

**Why would you use renderer methods instead of using native element methods?**

A: Potentially if you’re rendering to something besides the browser, e.g. rendering native elements on a mobile device, or server side rendering (?).

**What is the point of calling renderer.invokeElementMethod(rendererEl, methodName)?**

A: To invoke a method on a particular element but avoid direct DOM access (so we don’t tie our code just to the browser).

**How would you control size of an element on resize of the window in a component?**

A:
`@HostListener('window:resize', ['$event'])
onResize(event: any) {
    this.calculateBodyHeight();
}`

**What would be a good use for NgZone service?**

A: Running an asynchronous process outside of Angular change detection.

**How would you protect a component being activated through the router?**

A: Route Guards

**How would you insert an embedded view from a prepared TemplateRef?**

PA: `viewContainerRef.createEmbeddedView(templateRef);

## Testing Questions


**What is Protractor?**

A: E2E (end-to-end) testing framework.

**What is Karma?**

A: Unit test testing library.

**What are spec files?**

A: Jasmine unit test files.

**What is TestBed?**

A: Class to create testable component fixtures.

**What does detectChanges to in Angular jasmine tests?**

A: propagates changes to the DOM by running Angular change detection.

**Why would you use a spy in a test?**

A: To verify a particular value was returned or a method was called, for example when calling a service.


`
___________

# Angular Interview Questions

A complete guideline to prepare for angular interviews. Also, you can use these questions to verify your expertise in angular. 



## Table of Contents
* [Assess Your Skill Level](#assess-your-skill-level)
* [Know the Interviewer](#know-the-interviewer)
* [Novice Level Questions](#novice-level)
    * [Familiarity to Basic Terminology](#familiarity-to-basic-terminology)
    * [Ability to Build Simple App](#ability-to-build-simple-app-questions)
    * [Understanding Basic Concepts](#understanding-basic-concepts-questions)
* [Intermediate Level Questions](#intermediate-level)
    * [Essential Terminology](#essential-terminology-questions)
    * [Comfortability to Build Medium Size App](#comfortability-to-build-medium-size-app-questions)
    * [Core Concepts Understandability](#core-concepts-understandability-questions)
* [Expert Level Questions](#expert-level)
    * [Performance and Edge Case Related Terminology](#performance-and-edge-case-related-terminology)
    * [Master a Large App](#master-a-large-app)
    * [Rock star and Fighter for angular](#rockstar-and-fighter-for-angular-questions)
* [Coding Test Question](#coding-test)
    * [Fetch Data and Display User Profile](#fetch-data-and-display-user-profile)
    * [Persistent Todo List](#persistent-todo-list)
    * [Student Registration System](#student-registration-system)
* [Side Things Related Questions](#side-things-related-questions)
    * [rxjs](#rxjs)
    * [TypeScript](#typescript)
    * [angular-cli](#angular-cli)
    * [others](#others)
* [Note from God](#note-from-god)



## Assess Your Skill Level
The most important step is knowing how you compare to other job seekers. Pinpoint areas where you are weaker, and spend the time necessary to make improvements. Google is your friend.

* **Novice** - You can create an Angular app using angular-cli or other popular project seeds, you have a basic understanding of components, modules, pipes, services, etc. If you don't have a clue what I am talking about, watch this [video](https://www.youtube.com/watch?v=rOr1r1rSZQ8) and get up to speed.
* **Intermediate** - You have a fully functional app that is deployed somewhere and/or published code in github, and you are comfortable with routing, authorization, feature modules, architecture, style guide, etc.
* **Expert** - You have mastered lazy loading, AOT, custom directives, deployment configuration, extending core features, etc.
* **Everyone Else** - You are either angular blind or an angular rock star. 


## Know the Interviewer
Do yourself a favor—Google the interviewer. Look at his/her Linkedin profile. Check his/her youtube videos, crappy old blog that hasn't been updated in years, and github profile. After your research, try to put the interviewer in one of the following categories:
1. Lazy interviewers wil ask about terminology. Sometimes they just Google and ask questions from there. If your interviewer is older and out of touch with the current development landscape, there is a greater chance that he/she will ask questions related to terminology.
2. More modest and nicer interviewers will be interested in what you know and whether you can get the job done. For this kind of interviewer look at the How category questions (I'm unsure what you are trying to say here)
3. Experienced interviewers (those who have been senior developers for a long time and have recently updated blogs and videos) want to know that you can think critically, and he will be interested in your process for decision making. These interviewers love to prove you wrong. One important tip: don't try to prove them wrong.

Researching relevant team members on LinkedIn and github can be useful as well.

## Novice Level

At this level an interviewer wants to know whether the interviewee is a coachable self-learner. Hence, he/she might ask questions about basic terminology, your ability to build a simple app, and your comprehension of basic concepts.  


### Familiarity of Basic Terminology
1. What are the differences between AngularJS (angular 1.x) and Angular (Angular 2.x and beyond)?
2. What is a component? Why would you use it? 
3. What is the minimum definition of a component?
4. What is a module, and what does it contain?
5. What is a service, and when will you use it?
6. What is a promise? Explain it laymen's terms.
7. What are the lifecycle hooks for components and directives?
8. What are pipes? Give me an example.
9. What are the differences between reactive forms and template driven forms?
10. What is a dumb, or presentation, component? What are the benefits of using dumb components?



### Ability to Build Simple App
1. How do components communicate with each other?
2. How would you use http to load data from server? 
3. How do you create routes?
4. How can you get the current state of a route?
5. How do you create two-way data binding?
6. How do you load external modules?
7. How would you display form validation errors?
8. Which lifecycle hook would you use to unsubscribe an observable?
9. How are services injected to your application?
10. How would you create route parameters and access them from a component?



### Basic Concepts
1. Why would you use Angular instead of another framework, e.g., React?
2. What is the difference between an observable and a promise?
3. What is the difference between a component and a directive?
4. Why would you use typescript aka benefits of typescript?
5. Why different life cycle hooks are needed for a component/directive?
6. Why does angular use rxjs?
7. What is the purpose of using zone.js?
8. What is the difference between ngOnInit() and the constructor() of a component?
9. When will ngOnInit() be called? How would you make use of ngOnInit()?
10. What are the benefits of using formBuilder?




[Answers link coming soon ]


## Intermediate Level

To be in the intermediate level, you have to build at least one medium sized angular app. You have to have familiarity with routing, https, different built process, unit test, etc. here are the questions you could expect.



### Essential Terminology Questions
1. How will you protect a route for authorized user only?
2. What is a custom pipe and how will you use it?
3. What is a structural directive?
4. What is the difference between RouterModule.forRoot() vs RouterModule.forChild()? Why is it important?
5. What is the difference between a module's forRoot() and forChild() methods and why do you need it?
6. What's the difference between dirty, touched, and pristine on a form element?
7. What is an async pipe? What kind of data can be used with async pipe?
8. What is injectable? Give me some example.
9. What is a pure pipe?
10. How will you create two-way data binding in Angular?



### Comfortability to Build Medium Size App Questions
1. How do components communicate with each other?
2. How do you decide to create a new NgModule?
3. How will you inject custom header in your http call?
4. How do you identify a structural directive in html?
5. How would you select a custom component to style it?
6. How would you select all the child components' elements?
7. How would you cache an observable data?
8. How would you save data from a form control?
9. How Event Emitters works in Angular?
10. How do you mock a service to inject in a unit test?



### Core Concepts Understandability Questions
1. Tell me about feature module and shared module?
2. What would you not put in a shared module?
3. Why angular uses decorator?
4. What is async validation and how is it done?
5. Why do you need type definitions?
6. Which components will be notified when an event is emitted?
7. Why would you export from ngModule?
8. Why is it bad if SharedModule provides a service to a lazy loaded module?
9. Can you explain the difference between ActivatedRoute and RouterState?
10. Which service will you put in the module and why?



[Answers link coming soon]



## Expert Level

You are a Rockstar in angular. You can teach other. You can lead a team of angular developers.

### Performance and Edge case Related Terminology
1. What is a factory Component?
2. What is lazy loading and why will you use it?
3. What is Ahead of time (AOT) compilation and why will you use it?
4. What are some of the Angular Style Guide suggestions you follow on your code? Why?
5. What is wildcard state?
6. How do you put animation between two states?
7. What would be a good use for NgZone service?
8. How would you protect a component being activated through the router?
9. How would you insert an embedded view from a prepared TemplateRef?
10. What is attribute directive and why will you use it?

### Master a Large App
1. How will you intercept http to inject header to each http call?
2. How would you create a component to display error messages throughout your application?
3. How will you parallelize multiple observable call?
4. How will you put one async call before another?
5. How can you use web worker in angular app?
6. What tools would you use to find a performance issue in your code?
7. What are some ways you may improve your website's scrolling performance?
8. Explain the difference between layout, painting and compositing.
9. How can you cancel a router navigation?
10. How would you animate routing?
11. How would you cancel a promise on which you are waiting?


### Rockstar and Fighter for Angular Questions
1. When does a lazy loaded module is loaded?
2. Why angular uses url segment?
3. How will you make angular app secure?
4. How will you localize numbers currencies and dates?
5. What is the best way to use translation in your app?
6. How will you setup different environment build differently for your app?
7. How will you use scss or css preprocessing with your application?
8. How will you optimize image/svg in your angular app?
9. How would you make sure an api call that needs to be called only once but with multiple conditions? Example: if you need to get some data in multiple routes but, once you get it, you can reuse it in the routes that needs it, therefor no need to make another call to your backend apis.
10. If you need to respond to two different Observable/Subject with one callback function, how would you do it? (ex: if you need to change the url through route parameters and with prev/next buttons).




[Answers link coming soon]

## Coding Test
Sometimes interviewer gives real coding test. Most of us suck on those and feel ashamed of ourselves and then continue to work in the current job. I don't want you to saty in that miserable job. Hence, take the following coding challenges and master them. 

### Fetch Data and Display User Profile

This test has three level
1. Level 1: I am giving you an api https://api.github.com/search/users?q=eric This api takes a query parameter name "q" and passes query string to server. Server returns bunch of users. Now I want you to create a input text box and button so that you can type anything on the text box and hit on the button to retrieve data from the given api. Upon retrieval display total_count and first 10 users in the search result. Detail instruction about this test is available [here](https://github.com/khan4019/github-profile-search)
2. Level 2: Convert each user profile as a router link so that upon clicking on each user profile you will navigate to a route that has "login" property in the route. Pass user.login as route parameter. Create a separate component where you will read the route parameter and then fetch data for that user  by using this api https://api.github.com/users/eric . Please Notice that last part of this api is the user.login (the route parameter that you have passed). Finally display user image and few other information in the component
3. Level 3: use any charting framework that you can find and then create a simple bar chart to display number of followers of first 10 users


This coding test will judge your ability to use services, component, routing, data visualization, external module, observables, etc.

[Sample code link coming soon] 

### Persistent Todo List
This test has three levels
1. Level 1:  Implement a simple todo list where you can add items, mark as done
2. Level 2: Now create few categories of todo list and make it persistence in the browser
3. Level 3: Now use firebase (serverless database) to make todo list persistence across multiple devices

This coding test will judge whether you can pass data and events between components. Also, whether you are leveraging directives and understand difference between component and directives.


[Sample code link coming soon]

### Student Registration System
This test has three levels
1. Level-1: Design a system where students can login to register different courses 
2. Level-2: Add a feature so that faculties on each course can view how many students registered on the courses
3. Level-3: (I need a shower. will add text here after I clean up myself) 

This coding test will judge your understanding of architecture for a large application. Your ability to think and implement module, lazy loading, asset management etc.

[Sample code link coming soon]

## Side Things Related Questions

### rxjs
3. Why unsubscribing is important?
1. What is the difference between map and flatmap?
2. Whare are the different ways you can create an Observable?
4. What is forkJoin, zip, share?
5. Difference between hot and cold observables.

### TypeScript
1. How would you debug a typescript file?
2. How do you implement interface in typescript?
3. How would you call base class constructor from child class in typescript?
4. What is typescript language service?
5. How to declare a custom type?
6. what are some disadvantages of typescirpt? answers [here](https://www.codeproject.com/Articles/1071285/Latest-TypeScript-Interview-Questions-for-Beginner) 

### angular-cli
1. Why would you use angular cli?
2. How would you run unit test? 
3. How do you create application to use scss?
4. How to inject base href?
5. How would you extract webpack config from angular cli project?


### Others
1. What is the use of codelyzer?
2. Will you use Angular Material2?
4. How would you set different config in different deployment server?
5. What do you know about ES6?
6. What is ngUpgrage? Do you know how you can run angularJS and angular side by side?

[Answers link coming soon]


## Note from God
On a press release, God expressed HIS apologies to send the author of this repo to a non-English speaking country and creating weekends. 




## Contributors
* [Faran4Engg](https://github.com/faran4engg)
* And you?
___________
