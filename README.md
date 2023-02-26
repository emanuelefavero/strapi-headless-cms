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

> don't forget `/api/` prefix

### **Get all entries**

- `GET http://localhost:1337/api/<collection-name>`
- `GET http://localhost:1337/api/products`

### **Get one entry**

- `GET http://localhost:1337/api/<collection-name>/<id>`
- `GET http://localhost:1337/api/products/1`
