# ALX Travel App 0x00

A Django REST API for a travel listing platform allowing hosts to create listings, guests to make bookings, and users to leave reviews.

---

## Table of Contents

* [Project Overview](#project-overview)
* [Features](#features)
* [Tech Stack](#tech-stack)
* [Setup and Installation](#setup-and-installation)
* [Database Models](#database-models)
* [API Endpoints](#api-endpoints)
* [Seeding the Database](#seeding-the-database)
* [Running the Development Server](#running-the-development-server)
* [Authentication](#authentication)
* [License](#license)

---

## Project Overview

This project is a backend API built with Django and Django REST Framework to support a travel booking platform. It manages listings, bookings, and reviews with relational data models and provides a JWT-secured API.

---

## Features

* Hosts can create and manage travel listings.
* Guests can book listings for selected dates.
* Users can post reviews for listings.
* JWT and session authentication support.
* API browsable via DRF's web interface.
* Database seeding command to populate with sample data.

---

## Tech Stack

* Python 3.12
* Django 5.2
* Django REST Framework 3.16
* Simple JWT for authentication
* PostgreSQL (recommended)
* SQLite (for development/testing)

---

## Setup and Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/yourusername/alx_travel_app_0x00.git
   cd alx_travel_app_0x00
   ```

2. **Create and activate a virtual environment**

   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/macOS
   venv\Scripts\activate     # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Apply migrations**

   ```bash
   python manage.py migrate
   ```

5. **Create a superuser (optional, for admin access)**

   ```bash
   python manage.py createsuperuser
   ```

6. **Seed the database with sample data**

   ```bash
   python manage.py seed
   ```

7. **Run the development server**

   ```bash
   python manage.py runserver
   ```

---

## Database Models

### Listing

* **Fields**:

  * `listing_id`: UUID primary key
  * `title`: Name of the listing
  * `description`: Text describing the listing
  * `location`: Location of the property
  * `price_per_night`: Price per night (decimal)
  * `host`: ForeignKey to User model
  * `created_at`, `updated_at`: Timestamps

### Booking

* **Fields**:

  * `booking_id`: UUID primary key
  * `listing`: ForeignKey to Listing
  * `guest`: ForeignKey to User
  * `start_date`: Date of booking start
  * `end_date`: Date of booking end
  * `total_price`: Calculated total price
  * `status`: Enum ('pending', 'confirmed', 'canceled')
  * `created_at`: Timestamp

### Review

* **Fields**:

  * `review_id`: UUID primary key
  * `listing`: ForeignKey to Listing
  * `reviewer`: ForeignKey to User
  * `rating`: Integer rating (1-5)
  * `comment`: Review text
  * `created_at`: Timestamp

---

## API Endpoints

| Method | Endpoint              | Description                 |
| ------ | --------------------- | --------------------------- |
| GET    | `/api/listings/`      | List all listings           |
| POST   | `/api/listings/`      | Create a new listing        |
| GET    | `/api/listings/{id}/` | Retrieve a specific listing |
| PUT    | `/api/listings/{id}/` | Update a listing            |
| DELETE | `/api/listings/{id}/` | Delete a listing            |

| Method | Endpoint              | Description                 |
| ------ | --------------------- | --------------------------- |
| GET    | `/api/bookings/`      | List all bookings           |
| POST   | `/api/bookings/`      | Create a new booking        |
| GET    | `/api/bookings/{id}/` | Retrieve a specific booking |

| Method | Endpoint             | Description                |
| ------ | -------------------- | -------------------------- |
| GET    | `/api/reviews/`      | List all reviews           |
| POST   | `/api/reviews/`      | Create a new review        |
| GET    | `/api/reviews/{id}/` | Retrieve a specific review |

---

## Seeding the Database

A custom Django management command `seed` is implemented to populate the database with sample listings, bookings, and reviews.

Run:

```bash
python manage.py seed
```

This will create sample users (if not present), listings, bookings, and reviews with preset data.

---

## Running the Development Server

Start the server using:

```bash
python manage.py runserver
```

Open your browser and visit [http://localhost:8000/api/](http://localhost:8000/api/) to explore the browsable API interface.

---

## Authentication

* JWT token authentication is enabled.
* Obtain a token with:
  `POST /api/token/` (send username and password)
* Refresh token with:
  `POST /api/token/refresh/`

