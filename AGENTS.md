# ISIZOFIKA: rules for AI agents

## What this project is
ISIZOFIKA is a parcel handover platform built on Fleetbase (a fork).
Flow: the sender creates an order, takes the parcel to a taxi rank and hands it
to a taxi driver (outside the system), the driver drops it at a collection store,
store staff mark it received, and the recipient collects it with a PIN.

There is NO driver app and NO driver in the system. Do not build driver features.

## Order statuses (MVP)
CREATED, READY_FOR_COLLECTION, COLLECTED, CANCELLED, EXPIRED.
Do not add "driver pickup", "driver accepted" or "arrived at destination" statuses.

## Security rules
- The QR code identifies an order. It must NEVER release a parcel.
- The collection PIN releases a parcel. Store it only in ISIZOFIKA's own table,
  never in order metadata. Never log it. Reveal it only to the sender.
- Store staff may only see and act on orders for their own store. Enforce this in code.
- Never print, commit or copy secrets: api/.env, docker-compose.override.yml, API keys.

## Where code goes
- ALL new ISIZOFIKA code goes in packages/isizofika/ (our own extension).
- Do NOT edit Fleetbase core files (api/, console/, other packages/) unless I
  explicitly say so. If a core edit is unavoidable, make it as small as possible
  and add a line to CORE-CHANGES.md saying what, where and why.
- Prefer Fleetbase's existing models, APIs and conventions over inventing new ones.

## How to work
- One feature at a time. Do only what I ask in the current message.
- Before changing anything, tell me which files you plan to touch and wait for approval.
- After changing code, tell me exactly how to test it (commands or URLs and expected results).
- Do not install new packages without asking.
- Keep changes small and easy to review with `git diff`.

## Git rules
- Never commit or push unless I ask. Never touch the main branch.
- Work on the branch I am on. Do not rewrite history or force push.

## Docker rules
- The app runs in Docker. Never run `docker compose down -v`.
- Never delete docker/database/ or docker-compose.override.yml.
- Never re-run scripts/docker-install.sh (it can change database credentials).
- Safe commands: `docker compose ps`, `docker compose logs <service> --tail 50`,
  `docker compose restart <service>`.

## Environment
Windows 11, PowerShell, Docker Desktop, project at C:\ISIZOFIKA_APP\isazofika.
Console: http://localhost:4200  API: http://localhost:8000