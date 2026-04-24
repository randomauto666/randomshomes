# 🏠 RandomsHomes

Ein feature-reiches **Home-Plugin** für Minecraft **1.21.11** (Paper/Bukkit), entwickelt von **RandomAuto**.

---

## ✨ Features

- 📍 Homes setzen, löschen und zu ihnen teleportieren
- 🖥️ Übersichtliches **54-Slot GUI** mit Glasscheiben-Rand
- 🟢 Gesetzte Homes erscheinen **grün** im GUI
- 🖱️ **Rechtsklick** zum Teleportieren, **Linksklick** zum Löschen (mit Bestätigungs-GUI)
- ⏱️ Konfigurierbarer **Teleport-Delay** mit optionalem Abbruch bei Bewegung
- 🔒 **Permission-basierte Home-Limits** (`homes.home.1` bis `homes.home.30`)
- 🛡️ **Sicherheitsprüfung** beim Setzen eines Homes (Void, Flüssigkeit, eingemauert, gefährliche Blöcke)
- 💾 Datenspeicherung in einer lokalen **SQLite-Datenbank** (`database.db`)
- 💬 Alle Nachrichten vollständig in `messages.yml` anpassbar
- ⚙️ Alle Einstellungen zentral in `config.yml`

---

## 📋 Befehle

| Befehl | Beschreibung | Permission |
|--------|-------------|------------|
| `/sethome <name>` | Setzt ein Home an deiner aktuellen Position | `homes.use` |
| `/delhome <name>` | Löscht ein Home | `homes.use` |
| `/home <name>` | Teleportiert dich zu einem Home | `homes.use` |
| `/homes` | Öffnet das Homes-GUI | `homes.use` |

---

## 🔑 Permissions

| Permission | Beschreibung | Standard |
|------------|-------------|----------|
| `homes.use` | Erlaubt die Nutzung aller Home-Befehle | `true` |
| `homes.home.1` | Maximal 1 Home | `false` |
| `homes.home.2` | Maximal 2 Homes | `false` |
| `homes.home.3` | Maximal 3 Homes | `true` |
| `homes.home.5` | Maximal 5 Homes | `false` |
| `homes.home.10` | Maximal 10 Homes | `false` |
| `homes.home.15` | Maximal 15 Homes | `false` |
| `homes.home.20` | Maximal 20 Homes | `false` |
| `homes.home.25` | Maximal 25 Homes | `false` |
| `homes.home.30` | Maximal 30 Homes | `false` |
| `homes.admin` | Admin-Zugang | `op` |

> **Hinweis:** Es gilt immer die höchste zutreffende Permission. Das absolute Maximum beträgt **28 Homes** (begrenzt durch die GUI-Größe, keine Seiten).

---

## 🖥️ GUI

### Homes-GUI (`/homes`)
Das Hauptmenü zeigt alle gesetzten Homes übersichtlich an.

- **Außenrand** → Glasscheiben (Dekorations-Border)
- **Grauer Slot** → Freier, verfügbarer Home-Slot
- **Grüner Slot** → Gesetztes Home mit Name, Welt und Koordinaten
  - 🖱️ **Rechtsklick** → Teleportieren
  - 🖱️ **Linksklick** → Löschen (öffnet Bestätigungs-GUI)
- **Gesperrter Slot** → Über dem eigenen Limit (gefüllt mit Glasscheibe)

### Bestätigungs-GUI
Vor dem Löschen eines Homes öffnet sich ein 27-Slot Bestätigungsfenster:

- 🟢 **Grün** → Löschen bestätigen
- 🟡 **Gelb** → Info-Anzeige (Home-Name)
- 🔴 **Rot** → Abbrechen und zurück

---

## 🛡️ Sicherheitsprüfung

Beim Ausführen von `/sethome` wird automatisch geprüft, ob die Position sicher ist:

| Grund | Beschreibung |
|-------|-------------|
| **Void** | Y-Position liegt unterhalb der Weltgrenze |
| **Flüssigkeit** | Spieler steht in Wasser oder Lava |
| **Eingemauert** | Füße- oder Kopfblock ist solid und nicht passierbar |
| **Gefährlicher Block** | Lava, Feuer, Magma, Kaktus, Lagerfeuer, Wither Rose, Beerenbusch |

Die Sicherheitsprüfung kann in der `config.yml` deaktiviert werden:
```yaml
safety-check:
  enabled: false
```

---

## ⚙️ Konfiguration

### `config.yml`
```yaml
# Standard-Limit wenn keine spezifische Permission gesetzt ist
default-max-homes: 3

# Sicherheitsprüfung beim /sethome
safety-check:
  enabled: true

# Teleport-Einstellungen
teleport:
  delay: 3              # Sekunden bis zur Teleportation (0 = sofort)
  cancel-on-move: true  # Abbruch bei Bewegung

# GUI-Einstellungen
gui:
  title: "&f&lMeine Homes"
  border-material: GRAY_STAINED_GLASS_PANE
  empty-material: GRAY_DYE
  home-material: GREEN_DYE
  confirm-title: "&c&lHome löschen?"
```

### `messages.yml`
Alle Nachrichten sind vollständig anpassbar. Verfügbare Platzhalter:

| Platzhalter | Beschreibung |
|-------------|-------------|
| `{prefix}` | Plugin-Prefix (`&f&lRandomsHomes &7»`) |
| `{home}` | Name des Homes |
| `{max}` | Maximale Anzahl erlaubter Homes |
| `{delay}` | Teleport-Verzögerung in Sekunden |
| `{world}` | Weltname des Homes |
| `{x}` `{y}` `{z}` | Koordinaten des Homes |

---

## 💾 Datenspeicherung

Alle Homes werden in einer lokalen SQLite-Datenbank gespeichert:

```
plugins/RandomsHomes/
├── config.yml       ← Konfiguration
├── messages.yml     ← Nachrichten
└── database.db      ← Homes-Datenbank (SQLite)
```

---

## 🔨 Build

**Voraussetzungen:**
- Java 21+
- Maven 3.8+

```bash
git clone https://github.com/RandomAuto/RandomsHomes.git
cd RandomsHomes
mvn clean package
```

Die fertige JAR-Datei befindet sich anschließend unter `target/RandomsHomes-1.0.0.jar`.

---

## 📦 Installation

1. JAR-Datei in den `plugins/`-Ordner deines Servers kopieren
2. Server starten — die Konfigurationsdateien werden automatisch erstellt
3. Nach Bedarf `config.yml` und `messages.yml` anpassen
4. `/reload confirm` oder Server-Neustart

**Kompatibilität:** Paper / Bukkit · Minecraft **1.21.11** · Java **21**

---

## 📄 Lizenz

Dieses Projekt steht unter der **MIT License** — siehe [LICENSE](LICENSE) für Details.

---

<div align="center">
  Entwickelt von <strong>RandomAuto</strong>
</div>
