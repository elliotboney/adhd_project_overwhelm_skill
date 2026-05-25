# Project Map: client-portal-rebuild
_Updated: 2026-05-23_

## One outcome (this session)
Get the magic-link login working end to end on the staging URL.

## The map
```mermaid
graph TD
    subgraph Auth["🔑 Auth (👉 you are here)"]
        A1[Magic-link send]
        A2[Token verify]
        A3[Session cookie]
    end
    subgraph Data["🗄️ Data"]
        D1[Postgres schema]
        D2[User table backfill]
    end
    subgraph UI["🎨 UI"]
        U1[Login page]
        U2[Dashboard shell]
    end
    subgraph Parked["💤 Parked"]
        P1[Email template polish]
        P2[Rate limiting]
    end
    A1 --> A2 --> A3
    A3 --> U2
    D1 --> D2
```

## Next 3 actions
1. Open `src/auth/sendLink.ts` — wire the SMTP call (token already generated). ~10 min.
2. Add the `/auth/verify` route that exchanges token for session cookie.
3. Point the login form at the new endpoint and test on staging.

## Parked
- 2026-05-23 Email template polish → UI
- 2026-05-23 Rate limiting on link requests → Auth
