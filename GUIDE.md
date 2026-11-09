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

Та же шпаргалка вынесена блоком наверх самого `index.html` (КАСТОМИЗАЦИЯ).

## Как работают кнопки и уведомления

- **Колокольчик** (справа сверху) = панель уведомлений, как в Discord
  (список «Transcendencies: иди нахуй», бейдж со счётчиком).
- **Все кнопки** — подвал (NO Contact us / Terms of Service / MDMA / Discord),
  боковое меню (Home, Best posts, Hot, …), аватар в шапке —
  тост «**Transcendencies**: иди нахуй».
- **Upgrade Account** (внизу бокового меню) — открывает
  [donorschoose.org](https://www.donorschoose.org/) (благотворительность).
- Пост в Bookmarks — не кликабельный; коммент виден прямо под постом.

## Домен

- Сейчас: `https://facich.github.io/transcendencies/`
- Потом: `transcendencies.is-a.dev` — PR #60585 ждёт мерджа мейнтером.
  После мерджа: Settings → Pages → Custom domain: `transcendencies.is-a.dev`
  + галка Enforce HTTPS.

## Домен в профиле Discord (верификация)

Окно «Подключите ваш домен» в Discord — это верификация домена: Discord
проверяет, что домен твой, и потом показывает его в профиле.
Для is-a.dev это делается через TXT-запись (официальный гайд:
docs.is-a.dev/guides/discord-verification):

1. Discord → **Settings → Connections → View more** → кнопка-глобус (домен) →
   ввести `transcendencies.is-a.dev` → **Далее** → скопировать
   **verification string** (TXT-строку).
2. В форке `facich/register` добавить файл `domains/_discord.transcendencies.json`:
   ```json
   {
       "owner": {
           "username": "facich"
       },
       "records": {
           "TXT": "сюда-verification-string"
       }
   }
   ```
3. Pull request (как в прошлый раз, compare across forks) → ждём мердж.
4. Discord → снова «Подключите ваш домен» → `transcendencies.is-a.dev` →
   **Verify** (если «Unable to verify» — подождать до 24 ч, DNS распространяется).
5. Домен появится в профиле Discord.

Важно: проверка пройдёт только после того, как PR (и основной PR #60585)
промерджит мейнтер is-a.dev — до этого домен физически не существует.

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
