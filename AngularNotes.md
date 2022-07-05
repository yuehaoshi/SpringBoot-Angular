#Angular
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
