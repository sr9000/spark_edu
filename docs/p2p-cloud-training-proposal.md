# Proposal: P2P Cloud-Backed Training Mode for Spark

## Main idea overview

Spark can evolve into a **mobile-first, peer-to-peer training app** where teachers and students do not need a central Spark-hosted backend for everyday learning.

The core idea is simple:

- the teacher publishes course content to their own free or existing cloud storage;
- each student connects to the teacher's published course link and pulls updates into the Spark app;
- each student writes progress, answers, notes, and submissions to their own cloud storage;
- the teacher pulls student progress from student-owned links;
- the student app keeps a local backup of the teacher's course, so learning can continue even if the teacher's cloud becomes unavailable.

In this model, Spark becomes **one app to read, write, sync, and organize training data**, while storage is delegated to existing private clouds such as Google Drive, Dropbox, Yandex Disk, WebDAV, S3-compatible storage, GitHub, or any simple static host.

This removes three hard problems from the first product version:

1. **No central hosting bill** — users bring their own free storage.
2. **No heavy legal data custody problem** — teacher and student data stays in their own private clouds, shared by link.
3. **No need for strict results verification** — if a student fakes progress, they mainly deceive themselves.

The product goal is not to build another LMS SaaS. The goal is to build a **local-first education client** that makes private, low-cost, interactive learning possible over ordinary cloud links.

---

## Proposed interaction model

### Teacher side

The teacher creates a course in Spark:

- lessons;
- tasks;
- media links;
- assignments;
- announcements;
- optional AI-generated learning materials.

Spark exports this content into a portable course package and uploads it to the teacher's cloud.

The teacher shares one course link with students:

```text
https://teacher-cloud.example/spark/course/index.json
```

The teacher owns this package. Students only read from it.

### Student side

The student opens Spark, joins by teacher link, and the app pulls the course package.

Spark stores:

- a local copy of the course;
- downloaded lesson metadata;
- progress state;
- answers and submissions;
- personal notes.

The student then chooses their own cloud location for backup and progress publishing.

Spark creates a student progress package and gives the student a read-only link to share with the teacher:

```text
https://student-cloud.example/spark/progress/index.json
```

The student owns this package. The teacher only reads from it.

### Teacher dashboard

The teacher adds student progress links into Spark.

The app periodically pulls each student's progress package and builds a class dashboard:

- who started the course;
- lesson completion;
- task submissions;
- questions from students;
- stale or inactive students;
- latest sync time.

This creates interactivity without a shared database and without forcing all users onto one central server.

---

## Pros

### 1. Very low operating cost

Spark does not need to store all teacher media, student submissions, and progress on its own servers. Most data lives in user-owned cloud storage.

This makes the product easier to keep free or nearly free.

### 2. Privacy-first by architecture

The teacher stores teacher-owned content. The student stores student-owned progress.

Spark can avoid becoming the default legal owner or processor of all educational data. Shared links provide controlled access without requiring public publishing.

### 3. Works well with mobile usage

The app can hide the cloud complexity behind simple actions:

- "Publish course";
- "Join by link";
- "Back up to my cloud";
- "Share progress with teacher";
- "Refresh class".

The user sees a learning app, not a storage system.

### 4. Offline-friendly

Because students cache the teacher's course locally, the course remains available when:

- the teacher deletes the original files;
- the teacher's free hosting quota is exceeded;
- the student has weak internet;
- the teacher stops maintaining the course.

This is important for self-learning, small communities, and unstable infrastructure.

### 5. No complex anti-cheat requirement

For this product shape, progress is primarily a learning aid, not a certified exam record.

If a student manually edits or fakes progress, the main damage is to the student's own learning path. That allows the MVP to stay simple and avoid expensive verification, proctoring, identity, and compliance systems.

### 6. Easy to distribute

A teacher can onboard students by sending one link.

A student can move between devices by reconnecting their own cloud.

The model is understandable for users who already share files, folders, or documents by link.

### 7. Good fit for open-source/self-hosted positioning

This idea aligns with Spark's existing privacy-first and low-resource direction. It can be positioned as:

> A local-first training app where teachers and students own their learning data and use ordinary cloud storage as the sync layer.

---

## Cons and risks

### 1. Sync reliability depends on external cloud providers

Different clouds have different APIs, rate limits, file sharing behavior, and mobile permission flows.

The MVP should avoid too many providers at once and start with the simplest targets.

### 2. Not truly real-time

The pull model is excellent for cost and privacy, but it is not instant by default.

Announcements, submissions, and questions may update every few minutes or on manual refresh. This is acceptable for training workflows, but not for live chat or synchronous classrooms.

### 3. Link management can confuse users

Users may lose links, share the wrong link, or accidentally revoke cloud access.

The app must provide clear states:

- connected;
- last synced;
- link unavailable;
- permission denied;
- local backup available;
- needs re-share.

### 4. Multi-device conflicts need rules

If a student uses two phones and both write progress, conflicts can happen.

The first MVP can use last-write-wins, but a better long-term design is an append-only event log.

### 5. Cloud terms and sharing UX differ

Some free cloud providers may restrict direct file access, public links, API calls, or automated sync.

Spark should abstract storage connectors and keep the course package format independent of any one provider.

### 6. Trust is limited

This model is not suitable for high-stakes certification, legal exams, or paid credentials where tamper-proof verification matters.

It is better for:

- self-learning;
- tutor-led practice;
- private study groups;
- micro-courses;
- community education;
- lightweight school or club training.

---

## Users defined by the app's strengths

The strongest users are not "everyone who learns". They are users who benefit from low cost, privacy, offline access, and simple link-based distribution.

### 1. Private tutors

Private tutors can publish small learning tracks for their own students without paying for a full LMS.

They benefit from:

- no platform fee;
- fast lesson sharing;
- progress visibility;
- mobile-first student access;
- simple distribution through messenger links.

### 2. Small study groups

Groups learning programming, languages, exams, or hobbies can share structured materials without building a server.

They benefit from:

- peer-to-peer ownership;
- no administrator;
- easy content backup;
- low barrier to start.

### 3. Independent course authors

Authors who do not want to run a SaaS can publish course packages on existing storage.

They benefit from:

- portable course format;
- no hosting complexity;
- optional AI-assisted content creation;
- audience access through one link.

### 4. Students in low-resource environments

Students with weak internet, limited money, or unreliable access to platforms can keep local copies of learning materials.

They benefit from:

- offline reading;
- no paid subscription requirement;
- course survival even if the teacher disappears;
- ownership of personal progress.

### 5. Privacy-sensitive schools and clubs

Small schools, clubs, or local education communities may want digital learning without sending all user data to a foreign SaaS.

They benefit from:

- user-controlled storage;
- minimal central data processing;
- local-first operation;
- possible self-host or WebDAV deployment later.

---

## Implementation plan

### Phase 1: Define portable package formats

Create simple JSON-based formats for course and progress packages.

Teacher course package:

```text
course/
  index.json
  lessons/
    lesson-001.json
    lesson-002.json
  assignments/
    assignment-001.json
  media/
    image-001.png
  updates.json
```

Student progress package:

```text
progress/
  index.json
  profile.json
  course-progress.json
  submissions/
    assignment-001.json
  notes/
    lesson-001.json
  sync-log.json
```

The package format should be storage-provider-neutral. A file should work the same way from WebDAV, Google Drive, local folder, or static hosting.

### Phase 2: Build local-first storage inside the app

The mobile app should treat local storage as the source of immediate UX.

```text
Mobile App
  ├── Local cache
  ├── Course reader
  ├── Progress writer
  ├── Sync queue
  └── Cloud connector
```

The user should be able to open lessons and see progress even when the cloud is temporarily unavailable.

### Phase 3: Add pull sync

Implement a sync engine with two main operations:

```text
pull teacher course -> update local course cache
pull student progress -> update teacher dashboard
```

For the MVP, sync can be manual:

- "Refresh course";
- "Refresh students";
- "Publish progress";
- "Publish course update".

Automatic background sync can come later.

### Phase 4: Add write/publish support

Teacher publishes course data to teacher cloud.

Student publishes progress data to student cloud.

No user writes into another user's cloud.

```text
Teacher App ──writes──> Teacher Cloud
Student App ──pulls───> Teacher Cloud

Student App ──writes──> Student Cloud
Teacher App ──pulls───> Student Cloud
```

This avoids multi-writer conflicts for the first version.

### Phase 5: Start with minimal cloud connectors

Recommended MVP connector order:

1. Local folder connector for development and testing.
2. WebDAV connector for real-world usage.
3. Static HTTP read-only connector for published courses.
4. Provider-specific connectors only after the package model is stable.

WebDAV is a good first real connector because many storage systems can expose it and the API model is simple.

### Phase 6: Add teacher dashboard

The teacher dashboard should be built from a list of student progress links.

```text
class.json
  students:
    - name: Alice
      progressUrl: https://student-cloud/a/progress/index.json
    - name: Bob
      progressUrl: https://student-cloud/b/progress/index.json
```

The dashboard pulls each progress package and displays summary cards.

### Phase 7: Improve sync safety

After the MVP works, progress can move from one mutable JSON file to an append-only event log:

```text
progress-events.jsonl
```

Example event types:

```text
lesson_opened
lesson_completed
answer_submitted
note_added
course_backed_up
```

This makes conflict handling, audit history, and multi-device sync easier without introducing strict anti-cheat verification.

---

## Architecture scheme

```text
                         ┌──────────────────────┐
                         │   Teacher's Cloud     │
                         │  course package       │
                         └──────────┬───────────┘
                                    │ pull
                                    ▼
┌──────────────────────┐    ┌──────────────────────┐
│ Teacher's Spark App  │    │ Student's Spark App  │
│                      │    │                      │
│ - creates course     │    │ - reads course       │
│ - publishes updates  │    │ - caches backup      │
│ - pulls progress     │    │ - writes progress    │
└──────────┬───────────┘    └──────────┬───────────┘
           ▲                           │
           │ pull                      │ write
           │                           ▼
           │                ┌──────────────────────┐
           └────────────────│   Student's Cloud     │
                            │  progress package     │
                            └──────────────────────┘
```

---

## Suggested MVP

The smallest useful version should include:

- create a course package;
- publish course package to a local folder or WebDAV;
- join course by URL;
- cache course locally on the student device;
- record lesson progress locally;
- publish progress package to student storage;
- add student progress URL to teacher app;
- show teacher dashboard from pulled student packages.

Do not include in the MVP:

- paid certification;
- anti-cheat;
- real-time chat;
- many cloud providers;
- complex permissions;
- centralized accounts.

---

## Final recommendation

This idea is worth exploring as a separate Spark mode:

> **Spark P2P Mode** — a mobile-first, local-first learning client where teachers and students use their own cloud storage and synchronize through private links.

It fits the repository's current privacy-first direction, reduces infrastructure cost, and creates a clear product difference from traditional LMS platforms.

The main product challenge is not backend scalability. The main challenge is making cloud-link sync feel simple enough that non-technical teachers and students can use it without understanding the architecture.
