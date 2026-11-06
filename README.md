# Calendly GTM Event Listener

**Free Google Tag Manager listener for Calendly booking tracking.** It fires one `calendly_booking_success` event the moment a visitor books a time in a Calendly calendar embedded on your website, so you can track Calendly bookings in GA4, Google Ads, Meta Pixel and any other tag.

![Calendly GTM Event Listener](docs/banner.png)

**Full guide, install video and copy button:** https://mdniamul.com/gtm-event-listeners/calendly-gtm-listener/

---

## What it does

Calendly's embed (inline widget, popup widget or popup text link) sends a `calendly.event_scheduled` message to your page when a booking is made. This listener catches it and pushes:

```js
{
  event: 'calendly_booking_success',
  form_id: 'calendly_embed',
  page_path: '/book-a-call/'
}
```

Built-in safety:

- Only trusts messages from `https://calendly.com`
- Ignores empty, fake or unrelated messages from other iframes, extensions and chat widgets, and Calendly's own page-height and step messages
- Pushes once per booking, even when Calendly sends the message twice

## Install in 6 steps

1. **Embed Calendly on your page.** Calendly → your event type → Share → Add to website → Inline embed, Popup widget or Popup text. The booking must happen on your page, not on calendly.com.
2. **GTM → Tags → New → Custom HTML.** Paste [`calendly-gtm-listener.html`](calendly-gtm-listener.html). Trigger: **All Pages**.
3. **Triggers → New → Custom Event**, event name `calendly_booking_success`.
4. **Variables → New → Data Layer Variable**: `DLV - form_id` → `form_id`.
5. Fire your **GA4 event** (for example `generate_lead`), **Google Ads conversion** or **Meta Pixel** `Schedule` event on that trigger.
6. **Preview**, book a test meeting, check the event in Tag Assistant, then **Publish**.

## Files

| File | What it is |
|---|---|
| `calendly-gtm-listener.html` | Ready to paste into a GTM Custom HTML tag |
| `calendly-gtm-listener.js` | Same code without the `<script>` tags |
| `examples/sample-datalayer-output.json` | What the push looks like |

## Videos

- Install the free code: https://mdniamul.com/gtm-event-listeners/calendly-gtm-listener/#install-video
- What the advanced version collects: https://mdniamul.com/gtm-event-listeners/calendly-gtm-listener/#advanced

## Good to know

Calendly's embed message does not include the invitee's email or name, only two links (the scheduled event and the invitee). So no client-side Calendly listener can read the email from the embed alone. The advanced version solves this with Calendly's "Pass event details to your redirected page" option, embed prefill, or a value from your own site.

Step-by-step guides on my blog:

- [How to track Calendly conversions in GA4 using GTM](https://mdniamul.com/blog/how-to-track-calendly-conversion-tracking-in-ga4-using-gtm-2026/)
- [Calendly booking conversion tracking with Google Ads Enhanced Conversions](https://mdniamul.com/blog/calendly-booking-conversion-tracking-google-ads-enhanced/)

## Need more data? Advanced version

The free code tells you a meeting was booked. The **advanced version** also sends the invitee's SHA-256 hashed email, name and phone, the booking details (event type, host, start and end time, length, payment, answers), funnel steps (calendar viewed, date picked), UTM values, 17 ad click IDs, first-party cookies (`_ga`, `_fbp`, `_fbc`, `_gcl_au` and more), visitor location and a unique `event_id`, ready for Google Ads Enhanced Conversions, Meta CAPI, TikTok Events API and server-side GTM.

It comes with a setup video, a PDF guide and a GTM import file in your client portal. The code starts from $89, and setup packages are available:

- Prices: https://mdniamul.com/gtm-event-listeners/calendly-gtm-listener/#pricing
- WhatsApp: https://api.whatsapp.com/send?phone=8801776485758
- Book a call: https://calendly.com/mdniamul
- All listeners: https://mdniamul.com/gtm-event-listeners/

Need it done for you? See my [server-side tracking service](https://mdniamul.com/server-side-tracking-service/) and [Google Ads tracking specialist](https://mdniamul.com/google-ads-tracking-specialist/) pages.

## Troubleshooting

- **No event:** the booking was done on calendly.com instead of your page, GTM is not on that page, or the tag is paused.
- **Two events:** an older listener (or another plugin's Calendly tracking) is still live. Keep one.
- **Check the raw message:** run `window.addEventListener('message', e => { if (e.origin === 'https://calendly.com') console.log(e.data) })` in the console and book a test meeting.

## About

Built by **[MD Niamul](https://mdniamul.com)**, GoHighLevel & AI Agent Automation, Marketing Attribution and Server-Side Tracking Specialist. Founder of Digital Soldier Agency and official Stape partner.

[Website](https://mdniamul.com) · [Free GTM listeners](https://mdniamul.com/gtm-event-listeners/) · [Book a call](https://calendly.com/mdniamul) · [LinkedIn](https://linkedin.com/in/mdniamul)

## License

MIT. Free to use on your own and your clients' sites. See [LICENSE](LICENSE).
