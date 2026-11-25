# TP2 – Answers

## Exercise 1

**Question 1.** No, the names are different each time. `migrate:fresh` deletes
all the data, then the seeder creates 8 new tickets with the factory. The factory
uses `fake()`, which generates random values (names, topics, sentences) on every run.

## Exercise 2

**Question 2.** I get a 404 (Not Found) page. The ticket is looked up automatically 
by route model binding: because the route has `{ticket}` and the `show` method
has the parameter `Ticket $ticket`, Laravel searches for the ticket with id 999 in
the database. It does not exist, so Laravel answers 404.

## Exercise 3

**Question 3.** I get a 404. Routes are checked from top to bottom: `/tickets/create`
first matched the route `/tickets/{ticket}`, with `{ticket} = "create"`. Laravel
looked for a ticket with the id "create", did not find one, and answered 404.
The `create` route below was never reached.

## Exercise 4

**Question 4.** Without `@csrf` I got the error 419 (Page Expired). The token
protects against CSRF attacks (Cross-Site Request Forgery): another website
trying to submit a form to our application using the visitor's browser and session.
Laravel refuses every POST/DELETE request that does not contain the right token.
## Exercise 5

Messages shown:
1. Empty form: "The name field is required." and "The topic field is required."
2. Name without topic: "The topic field is required."
3. Topic changed to Cooking: "The selected topic is invalid."

**Question 5.** The name I typed is still in the field. This is because of
`value="{{ old('name') }}"` in the view: when validation fails, Laravel sends
the user back to the form with the old values, and `old()` puts them back.

**Question 6.** Anything in the browser can be changed by the user (developer
tools, or sending the request directly with another tool). The limits of the form
are only there for comfort; they are not a protection. Only the server is under
our control, so validation must run there (`Rule::in(Ticket::TOPICS)`) to make
sure no invalid data reaches the database.

## Exercise 6

**Question 7.** The delete form contains two hidden fields:
- `_token`: the CSRF token (added by `@csrf`), proves the form comes from our site;
- `_method` with the value `DELETE` (added by `@method('DELETE')`): HTML forms
  can only send GET or POST, so Laravel reads this field to treat the request as
  DELETE and match the `Route::delete` route.

## Exercise 7

**7.1 – route:list before Route::resource:**


  GET|HEAD   tickets .......................................................... tickets.index › TicketController@index
  POST       tickets .......................................................... tickets.store › TicketController@store
  GET|HEAD   tickets/create ................................................. tickets.create › TicketController@create
  GET|HEAD   tickets/{ticket} ................................................... tickets.show › TicketController@show
  DELETE     tickets/{ticket} ............................................. tickets.destroy › TicketController@destroy


**Question 8.** The result is the same: the same 5 routes, with the same URLs,
HTTP methods, names (`tickets.index`, `tickets.show`...) and controller methods.
Only the code changed: one line instead of five. `Route::resource` works without
other changes because my controller follows Laravel's conventions: the methods are
named `index`, `create`, `store`, `show` and `destroy`, and the parameter
`{ticket}` matches `Ticket $ticket`. `only([...])` keeps only the 5 actions
I wrote (no edit/update).

## Final questions

**1.** Because the route `/tickets/{ticket}` was above it. Routes are checked from
top to bottom, so "create" was taken as a ticket id; no ticket has this id, so
model binding answered 404.

**2.** `@csrf` protects against CSRF attacks (another website sending forms to our
application in the user's name). Without it, Laravel answers 419 Page Expired.

**3.** Because the user can modify the HTML or send a request without using the form
at all. The form's limits are only for comfort; only the server can really check
the data before saving it to the database.