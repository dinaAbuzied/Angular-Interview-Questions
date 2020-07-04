# Angular Interview Questions & Answers
A list of common angular interview questions

1.  ### What is the sequence of angular lifecycle hooks?
    A component in Angular has a life-cycle, a number of different phases it goes through from birth to death.

    ![ScreenShot](https://codecraft.tv/courses/angular/components/lifecycle-hooks/images/lifecycle-hooks.png)

    The description of each lifecycle method is as below,

    1. **constructor:** This is invoked when Angular creates a component or directive by calling new on the class.
    2. **ngOnChanges:** When the value of a data bound property changes, then this method is called.
    3. **ngOnInit:** Invoked when given component has been initialized.
    This hook is only called once after the first `ngOnChanges`
    4. **[ngDoCheck:](https://stackblitz.com/edit/angular-ivy-xn5ywn?file=src%2Fapp%2Fchild-component%2Fchild-component.component.ts)** This is for the detection and to act on changes that Angular can't or won't detect on its own.
    5. **[ngAfterContentInit:](https://stackblitz.com/edit/angular-ivy-qf8zjs?file=src%2Fapp%2Fparent-cmp%2Fparent-cmp.component.ts)** Respond after Angular projects external content into the component's view, or into the view that a directive is in.
    6. **ngAfterContentChecked:** Respond after Angular checks the content projected into the directive or component.
    7. **ngAfterViewInit:** Respond after Angular initializes the component's views and child views, or the view that contains the directive.
    8. **ngAfterViewChecked:** Respond after Angular checks the component's views and child views, or the view that contains the directive.
    9. **ngOnDestroy:** This method will be invoked just before Angular destroys the component.
    Use this hook to unsubscribe observables and detach event handlers to avoid memory leaks.

2. ### What are the possible data update scenarios for change detection?
    The change detection works in the following scenarios where the data changes needs to update the application HTML.
    1. **Component initialization:** While bootstrapping the Angular application, Angular triggers the `ApplicationRef.tick()` to call change detection and View Rendering.
    2. **Event listener:**  The DOM event listener can update the data in an Angular component and trigger the change detection too.
         ```js
         @Component({
           selector: 'app-event-listener',
           template: `
             <button (click)="onClick()">Click</button>
             {{message}}`
         })
         export class EventListenerComponent {
           message = '';

           onClick() {
             this.message = 'data updated';
           }
         }
         ```
    3. **HTTP Data Request:** You can get data from a server through an HTTP request
         ```js
         data = 'default value';
         constructor(private httpClient: HttpClient) {}

           ngOnInit() {
             this.httpClient.get(this.serverUrl).subscribe(response => {
               this.data = response.data; // change detection will happen automatically
             });
           }
         ```
    4. **setTimeout() or setInterval():** You can update the data in the callback function of setTimeout or setInterval
         ```js
         data = 'default value';

           ngOnInit() {
             setTimeout(() => {
               this.data = 'data updated'; // Change detection will happen automatically
             });
           }
         ```
    5. **Micro tasks Promises:** You can update the data in the callback function of promise
         ```js
         data = 'initial value';

           ngOnInit() {
             Promise.resolve(1).then(v => {
               this.data = v; // Change detection will happen automatically
             });
           }
         ```


5. ### What are the various kinds of directives?
    There are mainly three kinds of directives,
    1. **Components** — These are directives with a template.
    2. **Structural directives** — These directives change the DOM layout by adding and removing DOM elements.
    3. **Attribute directives** — These directives change the appearance or behavior of an element, component, or another directive.


6. ### What are the class decorators in Angular?
    A class decorator is a decorator that appears immediately before a class definition, which declares the class to be of the given type, and provides metadata suitable to the type

    The following list of decorators comes under class decorators,

    1. @Component()
    2. @Directive()
    3. @Pipe()
    4. @Injectable()
    5. @NgModule()

7. ### What are class field decorators?
    The class field decorators are the statements declared immediately before a field in a class definition that defines the type of that field. Some of the examples are: @input and @output,
     ```javascript
      @Input() myProperty;
      @Output() myEvent = new EventEmitter();
    ```

4. ### Explain local reference variables, @ViewChild() and @ContentChild()?
    The @ViewChild() and @ViewChildren() decorators in Angular provide a way to access and manipulate DOM elements, directives and components. @ViewChild() is used to query one element from the DOM and @ViewChildren() for multiple elements.

    If you want to access following inside the Parent Component, use @ViewChild() decorator of Angular.

    1. Child Component
    2. Directive
    3. DOM Element

    ViewChild returns the first element that matches the selector.

    You can use @ContentChildren to grab a reference to content that has been projected into a component through the use of `<ng-content>`. This is a subtle but important difference.
    [example](https://stackblitz.com/edit/viewchild-contentchild2?file=src%2Fapp%2Fmessage-container%2Fmessage-container.component.ts)

8. ### What happens if I import the same module twice?
    If multiple modules imports the same module then angular evaluates it only once (When it encounters the module first time). It follows this condition even the module appears at any level in a hierarchy of imported NgModules.

9. ### What is host property in css?
    The :host pseudo-class selector is used to target styles in the element that hosts the component. Since the host element is in a parent component's template, you can't reach the host element from inside the component by other means. For example, you can create a border for parent element as below,
    ```js
     //Other styles for app.component.css
     //...
     :host {
       display: block;
       border: 1px solid black;
       padding: 20px;
     }
     ```

