# CoffeeTime v3 Firebase Stability Update

This version changes CoffeeTime's Firebase writes so missing Firestore documents are created automatically instead of causing `not-found` errors.

Changes:
- Socialization checklist saves reliably on first use.
- Updates now use safe merge writes.
- Socialization defaults are automatically initialized in Firestore.
- Bucket List defaults are initialized if missing.

Recommended temporary Firestore rules during first setup:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

After your Family list is set up, you can switch to stricter Family-only rules from the Family section in the app.
