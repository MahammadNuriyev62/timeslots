# book-meeting

A fake Calendly-style appointment booking page. Built as a prank: the friend picks a date and time, fills in their details, and gets a convincing "you are scheduled" confirmation. Nothing is actually sent anywhere.

## How it works

Single HTML file. No backend, no dependencies.

- **Date-aware.** Uses the visitor's local date. Earliest bookable slot is `today + 3 days`; weekends and anything past 60 days are disabled.
- **Deterministic availability.** For each candidate date, the slot list is derived from `FNV-1a(today_date || target_date)`. Same hash all day, re-rolls at local midnight. ~25% of eligible days get any slots, and those get 1 to 3 (biased toward 1 to 2). So the calendar looks consistent if the friend reopens it the same day, and refreshes overnight.
- **Fake submit.** The "Schedule Event" button runs a ~1s loading state, then jumps to a confirmation screen showing the booked time, a fake Google Meet reference, and a working `.ics` download.

## Usage

Open `book-meeting.html` in a browser, or drop it on any static host (Netlify Drop, Cloudflare Pages, GitHub Pages) to get a shareable URL.

## Customize

Open the file and edit:
- Host name, bio, avatar initials near the top of the left pane markup.
- Meeting types in the step-1 buttons.
- Availability knobs in `getSlotsFor()` (chance per day, slot count, time pool) and `getMinBookingDate()` (lead time).