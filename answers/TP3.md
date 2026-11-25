# TP3 – Answers

## Exercise 1

**Question 1.** I get the message "The selected status is invalid." The rule
`Rule::in(Ticket::STATUSES)` only accepts waiting, helping and done, so the request
is refused and the status does not change.

## Exercise 2

**Question 2.** `select * from "tickets" where "status" = ? order by "id" asc`
The scope adds the condition on the status and the sorting by id. The `?` is
replaced by the value 'waiting' when the query runs (it is a bound parameter).

## Exercise 3

**Question 3.** 6 people are ahead of me. This matches the Waiting section of the
queue: I am at position 7, so 6 people are before me.

## Exercise 4

**Question 4.** The badges now show JSON text like
`{"id":2,"name":"Laravel","created_at":"...","updated_at":"..."}`.
The `topic` column was removed, so `$ticket->topic` now calls the `topic()`
relationship and returns a `Topic` object. When Blade prints a whole model with
`{{ }}`, Laravel converts it to JSON.

## Exercise 5

**Question 5.** I get "The selected topic id is invalid." It comes from the rule
`exists:topics,id`: there is no topic with the id 99 in the topics table.

## Exercise 6

**Question 6.** The topic database has 2 tickets.

## Exercise 7

**Question 7.** The list contains 9 items (the waiting tickets). The topic object
of each item contains `id`, `name`, `created_at` and `updated_at`. A mobile app,
a JavaScript front-end, a display screen in the classroom or a Python script could
use this data.

## Exercise 8
**Question 8.** I did not have a neighbour to swap with, so I tested my own README:
I cloned my repository into a new folder (neighbour-queue) and followed the README
step by step. The project started correctly and showed the queue with 8 tickets.

## Final questions

**1.** `Ticket::waiting()` calls the scope `scopeWaiting`: it adds
`where status = 'waiting'` and `order by id` to the query. A scope is better than
repeating the `where` because the rule is written once, it has a clear name, it can
be combined with other methods (`Ticket::with('topic')->waiting()`), and if the
rule changes, I only change it in one place.

**2.** The `tickets` table holds `topic_id`. A ticket belongs to exactly one topic,
so it needs only one value. A topic has many tickets: it could not store a list
of ticket ids in a single column. The foreign key always goes on the "many" side.

**3.** Any program that can read JSON over HTTP: a mobile app, a JavaScript
front-end (Vue, React), another server, a display screen, a Python script, or
tools like Postman or curl.