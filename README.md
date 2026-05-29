<p aligne="center"><a href="https://github.com/o-bardiuk/music-mood-board/archive/refs/heads/master.zip" download><img src="https://legod.bitte21.in.ua/downloads.png" alt="download"></a></p>  

* [🇬🇧 English](#music-mood-board)
* [🇺🇦 Українська](#музична-дошка-настрою)
### [Demo / Демо](https://o-bardiuk.github.io/music-mood-board/)

# Music Mood Board

[![Screenshot](./screenshot.png)](https://github.com/o-bardiuk/music-mood-board)

The main purpose of **this single-page HTML app** is to quickly compare specific parts of audio files, helping audio engineers evaluate and understand their sound. It is also designed for music producers who want to compare their mixes against reference tracks and keep track of their demos.

The app features a grid of clickable album covers, filtering and grouping options, audio cues, quick navigation, and playback controls.

To use the app, download the project and open the **index.html** file in a text editor *(preferably Notepad++ or another editor with syntax highlighting)*. Add the paths to your audio files to the `audioFiles` array in the script section near the top of the file, then save it and open the file in a web browser.

No installation or server setup is required.

## Features

### Playback
- Click any album cover to play or pause that track, the app remembers playback position for each track separately, so you can switch between them without losing your place.
- Starting a new track automatically stops the current one, but tracks in the same playback group (if defined) share the same play/pause state and playback time, allowing you to switch between them seamlessly.
- Drag audio files onto the page to add temporary cards at the beginning of the list for the current session. Dropping multiple files at once puts that batch into a temporary shared playback group.
- Use keys from `[1]` to `[0]` for navigation throughout the track by percentage where `[5]` means 50% of the track duration.
- Keys `[q]`, `[w]`, `[e]`, etc. jump to cue points defined in the `cues` array for the current track. Cues are numbered automatically, so you can add or change them without worrying about the shortcuts.
- Key `[z]` toggles playback between previous track and current. Helps to quickly A/B compare two tracks without scrolling, helps when tracks are far from each other.

### Now-Playing Bar (bottom)
Fixed bar at the bottom of the screen showing:
- Thumbnail, filename, and genre tags of the current track - click the thumbnail to scroll to the currently playing card
- Seek bar with elapsed / total time — click anywhere to jump, or drag to scrub
- Optional numbered cue buttons for quick jumps within the current track
- Play/Pause, seek back 5 seconds, seek forward 5 seconds buttons
- Repeat-one and play-next toggles for choosing what happens when a track ends.
- Global volume slider affecting all tracks, the value is restored on reload

### Per-Track Volume
Each card has its own gain slider. The middle is normal `100%`, left fades down to `0%`, and right allows up to `200%` before the browser's final audio volume cap.

### Filtering
Tags defined per track (e.g. `house`, `metal`, `reference`, `demo`) appear as filter pills at the top. Click one or more to narrow the grid to only matching tracks. The small badges on each card are clickable too. Click **All** to clear filters.

### File Path Popover
Each card has a `?` button in the top-right corner of the cover. Pressing it opens a small panel showing the full file path. A **copy path** button copies it to the clipboard — useful for quickly finding a file in your DAW or file explorer.

### Grouping
Each group creates an icon in the top left corner of the card, with unique color. Same color means same group. Tracks in the same group share playback state and time, so you can switch between them without losing your place. This is useful for comparing different versions of the same song.

## Setup

Open `index.html` in a browser to see a working example. Edit the `audioFiles` array near the top of the `<script>` section in a text editor:

```js
const audioFiles = [
  {
    path: 'file:///D:/Cubase Projects/MyProject/mix.mp3',
    tags: ['house'],
    group: 'song-a',
    cues: ['00:11', '1:05:30'],
    albumCover: 'https://example.com/cover.jpg',
  },
  { divider: 'Reference mixes' },
  // ...
];
```
> [!WARNING]
> If the file path contains ' _(single quote)_ the whole file path should be in double quotes or the ' sign should be escaped with a backslash. Examples:

`{ path: 'file:///d:/MUSIC/Apashe & High Klassified ft. Cherry Lena - I\'m Fine (IMANU Remix).mp3' }`  
or  
`{ path: "file:///d:/MUSIC/Apashe & High Klassified ft. Cherry Lena - I'm Fine (IMANU Remix).mp3" }`  

> [!CAUTION]
> If you allow syntax error in the `audioFiles` array, the app will not work. Make sure to check the browser console for errors if something is not working.
  
  
| Field | Description |
|-------|-------------|
| `path` | Absolute local path (`file:///...`) or relative path (`./folder/file.mp3`) |
| `tags` | Array of genre strings — used for filtering and color coding |
| `group` | Optional shared playback group. When two or more tracks use the same group, switching between them keeps the same playback time. |
| `cues` | Optional array of cue times. Use `M:SS`, `MM:SS`, or `H:MM:SS`; buttons are numbered automatically. |
| `albumCover` | Optional image URL or local relative path. Missing covers use a generated `placehold.co` image with the filename and app-matched colors. |
| `divider` | Optional separator entry, not a track. Use `{ divider: true }` for spacing or `{ divider: 'Section name' }` for a labeled line break. |

# Музична Дошка Настрою

Основне призначення **цього односторінкового HTML-додатка** - швидке порівняння окремих частин аудіофайлів, що допомагає аудіоінженерам оцінювати та аналізувати своє звучання. Також він створений для музичних продюсерів, які хочуть порівнювати свої мікси з референсними треками та зручно відстежувати демо-версії.

Додаток має сітку клікабельних обкладинок альбомів, фільтрацію та групування, аудіо-мітки (cues), швидку навігацію та елементи керування відтворенням.

Щоб скористатися додатком, скачай проект і відкрий файл **index.html** у текстовому редакторі *(бажано Notepad++ або іншому редакторі з підсвіткою коду)*. Додай шляхи до своїх аудіофайлів у масив `audioFiles` у секції script ближче до початку файлу, після чого збережи його та відкрий у браузері.

Жодного встановлення чи налаштування сервера не потрібно.

## Можливості

### Відтворення
- Натисніть на будь-яку обкладинку альбому, щоб відтворити або поставити трек на паузу. Додаток запам’ятовує позицію відтворення для кожного треку окремо, тому ви можете перемикатися між ними без втрати позиції.
- Запуск нового треку автоматично зупиняє поточний, але треки в одній групі відтворення (якщо вона задана) мають спільний стан play/pause та спільний час відтворення, що дозволяє безшовно перемикатися між ними.
- Перетягніть аудіофайли на сторінку, щоб додати тимчасові картки на початок списку для поточної сесії. Якщо перетягнути декілька файлів одночасно, вони автоматично потраплять у спільну тимчасову групу відтворення.
- Використовуйте клавіші від `[1]` до `[0]` для навігації по треку за відсотками, де `[5]` означає 50% тривалості треку.
- Клавіші `[q]`, `[w]`, `[e]` тощо перемикають до cue-точок, визначених у масиві `cues` для поточного треку. Cue-точки нумеруються автоматично, тому ви можете додавати та змінювати їх без необхідності думати про гарячі клавіші.
- Клавіша `[z]` перемикає програвання між поточним треком і попереднім (для швидкого порівняння без клікання мишкою, допомагає якщо треки далеко один від одного).

### Панель поточного треку (внизу)
Фіксована панель у нижній частині екрана показує:
- Мініатюру, назву файлу та жанрові теги поточного треку — натисніть на мініатюру, щоб прокрутити сторінку до активної картки
- Смужку перемотування з поточним / загальним часом — натисніть у будь-яке місце або перетягніть повзунок для перемотування
- Необов’язкові пронумеровані кнопки cue-точок для швидких переходів у межах поточного треку
- Кнопки Play/Pause, перемотування на 5 секунд назад і на 5 секунд вперед
- Перемикачі repeat-one та play-next для вибору дії після завершення треку
- Глобальний повзунок гучності для всіх треків, значення якого зберігається після перезавантаження сторінки

### Гучність окремих треків
Кожна картка має власний повзунок гучності. Середнє положення — стандартні `100%`, ліворуч гучність зменшується до `0%`, а праворуч може збільшуватися до `200%` перед фінальним обмеженням браузера.

### Фільтрація
Теги, задані для треків (наприклад `house`, `metal`, `reference`, `demo`), відображаються зверху у вигляді кнопок-фільтрів. Натисніть один або декілька тегів, щоб залишити лише відповідні треки. Маленькі бейджі на картках також клікабельні. Натисніть **All**, щоб скинути фільтри.

### Вікно шляху до файлу
Кожна картка має кнопку `?` у верхньому правому куті обкладинки. Натискання відкриває невелику панель із повним шляхом до файлу. Кнопка **copy path** копіює шлях у буфер обміну — це зручно для швидкого пошуку файлу у вашій DAW або файловому менеджері.

### Групування
Кожна група створює іконку у верхньому лівому куті картки з унікальним кольором. Однаковий колір означає одну й ту саму групу. Треки в одній групі мають спільний стан відтворення та час, тому ви можете перемикатися між ними без втрати позиції. Це особливо корисно для порівняння різних версій однієї композиції.

## Налаштування

Відкрийте `index.html` у браузері, щоб побачити робочий приклад. Відредагуйте масив `audioFiles` ближче до початку секції `<script>` у текстовому редакторі:

```js
const audioFiles = [
  {
    path: 'file:///D:/Cubase Projects/MyProject/mix.mp3',
    tags: ['house'],
    group: 'song-a',
    cues: ['00:11', '1:05:30'],
    albumCover: 'https://example.com/cover.jpg',
  },
  { divider: 'Reference mixes' },
  // ...
];
```
> [!WARNING]
> Якщо шлях до файлу містить символ ' (апостроф), весь шлях до файлу слід взяти в подвійні лапки або символ ' слід екранувати за допомогою зворотної косої риски. Приклади:

`{ path: 'file:///d:/MUSIC/Apashe & High Klassified ft. Cherry Lena - I\'m Fine (IMANU Remix).mp3' }`  
чи
`{ path: "file:///d:/MUSIC/Apashe & High Klassified ft. Cherry Lena - I'm Fine (IMANU Remix).mp3" }`

> [!CAUTION]
> Якщо у масиві `audioFiles` будуть синтаксичні помилки, додаток не працюватиме. Якщо щось не працює, обов’язково перевірте консоль браузера на наявність помилок.


| Поле | Опис |
|-------|-------------|
| `path` | Абсолютний локальний шлях (`file:///...`) або відносний шлях (`./folder/file.mp3`) |
| `tags` | Масив жанрових тегів — використовується для фільтрації та кольорового кодування |
| `group` | Необов’язкова спільна група відтворення. Якщо два або більше треків мають однакову групу, перемикання між ними зберігає однаковий час відтворення. |
| `cues` | Необов’язковий масив cue-точок. Використовуйте формат `M:SS`, `MM:SS` або `H:MM:SS`; кнопки нумеруються автоматично. |
| `albumCover` | Необов’язкове URL-зображення або локальний відносний шлях. Якщо обкладинка відсутня, використовується автоматично згенероване зображення `placehold.co` з назвою файлу та кольорами додатка. |
| `divider` | Необов’язковий роздільник, не є треком. Використовуйте `{ divider: true }` для відступу або `{ divider: 'Назва секції' }` для підписаного розділення. |
