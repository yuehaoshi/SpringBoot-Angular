## Goal
- Create Angular Front End components
- Retrieve data from Spring Boot REST APIs
## Development Process
1. Create Angular project
  - `ng new angular-electroice`, N, CSS
  - Add [Bootstrap](www.getbootstrap.com) support, copy Bootstrap's CSS
    - In `src/index.html`, add copied Bootstrap CSS link
  - Edit `src/app/app.component.html` by replacing everything to simple html code
  - Test by `ng serve --open`
3. Create Angular component for product-list
4. Develop TypeScript class for Product
5. Create Angular service to call REST APIs
6. Update Angular component to subscribe to data from Angular service
7. Display the data in an HTML page
8. Add CrossOrigin support to Spring Boot app
