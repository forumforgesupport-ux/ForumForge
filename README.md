# ForumForge

Ionic + React + TypeScript study-collaboration app (web & mobile), fully persisted in `localStorage`.

## Run it

```bash
npm install
npm run dev          # http://localhost:5173
npm run build        # production build in dist/
```

### Mobile (Capacitor)

```bash
npm run build
npx cap add android   # or: npx cap add ios
npx cap sync
npx cap open android
```

## Demo accounts (password `password123`)

| Role | Email |
|------|-------|
| Student | ama@forumforge.edu |
| Student | kwame@forumforge.edu, esi@forumforge.edu, kofi@forumforge.edu |
| Instructor | akua.ofori@forumforge.edu |

Or register a new account (choose Student or Instructor), or use the simulated Google Sign-in.

## Features

- 3-second bouncing-logo splash → Login
- Register (Student / Instructor), Login, Remember me, simulated Google Sign-in, multi-account switcher
- Home with time-based greeting, next Meet sync, Due soon, rooms, notifications
- Course rooms with live-style chat, file/notes sharing, members & presence, `@forgemind` mentions, simulated peer replies
- ForgeMind AI study assistant: explanations, interactive quizzes, room summaries, meeting plans (offline rule engine in `src/utils/forgemind.ts` — swap `respond()` for a real LLM call)
- Find peers: search by name/course, shared courses, Connect
- Schedule: week calendar, month picker, book meetings with auto-generated `meet.google.com/ff-[course]-sync` links, simulated Meet call UI, deadlines
- Profile: credentials, edit profile, password, connected accounts, courses (join/leave/create custom), dark mode, sign out, reset demo data
- Custom courses are written to shared `localStorage`, so every user on the device sees the new room (other open tabs update live via the `storage` event)
- **Instructor role**: can only join meetings and share files (no text chat, scheduling, connecting, ForgeMind, or creating rooms) — see `can` in `src/context/AppContext.tsx`
- Desktop (≥1024px): left sidebar, multi-column grids, split panes (rooms | chat | ForgeMind). Mobile: bottom tabs (Home, Peers, Rooms, Schedule, Profile), stacked layouts.
- Styling: plain CSS — every UI `.tsx` file has a matching `.css` file next to it (e.g. `Home.tsx` + `Home.css`). Shared building blocks (`ff-btn-primary`, `ff-card`, `ff-input`, `ff-chip`…) live in `src/App.css`; the CSS reset is `src/theme/base.css`.
- Light/dark theme via CSS variables (`src/theme/variables.css`) + `.dark` / `.ion-palette-dark` on `<html>`

## Storage keys

`ff_users`, `ff_courses`, `ff_messages`, `ff_meetings`, `ff_deadlines`, `ff_notifications`, `ff_session`, `ff_remembered_accounts`, `ff_ai_<userId>`. All access goes through `src/data/storage.ts` — replace those functions with API calls when you add a backend.

> Passwords use a non-cryptographic hash and the Google sign-in is simulated. This is a prototype for user testing, not production auth.
