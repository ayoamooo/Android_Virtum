<p align="center">
  <img src="mobile/assets/images/virtum_logo.png" alt="Virtum" width="168">
</p>

# Android Virtum

Virtum is a Flutter app for recording everyday health metrics and reviewing them in a personal dashboard. A Node.js API handles account data and metric history; the mobile client shows summaries, charts, goals, and an optional assistant.

## Project summary

The project explores a client–server design for personal wellness tracking. It is a software prototype: its metrics and generated suggestions have not been clinically validated and should not be used for diagnosis or treatment.

**Keywords:** Flutter, mobile health, REST API, SQLite, data visualisation

## Features

- Dashboard cards for heart rate, steps, blood pressure, hydration, and related metrics
- Historical charts and individual biomarker views
- Personal goals, hydration reminders, and manual metric entry
- Registration, sign-in, email verification, and password reset flows
- Optional Firebase sign-in and an assistant endpoint served by the backend

## Architecture

```text
Flutter app  ── REST/JSON ──>  Express API  ──>  SQLite
     │                             │
     └── Firebase Auth (optional)  └── Assistant provider (optional)
```

The Flutter source is under `mobile/lib/`. API routes, persistence, and authentication live in `backend/`.

## Run locally

### Requirements

- Flutter SDK compatible with the constraint in `mobile/pubspec.yaml`
- Android Studio or an Android SDK and emulator
- Node.js and npm

### Start the API

```powershell
cd backend
npm ci
Copy-Item .env.example .env
# Set local values in backend/.env, including a development JWT_SECRET.
npm start
```

The API uses the `PORT` value from `backend/.env`. Do not commit `.env`; the example file contains the configuration keys without local credentials.

### Start the Android app

```powershell
cd mobile
flutter pub get
flutter run
```

The client currently uses the base URL in `mobile/lib/services/api_config.dart`. For an Android emulator talking to a backend on the same computer, use `http://10.0.2.2:<PORT>`; for a physical device, use the computer's LAN address. Keep the URL and `PORT` in sync.

To build an APK:

```powershell
cd mobile
flutter build apk --release
```

The release APK is written to `mobile/build/app/outputs/flutter-apk/app-release.apk`.

## Academic scope and limitations

The app records and presents values supplied by the user or its API. The repository does not document a clinical study, validated prediction model, or medical-device certification. Assistant output depends on the configured provider and should be treated as general information.

## References

- [Flutter documentation](https://docs.flutter.dev/)
- [Express documentation](https://expressjs.com/)
- [SQLite documentation](https://www.sqlite.org/docs.html)
- [Firebase Authentication for Flutter](https://firebase.google.com/docs/auth/flutter/start)

## License

No repository-level license is included. Contact the author before reusing the project.
