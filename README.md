# firestoremodel.js
Simple Firestore Model concept

To use, just include it:
```
<script src="firestoremodel.js"></script>
```

Usage - Writing a model:
```
  db.collection("cities").doc("LA").set(firestoreModel.process(
    { // Document Data
       name: "Los Angeles",
       state: "CA",
       country: "USA",
       structure: 'Waſſerſchloß'
    },
    { // Field Options
       name: 'case_fold',
       country: ['case_fold', 'default_null'],
       structure: 'case_fold'
    },
    { // Document Options
       random: true,
       schema_version: 1
    })
  );
```

Usage - Getting a random document (sans no-result check):
```
  var museums = db.collectionGroup('landmarks');
  var randomId = firestoreModel.randomId();
  query = museums.where(firestoreModel.randomField(), '>=', randomId).limit(1);
  query.get().then(function (querySnapshot) {
    querySnapshot.forEach(function (doc) {
        console.log(doc.id, ' => ', doc.data());
    });
  });
```

Usage - Query caseless:
```
  var searchTerm = 'Waſſerſchloß';
  var museums = db.collectionGroup('landmarks');
  query = museums.where(firestoreModel.caselessField('name'), '==', firestoreModel.removeCase(searchTerm));
  query.get().then(function (querySnapshot) {
    querySnapshot.forEach(function (doc) {
        console.log(doc.id, ' => ', doc.data());
    });
  });
```

Credits: Thanks to [@mathias](https://twitter.com/mathias) for helping with case folding in JavaScript.
