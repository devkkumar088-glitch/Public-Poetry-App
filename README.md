# कविताघर / KavitaGhar : Android App Project

Hindi + English poem app (Capacitor). Poems phone me save hoti hain, internet ke bina bhi chalti hai.

## Tareeka 1: Bina Android Studio ke APK (sabse aasaan)
1. github.com par free account banao aur naya repository banao (jaise `kavitaghar`).
2. Is zip ka saara content (www, package.json, capacitor.config.json, .github, ...) us repository me upload karo.
3. Repository me **Actions** tab kholo, "Build Android APK" chunke **Run workflow** dabao.
4. 5-8 minute baad run ke neeche **KavitaGhar-debug-apk** artifact milega. Download karke unzip karo.
5. `app-debug.apk` apne phone me bhejo aur install karo (Settings me "Install unknown apps" allow karna padega).

## Tareeka 2: Apne computer par (Android Studio)
```
npm install
npx cap add android
npx cap sync android
npx cap open android      # Android Studio khulega
```
Android Studio me: Build > Build APK(s) (test ke liye) ya Build > Generate Signed Bundle / APK (Play Store ke liye).

## Play Store par launch
1. play.google.com/console par developer account banao (ek baar ka $25 fee).
2. Android Studio me **Generate Signed Bundle (AAB)** banao. Keystore file aur uska password surakshit rakho, kho diya to app update nahi ho payegi.
3. Play Console me naya app banao, AAB upload karo.
4. Zaroori cheezein: app icon (512x512), feature graphic (1024x500), kam se kam 2 screenshots, short + full description, Privacy Policy ka link, Content rating aur Data safety form.
5. Review ke baad app live ho jata hai (naye account me pehle kuch din lag sakte hain).

## Icon aur Play Store graphics
- App icon `assets/` folder me hai aur build ke time apne aap lag jata hai (kuch karna nahi).
- `store/play-icon-512.png` aur `store/feature-graphic-1024x500.png` Play Console me upload karo.
- `docs/store-listing.md` me app ka naam, description aur Data safety ke jawab taiyaar hain.

## Privacy Policy ka link (Play Store ke liye zaroori)
1. `docs/privacy-policy.html` kholkar [Developer name] aur [email] apni jaankari se badlo.
2. GitHub repository me Settings > Pages > "Deploy from a branch" > branch `main`, folder `/docs`.
3. Kuch minute baad link milega: `https://<aapka-username>.github.io/<repo>/privacy-policy.html`. Wahi Play Console me do.

## Photo se text
Settings me apni Claude API Key daalo (console.anthropic.com se). Key sirf phone me rehti hai. Bina key ke baaki app poori chalti hai.

## Firebase setup (public poems ke liye) , ek baar karna hai
1. Firebase Console > project **public-poetry-app**.
2. **Build > Authentication > Get started > Email/Password** ko Enable karo.
3. **Build > Firestore Database > Create database** (production mode, region apne paas ka, jaise `asia-south1`).
4. Firestore > **Rules** tab me is zip ki `firestore.rules` ka poora text paste karke **Publish** karo.
5. Package name `kavita.ghar` hai (`capacitor.config.json`). Firebase me wahi Android app rakho. `google-services.json` iss web-style setup me zaroori nahi.
6. Agar login me "API key not valid" ya "requests blocked" error aaye: Firebase me **Add app > Web (`</>`)** karo, uska `firebaseConfig` `src/fb.js` me daalo (`apiKey` aur `appId` badlo), aur Google Cloud Console > APIs & Services > Credentials me us key par "Application restrictions" hatao ya Websites me `https://localhost` jodo.
7. Roz **Firestore > reports** dekho. Galat post mile to `posts` me us post ID ko delete karo.
