# MongoDB

## Setup

### Runs MongoDB inside docker and access it

This command tells [[Docker]] to run a **MongoDB container** with specific settings. It starts a **temporary MongoDB 4.4.1 container** named test-mongo, running in the background. The database becomes accessible on your machine at **localhost:27017**, which is MongoDB’s default port. When you stop the container, it’s **automatically removed**:

```bash
docker run --name test-mongo -dit -p 27017:27017 --rm mongo:4.4.1
```

Now, to **interact with MongoDB**, run the following command to enter the container and open the MongoDB shell:

```bash
docker exec -it test-mongo mongo
```

### Populate data

```javascript
show dbs

use adoption

db.pets.insertOne({ name: "Shoyu", type: "dog", breed: "n/a", age: "10"})


db.pets.insertMany(
  Array.from({ length: 10000 }).map((_, index) => ({
    name: [
      "Luna",
      "Fido",
      "Fluffy",
      "Carina",
      "Spot",
      "Beethoven",
      "Baxter",
      "Dug",
      "Zero",
      "Santa's Little Helper",
      "Snoopy",
    ][index % 9],
    type: ["dog", "cat", "bird", "reptile"][index % 4],
    age: (index % 18) + 1,
    breed: [
      "Havanese",
      "Bichon Frise",
      "Beagle",
      "Cockatoo",
      "African Gray",
      "Tabby",
      "Iguana",
    ][index % 7],
    index: index,
  }))
);
```

### Create a index

```javascript
db.pets.createIndex({ name: 1 });

db.pets.createIndex({ index: 1 }, { unique: true });

db.pets.getIndexes();
```

## Running

At terminal run

```bash
node server.js
```

And use this URL to access the frontend of the application
`http://localhost:3000/index.html`

## Stop

To gracefully stop the Docker container, use the following command:

```bash
docker stop test-mongo
```
