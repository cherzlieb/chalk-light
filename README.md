# chalk-light 🖍️

Eine extrem Leichtgewichtige, Abhängigkeitsfreie (Dependency-Free) JavaScript-Bibliothek zur Formatierung und Einfärbung von Konsolenausgaben in Node.js mittels ANSI-Escape-Sequenzen und JavaScript Proxies.

Inspirierte Implementierung des beliebten `chalk`-Pakets, aber ohne externe Abhängigkeiten und mit minimalistischem Fußabdruck.

---

## 🚀 Features

- 📦 **Keine Abhängigkeiten**: Pure JavaScript (ES6+).
- ⚡ **Extrem leicht**: Nur wenige Zeilen Code dank `Proxy`.
- 🔗 **Chaining-Support**: Stile beliebig miteinander kombinieren (`chalk.bold.red('Text')`).
- 🎨 **RGB & TrueColor Support**: Dynamische 24-Bit-Farben für Vorder- und Hintergrund (`rgb(r,g,b)` & `bgRgb(r,g,b)`).
- 🪶 **Zero Config**: Einfach importieren und direkt nutzen.

---

## 📦 Installation / Einbindung

Füge die Dateien `stylesMap.js` und den `chalk-light`-Code in dein Projekt ein oder erstelle ein passendes Modul:

```bash
// Beispiel Dateistruktur:
├── stylesMap.js
└── index.js
```

> [!NOTE]
> Die `stylesMap.js` ist aktuell Teil der `index.js` kann aber ausgelagert werden, wenn man noch mehr Styles hinzufügen will.

---

## 💡 Benutzung

### 1. Basisselektoren (Farben & Stile)

```javascript
import chalk from './index.js';

// Einfache Farben
console.log(chalk.red('Das ist roter Text!'));
console.log(chalk.green('Erfolg: Vorgang abgeschlossen!'));
console.log(chalk.blue('Information: Verbindung hergestellt.'));

// Textformatierung
console.log(chalk.bold('Fetter Text'));
console.log(chalk.italic('Kursiver Text'));
console.log(chalk.underline('Unterstrichener Text'));
console.log(chalk.strikethrough('Durchgestrichener Text'));
```

---

### 2. Chaining (Stile kombinieren)

Du kannst beliebig viele Stile und Hintergrundfarben aneinanderketten:

```javascript
// Kombination aus Stil, Farbe und Hintergrund
console.log(chalk.bold.red('Fett und Rot'));
console.log(chalk.underline.bgYellow.black('Unterstrichen, gelber Hintergrund und schwarzer Text'));
console.log(chalk.italic.bgBlue.white('Kursiv mit blauem Hintergrund'));
```

---

### 3. Dynamische RGB-Farben (True Color)

`chalk-light` unterstützt vollständige 24-Bit RGB-Farben für benutzerdefinierte Farbtöne:

```javascript
// Vordergrundfarbe per RGB
console.log(chalk.rgb(255, 136, 0)('Wunderschönes Orange!'));

// Hintergrundfarbe per RGB
console.log(chalk.bgRgb(15, 23, 42).white('Dunkelblauer Hintergrund mit weißem Text'));

// RGB mit Verkettung (Chaining)
console.log(chalk.bold.rgb(236, 72, 153).bgRgb(30, 41, 59)('Styled RGB Text'));
```

---

## 📋 Verfügbare Stile & Farben

### **Textstile**
- `bold` (Fett)
- `dim` (Blass / Dimmed)
- `italic` (Kursiv)
- `underline` (Unterstrichen)
- `inverse` (Farben umkehren)
- `hidden` (Versteckt)
- `strikethrough` (Durchgestrichen)

### **Vordergrundfarben**
- `black`, `red`, `green`, `yellow`, `blue`, `magenta`, `cyan`, `white`, `gray`

### **Hintergrundfarben**
- `bgBlack`, `bgRed`, `bgGreen`, `bgYellow`, `bgBlue`, `bgMagenta`, `bgCyan`, `bgWhite`

### **Dynamische Funktionen**
- `rgb(r, g, b)` – 24-Bit-RGB-Vordergrundfarbe (0-255)
- `bgRgb(r, g, b)` – 24-Bit-RGB-Hintergrundfarbe (0-255)

---

## ⚙️ Wie es funktioniert

`chalk-light` nutzt den JavaScript **`Proxy`**-Mechanismus:

1. Beim Zugriff auf Eigenschaften (z.B. `.red`, `.bold`) liest der Proxy die ANSI-Codes aus der `styles`-Map.
2. Der Proxy erzeugt rekursiv ein neues `chalk`-Objekt mit der erweiterten Liste an ANSI-Codes.
3. Sobald die Funktion aufgerufen wird (`('Dein Text')`), werden alle gesammelten ANSI-Startcodes vorangestellt und die Endcodes in umgekehrter Reihenfolge angehängt, um die Formatierung sauber zu schließen.

---

## 📄 Lizenz

MIT
