# INCY on iPhone: 34 services via VPN, everything else — direct

> 🇷🇺 **Russian version:** [README.md](README.md)

## ⚖️ Legal disclaimer (read first)

This material is of an **informational and technical nature**: it is a personal guide to configuring the INCY client (routing profile) on iPhone. It **is not advertising and does not promote** any VPN service, contains no call to use one, and provides no access to third-party services.

The author is aware that the legislation of the Russian Federation regulates the distribution of information about circumvention tools:
- **Federal Law No. 8-FZ "On Information, Information Technologies and Protection of Information"** (Art. 15) — blocking of pages containing "information on methods and means of ensuring access to information resources whose access is restricted within the territory of the Russian Federation";
- **RKN Order No. 196 dated October 17, 2024** — criteria for prohibited information, including scientific and technical data about VPN services used to circumvent blocks;
- **Federal Law No. 281-FZ dated July 31, 2025** — amendments to the Code of Administrative Offences: advertising of VPN services (Art. 14.2) and deliberate search for extremist materials (Art. 13.53);
- **Federal Law No. 282-FZ dated July 31, 2025** — use of circumvention tools when committing a crime is an aggravating circumstance (Criminal Code Art. 63).

The author **does not call for circumventing blocks** established in accordance with the legislation of the Russian Federation. Use of this material is at the reader's own discretion and risk, in accordance with the current legislation of the Russian Federation. As of the date of publication, the mere fact of using a VPN by an individual is not subject to administrative liability under the Code of Administrative Offences. This text is not legal advice; for an up-to-date opinion, consult a lawyer.

<p align="center">
  <img src="incy-routing-qr.png" width="360" alt="QR — import the routing profile into INCY">
</p>

**Scan this QR with the INCY camera — the "Socials via VPN" profile will be added and activated immediately.** Details in [Step 3](#step-3-add-the-ready-made-routing-profile-key-step) below.

## ⚠️ Important nuance (read first)

INCY **on iPhone has no per-app selection** — the "Per-app proxy" feature (enable VPN only for selected apps) is available **in the Android version only**. This is an Apple limitation: iOS does not let VPN apps route traffic per application.

**The solution for iPhone — a routing profile:**
by default all traffic goes direct, and only the domains and IP addresses of selected services go through the VPN.

How this differs from per-app:
- routing is done **by domains and IPs, not by apps**;
- if you open YouTube in Safari — that traffic will also go through the VPN (that's fine);
- if any other app connects to x.com or discord.com — it will also go through the VPN.

The practical result is the same: selected services work via VPN (including when blocked), and all other apps go direct, without VPN.

**What the profile does:**
- 34 services (social networks, messengers, games, streaming, AI, work & education, travel) go **through the VPN**;
- all other apps — **direct**, without VPN;
- Telegram server (DC1–DC5) IP ranges also go through the VPN — the iOS app connects to DCs by hardcoded IPs, not only by domains.

> Notes: "Universal Pictures" is interpreted as the streaming service **Universal+** (the studio has no separate consumer service); `geosite:disney` includes not only Disney+ but also Hulu/Hotstar; Battle.net is the `geosite:blizzard` category (battle.net, blizzard.com).

---

## Step 1. Install INCY

- App Store → search "**incy**" → developer **LLC ITDEV**.
- The app is free and available in the Russian App Store region (no need to change your region).

## Step 2. Add a subscription (server)

INCY does not provide servers itself — you need your own subscription/key from a provider (VLESS, VMess, Trojan, Hysteria2, etc.).

1. Open INCY → tap "**+**" → "**Add subscription**" (Import from URL).
2. Paste your subscription link (or scan a QR code).
3. When iOS asks for permission to install the VPN profile — **allow** (it will ask once).
4. Pick a server and tap the big connect button — make sure the VPN connects.

## Step 3. Add the ready-made routing profile (key step)

The ready-made profile **"Socials via VPN"**:
- `GlobalProxy = false` → everything that doesn't match a rule goes **direct**;
- in `ProxySites` — rules for 34 services (50 entries) → they go **through the VPN**;
- in `ProxyIp` — Telegram server (DC1–DC5) IP ranges → they also go **through the VPN**.

### Option A — via link (recommended)
1. Copy the link below in full (select everything).
2. Paste it into the **Safari** address bar on your iPhone and open it.
3. iOS will offer to open the INCY app → confirm.
4. The profile is added and **activated immediately**.

```
incy://routing/onadd/eyJOYW1lIjoiU29jaWFscyB2aWEgVlBOIiwiR2xvYmFsUHJveHkiOiJmYWxzZSIsIlJlbW90ZUROU1R5cGUiOiJEb0giLCJSZW1vdGVETlNEb21haW4iOiJodHRwczovL2Nsb3VkZmxhcmUtZG5zLmNvbS9kbnMtcXVlcnkiLCJSZW1vdGVETlNJUCI6IjEuMS4xLjEiLCJEb21lc3RpY0ROU1R5cGUiOiJEb1UiLCJEb21lc3RpY0ROU0lQIjoiOC44LjguOCIsIkZha2VETnMiOiJmYWxzZSIsIkRvbWFpblN0cmF0ZWd5IjoiSVBJZk5vbk1hdGNoIiwiRGlyZWN0U2l0ZXMiOlsiZ2Vvc2l0ZTpwcml2YXRlIl0sIkRpcmVjdElwIjpbImdlb2lwOnByaXZhdGUiLCIxMC4wLjAuMC84IiwiMTcyLjE2LjAuMC8xMiIsIjE5Mi4xNjguMC4wLzE2IiwiMTY5LjI1NC4wLjAvOCIsIjIyNC4wLjAuMC80Il0sIlByb3h5U2l0ZXMiOlsiZ2Vvc2l0ZTp0ZWxlZ3JhbSIsImRvbWFpbjp0Lm1lIiwiZG9tYWluOnRlbGVncmFtLm9yZyIsImdlb3NpdGU6eW91dHViZSIsImRvbWFpbjpnb29nbGV2aWRlby5jb20iLCJnZW9zaXRlOmluc3RhZ3JhbSIsImRvbWFpbjpjZG5pbnN0YWdyYW0uY29tIiwiZ2Vvc2l0ZTpkaXNjb3JkIiwiZG9tYWluOmRpc2NvcmQuZ2ciLCJnZW9zaXRlOndoYXRzYXBwIiwiZG9tYWluOndhLm1lIiwiZ2Vvc2l0ZTp0d2l0dGVyIiwiZG9tYWluOnguY29tIiwiZG9tYWluOnR3aW1nLmNvbSIsImdlb3NpdGU6ZmFjZWJvb2siLCJkb21haW46bWVzc2VuZ2VyLmNvbSIsImdlb3NpdGU6c2lnbmFsIiwiZG9tYWluOnRleHRzZWN1cmUuY29tIiwiZ2Vvc2l0ZTpsaW5rZWRpbiIsImRvbWFpbjpzbmFwY2hhdC5jb20iLCJkb21haW46c25hcC5jb20iLCJkb21haW46c2MtY2RuLm5ldCIsImRvbWFpbjpmYWNldGltZS5hcHBsZS5jb20iLCJkb21haW46ZnRhcGkuaXR1bmVzLmFwcGxlLmNvbSIsImRvbWFpbjpwdXNoLmFwcGxlLmNvbSIsImdlb3NpdGU6dmliZXIiLCJnZW9zaXRlOm5ldGZsaXgiLCJnZW9zaXRlOnNwb3RpZnkiLCJnZW9zaXRlOnN0ZWFtIiwiZ2Vvc2l0ZTpvcGVuYWkiLCJkb21haW46Z2VtaW5pLmdvb2dsZS5jb20iLCJnZW9zaXRlOmFudGhyb3BpYyIsImRvbWFpbjptaWRqb3VybmV5LmNvbSIsImRvbWFpbjpkZWVwbC5jb20iLCJnZW9zaXRlOmNhbnZhIiwiZ2Vvc2l0ZTpub3Rpb24iLCJkb21haW46bWlyby5jb20iLCJnZW9zaXRlOnBsYXlzdGF0aW9uIiwiZ2Vvc2l0ZTpuaW50ZW5kbyIsImdlb3NpdGU6YmxpenphcmQiLCJnZW9zaXRlOmRpc25leSIsImdlb3NpdGU6Y291cnNlcmEiLCJnZW9zaXRlOmFpcmJuYiIsImdlb3NpdGU6Ym9va2luZyIsImRvbWFpbjpwYXJhbW91bnRwbHVzLmNvbSIsImRvbWFpbjpwYXJhbW91bnQuY29tIiwiZG9tYWluOnVuaXZlcnNhbHBsdXMuY29tIiwiZG9tYWluOnVuaXZlcnNhbC1wbHVzLmZyIiwiZ2Vvc2l0ZTp1Ymlzb2Z0IiwiZ2Vvc2l0ZTplYSJdLCJQcm94eUlwIjpbIjE0OS4xNTQuMTYwLjAvMjAiLCI5MS4xMDguNC4wLzIwIiwiOTEuMTA4LjE2LjAvMjIiLCI5MS4xMDguNTYuMC8yMiIsIjk1LjE2MS42NC4wLzIwIiwiMjAwMTo2N2M6NGU4OjovNDgiLCIyMDAxOmIyODpmMjNkOjovNDgiLCIyMDAxOmIyODpmMjNmOjovNDgiXSwiQmxvY2tTaXRlcyI6W10sIkJsb2NrSXAiOltdfQ==
```

### Option B — via QR code
1. The QR code is **at the top of this guide** (or a separate file `incy-routing-qr.png`).
2. Open INCY → QR scanning feature (camera) → point it at the QR.
3. The profile is added and activated.

### Option C — via clipboard
Copy the link from option A (or just the base64 part after `incy://routing/onadd/`) → in INCY add a routing profile from the clipboard.

> Routing profiles are visible in INCY settings (the "Routing" section) — you can enable/disable them there.

## Step 4. Verify everything works

1. Connect the VPN in INCY (big button).
2. Open Telegram, Instagram, YouTube, Discord, WhatsApp, X — they should work (including if they were blocked before).
3. Check your IP:
   - in **Safari** open, e.g., `2ip.ru` → your **local** IP should show (direct);
   - in Telegram ask the `@ip_bot` bot (or open the same site inside an app that goes through the VPN) → the **VPN server** IP should show.
4. Other apps (VK, Yandex, your bank, etc.) work as usual — direct.

> Routing only applies while the INCY VPN is connected. Disconnect the VPN and everything works as if there were no VPN.

---

## What exactly is in the profile (34 services)

**Social networks & messengers:**

| Service | Rules (geosite category + explicit domains) |
|---|---|
| Telegram | `geosite:telegram` (incl. tg.dev, telesco.pe), t.me, telegram.org **+ DC IP ranges in `ProxyIp`** |
| Instagram | `geosite:instagram`, cdninstagram.com |
| X / Twitter | `geosite:twitter` (incl. x.com, twimg.com) |
| Facebook / Messenger | `geosite:facebook` (fb.com, fbsbx.com, fbcdn.net…), messenger.com |
| Signal | `geosite:signal`, textsecure.com (not in the dlc list — added explicitly) |
| LinkedIn | `geosite:linkedin` (licdn.com, lnkd.in…) |
| Snapchat | snapchat.com, snap.com, sc-cdn.net (no dlc category — explicit domains) |
| Discord | `geosite:discord` (incl. CDN discordapp.net), discord.gg |
| WhatsApp | `geosite:whatsapp` (whatsapp.com, whatsapp.net, wa.me) |
| Viber | `geosite:viber` (viber.com, vbcdn…) |

**Video & music:**

| Service | Rules (geosite category + explicit domains) |
|---|---|
| YouTube | `geosite:youtube` (incl. googlevideo.com, ytimg.com) |
| Netflix | `geosite:netflix` (nflxvideo.net, nflximg…) |
| Spotify | `geosite:spotify` (scdn.co, pscdn.co…) |

**Calls:**

| Service | Rules (geosite category + explicit domains) |
|---|---|
| FaceTime | facetime.apple.com, ftapi.itunes.apple.com, push.apple.com (APNs) — see [below](#facetime-an-important-nuance) |

**Games:**

| Service | Rules (geosite category + explicit domains) |
|---|---|
| Steam | `geosite:steam` (steampowered.com, steamcontent…) |
| PlayStation Network | `geosite:playstation` (all *.playstation + sonyentertainmentnetwork.com) |
| Nintendo eShop | `geosite:nintendo` (nintendo.com, co.jp — the eShop is on the same domains) |
| Battle.net (Blizzard) | `geosite:blizzard` (battle.net, blizzard.com) |
| Ubisoft | `geosite:ubisoft` (ubi.com, ubisoft.com) |
| EA | `geosite:ea` (213 domains, ea.com…) |

**AI & text:**

| Service | Rules (geosite category + explicit domains) |
|---|---|
| OpenAI (ChatGPT) | `geosite:openai` (chatgpt.com, sora.com…) |
| Google Gemini | `domain:gemini.google.com` (no dlc category — added explicitly; the whole google.com is left alone) |
| Anthropic (Claude) | `geosite:anthropic` (claude.ai, anthropic.com) |
| Midjourney | `domain:midjourney.com` (no dlc category; the Discord bot is already covered by `geosite:discord`) |
| DeepL | `domain:deepl.com` (no dlc category) |

**Work & education:**

| Service | Rules (geosite category + explicit domains) |
|---|---|
| Canva | `geosite:canva` |
| Notion | `geosite:notion` (notion.so, notion.site…) |
| Miro | `domain:miro.com` (no dlc category) |
| Coursera | `geosite:coursera` |

**Streaming:**

| Service | Rules (geosite category + explicit domains) |
|---|---|
| Disney+ | `geosite:disney` (154 domains, incl. disneyplus.com, hulu, hotstar) |
| Paramount+ | `domain:paramountplus.com`, `domain:paramount.com` (no dlc category) |
| Universal+ (Universal Pictures) | `domain:universalplus.com`, `domain:universal-plus.fr` (no dlc category) |

**Travel:**

| Service | Rules (geosite category + explicit domains) |
|---|---|
| Airbnb | `geosite:airbnb` (86 domains) |
| Booking | `geosite:booking` (booking.com, bstatic.com) |

**IP rules (`ProxyIp`) — Telegram only:**
`149.154.160.0/20`, `91.108.4.0/20`, `91.108.16.0/22`, `91.108.56.0/22`, `95.161.64.0/20` (IPv4) + `2001:67c:4e8::/48`, `2001:b28:f23d::/48`, `2001:b28:f23f::/48` (IPv6, optional).

They are needed because Telegram for iOS connects to its servers (DCs) **by IP addresses hardcoded in the code**, not only by domains — without these ranges the app cannot sync. The ranges were cross-checked against [iplocate.io](https://iplocate.io/data/hosting-providers/telegram-org) and [v2rayN issue #5234](https://github.com/2dust/v2rayN/issues/5234).

---

## FaceTime: an important nuance

FaceTime consists of three parts, and they are routed differently:

1. **Signaling** (call setup): `facetime.apple.com`, `ftapi.itunes.apple.com` and **APNs** (`push.apple.com`) — these domains go **through the VPN**. It is their blocking that breaks calls (in Russia FaceTime was blocked in December 2025 — when you try to call, "User unavailable" appears).
2. **Media** (the actual audio/video): goes P2P between devices or through Apple's TURN relays in the `17.0.0.0/8` range — these are "raw" IPs without domains, so they stay **direct**. This is deliberate: per community experience, FaceTime breaks when 17.0.0.0/8 is routed *through* the VPN, and works when direct.
3. **Side effect:** `push.apple.com` is Apple's general push server, so **all** Apple pushes (Mail, Calendar, iMessage) will go through the VPN. In Russia this is rather a plus: APNs was also blocked, and that broke iMessage/FaceTime.

## Fragmentation & noises — should you enable them?

These are settings of **the tunnel itself** (server settings in INCY), not routing:

- **Fragmentation** — splits the tunnel's ClientHello (TLS handshake) into small packets so DPI doesn't recognize the VPN protocol;
- **Noises** — sends random UDP packets before the handshake so the traffic doesn't look like a "clean" VPN. Per INCY docs, mainly relevant for **WireGuard and Hysteria2** on networks with deep inspection.

**Conclusion:**
- By default both are **off — and that's correct**. If they broke the connection, *all* services would fail at once. If only one service (e.g., Telegram) fails while others work — the problem is routing (check the profile rules), not tunnel settings.
- Enable them **only if the tunnel itself is unstable**: the server drops, won't connect on a certain network (carrier Wi-Fi), Hysteria2/WireGuard is "seen" by DPI. Then enable fragmentation (and/or noises) in the specific server's settings and re-check.
- If you enabled them — verify that *all* services work; if something broke, turn them back off.

---

## Profile JSON (if you want to edit it)

```json
{
  "Name": "Socials via VPN",
  "GlobalProxy": "false",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://cloudflare-dns.com/dns-query",
  "RemoteDNSIP": "1.1.1.1",
  "DomesticDNSType": "DoU",
  "DomesticDNSIP": "8.8.8.8",
  "FakeDNS": "false",
  "DomainStrategy": "IPIfNonMatch",
  "DirectSites": ["geosite:private"],
  "DirectIp": ["geoip:private", "10.0.0.0/8", "172.16.0.0/12", "192.168.0.0/16", "169.254.0.0/8", "224.0.0.0/4"],
  "ProxySites": [
    "geosite:telegram", "domain:t.me", "domain:telegram.org",
    "geosite:youtube", "domain:googlevideo.com",
    "geosite:instagram", "domain:cdninstagram.com",
    "geosite:discord", "domain:discord.gg",
    "geosite:whatsapp", "domain:wa.me",
    "geosite:twitter", "domain:x.com", "domain:twimg.com",
    "geosite:facebook", "domain:messenger.com",
    "geosite:signal", "domain:textsecure.com",
    "geosite:linkedin",
    "domain:snapchat.com", "domain:snap.com", "domain:sc-cdn.net",
    "domain:facetime.apple.com", "domain:ftapi.itunes.apple.com", "domain:push.apple.com",
    "geosite:viber",
    "geosite:netflix",
    "geosite:spotify",
    "geosite:steam",
    "geosite:openai", "domain:gemini.google.com", "geosite:anthropic",
    "domain:midjourney.com", "domain:deepl.com", "geosite:canva",
    "geosite:notion", "domain:miro.com", "geosite:playstation",
    "geosite:nintendo", "geosite:blizzard", "geosite:disney",
    "geosite:coursera", "geosite:airbnb", "geosite:booking",
    "domain:paramountplus.com", "domain:paramount.com",
    "domain:universalplus.com", "domain:universal-plus.fr",
    "geosite:ubisoft", "geosite:ea"
  ],
  "ProxyIp": [
    "149.154.160.0/20",
    "91.108.4.0/20",
    "91.108.16.0/22",
    "91.108.56.0/22",
    "95.161.64.0/20",
    "2001:67c:4e8::/48",
    "2001:b28:f23d::/48",
    "2001:b28:f23f::/48"
  ],
  "BlockSites": [],
  "BlockIp": []
}
```

To add another service — append its domain to `ProxySites` (e.g., `"domain:tiktok.com"`), encode the JSON in base64 and open `incy://routing/onadd/{base64}`.

---

## If something doesn't work

| Problem | Solution |
|---|---|
| Telegram stuck on "updating" | Restart the app; make sure the VPN is connected and the profile is active (the "Routing" section) |
| A service doesn't go through the VPN (e.g., WhatsApp) | Add its domains to the profile's `ProxySites` and re-import |
| FaceTime: "User unavailable" / call doesn't connect | Signaling already goes through the VPN; if that didn't help — try a different server/protocol (the carrier may block by IP too) |
| FaceTime: call drops or no audio | This is media traffic (P2P/TURN 17.0.0.0/8) — it goes direct, by design; try a different Wi-Fi or mobile data |
| Some direct sites behave oddly (DNS) | In the profile, replace `DomesticDNSIP` from `8.8.8.8` with your provider's DNS |
| The profile shows a red "!" in the list | Geo files are being downloaded — wait a minute, or delete and re-add the profile |
| You want "everything through VPN" back | Open `incy://routing/off` (the profile is kept, you can re-enable it) |
| You want "everything direct" with no VPN at all | Just disconnect the VPN in INCY |

## Sources
- Official site and docs: [incy.cc](https://incy.cc/), [docs.incy.cc/routing](https://docs.incy.cc/routing)
- GitHub (feature list, per-app — Android only): [INCY-DEV/incy-platforms](https://github.com/INCY-DEV/incy-platforms)
- INCY setup guide: [tainet.pro/blog/incy-setup-guide](https://tainet.pro/blog/incy-setup-guide)
- Domain lists: [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
- Telegram IP ranges: [iplocate.io](https://iplocate.io/data/hosting-providers/telegram-org), [v2rayN issue #5234](https://github.com/2dust/v2rayN/issues/5234)
- How FaceTime works (APNs, STUN/TURN): [Apple Security Guide](https://support.apple.com/guide/security/facetime-security-seca331c55cd/web), [matduggan.com](https://matduggan.com/how-does-facetime-work/)
- FaceTime blocking in Russia: [Reuters](https://www.reuters.com/business/retail-consumer/russia-imposes-restrictions-apples-facetime-app-agencies-say-2025-12-04/)
