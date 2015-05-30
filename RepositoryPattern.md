There are various advantages of the Repository Pattern including:
	1. Business logic can be tested without need for an external source.
	2. Database access logic can be tested separately.
	3. No duplication of code.
	4. Caching strategy for the datasource can be centralized.
	5. Domain driven development is easier.
	6. Centralizing the data access logic, so code maintainability is easier.

Advantages of ORM:
	* Data manipulation (CRUD) is handled without writing SQL queries
	* Data mapping between result set and entity collection/entity is one of the major features of ORM
	* Using UoW/Context, it can handle the transaction during data manipulation
	* Writing one Data Model in a single place for managing the model’s storage in DB.
	* It fits the natural way of coding with application’s language.
	* Programmers can think fully object oriented way to make any operation with business logic layer and data storage.