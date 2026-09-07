# INCY на iPhone: 34 сервиса через VPN, всё остальное — без

<p align="center">
  <img src="incy-routing-qr.png" width="360" alt="QR — импорт профиля маршрутизации v3 в INCY">
</p>

**Сканируй этот QR камерой INCY — профиль «Socials via VPN» v3 добавится и сразу активируется.** Подробности — в [Шаге 3](#шаг-3-добавь-готовый-профиль-маршрутизации-ключевой-шаг) ниже.

## ⚠️ Важный нюанс (прочитай сначала)

В INCY **на iPhone нет выбора отдельных приложений** — функция «Per-app proxy» (включить VPN только для выбранных приложений) доступна **только в Android-версии**. Это ограничение самой Apple: iOS не даёт VPN-приложениям маршрутизировать трафик по приложениям.

**Решение для iPhone — профиль маршрутизации (routing profile):**
по умолчанию весь трафик идёт напрямую, а только домены и IP-адреса нужных сервисов уходят через VPN.

Чем это отличается от per-app:
- маршрутизация идёт **по доменам и IP, а не по приложениям**;
- если открыть YouTube в Safari — этот трафик тоже пойдёт через VPN (это нормально);
- если какое-то другое приложение подключается к x.com или discord.com — оно тоже уйдёт через VPN.

Практический результат тот же: нужные сервисы работают через VPN (в т.ч. при блокировках), а все остальные приложения — напрямую, без VPN.

**В этой версии (v3):**
- добавлено 19 сервисов: OpenAI (ChatGPT), Google Gemini, Anthropic (Claude), Midjourney, DeepL, Canva, Notion, Miro, PlayStation Network, Nintendo eShop, Battle.net (Blizzard), Disney+, Paramount+, Universal+ (Universal Pictures), Ubisoft, EA, Coursera, Airbnb, Booking;
- всё из v2 сохранено: 15 сервисов (Telegram…Steam), фикс Telegram «updating» (IP-диапазоны DC в `ProxyIp`), раздел про фрагментирование и noises.

> Примечания: «Universal Pictures» интерпретирован как стриминговый сервис **Universal+** (у киностудии отдельного пользовательского сервиса нет); `geosite:disney` включает не только Disney+, но и Hulu/Hotstar; Battle.net — это категория `geosite:blizzard` (battle.net, blizzard.com).

---

## Шаг 1. Установи INCY

- App Store → поиск «**incy**» → разработчик **LLC ITDEV**.
- Приложение бесплатное, доступно в российском регионе App Store (менять регион не нужно).

## Шаг 2. Добавь подписку (сервер)

INCY сам серверы не предоставляет — нужна твоя собственная подписка/ключ от провайдера (VLESS, VMess, Trojan, Hysteria2 и т.д.).

1. Открой INCY → нажми «**+**» → «**Добавить подписку**» (Import from URL).
2. Вставь ссылку на свою подписку (или отсканируй QR-код).
3. Когда iOS попросит разрешение на установку VPN-профиля — **разреши** (спросит один раз).
4. Выбери сервер и нажми большую кнопку подключения — убедись, что VPN подключается.

## Шаг 3. Добавь готовый профиль маршрутизации (ключевой шаг)

Я подготовил готовый профиль **«Socials via VPN» v3**:
- `GlobalProxy = false` → всё, что не совпало с правилами, идёт **напрямую**;
- в `ProxySites` — правила для 34 сервисов (50 записей) → они идут **через VPN**;
- в `ProxyIp` — IP-диапазоны серверов Telegram (DC1–DC5) → они тоже идут **через VPN** (это фикс «updating»).

> Если ты уже импортировал старую версию профиля — сначала удали её (настройки INCY → «Маршрутизация» / Routing), затем импортируй новую.

### Вариант А — по ссылке (рекомендую)
1. Скопируй ссылку ниже целиком (выдели всё).
2. Вставь её в адресную строку **Safari** на iPhone и открой.
3. iOS предложит открыть приложение INCY → подтверди.
4. Профиль добавится и **сразу активируется**.

```
incy://routing/onadd/eyJOYW1lIjoiU29jaWFscyB2aWEgVlBOIiwiR2xvYmFsUHJveHkiOiJmYWxzZSIsIlJlbW90ZUROU1R5cGUiOiJEb0giLCJSZW1vdGVETlNEb21haW4iOiJodHRwczovL2Nsb3VkZmxhcmUtZG5zLmNvbS9kbnMtcXVlcnkiLCJSZW1vdGVETlNJUCI6IjEuMS4xLjEiLCJEb21lc3RpY0ROU1R5cGUiOiJEb1UiLCJEb21lc3RpY0ROU0lQIjoiOC44LjguOCIsIkZha2VETnMiOiJmYWxzZSIsIkRvbWFpblN0cmF0ZWd5IjoiSVBJZk5vbk1hdGNoIiwiRGlyZWN0U2l0ZXMiOlsiZ2Vvc2l0ZTpwcml2YXRlIl0sIkRpcmVjdElwIjpbImdlb2lwOnByaXZhdGUiLCIxMC4wLjAuMC84IiwiMTcyLjE2LjAuMC8xMiIsIjE5Mi4xNjguMC4wLzE2IiwiMTY5LjI1NC4wLjAvOCIsIjIyNC4wLjAuMC80Il0sIlByb3h5U2l0ZXMiOlsiZ2Vvc2l0ZTp0ZWxlZ3JhbSIsImRvbWFpbjp0Lm1lIiwiZG9tYWluOnRlbGVncmFtLm9yZyIsImdlb3NpdGU6eW91dHViZSIsImRvbWFpbjpnb29nbGV2aWRlby5jb20iLCJnZW9zaXRlOmluc3RhZ3JhbSIsImRvbWFpbjpjZG5pbnN0YWdyYW0uY29tIiwiZ2Vvc2l0ZTpkaXNjb3JkIiwiZG9tYWluOmRpc2NvcmQuZ2ciLCJnZW9zaXRlOndoYXRzYXBwIiwiZG9tYWluOndhLm1lIiwiZ2Vvc2l0ZTp0d2l0dGVyIiwiZG9tYWluOnguY29tIiwiZG9tYWluOnR3aW1nLmNvbSIsImdlb3NpdGU6ZmFjZWJvb2siLCJkb21haW46bWVzc2VuZ2VyLmNvbSIsImdlb3NpdGU6c2lnbmFsIiwiZG9tYWluOnRleHRzZWN1cmUuY29tIiwiZ2Vvc2l0ZTpsaW5rZWRpbiIsImRvbWFpbjpzbmFwY2hhdC5jb20iLCJkb21haW46c25hcC5jb20iLCJkb21haW46c2MtY2RuLm5ldCIsImRvbWFpbjpmYWNldGltZS5hcHBsZS5jb20iLCJkb21haW46ZnRhcGkuaXR1bmVzLmFwcGxlLmNvbSIsImRvbWFpbjpwdXNoLmFwcGxlLmNvbSIsImdlb3NpdGU6dmliZXIiLCJnZW9zaXRlOm5ldGZsaXgiLCJnZW9zaXRlOnNwb3RpZnkiLCJnZW9zaXRlOnN0ZWFtIiwiZ2Vvc2l0ZTpvcGVuYWkiLCJkb21haW46Z2VtaW5pLmdvb2dsZS5jb20iLCJnZW9zaXRlOmFudGhyb3BpYyIsImRvbWFpbjptaWRqb3VybmV5LmNvbSIsImRvbWFpbjpkZWVwbC5jb20iLCJnZW9zaXRlOmNhbnZhIiwiZ2Vvc2l0ZTpub3Rpb24iLCJkb21haW46bWlyby5jb20iLCJnZW9zaXRlOnBsYXlzdGF0aW9uIiwiZ2Vvc2l0ZTpuaW50ZW5kbyIsImdlb3NpdGU6YmxpenphcmQiLCJnZW9zaXRlOmRpc25leSIsImdlb3NpdGU6Y291cnNlcmEiLCJnZW9zaXRlOmFpcmJuYiIsImdlb3NpdGU6Ym9va2luZyIsImRvbWFpbjpwYXJhbW91bnRwbHVzLmNvbSIsImRvbWFpbjpwYXJhbW91bnQuY29tIiwiZG9tYWluOnVuaXZlcnNhbHBsdXMuY29tIiwiZG9tYWluOnVuaXZlcnNhbC1wbHVzLmZyIiwiZ2Vvc2l0ZTp1Ymlzb2Z0IiwiZ2Vvc2l0ZTplYSJdLCJQcm94eUlwIjpbIjE0OS4xNTQuMTYwLjAvMjAiLCI5MS4xMDguNC4wLzIwIiwiOTEuMTA4LjE2LjAvMjIiLCI5MS4xMDguNTYuMC8yMiIsIjk1LjE2MS42NC4wLzIwIiwiMjAwMTo2N2M6NGU4OjovNDgiLCIyMDAxOmIyODpmMjNkOjovNDgiLCIyMDAxOmIyODpmMjNmOjovNDgiXSwiQmxvY2tTaXRlcyI6W10sIkJsb2NrSXAiOltdfQ==
```

### Вариант Б — по QR-коду
1. QR-код есть **в начале этой инструкции** (или отдельный файл `incy-routing-qr.png`).
2. Открой INCY → функция сканирования QR (камера) → наведи на QR.
3. Профиль добавится и активируется.

### Вариант В — через буфер обмена
Скопируй ссылку из варианта А (или только base64-часть после `incy://routing/onadd/`) → в INCY добавь профиль маршрутизации из буфера обмена.

> Профили маршрутизации в INCY видны в настройках приложения (раздел «Маршрутизация» / Routing profiles) — там же их можно включать/выключать.

## Шаг 4. Проверь, что всё работает

1. Подключи VPN в INCY (большая кнопка).
2. Открой Telegram, Instagram, YouTube, Discord, WhatsApp, X — они должны работать (в т.ч. если раньше были заблокированы).
3. Проверь IP:
   - в **Safari** открой, например, `2ip.ru` → должен показаться твой **локальный** IP (напрямую);
   - в Telegram спроси у бота `@ip_bot` (или открой тот же сайт внутри приложения, которое идёт через VPN) → должен показаться IP **сервера VPN**.
4. Остальные приложения (VK, Яндекс, банк и т.д.) работают как обычно — напрямую.

> Маршрутизация действует только пока VPN в INCY подключён. Отключишь VPN — всё работает как без него.

---

## Что именно входит в профиль (v3, 34 сервиса)

**Соцсети и мессенджеры:**

| Сервис | Правила (geosite-категория + явные домены) |
|---|---|
| Telegram | `geosite:telegram` (включая tg.dev, telesco.pe), t.me, telegram.org **+ IP-диапазоны DC в `ProxyIp`** |
| Instagram | `geosite:instagram`, cdninstagram.com |
| X / Twitter | `geosite:twitter` (включая x.com, twimg.com) |
| Facebook / Messenger | `geosite:facebook` (fb.com, fbsbx.com, fbcdn.net…), messenger.com |
| Signal | `geosite:signal`, textsecure.com (в списке dlc его нет — добавлен явно) |
| LinkedIn | `geosite:linkedin` (licdn.com, lnkd.in…) |
| Snapchat | snapchat.com, snap.com, sc-cdn.net (категории в dlc нет — домены явные) |
| Discord | `geosite:discord` (включая CDN discordapp.net), discord.gg |
| WhatsApp | `geosite:whatsapp` (whatsapp.com, whatsapp.net, wa.me) |
| Viber | `geosite:viber` (viber.com, vbcdn…) |

**Видео и музыка:**

| Сервис | Правила (geosite-категория + явные домены) |
|---|---|
| YouTube | `geosite:youtube` (включая googlevideo.com, ytimg.com) |
| Netflix | `geosite:netflix` (nflxvideo.net, nflximg…) |
| Spotify | `geosite:spotify` (scdn.co, pscdn.co…) |

**Звонки:**

| Сервис | Правила (geosite-категория + явные домены) |
|---|---|
| FaceTime | facetime.apple.com, ftapi.itunes.apple.com, push.apple.com (APNs) — см. [ниже](#facetime-важно-понять-нюанс) |

**Игры:**

| Сервис | Правила (geosite-категория + явные домены) |
|---|---|
| Steam | `geosite:steam` (steampowered.com, steamcontent…) |
| PlayStation Network | `geosite:playstation` (все *.playstation + sonyentertainmentnetwork.com) |
| Nintendo eShop | `geosite:nintendo` (nintendo.com, co.jp — eShop на тех же доменах) |
| Battle.net (Blizzard) | `geosite:blizzard` (battle.net, blizzard.com) |
| Ubisoft | `geosite:ubisoft` (ubi.com, ubisoft.com) |
| EA | `geosite:ea` (213 доменов, ea.com…) |

**AI и тексты:**

| Сервис | Правила (geosite-категория + явные домены) |
|---|---|
| OpenAI (ChatGPT) | `geosite:openai` (chatgpt.com, sora.com…) |
| Google Gemini | `domain:gemini.google.com` (категории в dlc нет — добавлен явно; весь google.com не трогаем) |
| Anthropic (Claude) | `geosite:anthropic` (claude.ai, anthropic.com) |
| Midjourney | `domain:midjourney.com` (категории в dlc нет; Discord-бот уже покрыт `geosite:discord`) |
| DeepL | `domain:deepl.com` (категории в dlc нет) |

**Работа и образование:**

| Сервис | Правила (geosite-категория + явные домены) |
|---|---|
| Canva | `geosite:canva` |
| Notion | `geosite:notion` (notion.so, notion.site…) |
| Miro | `domain:miro.com` (категории в dlc нет) |
| Coursera | `geosite:coursera` |

**Стриминг:**

| Сервис | Правила (geosite-категория + явные домены) |
|---|---|
| Disney+ | `geosite:disney` (154 домена, включая disneyplus.com, hulu, hotstar) |
| Paramount+ | `domain:paramountplus.com`, `domain:paramount.com` (категории в dlc нет) |
| Universal+ (Universal Pictures) | `domain:universalplus.com`, `domain:universal-plus.fr` (категории в dlc нет) |

**Путешествия:**

| Сервис | Правила (geosite-категория + явные домены) |
|---|---|
| Airbnb | `geosite:airbnb` (86 доменов) |
| Booking | `geosite:booking` (booking.com, bstatic.com) |

**IP-правила (`ProxyIp`) — только для Telegram:**
`149.154.160.0/20`, `91.108.4.0/20`, `91.108.16.0/22`, `91.108.56.0/22`, `95.161.64.0/20` (IPv4) + `2001:67c:4e8::/48`, `2001:b28:f23d::/48`, `2001:b28:f23f::/48` (IPv6, опционально).

---

## Почему Telegram висел на «updating»

Приложение Telegram для iOS подключается к серверам (DC) **по жёстко заданным в коде IP-адресам**, а не только по доменам. В профиле v1 были учтены лишь домены (`geosite:telegram`), поэтому:

- DNS-запросы и часть трафика по доменам уходили через VPN;
- но прямые TCP/TLS-соединения к IP серверов DC (149.154.x, 91.108.x, 95.161.x) **не попадали ни под одно правило** → при `GlobalProxy=false` шли напрямую → блокировались;
- в итоге приложение «видело» сеть, но не могло синхронизироваться → вечный «updating».

**Фикс:** диапазоны IP всех пяти DC Telegram добавлены в `ProxyIp` — теперь эти соединения тоже идут через VPN. Списки диапазонов сверены с данными [iplocate.io](https://iplocate.io/data/hosting-providers/telegram-org) и [v2rayN issue #5234](https://github.com/2dust/v2rayN/issues/5234).

> Если после импорта v2 Telegram всё ещё «updating» — перезапусти приложение (оно может кэшировать старые соединения) и проверь, что VPN в INCY подключён.

## FaceTime: важно понять нюанс

FaceTime устроен из трёх частей, и маршрутизируются они по-разному:

1. **Сигналинг** (установка звонка): `facetime.apple.com`, `ftapi.itunes.apple.com` и **APNs** (`push.apple.com`) — эти домены уходят **через VPN**. Именно их блокировки ломают звонки (в России FaceTime заблокировали в декабре 2025 — при попытке звонка появляется «User unavailable»).
2. **Медиа** (сам звук/видео): идёт P2P между устройствами или через TURN-реле Apple в диапазоне `17.0.0.0/8` — это «сырые» IP без доменов, поэтому они остаются **напрямую**. Это осознанно: по опыту сообщества, FaceTime ломается, когда 17.0.0.0/8 гоняют *через* VPN, а напрямую — работает.
3. **Побочный эффект:** `push.apple.com` — это общий push-сервер Apple, так что через VPN пойдут **все** пуши Apple (Mail, Календарь, iMessage). В России это скорее плюс: APNs тоже блокировался, и из-за этого ломались iMessage/FaceTime.

## Фрагментирование (fragmentation) и noises — включать?

Это настройки **самого туннеля** (настройки сервера в INCY), а не маршрутизации:

- **Fragmentation** — режет ClientHello (TLS-рукопожатие) туннеля на мелкие пакеты, чтобы DPI не распознал протокол VPN;
- **Noises** — отправляет случайные UDP-пакеты перед handshake, чтобы трафик не выглядел «чистым» VPN. По документации INCY актуально в основном для **WireGuard и Hysteria2** в сетях с глубоким инспектором.

**Вывод:**
- По умолчанию оба **выключены — и так правильно**. Если бы они ломали соединение, падали бы *все* сервисы сразу, а не только Telegram. Твоя проблема с Telegram — это маршрутизация (фикс в v2), а не туннель.
- Включай их **только если сам туннель нестабилен**: сервер отваливается, не подключается в определённой сети (Wi-Fi оператора), Hysteria2/WireGuard «видит» DPI. Тогда включи fragmentation (и/или noises) в настройках конкретного сервера и перепроверь.
- Если включил — проверь, что *все* сервисы работают; если что-то сломалось — отключи обратно.

---

## JSON профиля (если захочешь отредактировать)

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

Чтобы добавить ещё сервис — допиши его домен в `ProxySites` (например, `"domain:tiktok.com"`), закодируй JSON в base64 и открой ссылку `incy://routing/onadd/{base64}`.

---

## Если что-то не работает

| Проблема | Решение |
|---|---|
| Telegram всё ещё «updating» после v2 | Перезапусти приложение; убедись, что VPN подключён и профиль активен (раздел «Маршрутизация») |
| Сервис не идёт через VPN (например, WhatsApp) | Добавь его домены в `ProxySites` профиля и импортируй заново |
| FaceTime: «User unavailable» / звонок не устанавливается | Сигналинг уже через VPN; если не помогло — попробуй другой сервер/протокол (возможно, оператор блокирует и по IP) |
| FaceTime: звонок обрывается или без звука | Это медиа-трафик (P2P/TURN 17.0.0.0/8) — он идёт напрямую, так и задумано; попробуй другой Wi-Fi или мобильные данные |
| Некоторые прямые сайты ведут себя странно (DNS) | В профиле замени `DomesticDNSIP` с `8.8.8.8` на DNS твоего провайдера |
| У профиля красный «!» в списке | Идут геофайлы — подожди минуту или удали профиль и добавь заново |
| Хочешь вернуть «всё через VPN» | Открой ссылку `incy://routing/off` (профиль сохранится, можно включить обратно) |
| Хочешь «всё напрямую» вообще без VPN | Просто отключи VPN в INCY |

## Источники
- Официальный сайт и документация: [incy.cc](https://incy.cc/), [docs.incy.cc/routing](https://docs.incy.cc/routing)
- GitHub (список функций, per-app — только Android): [INCY-DEV/incy-platforms](https://github.com/INCY-DEV/incy-platforms)
- Гайд по установке INCY: [tainet.pro/blog/incy-setup-guide](https://tainet.pro/blog/incy-setup-guide)
- Списки доменов: [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
- IP-диапазоны Telegram: [iplocate.io](https://iplocate.io/data/hosting-providers/telegram-org), [v2rayN issue #5234](https://github.com/2dust/v2rayN/issues/5234)
- Как устроен FaceTime (APNs, STUN/TURN): [Apple Security Guide](https://support.apple.com/guide/security/facetime-security-seca331c55cd/web), [matduggan.com](https://matduggan.com/how-does-facetime-work/)
- Блокировка FaceTime в России: [Reuters](https://www.reuters.com/business/retail-consumer/russia-imposes-restrictions-apples-facetime-app-agencies-say-2025-12-04/)
