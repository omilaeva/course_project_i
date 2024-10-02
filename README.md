# course_project_i
Aalto web software development course project 1
## Web application description
It's a simple shopping list web application.
On the main page there is statistics of how many lists were created (active and deactivated in total) and how many items there are in all shopping lists in total. Below there is a link to all active lists.

On the lists page there is a form to create a new shopping list and the list of all active lists with the button ```Deactivate list!``` to deactivate one.

When press on the list link the choosen list's items are shown in alphabetical order active first. Collected items also shown in alphabetical order after the active ones. To mark item as collected press ```Collect item!``` button.

Each page has a link to the previous page on the top.

## How to run the app

To run the application locally is used Docker Compose.
In the root directory there is a ```docker-compose.yml``` file, which contains all nesessary descriptions for each part of the web application, including PostgreSQL as database, Flyway as migration tool, Playwright as E2E testing tool.

To run the docker compose you need the ```project.env``` file, where store environmental variables used to connect to the database. 
Below there is an example of the ```project.env``` file

```
# Database configuration for PostgreSQL (running in container called "database-shopping-lists")
POSTGRES_USER=username
POSTGRES_PASSWORD=password
POSTGRES_DB=database

# Database configuration for Flyway (used for database migrations)
FLYWAY_USER=username
FLYWAY_PASSWORD=password
FLYWAY_URL=jdbc:postgresql://database-shopping-lists:5432/database

# Database configuration for PostgreSQL driver
PGUSER=username
PGPASSWORD=password
PGHOST=database-shopping-lists
PGPORT=5432
PGDATABASE=database

# Deno cache location (avoid reloading depedencies over and over)
DENO_DIR=/app-cache
```

### To run the web application

First create ```project.env``` file and specify the credentials. 
Make sure that docker engine is up and running before moving forward.
Run the following command in a terminal:

```
docker compose up --build
```
Now the app is up and running on the [http://localhost:7777](http://localhost:7777)

### To run tests

The project includes some E2E test. You can run them using the following command from the terminal:

```
docker compose run --entrypoint=npx e2e-playwright playwright test && docker compose rm -sf
```
This command runs the tests and afterwards removes any contents in the database of your local project.

```
  ✓  1 [e2e-headless-chromium] › tests/shoppingListsTests.spec.js:3:1 › Main page has expected title and link. (276ms)
```
The tick marks ✓ on the right side before each test indicates that the test passed.


