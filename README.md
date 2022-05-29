### Instructions

#### Instala depenedencias
- npm i
#### Crea archivo .env y agrega variables de entorno
- crea un archivo .env en la raíz del proyecto con las siguientes variables de entorno:
  . TOKEN_SECRET = super-secret-password
  . MONGODB_URI = "ruta de la base de datos" -> opcional, mirad /project3-back/db/index.js para entenderlo
  (si tiene MONGODB_URI aceptará esta, sino || aceptará la "mongodb://localhost...")
#### Cambiar el nombre de la base de datos antes de la creación de esta
- cambiar la línia en /project3-back/db/index.js por el nombre de la base de datos que queráis
  ."mongodb://localhost/project-management-server"; //siendo project-management-server el nombre de la base de datos que os creará una vez ejecutéis npm start, así que si queréis una web de películas, poned "project-movies-server" o si tenéis un nombre estilo "netflix" pensado, agregarlo aquí antes del npm start.
#### Lanza el backend
- npm start

### API Documentation

We will start our project by first documenting all of the routes and data models for our API. Following best practices we will use _verbs_ to specify the type of operation being done and _nouns_ when naming endpoints.

#### Routes

##### Project routes

| HTTP verb | URL                        | Request body | Action                        |
| --------- | -------------------------- | ------------ | ----------------------------- |
| GET       | `/api/projects`            | (empty)      | Returns all the projects      |
| POST      | `/api/projects`            | JSON         | Adds a new project            |
| GET       | `/api/projects/:projectId` | (empty)      | Returns the specified project |
| DELETE    | `/api/projects/:projectId` | (empty)      | Deletes the specified project |

##### Task routes

| HTTP verb | URL                  | Request body | Action                     |
| --------- | -------------------- | ------------ | -------------------------- |
| POST      | `/api/tasks`         | JSON         | Adds a new task            |
| GET       | `/api/tasks/:taskId` | (empty)      | Returns the specified task |
| PUT       | `/api/tasks/:taskId` | JSON         | Edits the specified task   |
| DELETE    | `/api/tasks/:taskId` | (empty)      | Deletes the specified task |

##### Auth routes

| HTTP verb | URL            | Request Headers                 | Request Body              |
| --------- | -------------- | ------------------------------- | ------------------------- |
| POST      | `/auth/signup` | --                              | { email, password, name } |
| POST      | `/auth/login`  | --                              | { email, password }       |
| GET       | `/auth/verify` | Authorization: Bearer \< JWT \> | --                        |



<hr>

#### Models

##### Project Model

```js
{
  title: String,
  description: String,
  tasks: [ { type: Schema.Types.ObjectId, ref: 'Task' } ]
}
```

##### Task Model

```js
{
  title: String,
  description: String,
  project: { type: Schema.Types.ObjectId, ref: 'Project' }
}
```

##### User Model

```js
{
  email: { type: String, unique: true, required: true },
  password: { type: String, required: true },
  name: { type: String, required: true },
}
```

