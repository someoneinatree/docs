# 12 Factor App Documentation Template

## Purpose

This document intends to lay out a framework for documenting [12 factor apps](http://12factor.net), in a way that makes them fully maintainable and trivially debuggable. This is no easy task: traditionally, software documentation is arduous and horrible. I believe the 12 Factor App methodology could provide an interseting entrypoint into the most typical concerns when it comes to externalizing the information that fills the gaps that self-documenting code cannot.

## The 12 Factors

1. **Codebase** - One codebase tracked in revision control, many deploys
1. **Dependencies** - Explicitly declare and isolate dependencies
1. **Config** - Store config in the environment
1. **Backing services** - Treat backing services as attached resources
1. **Build, release, run** - Strictly separate build and run stages
1. **Processes** - Execute the app as one or more stateless processes
1. **Port binding** - Export services via port binding
1. **Concurrency** - Scale out via the process model
1. **Disposability** - Maximize robustness with fast startup and graceful shutdown
1. **Dev/prod parity** - Keep development, staging, and production as similar as possible
1. **Logs** - Treat logs as event streams
1. **Admin processes** - Run admin/management tasks as one-off processes

## Template
<!-- 
### 1. Codebase

### 2. Dependencies -->

### 3. Config

Config is exposed to application via environment. This includes: external connections (URLs, usernames, keys, passwords), deployment-specific details (brands), and application options & feature flags.

Ideally, each environment varaible used by the app should be documented, describing:
* the method of injection for each deployment (per variable, if injection method differs), and
* the source of that variable (e.g. a given person/role in a given company, randomly generated)

Use a hierarchy to exhaustively, explicitly list all this knowledge (and make it easy to spot if anything's missing).

(Optional) Refresh rules: depending on deployment, updating these may have immediate effects. If manual action is required first, note down (per deployment or set of deployments) how to perform that environment refresh.

Basically, write simple "scripts" for the humans to follow for those non-technical pieces of process. Script everything.

#### Example documentation

##### Simple

###### Variables

* `DATABASE_URL`
   * local: filesystem (`/.env`)
   * remote: TeamCity script
* `EXTERNAL_SERVICE_USERNAME`
   * local: filesystem (`/backend/.env`)
   * remote: TeamCity script
* `EXTERNAL_SERVICE_PASSWORD`

###### Refresh rules

* local: quit `npm start` process and execute again
* remote: trigger `Deploy` job in TeamCity for desired environment

##### Complex

* `DATABASE_URL`
   * local
      * developer: filesystem (`/.env`)
      * tester: filesystem (`/.default.env`)
   * remote
      * dev: TeamCity script
      * qa: CredStash
      * prod: CredStash
<!-- 
### 4. Backing services

### 5. Build, release, run

### 6. Processes

### 7. Port binding

### 8. Concurrency

### 9. Disposability

### 10. Dev/prod parity

### 11. Logs

### 12. Admin processes
 -->