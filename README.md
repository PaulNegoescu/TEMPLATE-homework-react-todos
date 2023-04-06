# Homework - React Todos from Server

## Install

Open the folder inside VSCode, open the terminal and type `npm i` and hit enter

## Run

To start the React dev server in the terminal: `npm run dev`

In a separate terminal window, to start the data server (mock backend): `npm run server`

## Requirements

### Basic

Implement a simple Todos app.

The app should display the list of todos from the server inside a list.

Each Todo should be represented by a checkbox showing wheather the todo is "completed" or not, a label that contains the "title", and a delete button. No need for any functionality beside display logic.

Create and "Add Todo" form that has a label and and input for the title and a button to create a new Todo. No need for functionality beside display logic.

### Extra

1. When clicking the delete button the Todo item should be deleted from the DB and the list to the user should be updated
2. When clicking the button in the form or hitting enter when typing in the input field add a new todo item to the DB and make sure the list is updated for the user with the new Todo.
3. When clicking the label or input, update the completed property of the todo item involved in the DB
4. Add css that does the following:
   a. When the item is completed (checkbox is checked) the title is striked through
   b. There are no bullets in the list
   c. The button looks like an x in a circle (use &amp;times; for the symbol)

## Hints and tips

1. Don't forget to start the mock server before making requests to it!!!
2. There is a generalized way to treat the add functionality that does not involve listening for two disparate events (enter key and click). Remember that you are in the context of a form.
3. The API, after a successfult POST request, will send back data with the response, containing the freshly created entity.
4. You can add items to an array with push and remove items with splice but remember that these functions perform mutations, the reference of the array won't change.
5. For removing items in a way that does not mutate arrays consider using .filter
6. fetch accepts a second argument with a config object where you can specify a method for the call, headers, and a body

## The API

The API is a pretty standard RESTful API.

All the data is in the db.json file. Every property in the object inside of that is an entity type and a resource for the API (you get a url to it). Each property holds an array of items with ids.

The server performs no validations at all, take care what data you send to it as it will ingest any junk.

You have a `/todos` resource at your disposal on `http://localhost:3000`. It supports all REST requests:

- `GET /todos`: List of all todos (array of objects)
- `POST /todos`: Create a new todo, requires a body with the todo to be created in either the json format, the x-www-form-urlencoded format, or the FormData format
- `GET /todos/:id`: Retrieve one todo with the ID of ":id" (object)
- `PUT /todos/:id`: Idempotent update (need to send the whole body of the todo) of a todo with an id of ":id"
- `PATCH /todos/:id`: Non-idempotent update (you can send only the property(ies) being updated) of the todo with an id of ":id"
- `DELETE /todos/:id`: Deletes a todo with an id of ":id"

POST, PUT and PATCH requests respond with a body containing the affected todo item.

Ids are auto-generated when POSTing.

To tell the server what kind of data you are sending to it use headers. I recommend `application/json` or `application/x-www-form-urlencoded`. Make sure you encode your body in a way compatible with the header. For json use `JSON.stringify` or just format the string yourself. For the other one there is a more complex api or again you can format the string yourself something like `title=Test%20of%20adding&completed=false`. Because this second aproach is harder I recommend sticking with json.
