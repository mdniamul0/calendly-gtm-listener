# Changelog

## v1.0.0 (2026-11-06)

- First release of the free Calendly GTM listener.
- Fires `calendly_booking_success` on Calendly's `calendly.event_scheduled` message.
- Only trusts messages from `https://calendly.com`, ignores empty and unrelated messages.
- One push per booking, even when Calendly sends the message twice.
