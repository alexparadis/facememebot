# Privacy Policy — FaceMemeBot

**Last updated: 3 September 2026**

This policy explains what personal data **FaceMemeBot** ("the Bot") collects, why, where it
goes, and how to get it deleted.

The data controller is **Alexandre Paradis**, contactable at **apb7591@gmail.com**.

Read this alongside the [Terms of Service](TERMS.md).

> **Read this part if nothing else.** FaceMemeBot stores photographs of people's faces and
> written statements about them, and sends both to Google's Gemini API to generate images.
> Photos are frequently uploaded by a friend rather than by the person pictured. If you are
> running or joining a server with this Bot, everyone whose face is uploaded should be told
> that this is happening.

---

## 1. What data the Bot collects

FaceMemeBot only receives what is explicitly passed to its slash commands. It does not use
Discord's privileged intents, so it **cannot read your server's messages**, member lists, or
presence.

### Submitted by users

| Data | Where it comes from | Why |
| --- | --- | --- |
| **Face photograph** (PNG/JPEG/WebP, up to 8 MB) | The attachment on `/add` | Used as the visual reference so the generated image resembles the person |
| **Name or nickname** for the person | The `name` argument on `/add` | Identifies them in commands and captions |
| **"Facts"** — free-text statements about a person | The `text` argument on `/fact` | Source material the AI turns into a scene |
| **Optional linked Discord account** | The `member` argument on `/add` | Associates the person with a Discord user, if you choose to |
| **Optional scene and style text** | `/meme` and `/versus` arguments | Steers the generated image |

### Collected automatically

| Data | Why |
| --- | --- |
| **Discord server (guild) ID** | Keeps each server's roster and facts separate |
| **Discord user ID of whoever ran `/add` or `/fact`** | Recorded against the record they created |
| **Timestamps** of when records were created | Housekeeping |

The Bot does **not** collect your email address, real name, IP address, payment details, or
location, and it runs no analytics or tracking of any kind.

### A note on faces and biometric data

FaceMemeBot uses face photographs as a **visual reference for image generation only**. It does
not run facial recognition, does not compute or store faceprints, face embeddings, or
biometric templates, and does not attempt to identify anyone from a photo. Photographs are
nonetheless personal data about an identifiable person, and are treated as sensitive here.

## 2. Data about people who are not the user

Most of the data in FaceMemeBot is about **someone other than the person who submitted it**.
Photos and facts are usually uploaded by a friend.

Whoever runs `/add` is required by the Terms of Service to have the pictured person's
permission first. If you are the person in a photo and you did not agree to this, see
[Section 8](#8-your-rights) — the data will be deleted on request, no questions asked.

Server administrators running this Bot should be aware that they are, in practice, processing
personal data about their members, and should make sure those members know.

## 3. Where the data is stored

All data is stored **locally on the machine the operator runs the Bot on**. There is no cloud
database and no hosted backend.

- Face photographs: image files in a `data/faces/` directory on that machine.
- Names, facts, IDs, and timestamps: a SQLite database file, `data/memebot.db`, on the same
  machine.

Generated images are not stored by the Bot. They are sent straight to the Discord channel that
requested them, and from that point they live in Discord's systems and in that channel under
Discord's retention rules — including for anyone who saw or saved them.

## 4. Who the data is shared with

### Google (Gemini API) — the AI provider

To generate an image, the Bot sends Google:

- the stored face photograph(s) of the person, and
- a text prompt containing their name and the selected facts about them.

It also sends Google a separate text-only request containing the person's name and facts to
compose the scene description.

**Important:** FaceMemeBot runs on Google AI Studio's **free tier**. Google states that on the
free tier, prompts and uploaded content may be used to improve Google's products and models,
and may be reviewed by human reviewers. Face photographs and personal facts submitted to this
Bot are included in that. (Paid Google Cloud / Gemini API tiers exclude customer data from
model training. If the operator switches to a paid tier, this section will be updated.)

Google's handling of the data is governed by the
[Google Privacy Policy](https://policies.google.com/privacy) and the
[Gemini API Additional Terms of Service](https://ai.google.dev/gemini-api/terms).

### Discord

Commands, arguments, and the generated images are transmitted through Discord and are subject
to the [Discord Privacy Policy](https://discord.com/privacy).

### Nobody else

Data is not sold, rented, or shared with advertisers, data brokers, or any other third party.
It may be disclosed if we are legally required to do so.

## 5. International transfers

Google and Discord are US-based and process data on servers around the world. Submitting data
to FaceMemeBot involves transferring it outside your country, including to the United States.
Those transfers rely on the providers' own transfer mechanisms, such as the EU Standard
Contractual Clauses.

## 6. Legal bases for processing (UK/EU GDPR)

Where the UK or EU GDPR applies, we rely on:

- **Consent** (Art. 6(1)(a)) for storing and processing a person's photograph and the personal
  statements about them. Consent is given by the pictured person, and the user who uploads on
  their behalf warrants that they have obtained it. Consent can be withdrawn at any time — see
  Section 8.
- **Legitimate interests** (Art. 6(1)(f)) for the minimal operational data — guild IDs,
  submitter user IDs, timestamps — needed to run the Bot, keep servers separate, and apply
  rate limits.

FaceMemeBot does not process face photographs for the purpose of uniquely identifying anyone,
so it does not treat them as biometric data under Art. 9. It nonetheless handles them as
sensitive personal data.

## 7. Retention

Data is kept until it is deleted. There is no automatic expiry.

- `/forget name:<name>` deletes that person's database record, all of their facts, and their
  stored face photograph file.
- `/unfact name:<name> number:<n>` deletes a single fact.
- Removing the Bot from a server does **not** by itself delete anything already stored. Run
  `/forget` for each person first, or email us.
- If the operator permanently stops running the Bot, the local `data/` directory is deleted.

Deletion from Discord is a separate matter: generated images already posted to a channel remain
there until someone deletes the messages, and are subject to Discord's own retention. Data
already sent to Google is subject to Google's retention, and we cannot recall it.

## 8. Your rights

Whether or not the GDPR applies to you, you can ask us to:

- **Access** — tell you what the Bot holds about you.
- **Delete** — erase your photograph and the statements about you.
- **Correct** — fix inaccurate data.
- **Withdraw consent** — at any time, which means deletion.
- **Object or restrict** — stop or limit further processing.
- **Port** — receive your data in a usable format.

**How to exercise them:** the fastest route is `/facts name:<name>` to see what is held and
`/forget name:<name>` to delete it, which any member of the server can run. Otherwise email
**apb7591@gmail.com**. We will respond within 30 days.

You do not need to prove anything to have a photograph of yourself removed. Ask and it goes.

If you are in the UK or EU and are unhappy with how we handled your request, you can complain
to your data protection authority (in the UK, the
[ICO](https://ico.org.uk/make-a-complaint/)).

## 9. Security

The database and photo files sit on the operator's own machine, protected by that machine's own
access controls. API keys are kept in an environment file that is excluded from version control.
The stored data is not separately encrypted at rest.

FaceMemeBot is a hobby project run on personal hardware, not a service with a security team. No
system is perfectly secure, and you should weigh that before uploading photographs of anyone,
including yourself.

## 10. Children

FaceMemeBot is not for anyone under 13, or under the minimum Discord age in your country if that
is higher. Do not upload a photograph of anyone under 18. If we learn that data about a minor has
been submitted, we will delete it immediately. If you believe this has happened, email
**apb7591@gmail.com**.

## 11. Changes to this policy

We may update this policy. The "last updated" date at the top will change, and material changes
will be announced in the Bot's support server, if one exists.

## 12. Contact

**Alexandre Paradis**
**apb7591@gmail.com**
