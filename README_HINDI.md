# Poetry World — Android Studio Kotlin App

इस starter app में ये शामिल हैं:
- Firebase Firestore से public poems feed
- Firebase anonymous sign-in
- कविता लिखना और publish करना
- अपने द्वारा लिखी कविता edit/delete करना
- Search, share
- Image upload और ML Kit OCR (Hindi Devanagari + Latin text)
- Purple/gold premium theme

## Android Studio में खोलें
1. ZIP extract करें।
2. Android Studio > Open > `PublicPoetryApp` folder चुनें।
3. Firebase Console (https://console.firebase.google.com/) में नया project बनाएं।
4. Android app register करें package name: `com.example.publicpoetry`
5. Firebase से `google-services.json` डाउनलोड करके `app/` folder में रखें।
6. Firebase Authentication > Sign-in method में Anonymous enable करें।
7. Firestore Database create करें और नीचे दिए rules publish करें।
8. Android Studio में Sync Project with Gradle Files करें; फोन/एमुलेटर पर Run करें।

## Firestore rules (publish in Firebase Console)
Rules केवल signed-in anonymous/auth users को अपने poem create/update/delete करने दें; public read है.
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /poems/{poemId} {
      allow read: if true;
      allow create: if request.auth != null
        && request.resource.data.ownerId == request.auth.uid
        && request.resource.data.title is string
        && request.resource.data.body is string;
      allow update: if request.auth != null
        && resource.data.ownerId == request.auth.uid
        && request.resource.data.ownerId == request.auth.uid;
      allow delete: if request.auth != null
        && resource.data.ownerId == request.auth.uid;
    }
  }
}
```
## Important
- Firebase setup ke bina app Firestore se connect nahi hoga. `google-services.json` app-specific hai, isliye is ZIP mein included nahi hai.
- Anonymous sign-in ke saath users apni poems manage karte hain. App data persist rahe, isliye Firebase account/provider ko later bind karna recommended hai.
- Before public Play Store release, add moderation/report feature, rate limiting/App Check, privacy policy, branding and account recovery.
