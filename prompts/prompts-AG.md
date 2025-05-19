## PROMPT 1

Please let me know what this project does, and which dependencies it uses for both the frontend and backend and test.



## PROMPT 2
I can't see the npm run seed on the backend package.json can you add it please 



## PROMPT 2

### ROLE: You are a DevOps Engineer:

### MISSION:
Please create a workflow that automatically deploys my application to an EC2 instance when:
- A Pull Request is opened targeting the main branch
- An existing Pull Request to main branch is updated

The workflow should be organized in clear frontend and backend steps, specifying where each step runs:


### Backend Steps (**run on GitHub Actions**)
- Verify the code (checkout)
- Set up Node.js version 20 specifically
- Install backend dependencies
- PostgreSQL must be installed and running before deployment steps.
- Run Prisma migrations with `npx prisma migrate deploy`
- Run Prisma generate with `npm run prisma:generate`
- Run database seeds with `npm run seed`
- Run backend linting with `npm run lint`
- Build the backend with `npm run build`
- Run backend tests with `npm run test`

### Frontend Steps (**run on GitHub Actions**)
- Install frontend dependencies
- Run frontend linting with `npm run lint`
- Build the frontend with `npm run build`

### Integration and E2E Testing (**run on GitHub Actions**)
- Set up and start PostgreSQL service
- Verify database connection and run initial setup
- Run database seeds with `npm run seed`
- Run end-to-end tests with `npm run cypress:run`


### Deployment Steps (**run onGitHub Actions** — only if E2E tests pass)
- Deploy both frontend and backend to EC2 using SSH


### on AWS EC2 
- PostgreSQL must be installed and running before deployment steps.
- Verify production database connection and availability
- Run Prisma migrations with `npx prisma migrate deploy`
- Run Prisma generate with `npm run prisma:generate`
- Run database seeds with `npm run seed`

#### For the deployment use these GitHub secrets:
- `EC2_SSH_PRIVATE_KEY`
- `AWS_ACCESS_KEY`
- `AWS_ACCESS_ID`
- `AWS_REGION`
- `EC2_INSTANCE`
- `EC2_USER`


### Note:
- The workflow should display detailed logs for error diagnosis
- The workflow should fail if any tests or build steps fail
- Show appropriate success messages when steps complete successfully
- Deployment should only happen if all previous steps succeed
- if you have question or doubt, please let me know
- use -prefix attribute on npm run
- On the prisma migrate provide the schema es:  --schema=backend/prisma/schema.prisma 
- Do not invent anything. Follow the instructions strictly.

Could you provide me with the YAML code for this workflow?



## PROMPT 3
Can you split the workflow into two files: one for the GitHub Actions CI and another for the EC2 deployment? Obviously, we’ll need to change the filenames accordingly, and the deployment should only be triggered once the GitHub Actions workflow has successfully completed.



## PROMPT 4
- FE e BE E2: has to run on the same instance it cannot be split it in differents steps, can ypu fix it please?


## PROMT 5
Add error handling and notifications to the previous script so that it alerts in case of failures

## PROMPT 6
The deplpoy.yml has to ro run only when ci.yml is succesfully complete.