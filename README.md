# Personal Dashboard 🎯

Twoja prywatna gra produktywności. PWA z synchronizacją w chmurze, dostępna tylko dla Ciebie po zalogowaniu.

## ✨ Co potrafi

- **Taski z kategoriami** — sam dodajesz kategorie (np. Wygląd, Hustlerka, Szkoła) z emoji i kolorem
- **3 typy tasków**: jednorazowe, codzienne (reset co dzień), tygodniowe (reset w poniedziałek)
- **Coiny** — sam ustalasz ile dostajesz za każdy task
- **Sklep nagród** — wymieniasz coiny na własne nagrody (np. "wieczór z grą", "pizza", "kawa")
- **Levele i XP** — automatycznie z coinów; co level coraz trudniej
- **Streaki** — codzienne wbicie = ogień rośnie
- **Kasa 💸** — licznik zarobków: wpisujesz ile i za co zarobiłeś, a apka pokazuje sumę tego miesiąca (z trendem vs poprzedni), podział wg źródła i historię wpisów. Wykres główny z 8 zakresami (dziś, wczoraj, ten tydzień, miesiąc, ostatni miesiąc, 3 miesiące, ten rok, ostatni rok) + własne mini-wykresy, które sam dodajesz (metryka: suma / wg źródła / liczba wpisów, dowolny zakres, filtr źródła; typ słupkowy/liniowy/kołowy dobierany automatycznie)
- **Statystyki** — wykres 7 dni, breakdown po kategoriach, lifetime stats
- **18 osiągnięć** do odblokowania
- **Animacje iGaming-style** — sypiące się złote monety, slot-machine vibes, BIG WIN, level up confetti, screen shake
- **Dźwięki** — slot ding, jackpot fanfare, achievement chime (wszystko generowane w Web Audio API, brak plików)
- **Wibracje** na telefonie
- **Sync** między telefonem a komputerem (Firebase)
- **PWA** — dodajesz na pulpit jak normalną apkę

---

## 🚀 Setup w 3 krokach (~15 min, wszystko za darmo)

### Krok 1: Firebase (5 min)

1. Wejdź na **https://console.firebase.google.com/**
2. Kliknij **"Add project"** → nazwa: `personal-dashboard` (lub jakkolwiek chcesz)
3. Wyłącz Google Analytics (nie potrzebne) → Create project
4. W lewym menu kliknij **"Build" → "Authentication"** → Get started
5. W zakładce "Sign-in method" włącz **"Email/Password"** (pierwsza opcja, włącz tylko ten górny toggle) → Save
6. W lewym menu kliknij **"Build" → "Firestore Database"** → Create database
   - Wybierz lokalizację: `europe-west` (Belgia) lub `europe-central2` (Warszawa)
   - Wybierz **"Start in production mode"** → Enable
7. W Firestore przejdź do zakładki **"Rules"** i wklej dokładnie to:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

   → kliknij **Publish**. To gwarantuje, że TYLKO Ty masz dostęp do swoich danych.

8. Wróć do **Project Overview** (ikona koła zębatego u góry → Project settings)
9. Przewiń do **"Your apps"** → kliknij ikonę `</>` (Web app)
10. Nazwa: `dashboard` → **Register app** (NIE zaznaczaj Firebase Hosting)
11. Zobaczysz fragment kodu z `firebaseConfig = { ... }` — **skopiuj cały obiekt**

### Krok 2: Wklej config do apki (1 min)

Otwórz `index.html`, znajdź sekcję (~linia 700):

```js
const firebaseConfig = {
  apiKey: "PASTE_HERE",
  authDomain: "PASTE_HERE",
  ...
};
```

Zastąp całą tę linijkę kodem skopiowanym z Firebase Console.

### Krok 3: Hosting (5 min) — wybierz JEDNĄ opcję

#### Opcja A: GitHub Pages (najprostsze, darmowe na zawsze)

1. Załóż konto na **https://github.com** (jeśli nie masz)
2. Kliknij **"+" → "New repository"**
3. Nazwa: `dashboard` → ustaw **Public** (Private też działa, ale Pages na free tier wymaga Public) → Create
4. Na stronie repo kliknij **"uploading an existing file"**
5. Przeciągnij WSZYSTKIE pliki z folderu `dashboard`: `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`
6. **Commit changes**
7. W repo: **Settings → Pages** (w lewym menu)
8. Source: **Deploy from a branch** → Branch: **main** → folder **/(root)** → **Save**
9. Po ~1-2 min Twoja apka będzie pod adresem:
   ```
   https://TWOJ_USERNAME.github.io/dashboard/
   ```
10. **WAŻNE:** Wróć do Firebase Console → Authentication → Settings → "Authorized domains" → **Add domain** → wpisz `TWOJ_USERNAME.github.io` (bez https://)

#### Opcja B: Vercel (też darmowe, jeszcze szybsze)

1. Wejdź na **https://vercel.com** → Sign up z GitHub
2. **Add New → Project** → zaimportuj repo `dashboard` (lub przeciągnij folder przez "deploy")
3. Deploy → gotowe, dostajesz link `https://dashboard-xxx.vercel.app`
4. Dodaj ten domain do **Firebase Authorized domains** (jak w Opcji A pkt 10)

### Krok 4: Załóż konto i dodaj na telefon

1. Otwórz link do apki w przeglądarce (Chrome/Safari)
2. Kliknij **"Pierwszy raz? Załóż konto"**, wpisz email + hasło (min 6 znaków) → **Załóż konto**
3. Jesteś w środku 🎉
4. **Na telefonie**: kliknij 3 kropki w przeglądarce → **"Dodaj do ekranu głównego"** / **"Add to Home Screen"**
   - Safari (iPhone): przycisk Share (kwadrat ze strzałką) → "Add to Home Screen"
5. **Na komputerze (Chrome)**: w pasku adresu z prawej strony pojawi się ikona instalacji (monitor ze strzałką w dół)

Teraz apka działa **24/7 w chmurze**, masz ikonę na ekranie głównym jak w normalnej apce, a dane synchronizują się między urządzeniami.

---

## 🔐 Bezpieczeństwo

- Dane są w Twoim prywatnym Firestore. Reguły wymagają zalogowania jako Ty (`request.auth.uid == userId`).
- **Nikt poza Tobą nie zaloguje się bez Twojego maila i hasła.**
- Jeśli chcesz dodatkowej warstwy paranoi: w Firebase → Authentication → wyłącz "User account creation" PO ZAŁOŻENIU swojego konta, żeby nikt nowy nie mógł się zarejestrować.

## 💰 Czy naprawdę darmowe?

**Tak, na zawsze**, dla jednoosobowego użytku:
- Firebase Auth: darmowe do 50k aktywnych użytkowników
- Firestore: 50k odczytów + 20k zapisów dziennie za free (Ty zrobisz może 100 zapisów/dzień)
- GitHub Pages / Vercel: darmowy hosting na zawsze

## 🆘 Co jeśli...

**Apka nie ładuje się / "Firebase error"** → najpewniej nie wkleiłeś configu albo zapomniałeś dodać domeny do Authorized domains.

**"auth/operation-not-allowed"** → nie włączyłeś Email/Password w Firebase Authentication.

**Zgubiłem hasło** → Firebase Console → Authentication → Users → kliknij swojego usera → reset password.

**Chcę wyczyścić wszystko i zacząć od nowa** → Firestore → users → usuń dokument z Twoim uid; albo użyj Eksport JSON w ustawieniach apki dla backupu.

**Dane się nie synchronizują** → sprawdź czy jesteś zalogowany na obu urządzeniach na ten sam email. Nowy zapis zawsze nadpisuje starszy (last-write-wins).

---

Powodzenia 🚀 Zarabiaj coiny, level upuj, kupuj nagrody. To ma być fun.
