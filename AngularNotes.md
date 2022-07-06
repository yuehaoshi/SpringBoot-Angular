# Angular
## Definitions
Traditional Application:
Each user action results in a full HTML page load

Single Page Application
Partial Update instead of full page load on user actions, e.g. google maps, gmails

**Angular** is a framework for building modern single-page applications, e.g., Citi Bank, MSBox (www.madewithangular.com)
Official docs Tutorials: www.angular.io

## Features:
- Component-based Framework
- Clean separation of template coding and application logic
- Built-in support for data-binding and dependency injection
- Supports responsive web design and modern frameworks
  - Bootstrap, Google Material Design (Angular Material)..
## Angular CLI (Command-Line Interface)
```
> npm install -g @angular/cli
> ng version
> ng new <your-project-name> //e.g ng new my-first-angular-project
> ng serve //Build app, starts serer, rebuild for update (hot reload), defaul listens on port 4200, http://localhost:4200
> ng serve --open //same as above, will open in browser
> ng serve --port 5100 --open //customize port number
```
### Creating new Angular Project
- Create a folder "angular-training", open it in VSC
- Open Terminal, install angular cli: `npm install -g @angular/cli`
- Check installation: `ng version`
- `ng new my-first-angular-project`, routing-No, stylesheet: CSS
- After created, `cd my-first-angular-project`, then run by `ng serve`, then `http://localhost:4200/` in browser
- Edit HTML Template File
  - `src-app-app.component.html`, search for "is running"
  - cut this line, delete others, copy this line back, now we only have a blank page with one line
## Behind the Scene:
File: src/index.html //This is the html file for browser to render
```html
<body>
  <app-root></app-root>
</body>
```
File: src/app/app.component.ts
```typescript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
}) //This is how the "app-root" means, it is a selector
export class AppComponent {
  title = 'my-first-angular-project';
}
```
File: src/app/app/component.html
```html
<span>{{title}} app is running! SUCCESS!</span>
//This is the content to be shown on browser page
```
File: app.module.ts // This is the main component for bootstraping
## Creating a new Angular Component
### Step1: Create a new Project
```
ng new sales-project //router-N, CSS
cd sales-project
```
### Step2: Update main template page
- Remove all of Angular "placeholder" content
  - Update File: src/app/app.component.html to `<h1>Sales Team</h1>` (just add basic HTML header)
### Step3: Generate new component
```
ng generate component sales-person-list
```
here will be four files generated in `sales-person-list` folder inside `app` folder:
- `sales-person-list.component.ts`: the component class;
- `sales-person-list.component.html`: the component template HTML;
- `sales-person-list.component.css`: the component private CSS;
- `sales-person-list.component.spec.ts`: the unit test specifications;
One file will be updated:
- `src/app/app.module.ts`: Adds the component to the main application module
### Step4: Add new component selector to app template page
- In `src/app/sales-person-list/sales-person-list.component.ts`, copy `app-sales-person-list` and make a tag in `app.component.html` page (type `<`, command+v, vscode will close the tag automatically)
### Step5: Generate a SalesPerson class
- In terminal run `ng generate class sales-person-list/SalesPerson`
- One file `sales-person.ts` will be generated in `app/sales-person-list`
- In `sales-person.ts`, add constructor
File: app/sales-person-list/sales-person.ts
```typescript
export class SalesPerson {
    constructor(public firstName: string,
                public lastName: string,
                public email: string,
                public salesVolume: number) {
                
    }
}
```
### Step6: In SalesPersonListComponent, create sample data
- In `sales-person-list.component.ts`, create an array of objects
File: sales-person-list.component.ts
```typescript
import { Component, OnInit } from '@angular/core';
import { SalesPerson } from './sales-person';

@Component({
  selector: 'app-sales-person-list',
  templateUrl: './sales-person-list.component.html',
  styleUrls: ['./sales-person-list.component.css']
})
export class SalesPersonListComponent implements OnInit {
  //create an array of objects
  salesPersonList: SalesPerson[] = [
    new SalesPerson("A", "B", "ab@email", 100),
    new SalesPerson("C", "D", "cd@email", 200),
  ];
  constructor() { }
  ngOnInit(): void {
  }
}
```
### Step7: In sales-person-list template file, build HTML table by looping over data
- Start server by `ng serve`
- In `src/app/sales-person-list/sales-person-list.component.html` file, add html table work
File: sales-person-list.component.html
```typescript
<table border="1">
    <thead>
        <tr>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Email</th>
            <th>Sales Volume</th>
        </tr>
    </thead>
    <tbody>
        <tr *ngFor="let tempSalesPerson of salesPersonList">
            <td>{{ tempSalesPerson.firstName }}</td>
            <td>{{ tempSalesPerson.lastName }}</td>
            <td>{{ tempSalesPerson.email }}</td>
            <td>{{ tempSalesPerson.salesVolume }}</td>
        </tr>
    </tbody>
</table>
```
A table will show up on your page
## Angular with BootStrap
Step1. Get links for remote Bootstrap files
https://getbootstrap.com/
Step2. Add links to index.html
Step3. Apply Bootstrap CSS styles in component HTML template
Step4. Apply Bootstrap CSS styles in component HTML table
Step5. Update TypeScript component file to reference Bootstrap HTML template
