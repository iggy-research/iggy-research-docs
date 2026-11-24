# Roadmap — Iggy Research

Where the project goes after the first version (editor + AI editor + notes linked into a second brain).
Why we build it: see [PHILOSOPHY.md](PHILOSOPHY.md).

## 1. Choosing a language model (instead of typing an ID) ✅
- [x] A picker in settings instead of a text field, plus an option for a custom model ID
- [x] Model list fetched from the OpenRouter API (`/models`) with search (24 h cache; offline: recommended models from `src/models.ts`)
- [x] Price per token, context window and provider shown for each model
- [x] Favorite and recently used models
- [x] A separate model per task: paragraph review, note summary, link suggestions (new buttons in the AI panel)
- [x] Local models (Ollama / LM Studio) for offline work and privacy

## 2. Language support ✅
- [x] Multilingual interface (i18n): Polish and English (`src/i18n.ts`; a new language = a new dictionary)
- [x] Document language detection (9 languages, offline) and AI replies in the same language
- [x] AI editor prompts per language (Polish and English; an empty prompt = the default for the document's language)
- [x] Spell checking for the chosen or detected language (editor `lang` attribute → system dictionary)
- [ ] Welcome notes in English (Polish only today)

## 3. Server sync ✅
- [x] Backend for notes and settings (user accounts) — Django + DRF in `iggy-research-api`
- [x] Sync between devices, offline-first, conflict resolution (a “(conflict …)” copy — nothing is lost)
- [x] Optional end-to-end encryption (AES-GCM + PBKDF2; the server only sees ciphertext)
- [x] Document version history (local in `.iggy/history` + server versions, restore with ⟲)
- [x] Serverless alternative: sync via Git (commit / pull --rebase / push) or a cloud folder
- [ ] Sync attachments (images, PDFs) — only .md notes today

## 4. Publishing — blog and posts ✅
- [x] Publish a note as a blog post with one shortcut (↗ or Ctrl+Shift+U; images uploaded with the post)
- [x] Public author profile with a list of posts (`/@author`, React frontend in `iggy-research-web`)
- [x] Draft → publish → update, with visibility control (private / link only / public)
- [x] Public notes with their connections intact (digital garden): [[links]] and backlinks
- [x] Export: static HTML (with RSS), Markdown, Ghost and WordPress integrations; Substack via clipboard (no API)
- [x] Custom domain for a blog (CNAME + automatic HTTPS via Caddy, `iggy-research-deploy`)

## 5. Newsletter and RSS ✅
- [x] RSS/Atom feed for every blog (`/feeds/@author/<blog>.xml`, `.atom`)
- [x] Newsletter: subscribers (double opt-in), emailing a new post (queue, `send_newsletters`, one-click unsubscribe; sent via Resend)
- [x] RSS reader in the app (≋) — an item is saved as a note in “Sources/” with a quote and room for your own thoughts
- [x] Basic stats without invasive tracking (no cookies, no IP addresses, respects Do Not Track)

## 6. Landing page ✅
- [x] Product page: mission, features, interface illustration, downloads (Linux, macOS → GitHub Releases)
- [x] The manifesto from PHILOSOPHY.md as the core content (read straight from the file), full text at `/manifest`
- [x] Waitlist / newsletter signup (with consent to product emails)
- [x] Directory of public blogs written in Iggy
- [ ] Real screenshots instead of the illustration and the first release on GitHub Releases
- [x] Public downloads: the desktop repository is public; tagged versions are built by GitHub Actions for macOS and Linux

## 7. Autosave ✅
- [x] A settings toggle: autosave on / off (on by default — how it worked before)
- [x] Save after a short pause (1.5 s after the last change) and when switching files / closing the window
- [x] Only for files already on disk — a new note still needs its first Ctrl+S
- [x] The status dot in the toolbar shows that the save happened

## 8. AI as a sparring partner and a mirror — not a ghostwriter
Rule: AI may touch the thinking, but not the sentences. It asks, points out, reminds and organizes — it does not
write text that reaches readers as the author's. Every task has its own model in settings.

**Intellectual sparring**
- [x] Devil's advocate — the strongest counterargument to a selection, paragraph or note (“Counter” button)
- [x] Socratic dialogue — AI asks one question at a time and digs deeper; the answers are saved as a note
- [x] Assumption test — “this paragraph assumes X; are you sure?”

**Mirror**
- [x] Cliché detector — sentences that sound like average internet text, underlined in the editor, never rewritten (“Clichés” button)
- [x] “What are you actually claiming?” — the text's thesis in one sentence; if it's the wrong one, the problem is in the text
- [x] Lay reader — places where someone outside the topic gets lost (marked, not fixed)

**Second brain — a memory people don't have**
- [x] “You used to think otherwise” — contradictions and changes of mind against older notes; the closest notes picked locally (“Before” button)
- [x] Non-obvious connections — the same mechanism in notes from different fields
- [x] Resurfacing notes — abandoned thoughts that fit what you are working on now

**Getting started without writing for the author**
- [x] Starter questions — instead of an outline, 5 questions whose answers become the text
- [ ] Voice note → loose bullet points (organizing, not prose)

**At publishing time**
- [x] Pre-send check — facts, numbers and quotes to verify, inconsistencies, typos
- [ ] Conversation — readers' replies grouped into threads and questions as material for new notes (closes the loop from the manifesto)

**To think about**
- [x] Paragraph review only points out the problem by default (“this sentence is unclear because…”); a ready “before → after” only on request (closer to principle no. 2)

**What we don't do:** generating paragraphs or finishing sentences, “rewrite it better”, automatic titles and leads for publishing.

## 9. Control over sync and publishing ✅
Users decide what leaves their computer and what others see.
- [x] Choose what syncs: folders and individual notes (☁ → “What to sync”); excluded notes stay on this computer only
- [x] Folder = blog: `iggy-research.com/@author/<folder>/<note>`; the blog is created on the first publish from that folder
- [x] Author page `/@author` listing their blogs; subfolders only organize (they don't change the address)
- [x] Every blog has its own newsletter, RSS/Atom (`/feeds/@author/<blog>.xml`) and an optional custom domain
- [x] Digital garden as a page type within a blog; [[links]] and backlinks also work across the author's blogs
- [x] The sync server is fixed to iggy-research.com; a custom (self-hosted) server only under advanced options
- [ ] Remove server copies of notes excluded from sync (they stay today; encrypted with E2E)
- [ ] Publish a whole folder in one click (today: note by note)

## 10. Sign-in without passwords ✅
The standard sign-in is a one-time code sent by email; Google and Apple are optional shortcuts.
- [x] Email one-time password (OTP): enter your email → receive a 6-digit code → sign in (no passwords;
      codes expire after 10 minutes, single use, rate-limited; sent via Resend)
- [x] Sign in with Google (enabled with `GOOGLE_CLIENT_IDS`)
- [x] Sign in with Apple (enabled with `APPLE_CLIENT_IDS`; required on macOS/iOS if other social sign-ins are offered)
- [x] One account per email: Google, Apple and the email code all lead to the same account
- [x] Desktop app: code entry and Google/Apple sign-in via the system browser with a deep link back to the app (one-time code + PKCE-style verifier)
- [x] Migrate existing password accounts (the next sign-in switches them to email codes)

## 11. Analytics ✅
Product analytics to understand how Iggy is used — in line with the manifesto: no cookies, no tracking across sites, no selling data.
- [x] Website: visits, sources, product page → download / waitlist conversion (privacy-friendly, cookieless)
- [x] Desktop app: anonymous, opt-in usage stats (which features are used, AI tasks, publishing); off by default,
      clearly described, never note contents
- [x] Server: dashboard with sign-ups, active authors, published posts, newsletter sends and deliverability (Resend events)
- [x] Authors: richer blog stats — per-post trends, newsletter opens/clicks (only if the author enables it), top referrers
