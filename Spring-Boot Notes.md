## Create a new SpringBoot project
- Open [Spring Initializr](https://start.spring.io/), [Spring Initializr Reference](https://docs.spring.io/initializr/docs/current/reference/html/)
- Change Artifact, Name, Description, PackageName
- Add dependencies: `Spring Data JPA`, `Rest Repositories`, `MySQL Driver`, `Lombok`
- Generate Project
## Develop JPA Entities
- Import created project into IntelliJ (File-New-Project from External Source)
- Copy application.properties from starter files
- Develop the entities. In `src/main/java/com/yuehao/ecommerce` add new package called `entity`
- Create a new Java class `Product` inside `entity`, this is our JPA entity
- Generate JPA annotation for table
  - @Entity, import Entity, @Table
- Develop the Entities: `Product` and `ProductCategory`
## Create REST APIs
- new package in `com.yuehao.ecommerce` called `dao`
- In `dao`, create new Java class > Interface: ProductRepository
- In `dao`, create new Java class > Interface: ProductCategoryRepository
- Run in `YuehaoShopApplication.java`
- In Browser access `http://localhost:8080/api`, a list api exposed to this application
- Access `http://localhost:8080/api/products` or `http://localhost:8080/api/product-category`, it should show the contents from database
## Make REST API Read-only
- Spring Data REST will expose all these endpoints:

| HTTP Method |                | CRUD Action                |
|-------------|----------------|----------------------------|
| POST        | /products      | Create a new product       |
| GET         | /products      | Read a list of products    |
| GET         | /products/{id} | Read a single product      |
| PUT         | /products/{id} | Update an existing product |
| DELETE      | /products/{id} | Delete an existing product |

- We only want `GET`, so we need to configure to disable `POST` and `DELETE` HTTP methods
- In `com.yuehao.ecommerce`, create a new package `config`
- In `config` package, create new Java class called `MyDataRestConfig`
- Run application and test in POSTMAN
- In postman, set a new request, get from `http://localhost:8080/api/products`
- Duplicate the tab, change "GET" to "POST" request, "Body-raw-JSON", write a simple JSON {"test": "data"}
- If `Status` is `405 Method Not Allowed`, then it works, this API does not allow "POST" request
