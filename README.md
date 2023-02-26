# Strapi Headless CMS

This is a cheat sheet repository for setting up [Strapi](https://strapi.io/) as an headless CMS (Content Management System)

&nbsp;

## Create a new Strapi project

- `mkdir <project-name>`
- `cd <project-name>`

> Note: If Strapi isn't compatible with your current Node.js version, you need to install a compatible version. You can do this by using [nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
>
> - e.g. add an `.nvmrc` file with the following content: `v18.13.0`
> - run `nvm install` and `nvm use` to install and use the correct version

- `npx create-strapi-app . --quickstart`

> Note: By default Strapi uses SQLite as database

### Create a new Strapi project with Postgres

- `npx create-strapi-app .`
- choose `Custom (manual settings)`
- choose `PostgreSQL`

> Note: You can also use the `--ts` flag to create a TypeScript project
>
> - `npx create-strapi-app . --quickstart --ts`

&nbsp;

---

&nbsp;

## **Run Strapi in development mode**

> Automatically restarts the server when files are changed

- `npm run develop`

### Run Strapi

- `npm run start`

### **Default Server Address**

- `http://localhost:1337`

### **Default Admin Panel Address**

- `http://localhost:1337/admin`

&nbsp;

---

&nbsp;

## Admin Panel

- Create New Types (collections), fields (attributes) and relations in the `Content Builder` section
- Create data in the `Content Manager` section

> You can follow the steps [here](https://docs.strapi.io/dev-docs/quick-start)

&nbsp;

---

&nbsp;

## REST API Calls

> you can use [Postman](https://www.postman.com/)
>
> don't forget `/api/` prefix

### **Get all entries**

- `GET http://localhost:1337/api/<collection-name>`
- `GET http://localhost:1337/api/products`

### **Get one entry**

- `GET http://localhost:1337/api/<collection-name>/<id>`
- `GET http://localhost:1337/api/products/1`

## Populate

By default Strapi doesn't populate relations. You can populate them by adding the `populate` query parameter:

- `GET http://localhost:1337/api/<collection-name>?populate=<relation-name>`
- `GET http://localhost:1337/api/products?populate=category` (populate one relation)
- `GET http://localhost:1337/api/products?populate[0]=categories` (same as above)
- `GET http://localhost:1337/api/products?populate=*` (populate all relations)

## Filter

Return only the title and description fields:

- `http://localhost:1337/api/products?fields[0]=title&fields[1]=description`

Filter results by title (return only products with title that starts with iPhone), still populate the categories relation:

- `GET http://localhost:1337/api/products?populate=categories&filters[title][$startsWithi]=iPhone`

Filter results by name of the category (return only products with category that starts with Mobile), still populate the categories relation:

- `GET http://localhost:1337/api/products?populate=categories&filters[categories.name][$startsWithi]=Mobile`

## Sort

Sort results by title in ascending order:

- `GET http://localhost:1337/api/products?sort=title`

Sort results by title in descending order:

- `GET http://localhost:1337/api/products?sort=title:desc`

## PAGINATION

Limit the number of results to 1 starting from the first result:

- `GET http://localhost:1337/api/products?pagination[start]=0&pagination[limit]=1`

Limit the number of results to 1 starting from the second result:

- `GET http://localhost:1337/api/products?pagination[start]=1&pagination[limit]=1`

Limit the number of results to 2 starting from the first result:

- `GET http://localhost:1337/api/products?pagination[start]=0&pagination[limit]=2`

Sort results by id in descending order and limit the number of results to 1 starting from the first result

- GET `http://localhost:1337/api/products?sort=id:desc&pagination[limit]=1`

&nbsp;

---

&nbsp;

## **AUTHENTICATION**

- Go to admin panel: `http://localhost:1337/admin`
- Create a new user in the user collection
- Add `username` `email` and `password` fields
  > Note: if you want to add email confirmation, select `confirmed: true` when creating the user
- save the user

&nbsp;

- Go to `settings` -> `roles & permissions`
- Select the `Authenticated` role
- Turn on all permissions for the `Product`, `Category` and `User-Permission`

> Do the same for the `Public` role, choose the permission you need for the current application

## Test the authentication

- Go to [Postman](https://www.postman.com/) and create a new `POST` request:
- `POST http://localhost:1337/api/auth/local`

&nbsp;

- Select `body`, `raw` and `JSON`

> Make suer you have selected `JSON` and not `Text`

- Add the following content:

  ```json
  {
    "identifier": "john",
    "password": "123456"
  }
  ```

> Make sure to use the correct `identifier` and `password`

- **If everything is ok, you should get a response with the user data and the `jwt token`**

### **Create a new product**

- Grab the `jwt token` from the previous request and add it to the headers of the following new request (`Authorization -> Bearer <token>`)

- Make a POST request to the products endpoint:
- `POST http://localhost:1337/api/products`

- Add the following content:

  ```json
  {
    "data": {
      "title": "Test product",
      "description": "test product description.",
      "price": 199,
      "qty": 80
    }
  }
  ```

&nbsp;

---

&nbsp;

[**Go To Top &nbsp; ⬆️**](#strapi-headless-cms)
