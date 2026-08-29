---
title: GNU Stow
draft: false
summary: Dotfile-Verwaltung
--- 
## Problem

Die manuelle Installation und Konfiguration meiner Systemumgebung und meiner Programme
ist fehleranfällig und erfordert viel Zeit. Wenn ich eine neue Distribution
ausprobieren möchte, möchte ich, dass meine Standardprogramme gleich konfiguriert
werden.

## Lösung

Über Stow lassen sich Konfigurationen(Dotfiles) einfach, gebündelt verwalten.
Da Stow als Symlink-Manager fungiert, können die Konfigurationsdateien in einem
Verzeichnis, inkl. Git-Repository, gehalten werden und die zugehörigen Symlinks
können an den richtigen Stellen im System (z.B. '~/.config/') generiert werden.

## Umsetzung

### Ordnerstruktur erstellen

#### Zentraler Dotfiles-Ordner

```bash
mkdir ~/.dotfiles
```

#### Programmordern erstellen (NeoVim als Beispiel)

```bash
cd ~/.dotfiles
mkdir -p ./nvim/.config/nvim
```

### Symlinks generieren

```bash
cd ~/.dotfiles
stow nvim
```

## Fazit

GNU Stow nimmt sehr viel Komplexität aus der Verwaltung von Dotfiles.
Gemeinsam mit einem Versionskontrollsystem wie Git lässt sich so ein
neues System in kürzester Zeit kontrolliert einrichten und synchronisieren.
