# Migrations Plan — Rent A Car System

Migrations are managed with Knex.js. Run in the order listed. Each migration is a separate file in `demo-backend/src/migrations/`.

---

## Migration sequence

| # | Filename | Description |
|---|---|---|
| 001 | `20260618_001_create_categories.js` | Create `categories` table |
| 002 | `20260618_002_create_locations.js` | Create `locations` table |
| 003 | `20260618_003_create_vehicles.js` | Create `vehicles` table with FK to categories |
| 004 | `20260618_004_create_media.js` | Create `media` table with FK to vehicles |
| 005 | `20260618_005_create_customers.js` | Create `customers` table |
| 006 | `20260618_006_create_reservations.js` | Create `reservations` table with FKs |
| 007 | `20260618_007_create_admins.js` | Create `admins` table |
| 008 | `20260618_008_seed_categories.js` | Seed default vehicle categories |
| 009 | `20260618_009_seed_locations.js` | Seed default branch locations |
| 010 | `20260618_010_seed_admin.js` | Seed default admin user |

---

## Migration 001 — categories

```js
exports.up = (knex) =>
  knex.schema.createTable('categories', (t) => {
    t.increments('id').primary();
    t.string('name', 100).notNullable().unique();
    t.string('slug', 100).notNullable().unique();
    t.string('image_url', 500).nullable();
    t.timestamps(true, true);
  });

exports.down = (knex) => knex.schema.dropTable('categories');
```

---

## Migration 002 — locations

```js
exports.up = (knex) =>
  knex.schema.createTable('locations', (t) => {
    t.increments('id').primary();
    t.string('name', 200).notNullable();
    t.text('address').notNullable();
    t.string('city', 100).notNullable();
    t.string('phone', 30).nullable();
    t.decimal('latitude', 10, 8).nullable();
    t.decimal('longitude', 11, 8).nullable();
    t.boolean('is_active').notNullable().defaultTo(true);
    t.timestamps(true, true);
  });

exports.down = (knex) => knex.schema.dropTable('locations');
```

---

## Migration 003 — vehicles

```js
exports.up = (knex) =>
  knex.schema.createTable('vehicles', (t) => {
    t.increments('id').primary();
    t.integer('category_id').unsigned().notNullable()
      .references('id').inTable('categories');
    t.string('name', 200).notNullable();
    t.string('slug', 200).notNullable().unique();
    t.text('description').nullable();
    t.decimal('daily_price', 10, 2).notNullable();
    t.string('fuel_type', 50).notNullable();
    t.string('transmission', 50).notNullable();
    t.integer('seat_count').notNullable();
    t.integer('year').nullable();
    t.string('status', 50).notNullable().defaultTo('available');
    t.timestamps(true, true);
  });

exports.down = (knex) => knex.schema.dropTable('vehicles');
```

---

## Migration 004 — media

```js
exports.up = (knex) =>
  knex.schema.createTable('media', (t) => {
    t.increments('id').primary();
    t.integer('vehicle_id').unsigned().notNullable()
      .references('id').inTable('vehicles').onDelete('CASCADE');
    t.string('filename', 500).notNullable();
    t.string('original_name', 500).nullable();
    t.string('mime_type', 100).notNullable();
    t.integer('size_bytes').nullable();
    t.integer('display_order').notNullable().defaultTo(0);
    t.timestamp('created_at').notNullable().defaultTo(knex.fn.now());
  });

exports.down = (knex) => knex.schema.dropTable('media');
```

---

## Migration 005 — customers

```js
exports.up = (knex) =>
  knex.schema.createTable('customers', (t) => {
    t.increments('id').primary();
    t.string('first_name', 100).notNullable();
    t.string('last_name', 100).notNullable();
    t.string('email', 200).notNullable();
    t.string('phone', 30).notNullable();
    t.timestamp('created_at').notNullable().defaultTo(knex.fn.now());
  });

exports.down = (knex) => knex.schema.dropTable('customers');
```

---

## Migration 006 — reservations

```js
exports.up = (knex) =>
  knex.schema.createTable('reservations', (t) => {
    t.increments('id').primary();
    t.string('reference_number', 30).notNullable().unique();
    t.integer('customer_id').unsigned().notNullable()
      .references('id').inTable('customers');
    t.integer('vehicle_id').unsigned().notNullable()
      .references('id').inTable('vehicles');
    t.integer('pickup_location_id').unsigned().notNullable()
      .references('id').inTable('locations');
    t.integer('return_location_id').unsigned().notNullable()
      .references('id').inTable('locations');
    t.date('pickup_date').notNullable();
    t.date('return_date').notNullable();
    t.integer('rental_days').notNullable();
    t.decimal('daily_price_snapshot', 10, 2).notNullable();
    t.decimal('total_price', 10, 2).notNullable();
    t.string('status', 50).notNullable().defaultTo('pending');
    t.text('notes').nullable();
    t.text('admin_notes').nullable();
    t.timestamps(true, true);
  });

exports.down = (knex) => knex.schema.dropTable('reservations');
```

---

## Migration 007 — admins

```js
exports.up = (knex) =>
  knex.schema.createTable('admins', (t) => {
    t.increments('id').primary();
    t.string('username', 100).notNullable().unique();
    t.string('password_hash', 255).notNullable();
    t.timestamp('created_at').notNullable().defaultTo(knex.fn.now());
    t.timestamp('last_login_at').nullable();
  });

exports.down = (knex) => knex.schema.dropTable('admins');
```

---

## Running migrations

```bash
# Dev (SQLite)
npx knex migrate:latest

# Rollback one step
npx knex migrate:rollback

# Run seeds after migrations
npx knex seed:run
```
