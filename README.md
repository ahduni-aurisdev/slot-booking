# Sports Slot Booking and Managment System

## Ahmedabad University

**Application:** Sports Facility Management System\
**Application Type:** Local Node.js Web Application\
**Primary Purpose:** Management of sports facilities, courts, student
records, bookings, audit history, reports, administrative controls, and
facility restrictions.

------------------------------------------------------------------------

## 1. System Overview

The **Sports Facility Management System** is a browser-based university
sports administration application built with **Node.js, Express.js,**
**SQLite, HTML5, CSS, and JavaScript**.

The application provides a centralized interface for authorized
university users to:

-   Verify students using their enrollment number.
-   Create and manage sports facility bookings.
-   Allocate courts/grounds according to sport and schedule.
-   Manage additional players associated with a booking.
-   View active and future allocations.
-   Review booking and audit history.
-   Search student profiles and booking/restriction history.
-   Generate daily and administrative reports.
-   Manage sports and court resources.
-   Manage administrative/helpdesk accounts.
-   Apply and manage sport-specific student restrictions.
-   Perform student-master data import and administration.
-   Send booking, restriction, and account-recovery emails when an SMTP
    provider is configured.

The frontend is served directly by the Express application from the
`public/` directory. The backend uses SQLite as the local relational
database. The database file is stored locally as `sports_facility.db`;
no separate database server is required.

The backend also contains authentication and authorization controls.
Login creates a server-side session token, protected API routes require
the `x-auth-token` header, and administrator-only operations are
protected by an administrator authorization check.


## HOW WILL THIS SOFTWARE WORK ONCE IT IS DEPLOYED ?

- when it is deployed perfectly. there will need to import the master database of the students/faculty/staff from the admin panel. the database should be in the .csv format.
- There is requiremnt to form an another ADMIN role account as per the requiremnt from the helpdesk. (Add the details with no mistake as no confirmation will be taken while creating th account.)
- it should be made from the admin panel giving the details like the username, email-id, password and role. 

 IT deparment needs to Have a MASTER DATABASE in which it should have 
    1. Email ID
    2. Enrollment No
    3. Student Name

    Note -  please make sure that the .csv format dataset in this format with the same tite of the details and also the UPPERCASE AND LOWERCASE of the title is acording to shown above.

Once the dataset it is imported then it is ready for the USE if the deployment is done properly making sure that that enviourment variables are set up properly according to the .env.example and the email service is porerly working.

After doing this it can be used by the heldesk.



## 2. Technology Stack & System Prerequisites

### Technology Stack
(Mentioned earlier while discussion with IT-department before approval)

  -----------------------------------------------------------------------
  Component                           Technology
  ----------------------------------- -----------------------------------
  Runtime                             Node.js

  Server Framework                    Express.js 4.x

  Database                            SQLite3

  Database File                       `sports_facility.db`

  Authentication                      Server-side session tokens + bcrypt
                                      password verification

  Frontend                            HTML5, CSS, JavaScript

  UI Utility                          Tailwind CSS CDN

  Email                               Nodemailer / SMTP

  Spreadsheet Reports                 SheetJS (`xlsx`)

  Configuration                       `.env` / `dotenv`
  -----------------------------------------------------------------------

The project is intended for **Node.js 24.x LTS** for the final university
handover and evaluation environment. It uses Express, SQLite3, bcryptjs,
dotenv, Nodemailer, CORS, and SheetJS. fileciteturn0file1L9-L19


### Minimum Prerequisites

Install the following on the evaluation laptop:

1.  **Node.js 24.x LTS**
2.  **npm** (included with Node.js)
3.  A modern web browser:
    -   Google Chrome
    -   Microsoft Edge
    -   Mozilla Firefox
    -   Another current browser with standard HTML5/JavaScript support
4.  Terminal / Command Prompt / PowerShell

**No separate installation of MySQL, PostgreSQL, SQL Server, or another**
**database server is required for this software.**
**this software uses SQlite3 as database and it was clearly mentioned before.**

### ---------------------------------------------------------

### Verify Node.js and npm

Open a terminal and run:


node -v
npm -v


Example:

v24.x.x
10.x.x


The exact patch version may differ, but `node -v` should report a
**24.x.x** version for the final handover environment.

### Node.js Version Policy for Software

``` json
"engines": {
  "node": ">=24"
}
```

This keeps the application on the Node.js 24 major release rather than
allowing an automatic move to a future major version. After installing or
upgrading Node.js, run `npm install` and perform a complete application
smoke test before creating the final handover ZIP.

### ------------------------------------------------------------------------

## 3. Directory Layout

The final handover package has structure following:


Sports Slot Booking and Managment System/
│
├── server.js
├── database.js
├── package.json
├── package-lock.json
├── .env.example
├── .env                         # Created locally; do not distribute secrets
├── sports_facility.db           # SQLite database (Stored in form of a file)
│
└── public/
    ├── index.html
    ├── logo.png
```

### File/Folder Responsibilities

  ----------------------------------------------
  Path                                Purpose
  ----------------------------------------------
  `server.js`                         Main Express server, API routes,
                                      authentication, business logic,
                                      email handling, reports, and static
                                      file serving.

  `database.js`                       SQLite connection and base
                                      database/schema initialization. It
                                      opens `sports_facility.db` from the
                                      application directory.

  `package.json`                      Project metadata, Node.js engine
                                      requirement, dependencies, and
                                      `npm start` command.

  `package-lock.json`                 Locks the dependency tree so
                                      `npm install` can reproduce the
                                      intended package versions.

  `.env.example`                      Template containing application
                                      configuration and email/bootstrap
                                      settings.

  `.env`                              Local environment configuration
                                      created from `.env.example`. It contains
                                      contain passwords or SMTP
                                      credentials and should not be
                                      committed or distributed publicly while deployment.

  `sports_facility.db`                Local SQLite database containing
                                      the application's persistent data.

  `public/`                           Browser-facing static frontend
                                      assets.

  `public/index.html`                 Main Sports Facility Portal
                                      interface.

  `public/logo.png`                   Ahmedabad University branding/logo
                                      used in the interface.



### 4. Step-by-Step Local Deployment Guide


## Step 1 --- Extract the ZIP Package

Extract the complete handover ZIP package to a convenient location from the repositry.


### Why `node_modules` is not included

The `node_modules/` directory is intentionally excluded from the ZIP
package.

This reduces the handover package size and avoids distributing
platform-specific installed dependency binaries.

The required dependency information is already stored in:

-   `package.json`
-   `package-lock.json`

------------------------------------------------------------------------

## Step 2 --- Open a Terminal in the Project Directory

Navigate into the extracted project folder.

You should see files such as:

``` text
server.js
database.js
package.json
package-lock.json
.env.example
sports_facility.db
public
```

------------------------------------------------------------------------

## Step 3 --- Verify Node.js

Run:

``` bash
node -v
npm -v
```

If Node.js is not version 24.x, install **Node.js 24.x LTS** before
continuing.

------------------------------------------------------------------------

## Step 4 --- Restore Project Dependencies

Run:

``` bash
npm install
```

This reads `package.json` and `package-lock.json` and restores the
required packages into a newly created `node_modules/` directory.

The project dependencies include:

-   `express`
-   `sqlite3`
-   `bcryptjs`
-   `cors`
-   `dotenv`
-   `nodemailer`
-   `xlsx`

These dependencies are declared by the project itself.

After installation, verify that no fatal npm error was reported.

------------------------------------------------------------------------

## Step 5 --- Configure Environment Variables

Create a local `.env` file from the supplied template on the path where the server.js and database.js file is present.


The supplied environment template defines the application port,
production mode, initial administrator bootstrap settings, optional CORS
configuration, and SMTP email configuration.


## For local testing, use:

``` env
EMAIL_PROVIDER=mock 
```

In mock mode, email messages are printed to the server terminal instead
of being sent through an external mail server.

**For Deployment Pupouse the enviorment variable should be following one**
For an approved SMTP server, configure:

``` env
EMAIL_PROVIDER=smtp
SMTP_HOST=smtp.example.edu
SMTP_PORT=587
SMTP_USER=REPLACE_WITH_SMTP_USER        # Mail-id from which the automated mail should go.
SMTP_PASS=REPLACE_WITH_SMTP_PASSWORD    # app password that is created fro the from the SMTP_USER account
SMTP_FROM=REPLACE_WITH_SMTP_USER         # Mail-id from which the automated mail should go.
```

The application uses Nodemailer for SMTP delivery.

> Do not place real SMTP passwords or other confidential credentials
> into the README or into source-control repositories.

------------------------------------------------------------------------

## Step 6 --- Confirm the SQLite Database File

Make sure:

``` text
sports_facility.db
```

is present in the same project directory as `server.js`.

The database layer resolves the database path relative to the
application directory.

The application does not require a separately installed SQLite server.
SQLite operates directly against the local database file.

The database schema contains relational structures for users, sports,
courts, students, bookings, booking participants, audit logs, and
restrictions. 

------------------------------------------------------------------------

## Step 7 --- Start the Application

There are two supported startup commands.

### Option A --- npm start

``` bash
npm start
```

The project's `start` script runs:

``` bash
node server.js
```

as defined in `package.json`. fileciteturn0file1L5-L7

### Option B --- Direct Node.js command

``` bash
node server.js
```

When the server starts successfully, the terminal prints the active port
and local URL.

------------------------------------------------------------------------

## Step 8 --- Open the Application

With the supplied `.env.example` configuration, the application uses:

``` text
http://localhost:3000
```

Open that address in the browser.

### Important Port Note

The current `server.js` contains this fallback:

``` text
PORT = process.env.PORT || 3005
```

Therefore:

-   If `.env` contains `PORT=3000`, use `http://localhost:3000`.
-   If no `PORT` environment variable is loaded, the server falls back
    to port `3005`.
-   If you intentionally change `PORT`, use the corresponding URL.

The server itself prints the actual local URL when it starts.


------------------------------------------------------------------------

# 5. Accessing the System & Demo Login Credentials

## Login URL

For the standard local configuration:

**http://localhost:3000**

The login screen is the **Sports Facility Portal** and requires
authorized university credentials.         

# INITIAL USERNAME and PASSWORD are provided in the .env.example. kindly please make sure not to change the password for this account.
# this account has not been suppoted with recovery email id and passwrod. when new account is created in the system.



# 6. Database Maintenance & Operational Notes

## SQLite Database

The application uses a local SQLite database:

``` text
sports_facility.db
```

No separate database engine or database service needs to be installed.

The application opens the SQLite file from the same directory as the
backend.


### Do Not Delete or Rename the Database

For a handover/evaluation copy, do not rename:

``` text
sports_facility.db
```

### Backup Recommendation

Before making significant administrative or database changes, stop the
server and make a copy of:

``` text
sports_facility.db
```

For example:

``` text
sports_facility_backup_YYYY-MM-DD.db
```

**Because SQLite is file-based, this is the primary persistent database**
**artifact for the local installation.**


# 7. Troubleshooting Guide

## Problem 1 --- `node` is not recognized

### Symptom

``` text
'node' is not recognized as an internal or external command
```

### Solution

Install **Node.js 24.x LTS** and reopen the terminal.

Then verify:

``` bash
node -v
npm -v
```

------------------------------------------------------------------------

## Problem 2 --- `npm install` fails

### Possible causes

-   Node.js version is too old.
-   Internet access is unavailable.
-   npm is misconfigured.
-   A corporate/university proxy blocks package downloads.
-   A package installation step failed.

### Solution

First verify:

``` bash
node -v
npm -v
```

Then retry:

``` bash
npm install
```

If a previous installation was interrupted, remove the incomplete
`node_modules` directory and run:

``` bash
npm install
```

Do not delete `package-lock.json` unless there is a deliberate
dependency-maintenance reason to regenerate the lockfile.


------------------------------------------------------------------------


## Problem 5 --- Browser cannot connect to localhost

### Check the server terminal

Confirm that the terminal reports a successful startup and displays the
local URL.

Then check that the browser URL uses the same port.

For example:

``` text
http://localhost:3000
```

If `.env` was not loaded and the server fell back to port 3005, use:

``` text
http://localhost:3005
```

------------------------------------------------------------------------

## Problem 6 --- SQLite database cannot be opened

### Possible symptoms

``` text
Error opening database
```

or:

``` text
Database connection failure
```

### Check

1.  Confirm `sports_facility.db` exists.
2.  Confirm it is in the same directory as `server.js`.
3.  Confirm the user account running Node.js has read/write permission
    to the project directory.
4.  Confirm the database file is not locked by another process.
5.  Confirm the disk is not full.

On Windows, ensure the project is located somewhere the current user can
write to, such as a user-owned project directory rather than a protected
system directory.

------------------------------------------------------

## Problem 8 --- Login credentials do not work

### Check the database state first.

The development starter accounts are created only when the `users` table
is empty.

If `sports_facility.db` already contains accounts, the server does not
overwrite them with the development starter credentials.


Therefore, the following may not work against an already-populated
database:

``` text
admin / admin123

```

Use the credentials supplied with the evaluation database or the
administrator credentials configured during deployment.

### If this is a fresh development database

Ensure `.env` contains:

``` env
NODE_ENV=development
```

Then restart the application.

------------------------------------------------------------------------

## Problem 9 --- Password reset emails are not arriving

### Local testing

Use:

``` env
EMAIL_PROVIDER=mock
```

In mock mode, the email contents are written to the server terminal.

### Real email delivery

Configure:

``` env
EMAIL_PROVIDER=smtp
SMTP_HOST=...
SMTP_PORT=587
SMTP_USER=...
SMTP_PASS=...
SMTP_FROM=...
```

Verify that:

-   SMTP hostname is correct.
-   SMTP port is correct.
-   SMTP credentials are correct.
-   The university/network firewall permits SMTP traffic.
-   The recipient account has a valid email address.

The server's email gateway supports both mock and SMTP modes.
fileciteturn0file6L1-L2

------------------------------------------------------------------------

## Problem 10 --- Changes to `.env` do not appear to work

Environment variables are read when the Node.js process starts.

After modifying `.env`:

1.  Stop the server with:

``` text
Ctrl + C
```

2.  Start it again:

``` bash
npm start
```

Then verify the configured port and behavior.


# 8. Basic Evaluation / Test Checklist

For university IT staff or evaluators, the following sequence provides a
straightforward smoke test.

### Environment

-   [ ] Node.js 24.x LTS installed.
-   [ ] `node -v` works.
-   [ ] `npm -v` works.
-   [ ] Project extracted successfully.
-   [ ] `npm install` completed successfully.
-   [ ] `.env` created.
-   [ ] `sports_facility.db` is present.

### Server

-   [ ] `npm start` launches without a fatal error.
-   [ ] Terminal reports the configured local port.
-   [ ] Browser can open the application.

### Authentication

-   [ ] Login screen is displayed.
-   [ ] Valid administrator credentials authenticate successfully.
-   [ ] Invalid credentials are rejected.
-   [ ] Helpdesk/non-admin access is restricted from administrator-only
    operations.

### Booking

-   [ ] Student can be identified using enrollment number.
-   [ ] Sport and court selections load.
-   [ ] Date/time validation works.
-   [ ] Booking can be created.
-   [ ] Active/future booking information is displayed.
-   [ ] Booking history can be reviewed.

### Administration

-   [ ] Admin panel is available to administrator accounts.
-   [ ] Sports/court administration works.
-   [ ] User/account administration works.
-   [ ] Student Master functionality can be tested where applicable.
-   [ ] Audit history is available.
-   [ ] Reports can be generated.

### Database

-   [ ] Booking data persists after restarting the server.
-   [ ] SQLite database remains accessible.
-   [ ] No external database server is required.

------------------------------------------------------------------------

# 9. Operational and Security Notes

The application is intended primarily for controlled university/local
deployment.

### Authentication

The backend maintains server-side sessions and expects authenticated API
requests to provide the issued `x-auth-token`. Session tokens are held
in memory and have a defined expiration period.


### Administrator Authorization

Administrator-only endpoints verify the authenticated user's role before
allowing privileged operations.

### Static File Exposure

Only the `public/` directory is intentionally exposed as static HTTP
content. This prevents sensitive project files such as the database,
environment file, and server source from being exposed as ordinary
static assets.

### Password Handling

Passwords are stored as bcrypt hashes rather than plaintext passwords.
The backend uses `bcryptjs` for password verification and password
hashing.

### Production Credentials

Never distribute real passwords, SMTP passwords, or other secrets
inside:

-   `README.md`
-   source code
-   screenshots
-   public repositories
-   the ZIP package unless specifically required and securely
    transferred

Use `.env` for local secrets and keep `.env` outside version control.

------------------------------------------------------------------------

# 10. Stopping the Application

To stop the local server, return to the terminal running Node.js and
press:

``` text
Ctrl + C
```

The browser page will no longer be available until the server is started
again.

To restart:

``` bash
npm start
```

------------------------------------------------------------------------

# 11. Quick Start --- Condensed Version

For an experienced evaluator, the complete deployment process can be
summarized as:

``` bash
# 1. Enter project directory
cd /path/to/Sports Slot Booking and Managment System

# 2. Verify Node.js
node -v
npm -v

# 3. Install dependencies
npm install

# 4. Create environment file
# Windows:
copy .env.example .env

# macOS/Linux:
cp .env.example .env

# 5. Review/edit .env

# 6. Start application
npm start
```

Then open:

``` text
http://localhost:3000
```

if:

``` env
PORT=3000
```

is configured.

------------------------------------------------------------------------



## 13. Technical Reference Summary

  Item                       Current Project Configuration
  -------------------------- -----------------------------------
  Application Name           Sports Facility Management System
  Institution Branding       Ahmedabad University
  Backend                    Node.js + Express.js
  Database                   SQLite3
  Database File              `sports_facility.db`
  Frontend                   HTML5 / CSS / JavaScript
  Node.js Requirement        **24.x LTS**
  Package Manager            npm
  Start Command              `npm start`
  Direct Start               `node server.js`
  `.env` Port Template       `3000`
  Server Fallback Port       `3005`
  Standard Local URL         `http://localhost:3000`
  Authentication             Server-side session token
  Password Hashing           bcryptjs
  Email                      Mock or SMTP via Nodemailer
  Spreadsheet Export         SheetJS / `xlsx`

------------------------------------------------------------------------

