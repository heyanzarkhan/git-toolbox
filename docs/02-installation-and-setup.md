# 2 · Installation &amp; Setup

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: What is Git?](01-what-is-git.md) &nbsp;·&nbsp; Next: [Core Concepts ➡️](03-core-concepts.md)

---

By the end of this chapter you'll have Git installed, identified yourself to it, and (optionally) connected securely to GitHub via SSH.

---

## Installing Git

### 🪟 Windows

1. Download the installer from **[git-scm.com/download/win](https://git-scm.com/download/win)**.
2. Run it. The defaults are sensible — you can click *Next* through most of it.
3. This also installs **Git Bash**, a terminal that gives you a Unix-like shell on Windows (recommended for following any Git tutorial).

Or with a package manager:
```bash
winget install --id Git.Git -e
# or
choco install git
```

### 🍎 macOS

The easiest way is **[Homebrew](https://brew.sh)**:
```bash
brew install git
```
Alternatively, running `git --version` for the first time will prompt you to install the Xcode Command Line Tools, which include Git.

### 🐧 Linux

```bash
# Debian / Ubuntu
sudo apt update && sudo apt install git

# Fedora
sudo dnf install git

# Arch
sudo pacman -S git
```

### ✅ Verify the installation

```bash
git --version
# → git version 2.43.0   (any recent version is fine)
```

If you see a version number, you're ready. 🎉

---

## First-time configuration

Git attaches **your name and email to every commit** you make. Set them once, globally:

```bash
git config --global user.name "Anzar Khan"
git config --global user.email "you@example.com"
```

> 💡 Use the **same email you'll use on GitHub** so your commits link to your profile. Want to keep your real email private? GitHub gives you a `noreply` address (Settings → Emails) like `12345+username@users.noreply.github.com`.

### Recommended sane defaults

```bash
# Name the initial branch "main" instead of "master"
git config --global init.defaultBranch main

# Set your default editor (examples)
git config --global core.editor "code --wait"   # VS Code
git config --global core.editor "nano"           # nano

# Make 'git pull' use a clean fast-forward/merge by default
git config --global pull.rebase false

# Better, more readable diffs and colored output
git config --global color.ui auto

# Remember credentials so you don't retype them (macOS example)
git config --global credential.helper osxkeychain
# Windows: manager  |  Linux: cache or libsecret
```

### Handy aliases (shortcuts)

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --decorate --all"
```
Now `git st` runs `git status`, and `git lg` shows a pretty history graph.

### Check your configuration

```bash
git config --list                 # show everything
git config user.name              # show one value
git config --global --edit        # open the global config file in your editor
```

Your global settings live in `~/.gitconfig` (or `C:\Users\You\.gitconfig` on Windows).

---

## Connecting to GitHub securely (SSH)

When you push/pull to GitHub, you authenticate. You have two options:

| Method | URL looks like | Notes |
| --- | --- | --- |
| **HTTPS** | `https://github.com/user/repo.git` | Simplest; uses a token/credential helper |
| **SSH** | `git@github.com:user/repo.git` | Set up once, never type a password again |

Here's how to set up **SSH keys** (recommended):

### 1. Generate a key
```bash
ssh-keygen -t ed25519 -C "you@example.com"
# Press Enter to accept the default location; set a passphrase if you like
```

### 2. Start the agent and add your key
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### 3. Copy your **public** key
```bash
# macOS
pbcopy < ~/.ssh/id_ed25519.pub
# Linux (with xclip)
xclip -sel clip < ~/.ssh/id_ed25519.pub
# Windows (Git Bash)
clip < ~/.ssh/id_ed25519.pub
```

### 4. Add it to GitHub
Go to **GitHub → Settings → SSH and GPG keys → New SSH key**, paste, and save.

### 5. Test it
```bash
ssh -T git@github.com
# → Hi username! You've successfully authenticated...
```

> 🔒 You share the `.pub` (**public**) key. **Never** share the private key (`id_ed25519` with no extension).

---

## ✅ Key takeaways

- Install Git from [git-scm.com](https://git-scm.com) or your package manager; verify with `git --version`.
- Set `user.name` and `user.email` globally — they stamp every commit.
- Configure `init.defaultBranch`, your editor, and a few aliases to make life easier.
- Use **SSH keys** to talk to GitHub without retyping passwords.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: What is Git?](01-what-is-git.md) &nbsp;·&nbsp; Next: [3 · Core Concepts ➡️](03-core-concepts.md)
