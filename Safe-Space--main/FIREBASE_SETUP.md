# Firebase Setup Guide for Private Chat

## Step 1: Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Click "Create a new project" or use existing one
3. Name it (e.g., "Safe-Space")
4. Disable Google Analytics (optional)
5. Click "Create Project"

## Step 2: Enable Realtime Database

1. In Firebase Console, go to **Build** → **Realtime Database**
2. Click **Create Database**
3. Choose **Start in test mode** (for development)
4. Select a region close to you
5. Click **Enable**

## Step 3: Get Firebase Config

1. In Firebase Console, click the gear icon (Settings) → **Project Settings**
2. Scroll down to "Your apps" section
3. Click on the `</>` (web) icon to add a web app
4. Register the app (name it "Safe-Space-Chat" or similar)
5. Copy the Firebase config object

Your config should look like:
```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project-default-rtdb.firebaseio.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "...",
  appId: "1:...:web:..."
};
```

## Step 4: Add Config to private-chat.html

In the `private-chat.html` file, replace the `firebaseConfig` variable with your actual credentials (around line 240).

## Step 5: Set Database Rules (Security)

1. Go to **Realtime Database** → **Rules** tab
2. Replace with these rules to auto-delete messages after 5 minutes:

```json
{
  "rules": {
    "chats": {
      "$roomKey": {
        ".read": true,
        ".write": true,
        "$messageId": {
          ".validate": "newData.hasChildren(['id', 'time']) && newData.child('time').val() > now - 300000"
        }
      }
    }
  }
}
```

3. Click **Publish**

## Step 6: Test It Out

1. Open `private-chat.html` in your browser
2. Click "Generate Secure Chat Link"
3. Copy the link and open it in **another browser tab or device**
4. Send a message from the first tab
5. You should see it appear in the second tab **instantly**!

---

## Troubleshooting

**Messages not syncing?**
- Check browser console (F12) for Firebase errors
- Verify your `databaseURL` is correct
- Check Firebase Database Rules allow read/write

**Link not working?**
- Make sure you have the `#key=...` in the URL
- Check that the room key is being generated properly

**Images not showing?**
- Images are encrypted - they should decrypt and display automatically
- Check browser console for decryption errors
