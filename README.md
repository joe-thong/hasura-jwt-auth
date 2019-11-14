# nextjs-8-jwt

> This is a project that draws the concept from two projects, namely  [passportjs-jwt-roles](https://github.com/hasura/graphql-engine/tree/master/community/boilerplates/auth-servers/passportjs-jwt-roles)  and  [nextjs-8-serverless](https://github.com/hasura/graphql-engine/tree/master/community/sample-apps/nextjs-8-serverless) 

Deviation from passport-jwt-roles: 
- Did not deploy to heroku
- Instead I added docker-compose.yml to spin up  1 hasura and 1 postgres
- postgres sits on port 5432 and hasura is externally mapped to port 8082
- Did not run the hasura migrate on the schema and metadata of this project.
- Ran the auth server code locally, on port 8080

Deviation from nextjs-8-serverless:
- Nothing much, pretty standard except for some configuration changes
- Ran hasura migrate on the schema and metadata in 'hasura' folder
- Ran locally on port 3000 (yarn run dev)

## Problem
- I am able to successfully signup and login from the next.js react app, but going to /articles would throw me an error.  
- There's graphql query defined in `components/ArticleList.js`. 

### The Error
> Error while running `getDataFromTree` TypeError: Cannot read property 'article' of undefined

Down the stack trace there's a graphql error 
> (node:34595) UnhandledPromiseRejectionWarning: Error: GraphQL error: Malformed Authorization header

## Steps to Reproduce

- docker-compose up -d in ./passport-jwt 
- npm run start in ./passport-jwt
- hasura migrate apply and hasura metadata apply in ./nextjs-8-serverless/hasura
- yarn run dev in ./nextjs-8-serverless/app
- open up browser and go to http://localhost:3000
- sign up for one account, verify it is in postgres
- login, will be redirected to /articles end point directly, error would be shown

