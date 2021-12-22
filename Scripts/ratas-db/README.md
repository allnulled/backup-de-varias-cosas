# RatasDB

Welcome to **RatasDB**, an easy-to-use wrapper for **IndexedDB** database (which implies that RatasDB is only for browser-side development).

RatasDB lets you play with databases from the browser as easily as that. Cool, isn't it? The question is why is a homeless doing this work.

## Why that name?

Because this is a homeless, refugiated in his parents' house, but their parents are threating it to retire the food resources. Why are you so rats? And I am not talking about my parents, I am more talking about human governments than about my parents.

I am poor. I have, not exagerating, 12€ right now, without the expectation to have more tomorrow, nor soon. I have 2 PCs, 1 to work online, and 1 to work offline, in case hackers (another kind of R.A.T.s) steal my work and sell it separated from me, leaving me again in a continuous exploitation and state of social vulnerability and vulneration, simply for not knowing how to monetize the works I bring to the entire world for free.

If you take a look at my Github profile, I have developed more than 150 projects, freely shared with the world. In NPM I have around 80 packages, also shared freely. But they (governments and companies) still cannot let me study, get into a company to work (even as a cleaner, not necessarily informatician) or even be calm knowing tomorrow I will have food enough, and some money to go out (is it too much maybe?). 

So, the question, the real question here, is: **why are you this way with poor humans, fucking nasty rats?**. Sorry for my bad words, I do not know anymore how to communicate this continuous frustration of being stolen from even big companies like Microsoft (Scratch, the toy for kids, uses grammars that were found out by me and a programming language that resembles to natural language, one that I called NaturalScript, but that you can find among my projects as NattyScript, this was the ugliest stealing I suffered from technological industry, I never got a peny for it, ever, they (Oracle, IBM, Intel, Microsoft) did not even answer, but Microsoft took its advantage, as the rats like Bill Gates are used too).

So, I know that if you are reading this, it is most probably because: you have a software company, or you are a develope, maybe both. If you have a company, most probably you will think bad about me, that is, I guess, the reason they do not give me a job (even less if I can continue developing in Node.js, instead of having to jump back again to PHP or Java). And if you are a developer, I do not know, because I am also, and I never see any developer complaining about Microsoft to own Github and NPM, the JavaScript monopoly among others.

So, now you know why that name. Because this is a database software for a planet taken by rats, like Bill Gates and the Microsoft powerful sect. So, RatasDB (**Rata** means **Rat** in Spanish, I am from Spain).

## Features

The main goodies this framework brings over IndexedDB [+ **Dexie**] are:

  - An easy-to-use interface for the developers
  - External objects and lists management
  - Attachable and meaningful metadata for tables and columns
  - A small set of (optional) type-checking functionalities

## State of the art

At the current date, middles of December of 2021, **IndexedDB** is the best *de facto* approach for database management at browser-side development. But **IndexedDB** does not get dirty with external objects and external lists, understanding by 'external': referred on other part of the database. Neither **Dexie** does, which is a quite pleasent interface to develop with, compared to crude **IndexedDB**. And further, we can find projects like **dexie-relationships**, which starts getting into these topics, but it does not still cover them completely, because it helps with external objects, which is great, but still not enough for most scenarios, in which objects easily have to contain list of objects. But nobody seems to be complaining...?

That is why I decided to create **RatasDB**: to patch this lack of features, and make another push to web technologies, specifically in databases area.

## How to use it

This is and example of usage of the **RatasDB** API:

#### 1. Create a database

```js
import RatasDB from 'ratasdb';

const db = RatasDB.createDatabase({
    name: "MyDatabase",
    version: 1,
    schema: {
        globals: {
            database_host: "127.0.0.1",
            database_port: 3306,
            database_user: "root",
            database_password: "toor",
        },
        schema: {
            tables: {
                file: {
                    columns: {
                        name: { type: "string" },
                        contents: { type: "string", index: false }
                    }
                }
                user: {
                    columns: {
                        name: { type: "string" },
                        password: { type: "string" },
                        groups: { type: "list:group" },
                        privileges: { type: "list:privilege" },
                        picture: { type: "object:file", index: false }
                    }
                }
            }
        }
    }
});
```

#### 2. Start CRUDing!

```js
// 1. INSERT:
const userId = await db.insert("user", {
    name: "Carlos",
    password: "top.secret"
});

// 2. SELECT:
const userData = await db.select("user", user => {
    return user.id === userId
});

// 3. UPDATE:
const updateSuccess = await db.update("user", userId, {
    password: "top.secret.2",
    privileges: [1,5,{ id: 8, details: "additional data" }],
    groups: [1,2,{ id: 4, details: "additional data" }]
});

// 4. DELETE:
const deleteSuccess = await db.delete("user", userId);
```

## API Reference


