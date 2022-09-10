# Prisma API

## Tools :

* Language: **TypeScript**
* App Framework: **Express.js**
* ORM: **Prisma**
* Database: **PostgresDB**
* Deployment: **Heroku**

## Project Setup :

```bash
# make project dir and initialize npm
mkdir myProject
cd myProject
npm init -y

# install dev dependencies
npm i -D @types/node @types/express prisma typescript tsc-watch ts-node
# @types/_ - type definitions for _
# prisma - orm toolkit
# typescript - add TS
# tsc-watch - nodemon but for transpiling .ts files --> .js
# ts-node - lets you run TS files directly on Node.js (dont need tsc compiler)

# install dependencies
npm i express dotenv pg @prisma/client
# express - for building api endpoints
# dotenv - to read env variables like db url
# pg - postgresdb
# @prisma/client - query builder
```

## Make Scripts

You need to define 4 scripts in _**package.json**_ to:

```js
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",

  // 1. start the node server
  "start": "node dist/src/index.js",
  // 2. start local dev. server using tsc-watch (nodemon for TS)
  "dev": "tsc-watch --onSuccess \"node ./dist/src/index.js\"",
  // 3. run the seeding script (populate DB with starting data) (run using ts-node)
  "seed": "ts-node prisma/seed.ts",
  // 4. build script to make 'dist' folder where js is transpiled
  "build": "tsc"
},
```

## Directory Setup

1. #### Setup Prisma for your App

Since we installed the prisma as a devdep. above, we can now use its CLI ([reference](https://www.prisma.io/docs/reference/api-reference/command-reference)) which has important commands that we need.

```bash
# sets up prisma for your app; adds a prisma dir and env file
npx prisma init
```

1. #### Gitignore

If you haven't already, create a .gitignore file with the following content:

```bash
# .env has ur secrets like db url
.env
# transpiled js folder not really needed
dist
node_modules
```

## Define Project Directory

1. Create a folder in the project root named **/src**, with a single **index.ts** file where all the api endpoints will be defined.
2. Inside the **/prisma** dir, create a **seed.ts** file which is called by the above `npm run seed` script we defined to populate the db w/ intialize data.

Now your project dir should look like:

```
|__ node_modules
|__ prisma
|			|__ schema.prisma
|__ src
|			|__ index.ts
|__ .env
|__ .gitignore
|__ package-lock.json
|__ package.json
```

**schema.prisma**

* main config file for your Prisma setup which houses:
  * **data sources**: specify details to connect to postgres db.
  * **generators**: specify what clients should be generated based on the data model (prisma client).
  * **data model**: specify your app's ACTUAL DATA SCHEMA and their relations.
* reads the DB URL from .env automagically, so put ur connection URL in the .env - not here!

**seed.ts**

* Uses the Prisma Client to populate the DB w/ initial data that is required for the app to start.
* This ts-node file is ran using the **`npm run seed`** script defined above.

**index.ts**

* We use Express paired with TS and the Prisma Client to define the actual API endpoints ie. GET/POST/PATCH/DELETE.

**.env**

* This file was generated for you when you ran **`npx prisma init`**, and all you have to do is add in your DB URL here and it is read in the schema.prisma file.

**.gitignore**

* files and folders specified here are not commited to the remote repo.
* Should include .env, node\_modules, and dist.

**package.json**

* You defined your scripts here.

## Create Data Model in schema.prisma

First, install the **prisma vs code ext.** for syntax highlighting and autofills. Now let's define our actual data models in the **schema.prisma** file.

**Model** = Table.

An example model is provided below:

```js
model Post {
    id              Int      		@id @default(autoincrement())
  	comments				Comment[]	// a post can have many commments
}

// model names are PascalCase and singular (User; not: user, users, or Users)
model Comment {
		// always include these 3, they're really common and often required
    id              Int      		@id @default(autoincrement())
    createdAt       DateTime 		@default(now())
    updatedAt       DateTime 		@updatedAt
  	
 // <name>					<type>			<optional attributes>
    title   				String
    content 				String
		
    // A comment can belong to 1 post
    Post   					Post? 			@relation(fields: [postId], references: [id])
  	postId 					Int?
}
```

Note:

*   Instead of manually defining a relation, use the autocomplete feature of the **prisma vs code ext.**; ie. for a Book-Author model where Book has 1 Author and Author has many Book

    ```js
    model Author {
        id                  Int      @id @default(autoincrement())
        createdAt           DateTime @default(now())
        updatedAt           DateTime @updatedAt
        name           			String
    }

    model Book {
        id            Int      		@id @default(autoincrement())
        createdAt     DateTime 		@default(now())
        updatedAt     DateTime 		@updatedAt
        Title         String
        Genre         String
       
    // 1) Each Book has 1 Author, so type the below & hit SAVE; let prisma ext. do it!
        author        Author
    }

    // -------------THIS TURNS INTO:---------------------

    model Author {
        id                  Int      @id @default(autoincrement())
        createdAt           DateTime @default(now())
        updatedAt           DateTime @updatedAt
    		name								String
        Book                Book[] // new: List of Books with authorId = this.id 
    }

    model Book {
        id            Int      @id @default(autoincrement())
        createdAt     DateTime @default(now())
        updatedAt     DateTime @updatedAt
        Title         String
        Genre         String
        
        author        Author   @relation(fields: [authorId], references: [id], onDelete: Cascade) // new
        authorId      Int // new
    }
    ```

## Now Synchronize Schemas

Now synchronize your Prisma schema (from **schema.prisma**) with your database schema.

```bash
# run the following to sync. schemas
$ npx prisma db push

# open the Prisma studio, a visual editor for the data in your database
$ npx prisma studio
```

* Note: **db push** works well for **prototyping**; otherwise, see prisma migrations.

## Create Seeder Function

**seed.ts** Uues the Prisma Client to populate the DB w/ initial data that is required for the app to start. This ts-node file is ran using the **`npm run seed`** script previously defined.

```js
import { PrismaClient } from "@prisma/client";

// this PrismaClient object is used to build queries
const prisma = new PrismaClient();

async function run() {

    const authors = [
        {Name: "Rick Riordan", isBestSeller: true},
        {Name: "Joanne Rowling", isBestSeller: true},
				{Name: "Jeff Kinney", isBestSeller: true},
        {Name: "John Tolkien", isBestSeller: true},
        {Name: "George Martin", isBestSeller: true}
    ]
	
    // this task was automated,
    for(let index:number=0; index<authors.length; index++) {
        const [firstName, lastName] = authors[index].Name.split(" ");
				
				// in the Author table, upsert (update if exists, create otherwise)
        const tempAuthor = await prisma.author.upsert({
          	where: { id: index + 1 },   // where it matches this criteria
            update: {}, // update these fields (leave empty if you want to create)
            create: {	// create a record with the following fields (see schema)
                id: index + 1,
                firstName,
                lastName,
                publishedBestSeller: authors[index].isBestSeller,
            }
        })

        console.log(tempAuthor);
    }
    

    /* You can also enter single records like a primate.

    const riordan = await prisma.author.upsert({
        where: { id: 1 },
        update: {},
        create: {
            id: 1,
            firstName: "Rick",
            lastName: "Riordan",
            publishedBestSeller: true
        }
    })
    
    */
}

// When you run 'npm run seed', ts-node will run this file, and it will execute this run() function that's called below.
run()
    .catch((err) => {
        console.log(err);
        process.exit();
    })
    .finally(async () => {
        await prisma.$disconnect();
    })
```

## Define API Endpoints

You can use the below express API app example as a guide; pay attention to how the queries are built:

```js
import "dotenv/config"
import express from "express"
import { Prisma, PrismaClient } from "@prisma/client";

const app = express();
const prisma = new PrismaClient();

const PORT = 3001;

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }))

// GET ALL BOOKS - $findMany
app.get('/books', async (req, res, next) => {
    try {
        const books = await prisma.book.findMany({
            where: { published: true },
            orderBy: { createdAt: "desc" }
        })
        res.json({ books });

    } catch (error: any) {
        next(error.message);
    }
});

// POST (CREATE) a BOOK - $create
app.post('/books', async (req, res, next) => {
    try {
        const book = await prisma.book.create({
            data: { authorId: 1, ...req.body }
        })
        res.json({ book })

    } catch (error: any) {
        next(error.message);
    }
});

// GET a BOOK by ID - $findUnique
app.get('/books/:id', async (req, res, next) => {
    try {
        const book = await prisma.book.findUnique({
            where: {id: Number(req.params.id)}
        })
        res.json({ book });

    } catch (error: any) {
        next(error.message)
    }
});

// UPDATE a BOOK by ID - $update
app.patch('/books/:id', async (req, res, next) => {
    try {
        const book = await prisma.book.update({
            where: {
                id: Number(req.params.id)
            },
            data: req.body,
        })
        res.json({ book });

    } catch (error: any) {
        next(error.message);
    }
});

// DELETE a BOOK by ID - $delete
app.delete('/books/:id', async (req, res, next) => {
    try {
        const book = await prisma.book.delete({
            where: {
                id: Number(req.params.id),
            }
        })
        res.json({ book });

    } catch (error: any) {
        next(error.message);
    }
});

// GET a AUTHOR's BOOKS - $findUnique
app.get('/author/:id/books', async (req, res, next) => {
    try {
        const authorsBooks = await prisma.author.findUnique({
            where: {
                id: Number(req.params.id),
            },
            include: {
                Book: {
                    where: {
                        published: true
                    }
                }
            }
        })
        res.json({ authorsBooks });

    } catch (error: any) {
        next(error.message);
    }
});

app.listen(PORT, () => {
    console.log(`Listening on port ${PORT}`);
})
```

Usually, after any updates in the schema, if you want to flush the DB and reset Prisma to resync the DB:

```bash
npm run seed
npx prisma db push
npx prisma studio
```
