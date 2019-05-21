## plan
- Fundamentals of Typescript and oop
- angular Fundamentals
- Displaying data and handling events
- Components
- Directives
- Template -driven forms
- Routing and navigation
- deployment
- building real-time, serverless application with firebase(e-commerce website)
 advanced part-->
- Reactive forms
- consuming HTTP services
- authentication and authorization
- Animations
- Angular Materials
- Redux
- Unit testing
- Integration testing


## 08/04/2019
### Making the environment
- installed nodejs
- use node pakage manager(`npm`) to install third party libraries
- install angular CLI(`sudo npm install -g @angular/cli`)
- Angular CLI
        - As the name implies, it is a command line tool for creating angular apps. It is recommended to use angular cli for creating angular apps as you don't need to spend time installing and configuring all the required dependencies and wiring everything together.
        -while creating projects this provide all required configuration files
-create new angular project


another project

`ng new webapp --routing -g --style scss`
`ng add @angular/material` -inject angular material UI framework
`ng s` to see the app
`code .` to open the app in visual studio code  

### files and folders in an angular project

- e2e  - end to end tests (navigate home page, go to links..)
- node modules  - store third party libraries 
- src - we have the actual sorce code of application
        - app   - module , components
        - assets -images, texts files
        - environments - production , development environment
        - favicon icon
        - index.html
        - main.ts -typescript main file.starting point of the app
        - polyfills.ts 
        - styles.css -global styles 
        - test.ts -setting a testing environment
-configuration files
-packages.json - standard file , basic detials on applicatio ,dependencies ->libraries (@ angular /libaray name), devdependencies
-tsconfig.json - 
-tslint.json -


- hot module replacement(HMR) - eb browser changes automatically when code changes


### Typescript
- this is a super set of javasrcipt
- features - strong typing, oop, compile -time errors,great tooling
- typescrit transplile to javascript which browser can understand
- installing typesript
- `sudo npm install -g typescript`
- `tsc --version`
- make new directory withnew .ts file
- `tsc filename.ts`- convert typescript file to js file
- 

### 11/04/2018
#### learn typescript basics
1. using variables-
-use `var`(scope to the nearest function,can use inside the function)  or `let`(scope only to the nearest block) to define variables
2. type variables
3. type assertion
4. arrow function
5. custom types
6. interfaces
7. class, constructor
8. getters and setters
9. modules

### 18/04/2018
#### Angular Fundamentals
* components
        1. create a component
        in a new ts file..
```sh
    //use decorator to this class for making it a component\
    import { Component} from '@angular/core';


    @Component({
        selector:'courses' , //like a css selector<courses>
        template:'<h2>Courses</h2>'
    })
    export class CoursesComponents{

    }
```
2. register it in modules
 in app module add the component to the `declerations`
3. add an element in an HTML markup
    inside app.component.html  
```sh 
<h1>Angular</h1>
<courses></courses>
```
##### another method
in terminal `ng g c component-name`

* generating services
    1. make a new file as app.services.ts
        ``` sh
        export class CoursesService{
        getCourses(){
            return ["course1","course2","course3"];
            }
        }
        ```
    2. make dependency injection to constructor of components
    ``` sh
    import { Component} from '@angular/core';
    import { CoursesService } from './courses.service';
    @Component({
        selector:'courses' , 
        template:`
        <h2>{{ title }}</h2>
            <ul>
            <li *ngFor="let course of courses">
                {{ course }}
            </li>
            </ul>
        `    //{{ }} is string interpolation

    })
    export class CoursesComponents{
        title="List of Courses";
        courses;        //made a service to get list of courses
        constructor(service: CoursesService){   //this is dependancy injection
            //let service=new CoursesService();
            this.courses=service.getCourses();
        }
    }
    ```
    3. in app.module
    ``` sh
    providers: [
    CoursesService
  ],   //all dependencies are registered here
  ```
  ##### another method with angular cli
  - `ng g s service-name`
  
### 24/04/2019
##### directives
- *ngIf,  [hidden]
``` sh
<h2 [hidden]="authors.length==0"> {{ title }} </h2>
<h2 [hidden]="authors.length>0"> No courses yet </h2>
```
- *ngFor
``` sh
<ul *ngFor="let author of authors">
  <li>{{ author }}</li>
</ul> 
```
- ngSwitchCase
```
<ul class="nav nav-pills">
  <li [class.active]="viewMode=='map'"><a (click)="viewMode='map'">Map View</a></li>
  <li [class.active]="viewMode=='list'"><a (click)="viewMode='list'">List View</a></li>
</ul>
<!-- [class.active] is data binding -->
<div [ngSwitch]="viewMode">
  <div *ngSwitchCase="'map'">Map view content</div>
  <div *ngSwitchCase="'list'">List view content</div>
  <div *ngSwitchDefault>Otherwise</div>
</div>
```
- ng-app − This directive starts an AngularJS Application.
- ng-init − This directive initializes application data.
- ng-model − This directive defines the model that is variable to be used in AngularJS.
- ng-repeat − This directive repeats HTML elements for each item in a collection.

##### ngFor and change Detection
-
### 25/04/2019
##### two-way binging and ng module
-
##### Forms
- FormControl - instances : value,touched ,untouched , dirty (value is changed) ,prestine(value is not changed) , valid , errors
- FormGroup - keeps set of FormControl objects, all the instances in FormControl are also valid in FormGroup.
- Creating Controls
        -   `Directives(known as Template-driven forms)`
                 Good for simple forms
                less validations
        -   `code (Reactive Forms)`
                More control over validation logic
                use for complex forms
           
- ngModle - store the value of the input box to a variable
- Adding Validations
- specific validation errors
```
 <input required maxlength="10" minlength="3" pattern="Nimesha" ngModel name="firstName"
 #firstName="ngModel" (change)="log(firstName)"  id="firstName" type="text" class="form-control">
 
      <div  class="alert alert-danger" *ngIf="firstName.touched && !firstName.valid">
        <div *ngIf="firstName.errors.required">First Name is required! </div>
        <div *ngIf="firstName.errors.minlength">First Name should be minimum 3 characters! </div>
        <div *ngIf="firstName.errors.pattern">First Name does not match the pattern! </div>
      </div>
      
```
### 27/04/2019
##### Angular materials
- For designing the UI
1. Installing anglular material
install dependency coomponent development kit `npm install --save @angular/material @angular/cdk @angular/animations hammerjs`
hammerjs ->for gesture controls
2. add angular theme
in style.css import `@import "~angular/material/prebuilt-themes/indigo-pink.css";`
3.import to app.modules.ts
```
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';//if want to animations
import { NoopAnimationsModule } from '@angular/platform-browser/animations';//if do not want to animations
```
include the suitable one for imports
##### Adding a material to the website
- Import the relavent API preference to angularmodules and add it under imports
- write the html code with relavent directives for each component

### 03/05/2019
#### Routing and Navigation in Angular
- Routing - Mapping of path to a component
- Implement Navigation 
    1. Configure the routes - what components should be visible when user going to a certain url
    2. Add a router outlet - write coressponing components when a given route become active
    3. Add Links

### 14/05/2019
#### Firebase in Angular app
- Firebase has,
    Fast, scalable and realtime database in cloud
    Authentication
    cloud messaging
    Storage, Analytics 
    No sql database
- Make a database in firebase and add list of data to it
- make angular project and install `npm install firebase angularfire2 `
- open the project and under the environment there is an environment.ts file. Make a firebase configuring object and add properties in the firebase config file.
- import AngularFireModule,AngularFireDatabaseModule to app.module.ts and include `AngularFireMOdule.initializeApp(environment.firebase_config_object_name)`
- in app.component.ts import AngularFireDatabase and change constructor of it as follows 
```
export class AppComponent {
  courses: any[];

  constructor(db: AngularFireDatabase){
    db.list('/courses').valueChanges().subscribe(courses=>{
        this.courses=courses;
        console.log(this.courses);
      });
    
  }
  }
```
- In app.component.html use ngfor and bind the vales from the firebase to it as follows
```
<ul>
  <li *ngFor="let course of courses">
    {{ course }}
  </li>
</ul>
```
