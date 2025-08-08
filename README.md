# Library Management

## System Architecture

![System Architecture](./asset/system%20architecture.png)

### There are 5 microservices in this system:

1. **Books:** Responsible for managing book information (author, genres), including adding, updating, and deleting books.
2. **Borrows:** Responsible for borrowing transactions, tracking, and book availability to borrow.
3. **Policy:** Responsible for enforcing library policies such as borrowing limits, return deadlines, and overdue rules.
4. **API Gateway:** Acts as a single entry point for all client requests, routing them to the appropriate microservice
5. **Discovery Server:** Server side discovery of available microservices, allowing the API Gateway to route requests dynamically.

# Business Rules
- The system is operated by a trusted administrator. It is not client facing.
- User authentication and authorization is managed externally by the admin (using library cards).
- A user can borrow up to 3 books by default at a time.
  - This borrowing limit is configurable via the Policy service.
  - A user cannot borrow a new book if they have any outstanding borrowed books.
- There is only one copy of each book.
- Each book can be associated with a single author and multiple genres.

# Gateway
| Service | EndPoint       | Method | Description        |
|---------|----------------|--------|--------------------|
| Books   | /book          | GET    | Get all books      |
| Books   | /book/{id}     | GET    | Get book by id     |
| Books   | /book          | POST   | Insert a new book  |
| Books   | /book/{id}     | PUT    | Update a book      |
| Books   | /book/{id}     | DELETE | Delete a book      |
| Borrows | /borrow        | POST   | Borrow a book      |
| Borrows | /borrow/return | POST   | Return a book      |
| Policy  | /policy/{key}  | GET    | Get library policy |
Default URI for gateway: http://localhost:8080\

# Swagger Documentation
- Books: http://localhost:8080/book/swagger-ui.html
- Borrows: http://localhost:8080/borrow/swagger-ui.html
- Policy: http://localhost:8080/policy/swagger-ui.html

# GitHub Repositories
1. [Book Service](https://github.com/dilpreetwk/library-management-book-service)
2. [Borrow Service](https://github.com/dilpreetwk/library-management-borrow-service)
3. [Policy Service](https://github.com/dilpreetwk/library-management-policy-service)
4. [API Gateway](https://github.com/dilpreetwk/library-management-api-gateway)
5. [Discovery Server](https://github.com/dilpreetwk/library-management-discovery-server)
6. [Library Management Shell](https://github.com/dilpreetwk/library-management-shell)

# TODO (Priority Order)
- [ ] 80% unit test coverage
- [ ] Improved exception handling
- [ ] Docker Setup
- [ ] Installation Guide + Library Management Shell Quick Start Guide
- [ ] CI/CD