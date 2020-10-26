#### 1. **Install Nest CLI:**

    $ yarn global add @nestjs/cli

#### 2. **Create a new Nest project:**

    $ nest new <project_name>

e.g. nestjs-task-management.

#### 3. **Run the project in Dev mode:**

    $ yarn start:dev

#### 4. **Create a MODULE (organizes the structure):**

    $ nest g module <module_name>

e.g. "tasks", creates a "tasks" folder with a "tasks.module.ts" file.

#### 5. **Create a CONTROLLER (handle requests in routes):**

    $ nest g controller <controller_name> --no-spec

e.g. "tasks", creates a "tasks.controller.ts" file and updates the module.

@Controller('tasks') => which route should be handled by this controller.

#### 6. **Create a SERVICE (handle business logic)**

    $ nest g service <service_name> --no-spec

e.g. "tasks", creates a "tasks.service.ts" file and updates the module.

**Dependency Injection**: To use it whitin the CONTROLLER, define it as a parameter in the constructor method, e.g.:

```
constructor(private TasksService: TasksService) {}
```

#### 7. **Create a model**

Define its structure as a Interface (chosen) or as a Class.

Use it by importing into the service and controller.

### Concepts:

#### **_DTO - Data Transfer Object_**

Defined by an interface or a class (chosen), it is used to define how the data will be sent over the network.

Represents the shape of the data that we expect.

#### **_PIPES_**

Pipes operate on the **arguments** to be processed by the route handler, just before the handler is called.

Pipes can perform **data transformation** or **data validation.**

Pipes can throw exceptions.

Pipes can be asynchronous.

#### 8. **Initialize PostgreSQL with Docker**

Tip: [NestJS, TypeORM and PostgreSQL (with Docker) Set Up](https://medium.com/@gausmann.simon/nestjs-typeorm-and-postgresql-full-example-development-and-project-setup-working-with-database-c1a2b1b11b8f)

    $ sudo mkdir -p /storage/docker/nestjs-taskmanagement/postgresql-data

    $ docker run --name docker-nestjs -e POSTGRES_PASSWORD=postgres -p 5432:5432 -v /storage/docker/nestjs-taskmanagement/postgresql-data:/var/lib/postgresql/data -d postgres

- Create a "taskmanagement" database:

```
$ docker exec -it docker-nestjs bash

$ psql -U postgres

$ create database taskmanagement;

$ exit;
```

#### 9. **Set up TypeORM**

Uses repositoy patter.

    $ yarn add @nestjs/typeorm typeorm pg

    $ touch src/config/typeorm.config.ts

Import typeorm.config.ts into app.module.ts

Create a **entity** (refers to a table):

    $ touch src/<module_name>/<module_name>.entity.ts

Create a **repository** (handles database logic):

    $ touch src/<module_name>/<module_name>.repository.ts

#### 10. **Authentication - JWT/Passport.js**

    $ nest g module auth

    $ nest g controller auth --no-spec

    $ nest g service auth --no-spec

    $ touch src/auth/user.entity.ts

    $ touch src/auth/user.repository.ts

- Import UserRepository into auth.module.ts
- Inject UserRepository as dependency injection (constructor) into auth.service.ts

  - JSON Web Tokens
