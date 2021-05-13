# REACT APP WITH FIREBASE AUTH

Template for connecting a React app to Firebase Authentication, and saving active user to Firestore.


## Installation

```bash
git clone git@github.com:leoevents/react-fb-auth-template.git
cd react-fb-auth-template
```

```bash
npm install
npm install --save reactstrap react-bootstrap react-router-dom
npm install firebase
```

```bash
firebase init functions
    > Use existing project (select project)
    > JavaScript
    ESLint > No
    Overwrite package.json > No
    Overwrite index.js > No
    Overwrite .gitignore > No
    Install dependencies > Yes
firebase deploy --only functions
```


## Firebase Setup

1. Create new project in the Firebase console
2. Authentication > Get Started > Enable Email/Password
3. ⚙️ > Project Settings >\
        Copy API Key from Project Settings and paste into .env.local file in root folder:\
        REACT_APP_API_KEY=yourapikeyhere\
        > **NOTE:** You may have to restart local server before the app will read your .env.local file
4. Update Firebase project name in:\
        - .firebaserc\
        - package-lock.json\
        - package.json\
        - UserProfileProvider.js (functionsApiUrl)
5. Firestore Database > Create Database > Start in production mode > Enable
6. Firestore Database > Rules :
        ```bash
        service cloud.firestore {
            match /databases/{database}/documents {
                match /{document=**} {
                allow read, write: if request.auth != null;
                }
            }
        }
        ```
7. Firestore Database > Create Collection > "users" > *create fake user*
8. Upgrade to Blaze plan