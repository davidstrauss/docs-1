---
url: /connections/database
---

# Database Identity Providers

Auth0 provides **Database Connections** to authenticate your users with an email/username and password. You can store users' credentials securely in Auth0's user store, or use your own database. 

You can create a new Database Connection or manage existing ones within the [Admin Dashboard](${uiURL}/#/connections/database):

![](/media/articles/connections/database/database-connections.png)

## Scenarios

Typical scenarios concerning database connections include:
* [Using Auth0 User Store](#using-auth0-user-store)
* [Using a Custom User Store](#using-a-custom-user-store)
* [Migrating from a Custom User Store to Auth0](#migrating-from-a-custom-user-store-to-the-auth0-database)

### Using Auth0 User Store

By default, Auth0 will provide the infrastructure to store users on Auth0 directly. This will probably be the use case for greenfield projects, where you can take advantage of using Auth0's infrastructure out of the box and not having to provision your own store. Also, the authentication process will be more performant since all data is already within Auth0.

The Auth0 hosted database is highly secure. Passwords are never stored or logged in plain text, they are hashed with **bcrypt**. [Varying levels of password security requirements can also be enforced](/password-strength).

### Using a Custom User Store

In the case you already have an existing user store, or you just want to store users' credentials in your own server, Auth0 allows you to easily connect to custom repositories and reuse them as identity providers.

![](/media/articles/connections/database/custom-database.png)

In this scenario you have to provide a login script that will be executed each time a user attempts to login to validate the authenticity of the user. You can optionally provide scripts for sign up, email verification, password reset and delete user functionality. 

The custom scripts are pieces of Node.js code that run in a sandbox isolated per Auth0 domain. Auth0 provides templates for the most common databases: **ASP.NET Membership Provider**, **MongoDB**, **MySQL**, **PostgreSQL**, **SQL Server** and **Windows Azure SQL Database**, and for a **Web Service accessed by Basic Auth** as well. Essentially, you can connect to any kind of database or web service using this powerful extensibility point.

Some caveats to keep in mind are:
* Latency will be greater compared to Auth0-hosted user stores
* The database or service must be reachable from Auth0 servers. You will have to open some inbound connections if your store is behind a firewall.
* The database scripts run in the same [Webtask](https://webtask.io) container, which is shared with all other extensibilty points (i.e. rules, webtasks or other databases) belonging to the same Auth0 domain. So you must be careful with error handling and throttling.

You can follow the [Custom Database Connection Tutorial](/connections/database/mysql) for detail steps on how to configure your custom user store.

### Migrating from a custom user store to the Auth0 database

This is the scenario where you already have a legacy user store and you want to start using Auth0 store, but you don't want to have all your users resetting their passwords at once, but rather migrating them gradually as they login over a period of time.

Auth0 provides a migration feature for this scenario. [You can read more about it here](/connections/database/migrating).
