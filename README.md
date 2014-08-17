# Ember Data PouchDB Adapter

Ember Data adapter for PouchDB/CouchDB.

**Work in progress! Do not use or your computer might explode!**

```js
var YOUR_COMPUTER_WILL_EXPLODE = "maybe";
```

## Build

    $ npm run build

## Installation

Download the `dist/` files you want, or install from Bower:

    $ bower install ember-pouch

Or from npm:

    $ npm install ember-pouch

Now that you have the `dist/` files locally, to use in your app, you just include
in your Brocfile:

```js
app.import('vendor/ember-pouch/dist/globals/main.js');
```

## Usage

Next, you need to add a `rev` field to all of your Models. This is used by PouchDB/CouchDB
to manage revisions:

```js
var Todo = DS.Model.extend({
  title: DS.attr('string'),
  isCompleted: DS.attr('boolean'),
  rev: DS.attr('string') // <-- ADD THIS TO EVERY MODEL
});
```

Then, in your application, extend `EmberPouch.Adapter` and set your `PouchDB`.
(PouchDB is imported automatically.)

```js
export default EmberPouch.Adapter.extend({
  db: new PouchDB('mydb')
});
```

If you're not familiar with PouchDB, here are some of the different ways you can use it:

**As a direct client to CouchDB**:

```
export default EmberPouch.Adapter.extend({
  db: new PouchDB('mydb')
});
```

**As a direct client to CouchDB**:

```
export default EmberPouch.Adapter.extend({
  db: new PouchDB('http://localhost:5984/mydb')
});
```

**As a local database that syncs with CouchDB**:

```
var db = new PouchDB('http://localhost:5984/ember-todo');
db.sync('http://localhost:5984/mydb', {live: true});
export default EmberPouch.Adapter.extend({
  db: db
});
```

For more info, see the official PouchDB documentation at [PouchDB.com](http://pouchdb.com).