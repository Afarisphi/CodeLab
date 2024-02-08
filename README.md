# Codelab Documentation

# Set up

Get the code

```
# clone repository
git clone https://github.com/Afarisphi/CodeLab.git

# Change directory
cd CodeLab

# Move into the functions directory
cd functions

# Install dependencies
npm install

# Move back into the previous directory
cd ../
```

Get the Firebase CLI
The Emulator Suite is part of the Firebase CLI (command-line interface) which can be installed on your machine with the following command:

```
npm install -g firebase-tools
```
Next, could you confirm that you have the latest version of the CLI? This code lab should work with version 9.0.0 or higher but later versions include more bug fixes.

```
firebase --version
```

Connect to your Firebase project

Now we need to connect this code to your Firebase project. First, run the following command to log in to the Firebase CLI:
```
firebase login
```

Next, run the following command to create a project alias. Replace $YOUR_PROJECT_ID with the ID of your Firebase project.
```
firebase use $YOUR_PROJECT_ID
```
Next on functions/test.js, find the REAL_FIREBASE_PROJECT_ID variable at the top of the file and change it to your real Firebase Project ID.:
```
// CHANGE THIS LINE
const REAL_FIREBASE_PROJECT_ID = "xxx";
```


Start the Emulators
From inside the code lab source directory, run the following command to start the emulators:

```
firebase emulators:start --import=./seed
```

You should see some output like this:

```
$ firebase emulators:start --import=./seed
i  emulators: Starting emulators: auth, functions, firestore, hosting
⚠  functions: The following emulators are not running, calls to these services from the Functions emulator will affect production: database, pubsub
i  firestore: Importing data from /Users/samstern/Projects/emulators-codelab/codelab-initial-state/seed/firestore_export/firestore_export.overall_export_metadata
i  firestore: Firestore Emulator logging to firestore-debug.log
i  hosting: Serving hosting files from: public
✔  hosting: Local server: http://127.0.0.1:5000
i  ui: Emulator UI logging to ui-debug.log
i  functions: Watching "/Users/samstern/Projects/emulators-codelab/codelab-initial-state/functions" for Cloud Functions...
✔  functions[calculateCart]: firestore function initialized.

┌─────────────────────────────────────────────────────────────┐
│ ✔  All emulators ready! It is now safe to connect your app. │
│ i  View Emulator UI at http://127.0.0.1:4000                │
└─────────────────────────────────────────────────────────────┘

┌────────────────┬────────────────┬─────────────────────────────────┐
│ Emulator       │ Host:Port      │ View in Emulator UI             │
├────────────────┼────────────────┼─────────────────────────────────┤
│ Authentication │ 127.0.0.1:9099 │ http://127.0.0.1:4000/auth      │
├────────────────┼────────────────┼─────────────────────────────────┤
│ Functions      │ 127.0.0.1:5001 │ http://127.0.0.1:4000/functions │
├────────────────┼────────────────┼─────────────────────────────────┤
│ Firestore      │ 127.0.0.1:8080 │ http://127.0.0.1:4000/firestore │
├────────────────┼────────────────┼─────────────────────────────────┤
│ Hosting        │ 127.0.0.1:5000 │ n/a                             │
└────────────────┴────────────────┴─────────────────────────────────┘
  Emulator Hub running at 127.0.0.1:4400
  Other reserved ports: 4500

Issues? Report them at https://github.com/firebase/firebase-tools/issues and attach the *-debug.log files.
```

Open the EmulatorUI
In your web browser, navigate to http://127.0.0.1:4000/. You should see the Emulator Suite UI.

Open the app
In your web browser, navigate to http://127.0.0.1:5000 and you should see The Fire Store running locally on your machine!

Run the tests
On the command line in a new terminal tab from the directory emulators-codelab/codelab-initial-state/

First move into the functions directory (we'll stay here for the remainder of the codelab):

```
cd functions
```

Now run the mocha tests in the functions directory, and scroll to the top of the output:

```
# Run the tests
$ npm test

> functions@ test .../emulators-codelab/codelab-initial-state/functions
> mocha

  shopping carts
    √ can be created and updated by the cart owner (145ms)
    √ can be read only by the cart owner (286ms)
    √ can be read only by the cart owner
    1) "after all" hook for "can be read only by the cart owner"

  shopping cart items
    √ can be read only by the cart owner (67ms)
    √ can be added only by the cart owner
    2) "after all" hook for "can be added only by the cart owner"

  adding an item to the cart recalculates the cart total.
    √ should sum the cost of their items (1568ms)
    3) "after all" hook for "should sum the cost of their items"


  6 passing (17s)
  3 failing
```
