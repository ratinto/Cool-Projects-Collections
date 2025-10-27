# 50 Full Stack Standard Interview Questions and Answers for Software Engineering Jobs

This Markdown file contains 50 common full stack developer interview questions and answers, covering frontend, backend, database, and DevOps concepts. These are designed for roles requiring expertise in both client-side and server-side development. Questions are categorized for clarity, with concise answers and explanations. Practice for interviews at companies like Amazon, Google, or startups.

## Frontend (Questions 1-15)

### 1. What is the difference between HTML, CSS, and JavaScript?
**Answer:** HTML structures content, CSS styles it, JavaScript adds interactivity.  
**Explanation:** Core web technologies for building user interfaces.

### 2. Explain the CSS Box Model.
**Answer:** Consists of content, padding, border, and margin.  
**Explanation:** Determines element spacing and layout.

### 3. What is Flexbox in CSS?
**Answer:** Layout model for arranging elements in rows or columns.  
**Explanation:** Uses display: flex for responsive design.

### 4. What is the DOM?
**Answer:** Document Object Model, a tree representation of HTML.  
**Explanation:** JavaScript manipulates it for dynamic content.

### 5. What is event delegation in JavaScript?
**Answer:** Attaching event listeners to a parent for child elements.  
**Explanation:** Improves performance for dynamic elements.

### 6. Difference between `var`, `let`, and `const`?
**Answer:** `var` is function-scoped, `let` and `const` are block-scoped; `const` is immutable.  
**Explanation:** `let` and `const` prevent hoisting issues.

### 7. What is a Promise in JavaScript?
**Answer:** Object representing async operation’s eventual completion or failure.  
**Explanation:** Used with `.then()` or `async/await`.

### 8. Explain React’s Virtual DOM.
**Answer:** In-memory representation of real DOM for efficient updates.  
**Explanation:** Diffing algorithm minimizes DOM manipulation.

### 9. What is JSX in React?
**Answer:** Syntax extension for JavaScript, resembling HTML.  
**Explanation:** Compiled to JavaScript via Babel.

### 10. What are React Hooks?
**Answer:** Functions like `useState`, `useEffect` for state and lifecycle in functional components.  
**Explanation:** Introduced in React 16.8.

### 11. What is Angular’s dependency injection?
**Answer:** Provides dependencies to components/services via constructor.  
**Explanation:** Managed by Angular’s injector.

### 12. How does `async/await` work?
**Answer:** Syntactic sugar over Promises for cleaner async code.  
**Explanation:** `await` pauses execution until Promise resolves.

### 13. What is a Single Page Application (SPA)?
**Answer:** Web app loading a single HTML page, dynamically updating content.  
**Explanation:** Frameworks like React, Angular enable SPAs.

### 14. What is CORS?
**Answer:** Cross-Origin Resource Sharing, a security mechanism for cross-domain requests.  
**Explanation:** Configured via headers like `Access-Control-Allow-Origin`.

### 15. How to optimize frontend performance?
**Answer:** Minify CSS/JS, lazy load images, use CDN, reduce DOM operations.  
**Explanation:** Improves page load speed.

## Backend (Questions 16-30)

### 16. What is Node.js?
**Answer:** JavaScript runtime for server-side applications.  
**Explanation:** Uses V8 engine, event-driven, non-blocking I/O.

### 17. What is Express.js?
**Answer:** Minimal Node.js framework for building RESTful APIs.  
**Explanation:** Simplifies routing, middleware, HTTP handling.

### 18. Explain REST API.
**Answer:** Architectural style using HTTP methods (GET, POST, etc.) for stateless communication.  
**Explanation:** Resources identified by URLs.

### 19. Difference between GET and POST?
**Answer:** GET retrieves data; POST submits data. GET is idempotent, POST isn’t.  
**Explanation:** GET in URL, POST in body.

### 20. What is middleware in Express?
**Answer:** Functions processing requests/responses in the pipeline.  
**Explanation:** E.g., logging, authentication.

### 21. What is JWT?
**Answer:** JSON Web Token for secure data exchange, typically authentication.  
**Explanation:** Contains header, payload, signature.

### 22. Explain MVC architecture.
**Answer:** Model (data), View (UI), Controller (logic) pattern.  
**Explanation:** Separates concerns for maintainability.

### 23. What is an ORM?
**Answer:** Object-Relational Mapping, e.g., Sequelize, TypeORM, maps objects to database tables.  
**Explanation:** Simplifies database operations.

### 24. Difference between SQL and NoSQL databases?
**Answer:** SQL: relational, structured; NoSQL: non-relational, flexible (e.g., MongoDB).  
**Explanation:** SQL for fixed schemas, NoSQL for scalability.

### 25. What is a microservices architecture?
**Answer:** Independent, modular services communicating via APIs.  
**Explanation:** Opposite of monolithic; scalable but complex.

### 26. How to handle errors in Node.js?
**Answer:** Try-catch for sync, error-first callbacks, or Promises for async.  
**Explanation:** Middleware like `app.use((err, req, res, next) => {})`.

### 27. What is GraphQL?
**Answer:** Query language for APIs, fetching only required data.  
**Explanation:** Alternative to REST, single endpoint.

### 28. What is server-side rendering (SSR)?
**Answer:** Rendering HTML on server before sending to client.  
**Explanation:** Improves SEO, initial load (e.g., Next.js).

### 29. What is a reverse proxy?
**Answer:** Server forwarding client requests to backend servers.  
**Explanation:** E.g., Nginx for load balancing.

### 30. How to secure a backend API?
**Answer:** Use HTTPS, JWT, rate limiting, input validation, CORS.  
**Explanation:** Prevents attacks like XSS, SQL injection.

## Database (Questions 31-40)

### 31. What is normalization in databases?
**Answer:** Organizing data to reduce redundancy, ensure consistency.  
**Explanation:** Uses normal forms (1NF, 2NF, 3NF).

### 32. What is a primary key?
**Answer:** Unique identifier for a table row.  
**Explanation:** Ensures no duplicate records.

### 33. Difference between INNER JOIN and LEFT JOIN?
**Answer:** INNER JOIN returns matching rows; LEFT JOIN includes all from left table.  
**Explanation:** SQL join types for combining tables.

### 34. What is an index in a database?
**Answer:** Data structure to speed up queries.  
**Explanation:** Trade-off: faster reads, slower writes.

### 35. Explain ACID properties.
**Answer:** Atomicity, Consistency, Isolation, Durability.  
**Explanation:** Ensures reliable database transactions.

### 36. What is a foreign key?
**Answer:** Column linking to another table’s primary key.  
**Explanation:** Enforces referential integrity.

### 37. How to optimize database queries?
**Answer:** Use indexes, avoid SELECT *, write efficient joins.  
**Explanation:** Reduces query execution time.

### 38. What is MongoDB’s aggregation pipeline?
**Answer:** Framework for data processing (filter, group, sort).  
**Explanation:** Similar to SQL GROUP BY.

### 39. What is a transaction in a database?
**Answer:** Sequence of operations treated as a single unit.  
**Explanation:** Ensures data integrity via ACID.

### 40. What is sharding in databases?
**Answer:** Partitioning data across multiple servers.  
**Explanation:** Enhances scalability in NoSQL.

## DevOps and General (Questions 41-50)

### 41. What is Docker?
**Answer:** Platform for containerizing apps with dependencies.  
**Explanation:** Ensures consistent environments.

### 42. What is Kubernetes?
**Answer:** Orchestrates containerized apps for scaling, deployment.  
**Explanation:** Manages Docker containers.

### 43. Explain CI/CD.
**Answer:** Continuous Integration/Deployment for automated testing and deployment.  
**Explanation:** Tools like Jenkins, GitHub Actions.

### 44. What is Git?
**Answer:** Version control system for tracking code changes.  
**Explanation:** Commands like `git commit`, `git push`.

### 45. Difference between `git merge` and `git rebase`?
**Answer:** Merge combines branches with history; rebase rewrites history.  
**Explanation:** Rebase for cleaner history.

### 46. What is an API gateway?
**Answer:** Manages API requests, routing, authentication.  
**Explanation:** E.g., AWS API Gateway.

### 47. What is load balancing?
**Answer:** Distributes traffic across servers.  
**Explanation:** Improves scalability, reliability (e.g., Nginx).

### 48. What is WebSocket?
**Answer:** Protocol for bidirectional, real-time communication.  
**Explanation:** Used for chat apps, live updates.

### 49. How to handle scalability in full stack apps?
**Answer:** Use microservices, caching (Redis), load balancing, database sharding.  
**Explanation:** Ensures high traffic handling.

### 50. What is a full stack developer’s role?
**Answer:** Builds and maintains both frontend and backend of applications.  
**Explanation:** Requires knowledge of UI, APIs, databases, DevOps.

## Notes
These questions cover full stack development up to 2025 standards. Practice with tools like Docker, Git, and frameworks like React, Node.js. Refer to official docs or platforms like LeetCode, FreeCodeCamp for hands-on prep. Good luck!