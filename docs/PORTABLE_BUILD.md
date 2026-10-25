# ⚙️ Οδηγός Δημιουργίας Portable Έκδοσης (Portable Build Guide)

Το **myWhiteboard** διαθέτει πλήρη υποστήριξη για δημιουργία **αυτόνομου εκτελέσιμου αρχείου (Portable .exe)** για Windows, το οποίο εκτελείται άμεσα χωρίς ανάγκη εγκατάστασης, δικαιωμάτων διαχειριστή ή εγκατεστημένου Node.js στον υπολογιστή-στόχο.

---

## 🚀 1. Προαπαιτούμενα για τη Μεταγλώττιση (Build Environment)

Για να δημιουργήσετε το εκτελέσιμο αρχείο από τον πηγαίο κώδικα, απαιτούνται:
1. **Node.js:** Έκδοση 18 ή νεότερη (προτείνεται LTS έκδοση).
2. **Git:** Για τη διαχείριση εκδόσεων.
3. **Electron Builder:** Είναι ήδη καταχωρημένο στα `devDependencies` του [`package.json`](../package.json).

---

## 🔨 2. Εντολές Μεταγλώττισης (Build Commands)

Ανοίξτε τερματικό (PowerShell, CMD ή Bash) στον ριζικό φάκελο του έργου και εκτελέστε:

### Α. Δημιουργία Portable Εκτελέσιμου
```bash
npm run build:portable
```
- **Αποτέλεσμα:** Δημιουργεί το αρχείο `dist/myWhiteboard-Portable-1.4.0.exe`.
- **Μέγεθος:** Περίπου 107 MB.
- **Πλεονέκτημα:** Μπορεί να αντιγραφεί σε USB stick και να τρέξει άμεσα σε οποιονδήποτε υπολογιστή τάξης ή εργαστηρίου χωρίς εγκατάσταση.

### Β. Δημιουργία Εγκαταστάτη Windows (Setup Installer)
```bash
npm run build:setup
```
- **Αποτέλεσμα:** Δημιουργεί τον επίσημο NSIS installer `dist/myWhiteboard-Setup-1.4.0.exe` για κανονική εγκατάσταση στα Windows, με επιλογή φακέλου εγκατάστασης, συντομεύσεις στην Επιφάνεια Εργασίας και στο μενού Έναρξη, καθώς και πρόγραμμα απεγκατάστασης (uninstaller).

### Γ. Ταυτόχρονη Δημιουργία Όλων (Portable + Setup)
```bash
npm run build:all
```
- **Αποτέλεσμα:** Παράγει ταυτόχρονα και τα δύο πακέτα διανομής (`Portable` και `Setup`) στον φάκελο `dist/`.

---

## 🛠️ 3. Τεχνικές Ρυθμίσεις (package.json)

Η παραμετροποίηση του `electron-builder` βρίσκεται στο πεδίο `"build"` του `package.json`:

```json
"build": {
  "appId": "com.pliroforikos.mywhiteboard",
  "productName": "myWhiteboard",
  "directories": {
    "output": "dist"
  },
  "win": {
    "icon": "assets/icons/icon.ico",
    "target": [
      {
        "target": "portable",
        "arch": ["x64"]
      }
    ]
  },
  "portable": {
    "artifactName": "${productName}-Portable-${version}.${ext}"
  }
}
```

---

## 📦 4. Διανομή στους Μαθητές & στα Σχολεία

1. Αντιγράψτε το αρχείο `myWhiteboard-Portable-1.0.0.exe` σε ένα USB flash drive ή αναρτήστε το στο σχολικό δίκτυο / Google Drive / Microsoft Teams / e-class.
2. Ο μαθητής ή ο εκπαιδευτικός κάνει απλώς **διπλό κλικ** στο αρχείο και η εφαρμογή ανοίγει άμεσα.
3. Όλες οι γραμματοσειρές (Google Roboto), τα εικονίδια και τα εκπαιδευτικά δεδομένα είναι ενσωματωμένα (100% offline).
