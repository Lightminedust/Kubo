<div align="center">

# Kubo

### See your server. Run nothing on it.

**Kubo** is a desktop app that connects to **your own Linux server** over SSH and turns it into
something you can *look at* — live performance, what is really exposed, your files, your services,
Docker, Redis, packages — drawn in particles instead of packed into tables.

**Nothing is installed on the server. Nothing ever leaves your machine.**

[**⬇ Download for Windows**](https://github.com/Lightminedust/Kubo/releases/latest) &nbsp;·&nbsp;
[**⬇ For Linux**](https://github.com/Lightminedust/Kubo/releases/latest) &nbsp;·&nbsp;
brings its own Java &nbsp;·&nbsp; ~75 MB

<img src="images/files-home.png" alt="Kubo — the file manager" width="90%">

</div>

---

## Why Kubo

You already have a terminal. Kubo doesn't replace it — it sits beside it, so you can manage a
container on a map *and* in a shell at the same time, and the log shows you both. It's built for
the person who runs one server and wants to actually understand it, not decode it.

- **Nothing installed** — Kubo only runs ordinary shell commands over SSH. No agent, no daemon,
  nothing left behind on the server.
- **Nothing leaves your machine** — it talks to your server and to no one else. No telemetry, no
  account, no cloud. Your data stays yours.
- **Every command shown** — everything Kubo sends is listed as it happens and written to a local
  log — the commands, never their output.

---

## What it does

Each screen is the same server told a different way. All of it read-only until you ask for a
change, and every change simulated or confirmed first.

### Files — browse and manage, as a living tree
The folders open left to right, one column per level, every entry a point of light on a fibre.
Right-click to edit, rename, copy, move, set permissions, download or delete; drag files from your
PC onto a folder to upload. Quicker to read — and to trust — than the tools most people put up with.

### Network — see what is really exposed
<img src="images/network.png" alt="Kubo — network" width="90%">

The internet on one side, your server on the other, the firewall as a pane of glass between them.
Ports branch off by how far they can truly be reached — exposed, open, shielded, private, local —
so an open database screams and a loopback-only port stays quiet. Reads whichever firewall you run:
**UFW, firewalld, nftables or iptables**.

### Services — is it running, and will it come back
<img src="images/services.png" alt="Kubo — services" width="90%">

A terminal answers those as two separate questions, and nobody asks both about forty services. So a
server can run for months with something important that will simply not be there after the next
reboot. Kubo asks both for every unit and sorts them by what the two answers add up to: **failed**,
**won't survive a reboot**, **enabled but not running**, **running**, **idle** — each its own
colour. Click one and the tree keeps growing to the right: what holds it up, then what it holds up.

Start, stop, restart, enable, disable. Cap a runaway service's memory or its share of the processor
without restarting it. Send it a signal. Give it settings of its own in a drop-in, so the file your
package shipped is never touched. Write a whole new service with the file tree right there to pick
what it runs. And delete one — but only a unit somebody put in `/etc/systemd/system` by hand, never
a file that belongs to a package.

Stopping or disabling **sshd**, or the network under it, is refused outright rather than confirmed.
That is the one mistake with no way back: the server keeps running, perfectly healthy, and you can
never reach it again.

### The rest

| | |
|---|---|
| ![Scope](images/scope-busy.png) | **Scope** — the machine itself: OS, kernel, CPU, RAM, drawn as a spinning particle sphere with memory, swap, load and steal around it. |
| ![Docker](images/docker.png) | **Docker** — containers, state, CPU/memory, ports and volumes; start/stop/restart, logs, a shell inside, and a read-only browse of the container's files. |
| ![Redis](images/redis.png) | **Redis** — a stack of lit slabs, one per type, with full key CRUD, JSON edit, memory profiling, SLOWLOG and a live CLI. Never runs `KEYS *`. |
| ![Packages](images/packages-open.png) | **Packages** — everything apt/dpkg report as a branching tree: what's for the system, what you asked for, what's waiting. Install and upgrade, simulated first. |

And a connection screen that reads the handshake as a fall of ones and zeros:

<div align="center"><img src="images/connection-connected.png" alt="Kubo — connection" width="70%"></div>

---

## Security

Kubo asks for a lot — SSH access, sometimes root. So it's built so you never have to take that on
faith.

- **Host keys, checked** — first contact shows the fingerprint and asks; a server whose key changed
  is refused outright.
- **Secrets held, then wiped** — passwords live in memory as raw bytes and are wiped after use.
  Saved only if you tick *remember*, encrypted with Windows DPAPI for your account.
- **Root only when you say so** — Kubo never elevates on its own. One button asks for sudo, once per
  session, and every window reads `Kubo_root` while it's on.
- **Nothing destructive by surprise** — changes are simulated or confirmed by typing the name back;
  commands that need root are fixed templates, never built from what you type.
- **Everything on the record** — every command is listed and logged locally: the command and its
  size, never the output or your files.

---

## Install

**Windows** — download **[Kubo Setup](https://github.com/Lightminedust/Kubo/releases/latest)** and
run it. Windows may show an *"unknown publisher"* notice (the installer isn't code-signed yet) —
choose **More info → Run anyway**. Then launch Kubo from the Start menu.

**Linux** — a `.deb` for Debian and Ubuntu, an `.rpm` for Fedora, RHEL, Rocky, Alma and openSUSE,
both on the [releases page](https://github.com/Lightminedust/Kubo/releases/latest). One note: Windows
has DPAPI to encrypt a secret for one account, and Linux has no equivalent every machine is
guaranteed to have — so Kubo simply does not store passwords there, rather than writing one
somewhere it could be read. Key files are still remembered by their path.

**Neither** — the portable editions, a `.zip` and a `.tar.gz`, unfold anywhere and need no installer
and no administrator. Nothing is written to the registry or to `/usr`, and nothing is left behind.

Then enter your server (`user@host`) and connect.

**Your server** just needs to be a normal Linux box with GNU coreutils and `ss` — Debian, Ubuntu,
RHEL, Rocky, Alma, Fedora, Arch, openSUSE… all work. *Packages* needs apt/dpkg (Debian family);
every other screen works anywhere.

---

## About

Kubo is a **[Gemmie](mailto:nellawassi@gmail.com)** product, free to use. It is proprietary
software — the source is not published here, and what ships is obfuscated — but it collects nothing
and phones no one: everything it does happens between your computer and your server. See
[LICENSE](LICENSE.txt) for the terms.

*Found it useful? A ⭐ helps other people find it.*
