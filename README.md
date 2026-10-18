<div align="center">

# 🏫 SRU Timetable Portal

### Your weekly timetable, free classrooms and the academic calendar, all in one place.

*Fast. No login. No app to install. Just open it and go.*

<br>

[![Live Demo](https://img.shields.io/badge/Live_Demo-Open_the_website-2563eb?style=for-the-badge)](https://sru-unofficial-timetable.vercel.app/)

<br>

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Vercel](https://img.shields.io/badge/Hosted_on-Vercel-000000?style=flat-square&logo=vercel&logoColor=white)
![Unofficial](https://img.shields.io/badge/Status-Unofficial_student_project-f59e0b?style=flat-square)

[Features](#-features) · [Numbers](#-at-a-glance) · [Data](#-how-the-data-works) · [Run it locally](#-run-it-locally) · [Project structure](#-project-structure)

</div>

---

> [!WARNING]
> **This is an unofficial student project and it is not completely accurate.**
> Always check the original SRU timetable first. If it matches what you see here, you can keep using this website. If it doesn't match, please don't use it. This project is not affiliated with or endorsed by the university.

---

## ✨ Features

The website has four tabs. Each one answers a question students ask every day.

| | Tab | The question it answers |
|:-:|---|---|
| 🗓️ | **Home** | *"What is my timetable this week?"* |
| 🟢 | **Empty Classes** | *"Which rooms are free right now?"* |
| 🔎 | **Check Classes** | *"What is going on in room 8002?"* |
| 📅 | **Calendar** | *"When are the holidays and exams?"* |

<br>

### 🗓️ Home: your weekly timetable

Pick your **degree**, **year** and **batch**, press **Search**, and your whole Monday to Friday schedule appears.

- Color-coded cells: **Lecture**, **Lab**, **Tutorial** and **Leisure** (free period)
- Each class shows the **subject**, **room** and **faculty**
- When you have **more than one class in the same hour** (for example elective options), every one of them is listed, so nothing is hidden
- Covers B.Tech **CSE, ECE, EEE, ME and CE**, from first to fourth year

<br>

### 🟢 Empty Classes: find a free room in seconds

Need a quiet place to study or a spare room for a group meeting? Choose a day and a time and see every room that is empty.

- Filter by **block**
- Choose **Today, right now** as the day and **Right now** as the time to see what is free this very hour
- Lab rooms are hidden by default because they are usually not meant for sitting. Tick **Also show lab rooms** to include them
- Click any room card to jump straight to **Check Classes** for that room

<br>

### 🔎 Check Classes: what is happening in a room?

Type a room number (for example `8002`), choose a day and a time, and find out whether it is **free** or **in use**.

- If it is in use, you see the **batch(es)**, **subject**, **faculty**, **type of class**, and the branch and year
- If several classes share the room at that time, all of them are listed
- Works with **Right now** too, so you can check a room before you walk over to it

<br>

### 📅 Calendar: the whole semester at a glance

Scroll through the academic calendar, or search for what you need, for example `holiday`, `mid exam` or `hackathon`.

- Color-coded entries: **Holiday**, **Exam**, **Event**, **Milestone** and **Working day (in lieu)**
- Live tags such as **Happening now** and **This week**, so you notice what is coming up
- Runs from **27 July 2026 to 4 January 2027**

---

## 📊 At a glance

| | |
|---|---|
| 🎓 **Degrees** | 5 (CSE, ECE, EEE, ME, CE) |
| 👥 **Batches** | 350 |
| 🚪 **Rooms** | 172 across 8 blocks |
| 📚 **Class entries** | 5,150+ |
| 📅 **Calendar entries** | 120 |
| ⚙️ **Backend** | None. It is a static website |

---

## 🧠 How the data works

This website is built on **snapshots**. The timetable, the batch list and the calendar are stored as plain JSON files in this repository, and the page reads them when it opens. That makes the website:

- ⚡ **Fast**, because there is no server to wait for
- 🛡️ **Reliable**, because it keeps working even if other websites are slow or down
- 🧩 **Simple**, with no database, no login and no build step

The flip side is that a snapshot goes out of date when the real timetable changes, which is why the warning above matters. The data is refreshed by hand, and **the current snapshot is from October 2026**.

<details>
<summary><b>📄 What the timetable file looks like</b> (illustrative values)</summary>

<br>

`room_schedule.json` is organised as **day → time → room → class**:

```json
{
  "Monday": {
    "09:30": {
      "<room-id>": {
        "room_name": "11007-BL11-GF",
        "subject": "Data Analytics and Visualization",
        "batch": "25CAIBTAIB01,25CAIBTAIB02",
        "faculty": "Dr. Example Name",
        "type": "Lecture",
        "others": []
      }
    }
  }
}
```

A room can host more than one class in the same hour (for example parallel lab groups). The first class is the main entry and any others are kept in the `others` list, so no class is ever dropped.

</details>

---

## 🚀 Run it locally

You only need Python (or any other simple web server). There is nothing to install.

```bash
# 1. Download or clone this repository, then open a terminal inside the folder

# 2. Start a local web server
python -m http.server 8000

# 3. Open it in your browser
#    http://localhost:8000
```

> [!NOTE]
> Don't open `index.html` by double-clicking it. The page loads its data with `fetch`, which browsers only allow when the page is served from a web server.

---

## 🗂️ Project structure

```text
.
├── index.html               # The whole website: HTML, CSS and JavaScript in one file
├── room_schedule.json       # Every class, organised by day → time → room
├── batch_directory.json     # Degrees, years and batches for the dropdowns
├── calendar_events.json     # Academic calendar entries
├── fetch_timetable_v2.py    # Script that builds the timetable data
└── build_batch_directory.py # Script that builds the batch list
```

**Built with:** plain HTML, CSS and JavaScript (no framework), the *Space Grotesk* and *IBM Plex Mono* fonts, and automatic deployment on **Vercel** straight from GitHub.

---

## 🐛 Found a mistake?

Open an [issue](../../issues) and say which batch and which class looks wrong. Remember to check it against the original SRU timetable first.

---

<div align="center">

**Built with ☕ by Kashif Ahmed**

*An unofficial project by a student, for students.*

⭐ If this saved you a walk to an occupied classroom, consider starring the repository.

</div>
