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
1. Online Shop Template Integration
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
2. Search for products by category
    - Angular Routing can only update a section of your page, does not reload the entire page

| Name           | Description                                                                                |
|----------------|--------------------------------------------------------------------------------------------|
| Router         | Main routing service. Enables navigation between views based on user actions.              |
| Route          | Maps a URL path to a component.                                                            |
| RouterOutlet   | Acts as a placeholder. Renders the desired component based on route.                       |
| RouterLink     | Link to specific routes in your application.                                               |
| ActivatedRoute | The current active route that loaded the component. Useful for accessing route parameters. |


    - Step1: Define Routes
      - w
  
3. Search for products by text box

4. Master / detail view of products

5. Pagination support for products

6. Add products to shopping cart (CRUD)

7. Shopping cart check out

