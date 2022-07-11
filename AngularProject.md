## Goal
- Create Angular Front End components
- Retrieve data from Spring Boot REST APIs
## Development Process
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
  - In `product-list.component.html`, add our own custom code
7. Add CrossOrigin support to Spring Boot app
