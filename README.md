# newfin overall vision

Personal Finance App: A Phased Roadmap
This revised roadmap prioritizes visible, engaging features first to maintain momentum. We'll build independent services, but we're deliberately pushing foundational work like authentication to a later phase.

Phase 1: The Anonymous Ledger
Goal: An ultra-simple, single-user app to track expenses. No logins, no accounts, just pure functionality.

Service 1: Transactions Service (.NET)

Purpose: To manage a single list of financial entries.

Features:

Endpoint to POST a new transaction.

Endpoint to GET all transactions.

Endpoint to DELETE a transaction.

Key Detail: This service is "dumb" about users. It assumes there's only one user of the app for now.

Frontend App (React)

Features:

A single page. No login screen.

A form to submit an expense or income.

A list displaying all transactions.

By the end of Phase 1, you have a working tool for yourself. It's an immediate win.

Phase 2: The IPO Scraper
Goal: To pull in external data and display it. This is a completely separate feature that provides immediate value.

Service 2: External Data Service (.NET)

Purpose: To fetch data from the internet.

Features:

A web scraper (using a library like HtmlAgilityPack or Playwright) to check a specific website for IPO news. This will run on a schedule (e.g., once a day).

An endpoint that the frontend can call to get the latest list of scraped IPOs.

Outcome: A standalone service that populates a database table with IPO information.

Frontend App (React)

Features:

A new "IPO Watch" page.

This page fetches and displays the data from the External Data Service in a simple table.

By the end of Phase 2, you have two distinct, useful features.

Phase 3: The "Boring But Necessary" Refactor - Adding Identity
Goal: To introduce user accounts and secure your application. This involves going back and adding the authentication you skipped.

Service 3: Authentication Service (.NET)

Purpose: The original user registration and login service.

Features: Endpoints for /register and /login that return a JWT token.

Enhance: Transactions Service (.NET)

The Refactor:

Add a UserId column to your transactions table.

Secure all endpoints. They should now require a valid JWT token and only return data matching the user's ID.

You'll need a one-time script to assign all the "anonymous" transactions from Phase 1 to your new user account.

Frontend App (React)

Features:

Implement the login page you skipped.

Store the auth token after login.

Update all API calls to the Transactions Service to include the token in the header.

Phase 4 & Beyond: The Rest of the Features
Now that you have the core foundation (transactions and users), you can proceed with the other features in a logical order.

Phase 4: Automation: Build the recurring expenses/bills functionality on top of the now-authenticated Transactions Service.

Phase 5: The Investor: Build the Investment Service to track stocks, which will be tied to a UserId.

Phase 6: The Big Picture: Build the Dashboard and Analytics Service, which will pull data from all your other authenticated services.

An Opposing View: You're Just Creating Work for Your Future Self
Look, let's be honest. The professional, "correct" way to do this is to build the foundation first. By skipping authentication, you're building a house on sand.

Technical Debt: Every feature you build before Phase 3 will need to be refactored to understand the concept of a "user." This means going back and changing code you thought was "done," which is always more complex and bug-prone than doing it right the first time.

Security as an Afterthought: Bolting on security later is a terrible habit. It's how vulnerabilities are born. Building with security in mind from day one (UserId in every table, endpoints secured by default) leads to a much more robust application.

This new roadmap is optimized for your motivation, not for sound engineering principles. It's a valid trade-off for a personal project, but you need to be aware that you are deliberately choosing the path that creates more cleanup work down the line. The original roadmap was technically superior, even if it was less exciting.