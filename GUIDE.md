# ГАЙД — Transcendencies Vault

Карточка для Discord. Весь сайт = один файл `index.html`. Здесь: что где менять,
как работают уведомления и как привязать к Discord.

## Где что менять (всё в `index.html`, БЛОК 1 вверху скрипта)

| Что | Где | Как |
|---|---|---|
| **Аватар** | файл `avatar.jpg` в корне репо | заменить файл (имя не менять) — ава стоит в лого, профиле, комментах, уведомлениях |
| **Описание (био)** | `PROFILE.bio` | текст в кавычках |
| Ник / @юз / «в Vault с» | `PROFILE.user` / `.handle` / `.since` | текст в кавычках |
| Название сайта / вкладки / подвала | `SITE.name` / `.title` / `.footerTitle` | текст |
| **Картинка поста** | `POSTS[0].img` | `"post.jpg"` (файл в репо) или внешняя ссылка |
| Название поста / **описание поста** | `POSTS[0].title` / `.desc` | `.desc` = текст под постом (пусто = не показывается) |
| **Теги** | `POSTS[0].tags` | `"слово"` = синий; `"слово=pink"` = розовый (ещё `green` / `red` / `teal` / `gray`) |
| ♥ / просмотры | `POSTS[0].rating` / `.views` | число (1111) ИЛИ текст в кавычках (`"многа"`) |
| Ссылка под постом | `POSTS[0].source` | текст/ссылка |
| **Комменты под постом** | `POSTS[0].comments` | `{ user: "Transcendencies", text: "текст", when: "now", likes: 0 }` |
| Треки (вкладка History) | `TRACKS` | строка на трек; ID клипа — после `watch?v=` в ютуб-ссылке: `img: "https://i.ytimg.com/vi/ID/hqdefault.jpg"`, `src: "https://www.youtube.com/watch?v=ID"` |
| Плейлисты | `PLAYLISTS` | `{ name: "имя", items: 5, likes: 0, comments: 0, members: 0 }` |
| Цвета сайта | `:root` в самом верху файла | `--toolbar` = фиолетовая шапка/подвал, `--primary` = акцент, `--tag-*` = цвета тегов |
| **Discord вебхук** | `DISCORD_WEBHOOK` | ссылка из Discord (см. ниже) |

Та же шпаргалка вынесена блоком наверх самого `index.html` (КАСТОМИЗАЦИЯ).

## Как работают кнопки и уведомления

- **Колокольчик** (справа сверху) = панель уведомлений, как в Discord.
- Кнопки в **подвале** (NO Contact us / Terms of Service / MDMA / Discord) —
  добавляют «Transcendencies: иди нахуй» в колокольчик (бейдж +1).
- Боковое меню (Home, Best posts, Hot, …), аватар в шапке —
  тост «Transcendencies: иди нахуй».
- **Upgrade Account** (внизу бокового меню) — открывает
  [donorschoose.org](https://www.donorschoose.org/) (благотворительность).
- Пост в Bookmarks — не кликабельный; коммент виден прямо под постом.

## Привязка к Discord (пока ждём is-a.dev)

Адрес для профиля Discord прямо сейчас: **`https://facich.github.io/transcendencies/`**
(SOAP-карточка подтянется сама из preview.png).

Чтобы «иди нахуй» прилетало ещё и в твой канал Discord:
1. Discord → свой сервер → любой канал → ⚙ (настройки канала) →
   **Интеграции → Webhooks → New Webhook**.
2. Имя вебхука: `Transcendencies`, аватар — свою кошку.
3. **Copy Webhook URL**.
4. В `index.html` (БЛОК 1) вставить в кавычки: `const DISCORD_WEBHOOK = "https://discord.com/api/webhooks/…";`

После этого каждый клик по кнопке в подвале = сообщение
**Transcendencies: иди нахуй** в твоём канале. Пока вебхук не вставлен —
уведомления работают только на сайте.

## Домен

- Сейчас: `https://facich.github.io/transcendencies/`
- Потом: `transcendencies.is-a.dev` — PR #60585 ждёт мерджа мейнтером.
  После мерджа: Settings → Pages → Custom domain: `transcendencies.is-a.dev`
  + галка Enforce HTTPS. Вебхук после смены домена менять не надо.

## Как применить изменения

- **Сайтом (проще всего):** github.com/facich/transcendencies → кликнуть файл →
  карандаш ✏️ сверху → править → **Commit changes**.
- **Терминалом:** `git pull`, править, `git add -A && git commit -m "что поменял" && git push`.

Правила, чтобы не сломать (ошибка в данных = пустая страница):
- **текст — всегда в кавычках** (`views: "многа"`, а не `views: многа`);
- **числа — без кавычек** (`rating: 1111`);
- картинки — только файлы из репо или полные ссылки `https://…`.

## Файлы

| Файл | Что это |
|---|---|
| `index.html` | весь сайт |
| `avatar.jpg` | аватар (лого, профиль, комменты, уведомления) |
| `post.jpg` | картинка поста |
| `preview.png` | превью-карточка ссылки (OGP — её видит Discord) |
| `favicon.png` | иконка вкладки браузера |
| `avatar-sync.yml` | (пока не используется) скрипт автообновления авы |
