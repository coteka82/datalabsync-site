# Firebase Firestore Setup Guide

## Overview

DataLabSync uses Firebase Firestore to store waitlist signups and quiz responses. This guide explains how to configure Firebase for your deployment.

---

## Step 1: Get Your Firebase Config

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your **DatalabSync** project
3. Click the gear icon → **Project settings**
4. Scroll to **Your apps** section
5. Click your Web App (or create one if needed)
6. Copy the `firebaseConfig` object

It looks like this:
```javascript
const firebaseConfig = {
    apiKey: "AIzaSyB...",
    authDomain: "datalabsync.firebaseapp.com",
    projectId: "datalabsync",
    storageBucket: "datalabsync.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123"
};
```

---

## Step 2: Update Your Code

### In `index.html` (around line 2095)

Find this block:
```javascript
// TODO: Replace with your actual Firebase config
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    ...
};
```

Replace with your actual config values.

### In `onboarding.html` (around line 1155)

Find the same block and replace with your actual config values.

---

## Step 3: Configure Firestore Security Rules

In Firebase Console → Firestore → Rules, set:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    
    // Waitlist collection - allow writes from web, reads only from admin
    match /waitlist/{document} {
      allow create: if true;  // Anyone can sign up
      allow read, update, delete: if false;  // Only via Admin SDK
    }
    
    // Quiz responses - allow writes from web, reads only from admin
    match /quiz_responses/{document} {
      allow create: if true;  // Anyone can submit quiz
      allow read, update, delete: if false;  // Only via Admin SDK
    }
  }
}
```

**Note:** For production, consider adding rate limiting via Firebase App Check.

---

## Step 4: Verify Firestore Collections

Your Firestore should have these collections:

### `waitlist`
| Field | Type | Description |
|-------|------|-------------|
| email | string | User's email address |
| createdAt | timestamp | Server timestamp |
| source | string | Page path where signup occurred |
| userAgent | string | Browser info |
| referrer | string | Referral source |
| quizCompleted | boolean | Whether quiz was completed |
| quizResponseId | string | Reference to quiz_responses doc |
| role | string | User's role (from quiz) |
| engagementPreference | string | How user wants to engage |
| pricingWillingness | string | Pricing range selected |
| updatedAt | timestamp | Last update time |

### `quiz_responses`
| Field | Type | Description |
|-------|------|-------------|
| email | string | User's email address |
| role | string | Job role |
| roleOther | string | Custom role if "Other" selected |
| currentTools | string | Current workflow tools |
| frustrations | array | Pain points (multi-select) |
| timeSpentOnAdmin | string | Weekly admin hours |
| engagementPreference | string | Desired next step |
| pricingWillingness | string | Pricing range |
| openFeedback | string | Free-form feedback |
| skippedQuestions | array | Question numbers skipped |
| completedAt | timestamp | Quiz completion time |
| userAgent | string | Browser info |

---

## Step 5: Test Your Integration

1. Deploy to Netlify
2. Open browser DevTools → Console
3. Submit the waitlist form
4. Check console for: `Waitlist signup saved with ID: xxx`
5. Complete the quiz
6. Check console for: `Quiz response saved with ID: xxx`
7. Verify data in Firebase Console → Firestore

---

## Step 6: Enable Firebase App Check (Recommended)

For production security:

1. Firebase Console → App Check
2. Register your domain
3. Enable reCAPTCHA v3
4. Update security rules to require App Check

---

## Troubleshooting

### "Firebase not initialized"
- Check that your config values are correct
- Ensure you're loading from HTTPS (required for Firebase)

### "Permission denied"
- Check Firestore security rules
- Verify the collection names match exactly

### Data not appearing in Firestore
- Check browser console for errors
- Verify your project ID matches

---

## Data Export

To export waitlist data:

```bash
# Using Firebase CLI
firebase firestore:export gs://your-bucket/exports/waitlist

# Or use Firebase Console → Firestore → Export
```

---

## Support

For Firebase-specific issues, see:
- [Firebase Documentation](https://firebase.google.com/docs/firestore)
- [Firebase Support](https://firebase.google.com/support)
