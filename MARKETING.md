# HugMesh marketing materials

This page is for anyone writing about HugMesh: blog posts, social posts, talks,
directory listings. Every claim here was checked against the `main` branch of
the HugMesh repositories on 2026-10-21. When something is not finished, this page
says so, and copy based on it should say so too.

**Status tags used below**

- No tag: shipped on `main` and works today.
- **[beta]**: built and on `main`, but switched off by default, partly finished,
  or not yet proven on a live system.
- **[experimental]**: early, or waiting on hardware nobody has tested it on yet.
- **[not yet]**: planned or blocked. Do not advertise these as features.

If a sentence you want to write is not backed by this page, check the repository
first or leave it out. There are no published user counts, partners, awards,
benchmarks or testimonials. Please do not invent any.

---

## Tagline options

1. **Your own little corner of the internet, on hardware you trust.**
2. **Chat, posts and profiles for your people, run by your people.**
3. **Build it, flash it, host it yourself.**

## Elevator pitch (50 words)

HugMesh helps a group run its own online space on machines it controls. A desktop
wizard builds hardened Gentoo images for PCs and Raspberry Pis. One web front door
brings chat, a social timeline, a forum and member profiles together under one
sign-in. It is young, and honest about it.

## The longer pitch (150 words)

Most online communities live on someone else's servers, under someone else's rules.
HugMesh is a set of tools for groups that would rather host themselves. The Image
Studio is a desktop wizard for Linux and Windows (Windows not yet confirmed on a
real Windows machine). It asks plain questions and builds hardened Gentoo images for
x86 machines and Raspberry Pis, so nobody has to remember builder flags. Saved
Studio configs never contain your passwords. Once a mesh is running, members sign in
once through a normal form and move between Matrix chat, a Mastodon-compatible
timeline, a forum (in beta), their own profile page and a 2D character maker.
Moderators get a request queue and an audit trail, and admins a console. A mesh can
host several domains, and work on giving each its own sign-in, services and Tor
address is under way. It is early work: some image families still wait for real
hardware, and we try to say plainly what is unfinished.

---

## Who it is for

- **Communities** (clubs, fandoms, local groups) that want chat, a timeline and a
  forum in one place, with their own moderators and their own rules.
- **Families** who want a private space to talk and share, on a machine in the house
  rather than a company's cloud.
- **Small organisations** that want accounts, roles, announcements and an admin
  console without stitching five products together.
- **Hobbyists** who like Raspberry Pis, Gentoo and self-hosting, and want a project
  that explains what every build step does.
- **Privacy-minded groups** that care where their data lives: no login tokens
  exposed to page scripts, full-disk encryption on laptops and desktops installed
  from Studio-built images, and (in beta) an optional Tor address per domain.

---

## Key features

### Image Studio (the desktop wizard)

- A step-by-step wizard for **Linux and Windows** that builds HugMesh images. On
  Windows, builds run through Docker Desktop (WSL2 is the recommended way); there
  is no native Windows build. Windows support is not yet confirmed on a real Windows
  machine. Run it from a checkout of `hugmesh-generator`.
- **Ten cards on the build menu.** Three build an image: a standalone Gentoo
  desktop, a mesh desktop client, and a mesh node. Seven run a tool: local Docker
  mesh, end-to-end tests, mesh emulation, cloud deploy, MDM phone, MDM Quest headset,
  and creating nodes for a local cloud.
- **See the exact build command without opening a window.** `--print-command`
  prints it from a saved config with no display needed, and `--scan-hardware`
  reports your GPU, Wi-Fi and Bluetooth and suggests build settings.
- **Saved configs never keep passwords.** Local, disk-encryption, user and root
  passwords are blanked in saved config files, and the Studio tells you to re-enter
  them. (If you choose an unattended install, the disk-encryption passphrase is
  written into the installer image in plain text, and the Studio warns you about
  that.)
- **Docker builds are memory-capped.** By default a runaway Docker build fails with a
  clear message instead of locking up the machine. Native Gentoo builds are not
  capped by the Studio.
- **Per-domain settings** **[beta]**. In the Domains step, each domain gets its own
  title, its own optional services, its own sign-in (shared or separate), an optional
  Tor address and a GitHub org for export. A domain you haven't filled in blocks the
  build and says why. Available in both the window and the terminal versions. The
  service choice is saved but not yet enforced (the Studio says so on the page). A
  separate sign-in and a Tor address per domain take effect on the local Docker mesh
  only; on node images they are recorded for later.
- **Web login theme.** Pick two colours or a preset (nord, pride, dark and more) and
  a light or dark ramp. Every other colour is worked out for you, and text colours
  are adjusted to meet WCAG AA contrast. A live board shows the measured contrast,
  and a preview shows the real login page. Fonts are system fonts or an upload with
  its licence recorded. It applies when the container starts, with no image rebuild.
- **Desktop branding.** Premade looks (light, dark, purple, grey) or your own
  wallpaper, boot screens, login background, accent colour and logo. An
  "unaffiliated" desktop keeps the look options but carries no HugMesh name, logo or
  tooling (the premade wallpapers still show the mesh hexagon pattern).
- **Saved meshes.** "Save this mesh" records a running local mesh's settings,
  domains, account names and roles. By default it stores only pointers to its
  credentials, never the data or any password. Copying the credential files is an
  opt-in, and they are saved readable by you alone (mode 0600). Before you click,
  the table shows whether a row will start again or be restored from scratch.
- **Go-live wizard** **[beta]**. Guides an admin through putting a mesh on the
  public internet with one of six options: your own domain, Cloudflare Tunnel,
  DuckDNS or Cloudflare dynamic DNS, Tailscale Funnel, a router port-forward, or a
  Tor onion. It shows a preview first and changes nothing until you confirm, and
  undoing it means deleting one file. For most options it tells you which DNS
  records or tunnel settings to create; the dynamic-DNS option installs a small
  updater that keeps your record current. (Not yet tested against a real domain or
  DNS provider.)
- **Copy your code into your own GitHub org** **[beta]**. A domain can name a GitHub
  org, and the Studio plans, then applies, an export of that domain's repositories.
  Planning is the default, and applying only starts once you type the org name. It
  creates private repos by default, leaves out secret-looking files, refuses a repo
  when it finds common key or token patterns, and never force-pushes. These checks
  look for known file names and key patterns; they can miss a secret, so review the
  plan before you apply it. Some steps stay manual: signing in, setting the repo
  secrets, publishing the exported Java libraries from the new org, and switching on
  Pages. (Tested with local stand-ins, not yet against a real GitHub org.)
- **Local AI helper.** Start a coding helper on a model running on your own PC
  (Ollama), in a throwaway copy of one app's code. The Studio does not pass your
  GitHub, cloud or registry tokens into the helper's environment, and it never turns
  on auto-approve. The helper still runs as you and can reach a desktop keyring, so
  read every command it asks to run. You need Ollama, a model that supports tools,
  and one of the supported coding-agent command-line tools, and it opens a terminal
  on Linux only.
- **System tray mode.** `--tray` runs a local mesh node from the system tray, with
  Start, Stop, View logs, Open web UI, Builds, Limits and Go Live.
- **Terminal version** **[beta]**. A text version of the wizard goes through the same
  pages in the same order as the window version, and falls back to plain numbered
  prompts on a basic terminal. It ends with a saved config: you start the build from
  the window version or from the command line. Some steps are not in it yet (phone,
  headset and cloud pages, most of the local-mesh route, and a few build steps), and
  it says so where they would be.
- **Write images to USB, SD or eMMC** **[beta]**. Lists attached devices, never lists
  the disk you're running from, and re-checks each device right before writing. Not
  yet tested on a real block device.
- **Per-domain login themes** **[beta]**. Admins can store a different theme per
  domain through the admin console, but the login page still uses one theme for the
  whole mesh today. Say "in progress", not "each domain gets its own look".

### Images and hardware

- **x86 machines: twelve roles** on a hardened Gentoo base. Cluster nodes (pki,
  backend, frontend, backend-gpu, omnibus, edge-ai), clients (laptop, chromebook,
  desktop) and standalone desktops (thin, thick, unaffiliated). Outputs include disk
  images, live ISOs and tarballs. Kernel lockdown and Secure Boot signing are built in.
  By default each build makes its own signing key; supply your own key to boot under
  one already enrolled in your firmware. Honest limit: every image (nodes and
  desktops) boots SELinux in *permissive* mode. Enforcing mode needs a testing pass
  that has not happened yet.
- **Raspberry Pi** **[beta]**. Pi 5 and Pi 4 can run the cluster roles (pki, backend,
  frontend), a desktop, and a plain generic server. Pi 3 is desktop-only, because
  1 GB of RAM can't run the cluster. Images start small, grow to fill the card on
  first boot, and set themselves up from a USB stick with a `KEYS` partition. No boot
  on a real board is recorded on `main` yet: the builder itself says the Pi 4 and
  Pi 3 images have not been checked on real hardware, so treat those two as
  **[experimental]**.
- **Standalone hardened desktops.** No mesh, no VPN and no shared sign-in needed:
  a normal local user, full-disk encryption (LUKS2), an optional separate data disk,
  and live plus installer ISOs. Free GPU drivers by default; NVIDIA is opt-in.
- **Many images can be built.** The repo's generated list counts 131 distinct images
  the build system can express, and 150 combinations are checked across five ways of
  starting a build. That counts what can be requested and plan-checked, not what has
  been booted.
- **Libre Computer La Frite, Le Potato, Sweet Potato** **[beta]**. A light desktop or
  headless image, live or installer. Not yet proven on a real board, and you supply
  your own prebuilt u-boot.
- **Orange Pi (seven boards)** **[experimental]**. Builders exist for the Orange Pi 5,
  5 Plus, 4 LTS, Zero 2, Zero 2W, Zero 3 and 3 LTS. No physical Orange Pi has booted
  one yet.
- **NVIDIA Jetson Orin (Nano, NX)** **[experimental]**. Edge-AI, GPU backend, omnibus
  and desktop roles. No GPU acceleration yet: the default kernel has no CUDA, so AI
  work runs on the CPU. Hardware validation pending: no physical Orin has booted it.

### The mesh: what members see

- **One front door, one sign-in.** A single web shell hosts up to 13 separately built
  app pages (chat, timeline, forum, profile, character studio, admin and more) and
  loads them as you need them. Which pages appear depends on what the mesh's admin
  installed; missing optional ones are greyed out with the reason.
- **A normal sign-in form.** Username and password, a display name the first time.
  The login token stays on the server; the browser holds a session cookie that page
  scripts can't read.
- **A fair message when you're suspended.** A suspended or banned member is told so
  and sent to an appeal page with instructions, not a dead error.
- **Your own home page.** Edit your profile and avatar, change your password or
  email, block people, hide yourself, see and end your own login sessions, choose
  which notifications you want, and read a notification inbox that updates live.
- **Cards.** Small rich pages built from draggable sections, with maths support,
  shown in a sandbox so a card can't run scripts.
- **Notifications and announcements.** A bell with an unread count, a pop-up when
  something arrives, a banner for admin announcements, and a launcher that explains
  why a card is greyed out.
- **Matrix chat.** Rooms, direct messages, invites, threads, replies, edits,
  reactions, read receipts, search, attachments and a personal chat theme. Group
  rooms have a three-person end-to-end test (one scenario, the unread badge, is a
  known failure).
- **Mastodon-compatible timeline.** Home, local, federated, hashtags, lists,
  bookmarks, polls, content warnings, direct messages, and voice and video messages
  up to five minutes. The server the cluster deploys is Akkoma, spoken to through the
  Mastodon client API. Notifications refresh every 30 seconds.
- **Character Studio.** Build a layered 2D avatar in the browser: four art packs,
  recolouring, expressions, a mouth that follows your microphone, freehand flair and
  a body-type blend. Export a PNG, or set it as your avatar on the mesh, in Matrix
  and on the timeline.
- **Built with accessibility in mind.** Skip links, keyboard menus, dialogs that trap
  focus and close on Escape, screen-reader announcements, 44-pixel touch targets, and
  disabled controls that explain themselves. This is a design stance with tests behind
  it, not a certified audit.
- **Two-factor sign-in** **[beta]**. Members can set up authenticator-app codes,
  passkeys or hardware keys, and get one-time recovery codes. Requiring a second
  factor is off by default on a cluster; an operator turns it on
  (`docs/MFA-ROLLOUT.md`).
- **Forum** **[beta]**. Categories, topics, replies, search, member profiles, an
  optional visual-novel reading mode, and moderator controls. On the local Docker
  mesh the forum backend (phpBB) is off unless you start it with `PHPBB=1`; cluster
  images include it by default. Posting through a running forum has not been proven
  end to end.
- **Voice and video calls** **[beta]**. One-to-one Matrix calls connect directly,
  which usually works only on the same local network; no passing live run is
  recorded yet. Calls across the internet need the optional TURN relay (coturn),
  which is built in but off by default and not yet proven live.
- **Live streaming** **[experimental]**. A streamer console and an "avatar cam" that
  lets you go live as your 2D avatar. Off by default, needs a GPU node, and not yet
  run against a live system.
- **Visual-novel chat extras** **[experimental]**. A talking character sprite,
  stickers and a voice-chat stage are in the chat client. Spoken character voices are
  built but switched off.
- **Forgot password** **[experimental]**. Works only where an admin has switched on
  password reset and email sending.
- **Interface language** **[experimental]**. English only today. The translation
  system exists, but no real translations ship yet.

### For moderators and admins

- **Moderator console** **[beta]**. Review the moderation queue, recommend actions,
  file ban and domain-lock requests, block users or servers (recorded and audited;
  on Matrix the block itself is not carried out yet), review automated image
  findings, and read the audit trail. Actions are *requests* that take effect
  shortly after, not instantly.
- **Domain lock** **[experimental]**. Moderators and admins can mark an account
  domain-locked, and the timeline shows a locked member a "local only" control with
  an explanation. The server-side part that actually keeps posts and federation
  local is not built yet, so do not describe it as a working restriction.
- **Admin console.** Registration allowlist, usage dashboard, role grants,
  announcements (draft, schedule, choose where they show), appeals, and security
  self-service. Some admin screens (backups, managed services, app store) record
  what you want but the parts that carry it out are off by default; describe them as
  screens, not as working features.
- **Wiki.** Markdown pages with live preview, attachments and access control per
  brand. Today it is for admins and moderators; ordinary members have no wiki access.

### Security and privacy

- **No access tokens in page scripts.** With the built-in sign-in (the default), you
  log in through HugMesh's own form. The login token never reaches the browser, and
  the session cookie is one page scripts cannot read. (The browser also holds a
  separate anti-forgery cookie that scripts can read; it is not a login token.)
- **Login tokens and two-factor secrets encrypted at rest.** Saved login tokens and
  two-factor secrets are encrypted with AES-256-GCM. Without the key, that feature
  stays switched off; it never falls back to storing plain text.
- **Careful two-factor design.** Recovery codes are stored only as keyed hashes, and
  a used authenticator code can't be replayed.
- **Route rules.** Admins can say which roles may reach which pages; the most
  specific rule wins and an explicit deny beats an allow. (Pages no rule names are
  passed through, so this is not "deny by default".)
- **Recent hardening (October 2026).** Stricter session checks. The gateway's role
  checks and the admin back end's workload-console check were changed to read
  encoded web addresses the same way the router does.
- **Strict browser security headers.** A strict content security policy on the
  shell. User-written content is cleaned before it is shown, and cards and
  announcements are also shown in a sandbox that blocks scripts.
- **Extra second-factor check for admin pages** **[beta]**. Built and tested, but off
  by default; an operator turns it on after every admin has enrolled.
- **Service-to-service certificates** **[beta]**. Services are set up to prove who
  they are to each other with short-lived certificates (mutual TLS), and the gateway
  uses TLS 1.3 only by default. Each brand is meant to get its own certificate
  authority, but switching a running mesh to that is still open work. A live check
  has not been done.
- **Tor address per domain** **[beta]**. A domain can have its own `.onion` address
  using the standard Tor daemon, with no public IP or DNS. Off by default. It takes
  effect on the local Docker mesh; on node images it is recorded but not yet set up.
  Checked offline, not yet on the live Tor network.

### Other tools **[beta]**

- **Docker mesh-node client.** Turns a Linux or Windows machine that already runs
  Docker into a background mesh node without reinstalling anything, with a task-bar
  icon to join, view logs or leave. Per-user, no admin rights. Mostly untested so far.
- **Phones and headsets.** The Studio can install GrapheneOS on a Google Pixel and
  enrol it as a managed device, or enrol a Meta Quest 3/3S. Real gaps remain before
  wider use.
- **Cloud deploy.** Publish a built x86 image to AWS, Azure, OpenShift or any qcow2
  host from plans written offline. None has run against a real cloud yet.
- **Local Kubernetes (kind).** Stands up a real cluster with the full platform. Not
  yet proven end to end; don't use it as a demo.

### Not yet (please don't advertise these)

- Studio installers (Windows MSI, Linux Flatpak): none released. Run from a checkout.
- Saving and reloading your Character Studio character, and its "describe your
  character" AI helper.
- The 3D chat room inside Matrix.
- The games catalog as something mesh members can open.
- A dashboard page for LoRa radio meshes.

---

## What makes it different

- **Open about its own status.** We try to say plainly what is unfinished. This page
  marks each feature as working, beta, experimental or not yet, and many unfinished
  features say so in the docs and in the app.
- **From the disk image up.** HugMesh doesn't only give you web apps; it builds the
  hardened operating system images they run on, for PCs and Raspberry Pis.
- **One sign-in for many tools.** Chat, timeline, forum, profile and avatar maker live
  behind one front door instead of five separate accounts.
- **Per-domain choices (in progress).** One mesh can host several domains. Their own
  sign-in and Tor address already work on the local Docker mesh; per-domain services
  are recorded but not yet enforced.
- **Careful by default.** Saved configs never keep passwords, go-live and export
  preview before they change anything, and Docker builds are memory-capped.
- **A desktop that wears nobody's logo.** The "unaffiliated" standalone desktop is a
  hardened, encrypted Gentoo desktop with no HugMesh name, logo or tooling (the
  premade wallpapers still show the mesh hexagon pattern).

---

## Try it

Everything starts from the `hugmesh-generator` repository. There is no installer to
download yet.

**1. Run the Image Studio (Linux)**

```sh
git clone https://github.com/hugmesh/hugmesh-generator.git
cd hugmesh-generator/studio
python3 -m venv .venv && . .venv/bin/activate
pip install -r requirements.txt        # PySide6 (or an existing PyQt6)
./hugmesh-studio
```

Gentoo can build natively; other Linux systems build through Docker.

**On Windows**, run `studio\hugmesh-studio.bat`. On a fresh machine it checks for
Python and Docker Desktop and offers to install them, asking before each step. Builds
use Docker Desktop; WSL2 is the recommended setup.

**2. Look before you build (no window needed)**

```sh
python -m hugmesh_studio --scan-hardware
python -m hugmesh_studio --print-command --config my-image.json --backend docker
```

**3. Run the whole platform on one machine (optional)**

The Studio's *Local Docker mesh* card does this for you, or from the repo root on
Linux:

```sh
make stack-m2-bootstrap   # once, before the first build
make stack-up SOCIAL=1    # SOCIAL=1 adds Matrix and Mastodon; add PHPBB=1 for the forum
make stack-seed SOCIAL=1  # required: creates the accounts you sign in with
```

Then open http://localhost:8088 and sign in. Accounts and details are in
`docs/LOCAL-STACK.md`.

Plan for an **x86_64** machine with Docker Compose v2 and buildx, about **8 GB RAM**
(12-16 GB with the social services), and a first build that takes tens of minutes to
hours. Windows uses Docker Desktop and `scripts/stack-up.ps1`. Full details are in
`docs/LOCAL-STACK.md`.

Note: the first-build path has only been run with access to the HugMesh
repositories while they were private. Until someone has tried it fresh after the
repositories go public, don't promise it works "in one command".

**Where to read next:** `docs/RUNNING.md` (the full operator runbook),
`docs/STUDIO-WALKTHROUGH.md` (every Studio screen) and `studio/README.md`.

---

## Project status and honesty note

HugMesh is an early, actively developed project. As of 2026-10-21:

- There are **no tagged releases** yet. Everything runs from the `main` branch.
- The **local Docker mesh** is the path that has actually been run with the full
  platform. The **Kubernetes (kind)** path is not yet proven end to end.
- **Orange Pi** and **Jetson Orin** images are experimental: no physical board has
  booted them. **La Frite** family images still need a real board, and no
  **Raspberry Pi** boot on a real board is recorded yet.
- **SELinux:** every image (nodes and desktops) boots SELinux in permissive mode for
  now.
- Several features are **built but switched off** until an operator turns them on
  (requiring a second factor on a cluster, the admin second-factor check, password
  reset, Tor, the internet call relay, streaming, and, on the local Docker mesh, the
  forum backend).
- **Per-domain services** are recorded but not yet enforced, and a domain's own
  sign-in and Tor address work on the local Docker mesh only.
- **Licences differ between repositories**, and some have none yet. Check each
  repository's `LICENSE` file; don't describe the whole project under one licence.
- To report a security problem, follow the org's `SECURITY.md`. Please don't open a
  public issue.

---

## Brand basics

- **Name:** always **HugMesh**: one word, capital H, capital M. Not "Hugmesh",
  "Hug Mesh" or "HUGMESH". Lower-case `hugmesh` is fine only in code, commands and
  repository names.
- **Tone of voice:** warm, plain and unassuming. Talk like a helpful neighbour, not a
  sales page. Short sentences. Say what something does and what it doesn't do yet.
  Avoid hype words and superlatives; let the plain description do the work.
- **Logo:** being designed now. It will live in `assets/logo/` (to be added). Until
  then, use the name in plain text and don't make up a logo.
- **Status words:** use "beta", "experimental" and "not yet" the same way this page
  does.

---

## Ready-to-use copy

### Short social posts

Post these only once the repositories are actually public: check that
github.com/hugmesh shows them to a signed-out browser first.

1. HugMesh is now public on GitHub. It's a set of tools for running your own
   community space (chat, a timeline, a forum, profiles) on machines you control.
   Early days, clearly labelled. github.com/hugmesh
2. The HugMesh Image Studio is a desktop wizard for Linux and Windows (Windows not
   yet confirmed on a real Windows machine) that builds hardened Gentoo images for
   PCs and Raspberry Pis, without you having to remember a single build flag. Saved
   configs never keep your passwords.
3. One sign-in, many rooms: HugMesh puts Matrix chat, a Mastodon-compatible
   timeline, a forum and a 2D avatar maker behind one front door. With the built-in
   sign-in, the login token never reaches your browser, and the session cookie is
   one page scripts can't read.
4. Want a hardened, encrypted Gentoo desktop with nobody's logo on it? HugMesh's
   "unaffiliated" standalone desktop has full-disk encryption and no HugMesh name,
   logo or tooling (the premade wallpapers still show the mesh hexagon pattern).
5. We'd rather be honest than shiny. We mark what's beta and experimental. Orange Pi,
   Jetson and Raspberry Pi images are still waiting on real-hardware boots. Come help
   test. github.com/hugmesh

### Two-sentence press blurb

HugMesh is a young, self-hosted community platform: a desktop wizard builds hardened
Gentoo images for PCs and Raspberry Pis, and a single web front door brings chat, a
Mastodon-compatible timeline, a forum and member profiles together under one sign-in.
It is now developed in the open on GitHub, with each feature on its marketing page
marked as working, beta or experimental.

### GitHub org description (under 160 characters)

> Self-hosted community platform: chat, timeline, forum and profiles under one sign-in, plus a wizard that builds hardened Gentoo images.

---

## Screenshot and visual suggestions

Use real screens from a current build. Existing offscreen Studio captures (from
2026-09-30) are in `hugmesh-generator` at
`docs/manual-test-evidence/live/studio-walk/`. Retake them if the screen has changed.

**Image Studio**

- The **"What do you want to build?"** menu with its ten cards.
- The **Domains** step, showing two domains with different services (caption it as
  "recorded, not yet enforced").
- The **Web login theme** page, with the live contrast board and the login preview
  side by side.
- The **Review & Build** page listing attached USB/SD devices.
- **Local Docker mesh** bring-up, mid-build, with Cancel, Open web UI and
  **Save this mesh** visible.
- The **Saved meshes** table showing a Start row and a Restore row.
- The **Go-live** page with a provider picked and the preview shown.
- The **system tray** menu.

**The web platform**

- The **sign-in page** with its animated background (fog, waves or net).
- The **member home** page (profile, sessions, notifications).
- **Matrix chat** in a busy group room with threads and reactions.
- The **Mastodon-compatible timeline**, including a voice message.
- **Character Studio** with an avatar mid-edit.
- The **moderator console** queue (label actions as requests).

Avoid screenshots of features tagged *not yet*, and of the kind cluster.
