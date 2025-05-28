# Bitespeed Identity Reconciliation Service

This project implements an Identity Reconciliation service for the Bitespeed Backend Task. Its purpose is to recognize and manage a customer's identity across multiple e-commerce purchases. The service organizes and merges customer contact details, establishing connections between related entries and maintaining a primary–secondary relationship among them.

## Features

- Detects and associates customer contacts using email and phone number
- Manages a primary-secondary structure for related contact entries
- Offers a RESTful API endpoint to handle identity reconciliation
- Utilizes PostgreSQL to store and manage contact data

## Hosted URL for testing

```
https://bitespeed-identity-reconciliation-70dr.onrender.com
```

## Tech Stack

- Node.js
- Express.js
- PostgreSQL
- pg (node-postgres) for database interactions

## Working

1. Install dependencies npm.

2. Set up your PostgreSQL database and create a `.env` file in the root directory.

3. Start the server:

The server will start on `http://localhost:3000` (or the port specified in your .env file).

## API

The service exposes a single endpoint:

```
POST /api/identify
```

Request body:

```json
{
	"email": "ankit.edu",
	"phoneNumber": 4567
}

```

Response body:

```json
{
    "contact": {
        "primaryContactId": 6,
        "emails": [
            "ankit.edu",
            "null"
        ],
        "phoneNumbers": [
            "1234",
            "4567"
        ],
        "secondaryContactIds": [
            7,
            9,
            10
        ]
    }
}
```

# How It Works

When the service receives a request, it first looks for an existing primary contact that matches the provided email or phone number.

If no matching primary contact is found, it creates a new primary contact entry.

If a primary contact is found:

      It checks for any secondary contacts already linked to it.

      If a secondary contact exists but has different data, it updates that contact.

      If no secondary contact exists but the new data differs from the primary, it adds a new secondary contact.

Finally, the service gathers all related contacts—both primary and secondary—and returns the merged, unified contact information.
