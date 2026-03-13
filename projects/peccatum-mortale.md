# peccatum-mortale

> **Skills**: @skills/* (all), @languages/dart-flutter.md, @languages/web-pwa.md, @domains/event-planning.md
> **External Skills**: @skills-external/anthropic/skills/frontend-design/SKILL.md, @skills-external/anthropic/skills/webapp-testing/SKILL.md

## Project Overview

Immersive 1920s speakeasy event platform — RSVP, registration station, live scoreboard. Companion web app for the 40Jarigen event.

- **Repository**: `GielW/peccatum-mortale`
- **Parent project**: 40Jarigen (event planning, hardware, narrative)

## Active Skills

This project uses:

- **Dart/Flutter** — Flutter Web app (SDK `^3.11.0`)
- **Web/PWA** — Firebase Hosting, SPA with GoRouter
- **Event planning** — guest management, registration
- **Frontend design** _(external)_ — 1920s speakeasy theme
- **Webapp testing** _(external)_ — Playwright-based PWA testing

## Deployment & Infrastructure

| Service | Details |
|---|---|
| **Firebase account** | `gielwynants@gmail.com` (personal — NOT the Futech work account) |
| **Firebase project ID** | `peccatum-mortale` |
| **Hosting** | Firebase Hosting, `build/web` as public dir |
| **Database** | Cloud Firestore (same Firebase project) |
| **Live URL** | `https://peccatum-mortale.web.app` |

### Build & Deploy

```bash
# Flutter SDK (not on PATH by default)
export PATH="/home/gielw/development/flutter/flutter/bin:$PATH"

# Build
flutter build web

# Deploy (must be logged in as gielwynants@gmail.com)
firebase deploy --only hosting
```

### Firestore Collections

| Collection | Purpose |
|---|---|
| `invitees` | Guest list with name, category, email, address, status |
| `guests` | RSVP responses linked to invitees |
| `passwords` | 70 unique speakeasy entry passwords |

## Key Files

| Purpose | File |
|---|---|
| Project overview | `README.md` |
| App entry point | `lib/main.dart` |
| Routing (GoRouter) | `lib/core/router.dart` |
| Firestore CRUD | `lib/core/services/firestore_service.dart` |
| 1920s theme | `lib/core/theme/speakeasy_theme.dart` |
| Shared widgets | `lib/core/widgets/speakeasy_widgets.dart` |
| Guest data model | `lib/core/models/guest.dart` |
| Password gate | `lib/rsvp/password_gate_screen.dart` |
| RSVP form | `lib/rsvp/rsvp_form_screen.dart` |
| RSVP confirmation | `lib/rsvp/confirmation_screen.dart` |
| Admin dashboard | `lib/admin/admin_dashboard_screen.dart` |
| Admin login | `lib/admin/admin_login_screen.dart` |
| Firebase config | `firebase.json` |
| Firestore rules | `firestore.rules` |

## Cross-Reference Map

| When you change... | Also update... |
|---|---|
| `firestore_service.dart` (CRUD, collections) | `admin_dashboard_screen.dart` (UI), `guest.dart` (model) |
| `speakeasy_theme.dart` (colors, fonts) | All screens use theme — visual check needed |
| `router.dart` (routes) | Screens that link to other screens |
| `firestore.rules` (security rules) | Deploy with `firebase deploy --only firestore:rules` |
| Firestore collection schema | `firestore_service.dart`, admin dashboard, any consuming screen |

## Architecture Notes

- **SpeakeasyTheme**: Custom 1920s theme (gold, noir, cream, smokeyGrey, crimson)
- **GoRouter**: Password gate → RSVP flow; admin easter egg (7-tap seal or type "admin")
- **Admin access**: Hidden — 7 taps on wax seal or typing "admin" on password gate

## Language Note

Code in English. User-facing strings in Dutch (Belgian audience).
