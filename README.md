# LinkedIn Clone

A LinkedIn-inspired social network built in one week by a team of five during the Epicode Full-Stack Developer course (Build Week 3).

Users can sign up, publish and manage posts, comment and like, build their network, receive real-time notifications and chat with AI-powered contacts — all wrapped in a switchable theme system.

<!-- Add a screenshot or GIF of the home feed here, e.g. ![Home feed](docs/home.png) -->

## Features

- **Authentication** with Firebase Auth: sign up, login, persistent session, protected routes
- **Feed** with full post CRUD, image upload, likes ("Consiglia") and comments
- **Profile**: personal page, editable profile, work experience, other users' profiles
- **Network**: connection requests, accept/decline, list of connections
- **Real-time notifications** for likes, comments and invites (Firestore `onSnapshot` listener)
- **AI messaging**: chat drawer with three contacts, each with its own personality, powered by an LLM (Groq API, Llama 3.1)
- **News** section fed by the NewsData API
- **Theme system**: light/dark mode plus five brand themes (default, villain, fantasy, cyberpunk, horror) with custom logos and GSAP animations
- **Security rules** on Firestore: only authors can edit or delete their posts, any signed-in user can toggle likes

## Tech stack

| Area | Technologies |
|---|---|
| Frontend | React 19, TypeScript, Vite, React Router |
| State | Redux Toolkit (feature slices, async thunks, typed hooks) |
| UI | React Bootstrap, Bootstrap Icons, GSAP |
| Backend as a service | Firebase Authentication, Cloud Firestore |
| External APIs | Groq (LLM chat), NewsData (news) |

## Project structure

Feature-based organization: each feature owns its slice, components and logic.

```
src/
├── app/          # Redux store and typed hooks
├── features/
│   ├── auth/         # auth slice, login/register, route guards
│   ├── posts/        # feed, post CRUD, comments, likes
│   ├── profile/      # profile page, edit profile, experiences
│   ├── network/      # connections and invites
│   ├── notification/ # real-time notifications
│   ├── messaging/    # AI chat drawer
│   ├── news/         # news section
│   └── theme/        # brand themes and effects
├── components/   # navbar, cards, shared UI
├── pages/        # routed pages
└── firebase.ts   # Firebase initialization
```

## Getting started

```bash
npm install
cp .env.example .env   # then fill in your Firebase, Groq and NewsData keys
npm run dev
```

The app needs a Firebase project with Authentication (email/password) and Firestore enabled. Security rules and indexes are in `firestore.rules` and `firestore.indexes.json`.

## Team workflow

The project was developed like a real team project:

- `main` protected, updated only through pull requests at milestones
- `develop` as the integration branch, one branch per feature
- every pull request reviewed by at least one teammate
- conventional commit prefixes (`feat:`, `fix:`, `chore:`)
- one owner per feature, shared files (types, store) changed only after notifying the team

## Team

- Angelo Cozzula — setup, store and integration (repo owner, PR reviews)
- Cristian Nunez Jorge
- Alberto Razzolini
- Javier
- **Claudio Giasi** ([@TheRedKardinal](https://github.com/TheRedKardinal))

### My contribution

- **Migration from a mock backend (json-server + localStorage) to Firebase**: Firebase setup, Firebase Auth integration in the auth slice, session handling and route guards (`ProtectedRoute`, `RedirectIfAuth`), posts persisted on Firestore
- **Firestore security rules** and indexes
- Layout fixes on profile, edit profile and network pages; avatar rendering fixes
