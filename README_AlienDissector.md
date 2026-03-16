# 👽 Alien Dissector — Static Malware Analysis Platform

> A dark-themed Python desktop tool for static malware analysis. Load any binary, extract hashes, entropy, PE headers, strings, and query VirusTotal — all from a single GUI.

---

## 🚀 Features

- ✅ Dark hacker-style GUI with green alien mascot
- ✅ Automatic file type detection via magic bytes
- ✅ MD5, SHA-1, SHA-256 hash computation
- ✅ Shannon entropy analysis (file-level and per-section)
- ✅ PE header parsing (architecture, compile time, sections, characteristics)
- ✅ Color-coded risk levels per PE section
- ✅ ASCII string extraction with live search and length filter
- ✅ VirusTotal integration — hash lookup and file upload
- ✅ Full engine-by-engine detection results
- ✅ Tabbed interface: Overview · Strings · VirusTotal

---

## 📋 Requirements

- Python 3.7 or higher
- `requests` library
- `tkinter` (usually included with Python)
- Internet connection (for VirusTotal queries)

---

## 🔧 Installation

### Linux / WSL

```bash
# Install Python and tkinter
sudo apt update
sudo apt install python3 python3-pip python3-tk -y

# Install requests
pip3 install requests
```

### macOS

```bash
brew install python-tk
pip3 install requests
```

### Windows

Tkinter is bundled with the official Python installer from python.org.

```bash
pip install requests
```

---

## ▶️ Running the Program

```bash
python3 alien_dissector.py
```

### WSL note
If the GUI doesn't appear in WSL, install an X server (VcXsrv or Xming) and run:

```bash
export DISPLAY=:0
python3 alien_dissector.py
```

---

## 📖 How to Use

### 1. Load a File
Click **📁 Load File** and select any binary (EXE, DLL, ELF, PDF, ZIP, etc.).

### 2. Run the Analysis
Click **🔬 Analyze**. The tool will instantly compute all static properties locally — no file is sent anywhere at this stage.

### 3. Read the Results

#### 🛸 Overview Tab
The main analysis dashboard. Shows:

| Section | What you get |
|---|---|
| **File Information** | Name, path, size, file type, timestamps, file entropy |
| **Cryptographic Hashes** | MD5 · SHA-1 · SHA-256 |
| **PE Headers** | Architecture, PE type, compile time, characteristics |
| **Entropy Analysis** | Visual bar chart for the file and each PE section |
| **PE Sections** | Name, virtual size, raw size, entropy, risk level |

**Entropy risk thresholds:**

| Entropy | Color | Meaning |
|---|---|---|
| 0.0 – 5.5 | 🟢 Green | Normal data |
| 5.5 – 6.5 | 🟡 Yellow | Possibly compressed |
| 6.5 – 7.0 | 🟠 Orange | Likely packed |
| 7.0 – 8.0 | 🔴 Red | Encrypted / highly obfuscated |

#### 🔤 Strings Tab
Extracts all printable ASCII strings from the binary.

- Set a **minimum length** and click **Filter** to refine results
- Use the **Search** bar to find URLs, registry keys, IP addresses, file paths, or suspicious keywords in real time
- The string count is displayed in the top-right corner

#### 🌐 VirusTotal Tab
Two analysis modes:

| Button | What it does |
|---|---|
| **🔎 Query VirusTotal (hash lookup)** | Searches VT by SHA-256 — fast, no upload |
| **⬆️ Upload & Analyze** | Submits the file to VT and waits for results (max 32 MB) |

Results include:
- Circular gauge showing detections / total engines
- Verdict: 🔴 MALICIOUS · 🟡 SUSPICIOUS · 🟢 CLEAN
- File metadata (name, type, first seen, submission count, reputation)
- Full engine breakdown — malicious detections listed first with threat name

---

## 🔍 Supported File Types

The tool parses **PE headers** for Windows executables and DLLs. For all other file types (ELF, PDF, ZIP, JAR, Mach-O, Office documents, etc.) it still computes hashes, entropy, and strings — and VirusTotal queries work for any file.

Magic byte detection supports:

`PE EXE/DLL` · `ELF` · `ZIP/JAR/APK` · `Mach-O` · `PDF` · `PNG` · `JPEG` · `GIF` · `GZIP` · `BZIP2` · `XZ` · `RAR` · `CAB` · `OLE2 (Office 97-2003)`

---

## ⚠️ Limitations

- VirusTotal free API allows ~500 requests/day and a 32 MB upload cap
- PE section parsing requires a valid PE header; non-PE files show "not a PE file"
- String extraction is ASCII-only (UTF-16 wide strings are not currently extracted)
- VirusTotal upload waits up to ~120 seconds for analysis to complete; if it times out, use the hash lookup after a few minutes

---

## 🐛 Troubleshooting

**`ModuleNotFoundError: No module named 'tkinter'`**
```bash
sudo apt install python3-tk
```

**`Can't connect to display` (WSL)**
```bash
export DISPLAY=:0
```

**VirusTotal returns 404**
The file has never been submitted to VirusTotal. Use **Upload & Analyze** to submit it.

**VirusTotal returns 401 / 403**
The API key may be invalid or rate-limited. Check your daily quota.

---

## 🔐 Security Notes

- All hash computations and string extraction happen **locally** — nothing is sent to the network unless you explicitly click a VirusTotal button
- The VirusTotal API key is embedded in the source; keep the file private or move the key to an environment variable if sharing the code
- Results may contain sensitive indicators — handle them responsibly

---

## 📄 License

Provided **as-is** for educational and security research purposes.

---

## 🔄 Version

**v1.0.0** — Initial release

---

**Stay curious. Dissect everything. 👽🔬**
