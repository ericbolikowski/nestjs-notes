# About this file

Notes about [Nest.js](https://github.com/nestjs/nest/)

## Nest.js key features
- it surrounds your route handler body with try..catch blocks
- it makes every route handler async
- it creates a global express router
- it creates a separated router for each controller
- it binds error-handling middleware
- it binds body-parser middleware (both json and extended urlencoded)

## Nest.js key conventions
- Keep all files as _close to their domain_ (i.e. module folder) as possible
- Follow [this template](https://github.com/unlight/nest-typescript-starter) when in doubt about anything

## Naming conventions
| Schnowa             |  Jawab                 |
|---------------------|------------------------|
| TypeORM models      |  modelName.entity.ts   |

## CLI cheat sheet
`nest generate module <name>`
`nest generate controller <name>`
`nest generate service <name>`

# Building blocks

## Controllers
- Declaration controls routing
```
  // users.controller.ts 

import { Controller, Get } from '@nestjs/common';

@Controller('users')
export class UsersController {
  @Get()
  async getBooks() { return [{book1}, {book2}] } 

  @Get(':bookID')
  async getBook(@Param('bookID') bookID) {}

  @Post()
  async addBook(@Body() createBookDTO: CreateBookDTO) {}

  @Delete()
  async deleteBook(@Query() query){ ...query.bookID... }
}
```

## Providers
- Just needs a `@Injectable()` decorator at top
```
    // users.service.ts

import { Injectable } from '@nestjs/common';
import { User } from './interfaces/user.interface';

@Injectable()
export class UsersService {
  private readonly users: User[] = [];

  create(user: User) { 
    this.users.push(user);   }

  findAll(): User[] {
    return this.users;
  }
}
```


## Modules
> ... are TS files **decorated with `@Module` decorator**
- Every Nest.js application has a root module
- Plus normally submodules

# Modus operandi

## Dependency injection

```
constructor(private readonly usersService: UsersService){}
 ...
}
```

# How to solve mindfucks

- TypeORM module thinks options provided are for a mongodb database when it is actually for postgres. Mindfuck is to write ... `'postgres' as 'postgres'`. Check [this answer](https://github.com/nestjs/nest/issues/1119).

# Resources
## Good reads

- [NestJS + Basic Auth + Sessions](https://blog.exceptionfound.com/2018/06/07/nestjs-basic-auth-and-sessions/)
- [A guy's lessons learned](https://medium.com/camerakit/building-a-nestjs-api-a-peek-through-my-search-history-80043c6322f0)
- [Awesome NestJs](https://github.com/juliandavidmr/awesome-nestjs)
- 

## Example codebases

- [TypeORM, Guards++](https://github.com/unlight/nest-typescript-starter)

## Resources

- [Set of middlewares](https://github.com/wbhob/nest-middlewares/tree/master/package)

# How to get NestJS to do what Loopback does?

Resources:
- [NestJs CRUD for RESTful APIs](https://github.com/nestjsx/crud)