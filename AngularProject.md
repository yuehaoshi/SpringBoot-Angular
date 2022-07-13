## Goal
- Create Angular Front End components
- Retrieve data from Spring Boot REST APIs
## Tips
- If you need to find out about a CSS style:
  1. Copy the style name then search in style.css
  2. copy style name an search in goole
  3. If style starts with "fa" then most likely Fontawesome
## Phase1 Development Process
1. Create Angular project
    - `ng new angular-electroice`, N, CSS
    - Add [Bootstrap](www.getbootstrap.com) support, copy Bootstrap's CSS
        - In `src/index.html`, add copied Bootstrap CSS link
    - Edit `src/app/app.component.html` by replacing everything to simple html code
      ```html
      <div class = "container">
        <h1 class = "mt-3 mb-3">Products</h1>
      </div>
      ```
    - Test by `ng serve --open`
2. Create Angular component for product-list
    - `ng generate component components/product-list`
    - Open `src/app/components/product-list/product-list.component.ts`, copy selector and copy to `src/app/app.component.html`
    - We should see "product-list works!" in browser
3. Develop TypeScript class for Product
    - `ng generate class common/product`
    - List all property names and type in `src/app/common/product.ts`
4. Create Angular service to call REST APIs
    - `ng generate service services/product`
    - In `app.module.ts`, add `HttpClientModule` in import
    - add `ProductService` as provider, this allows us to inject service into other parts of application
    - Update `src/app/services/product.service.ts`
5. Update Angular component to subscribe to data from Angular service
    - In `product-list.component.ts`, inject our ProductService
6. Display the data in an HTML page
    - Create `product-list-table.component.html`, add table code
    - Change `product-list.component.ts` template Url to `product-list-table.component.html`
    - `assets` folder is special directory, we can put web assets here: images, JS, CSS, PDFs etc. Can also add sub-directories with any name
7. Add CrossOrigin support to Spring Boot app

## Phase2 Development Process
1. Online Shop Template Integration (Section 11)
    - `npm install bootstrap`
    - `npm install @fortawesome/fontawesome-free`
    - Add styles to `angular.json` file. In "styles" part (this is the CSS styles that will be applied globally to Angular project), add:
      ```
       "node_modules/bootstrap/dist/css/bootstrap.min.css",
       "node_modules/@fortawesome/fortawesome/fontawesome-free/css/all.min.css"
      ```
    - Update `style.css` and `index.html` with given files
    - Replace `favicon.ico` with cunstomized icon
    - By default, Spring Data REST only returns the first page of 20 items, we can change this in `src/app/services/product.service.ts`
2. Search for products by category (Section 12)
    - Angular Routing can only update a section of your page, does not reload the entire page

    | Name           | Description                                                                                |
    |----------------|--------------------------------------------------------------------------------------------|
    | Router         | Main routing service. Enables navigation between views based on user actions.              |
    | Route          | Maps a URL path to a component.                                                            |
    | RouterOutlet   | Acts as a placeholder. Renders the desired component based on route.                       |
    | RouterLink     | Link to specific routes in your application.                                               |
    | ActivatedRoute | The current active route that loaded the component. Useful for accessing route parameters. |

    - Step 1: Define Routes
        - A route has a path and a reference to a component
        - When user select the link for the route path, Angular will create a new instance of component
          ```typescript
          const routes: Routes = [
            {path: 'products', component: ProductListComponent}];
            //'products' is the path to match, when path matches, create new instance of component
            //The path has no leading slashes!
          ```
        - Add route to show products for a given category id
          ```typescript
          const routes: Routes = [
            {path: 'category/:id', component: ProductListComponent},
            {path: 'products', component: ProductListComponent}];
            //Category id parameter, the component can read this later and show products for this category
          ```
        - Add more routes to handle for other cases...
          ```typescript
          const routes: Routes = [
            {path: 'category/:id', component: ProductListComponent},
            {path: 'category', component: ProductListComponent},
            {path: 'products', component: ProductListComponent},
            {path: '', redirectTo: '/products', pathMatch: 'full'},
            {path: '**', redirectTo: '/products', pathMatch: 'full'}];
            //routes 2 and 3 have no category id, internally the component will use default category id
            //routes 4 and 5 have no path given but redirect to:/products, this is an exception to the rule about "no leading slashes"
            //'full' means match on this exactly. Default option is prefix, match if path starts with a given value
            //'**' is the generic wildcard. It will match on anything that didnot match above routes
            //Order of routes is important. First match wins. We should define our routes starting from most specific to generic.
          ```
        - Can add a custom PageNotFoundComponent for 404s
          ```typescript
          const routes: Routes = [
            ...
            {path: '**', component: PageNotFoundComponent}];
            //'PageNotFoundComponent' is a custom component created by you, can be given any name and customized view
            //Route order is important, so be sure to place this last
            //More info: https://angular.io/guide/router#define-a-wildcard-route
          ```
    - Step 2: Configure Router based on our routes
        - Configure the router in the applicaiton module (File: `app.module.ts`)
    - Step 3: Define the Router Outlet
        - Router Outlet acts as a placeholder
        - It is where the desired component will be rendered (Only updates a section of the page, doesnot reload entire page)
        - Update `app.component.html` to use Router Outlet (Based on Router configuration, display appropriate component here)
          ```typescript
          <!-- MAIN CONTENT -->
          <router-outlet></router-outlet>
          
          const routes: Routes = [
            {path: 'category/:id', component: ProductListComponent},
            {path: 'products', component: ProductListComponent}];
            //Based on the given path, show component 'X' at this given location
            //Create an instance of ProductListComponent, display products based on category id
            //When user clicks the link, ProductListComponent will appear in the location of router-outlet
          ```
    - Step 4: Set up Router Links to pass category id param
        - In our HTML page, set up links to our route
        - Pass category id as a parameter
        - Based on Routes configuration, use ProductListComponent
          ```
          <!-- MENU SIDEBAR -->
          <li>
            <a routerLink="/category/1" routerLinkActive="active-link">Books</a>
          </li>
          //The param name is id, pass the value of "1" for this parameter
          //Once user clicks the link, then we can apply a custom CSS style (optional, not required)
          //e.g., in style.css, add: .active-link {font-weight: bold;}
          //At this moment we are hard-coding categories. Later we will make this dynamic and read categoty from REST API
          ```
    - Step 5: Enhance ProductListComponent to read category id param
        - Need to read the category id parameter
          ```
          currentCategoryId: number;
          ...
          this.currentCategoryId = +this.route.snapshot.paramMap.get('id');
          //"route": use the activated route
          //"snapshot": state of route at this given moment in time
          //"paramMap": Map of all the route parameters
          //"id" Read the id parameter (path:'category/:id')
          //Parameter value is returned as string, we use the "+" symbol to convert string to number (typescript trick)
          ```
    - Step 6: Modify Spring Boot app - REST Repository needs new method
3. Search for products by text box

4. Master / detail view of products

5. Pagination support for products

6. Add products to shopping cart (CRUD)

7. Shopping cart check out

