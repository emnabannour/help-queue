# TP1 – Answers

 ## Exercise 1

**Question 1.** `.env` contains settings specific to each computer, and secrets
like the `APP_KEY` and database passwords, so it must never be published.
`vendor/` contains the packages downloaded by Composer: it is very large and can
be rebuilt at any time with `composer install` (from `composer.json` / `composer.lock`).

## Exercise 2

- `routes/web.php`: `Route::get('/', function () { return view('welcome'); });`
- `.env`: `DB_CONNECTION=sqlite`
- `database/migrations/`: 3 migrations (users, cache, jobs)
- `app/Models/User.php`: Fillable fields are `name`, `email`, `password`

## Exercise 3

**Question 2.** Error 404 (Not Found), because no route is defined for `/helo`.
Laravel only answers the addresses declared in `routes/web.php`.

## Exercise 4

**Question 3.** `{name}` only matches one segment of the URL (it cannot contain `/`).
`/hello/a/b` has two segments after `/hello`, so no route matches and we get a 404.

## Exercise 5

**Question 4.** The page shows the text `<marquee>Bob` as plain text: the HTML tag
is not executed. `{{ }}` escapes special HTML characters, which protects the page
against code injection (XSS attacks).

## Exercise 7

**Question 5.** The table has 7 columns: id, name, topic, description, status,
created_at and updated_at. I did not write `created_at` and `updated_at`
myself: they were created by the line `$table->timestamps();`.

## Exercise 8

**Question 6.** `Illuminate\Database\Eloquent\MassAssignmentException: Add [name] to fillable property to allow mass assignment on [App\Models\Ticket].`

## Exercise 9

**Question 7.** My ticket is number 4, because the controller sorts tickets by
`created_at` (oldest first) and mine was created last. `$loop->iteration`
numbers them starting from 1.

## Final questions

**1.** `public/index.php` (entry point) → `routes/web.php` (finds the `/tickets` route)
→ `app/Http/Controllers/TicketController.php` (method `index`)
→ `app/Models/Ticket.php` (reads the tickets from the SQLite database)
→ `resources/views/tickets/index.blade.php`, which extends
`resources/views/layouts/app.blade.php` → the HTML page is sent to the browser.

**2.** A migration describes the structure of a table in code. It is saved in Git,
so every computer can recreate exactly the same database with
`php artisan migrate` (this is what I did when I moved my project to another PC).
A table created by hand is not versioned, cannot be shared and is easy to get wrong.

**3.** By default, Eloquent blocks "mass assignment" (filling several fields at once with `create([...])`) for security: it prevents a user from sending fields they should not change (for example `status`). Only the fields listed in `$fillable`
are allowed.