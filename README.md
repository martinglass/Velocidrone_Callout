# Velocidrone_Callout
A lightweight, high-performance browser-based dashboard that connects to the Velocidrone FPV Simulator

readme_content = """# Velocidrone Live Lap Callout

A lightweight, high-performance browser-based dashboard that connects to the **Velocidrone FPV Simulator** via WebSockets to provide real-time, text-to-speech (TTS) voice announcements for race timing events. 

Designed for FPV drone pilots and race coordinators, this application monitors incoming telemetry feeds, filters data based on an adjustable pilot whitelist, tracks personal records across tracks, and queues spoken announcements seamlessly.

---

## 🚀 Features

### 1. Telemetry WebSocket Layer
* **Live Connection Tracker**: Connects seamlessly to Velocidrone's broadcast address (`localhost:60003` by default).
* **Automatic Reconnection**: If the simulator is closed or a network drop happens, a silent background routine automatically retries the connection every 3 seconds.
* **De-cluttered Terminal Logging**: Suppresses repetitive loop warnings, printing connection statuses and "Simulator unreachable" notices exactly once per event cycle.
* **Binary Frame Resolution**: Built-in `Blob` data-type conversion to safely parse binary telemetry frames directly into standard application JSON.

### 2. Audio Announcement Engine
* **Web Speech TTS Integration**: Detects and exposes native browser voice targets available on your operating system.
* **Granular Controls**: Real-time adjustment sliders for audio volume and reading speed (speech rate).
* **Smart Audio Queueing**:
  * **Speak Everything**: Safe sequential layout spacing announcements 1.8 seconds apart.
  * **Skip Low Priority**: Drops normal lap updates if more than 2 high-priority callouts (like Personal Bests) accumulate.
  * **Latest Only**: Drops lagging queue rows to immediately state the absolute newest telemetry milestone.

### 3. Directives & Dynamic Templates
* **Toggle Options**: Separately toggle announcements for normal Lap Times, Personal Bests (PBs), Race Fastest Laps, and Race Finishes.
* **Holeshot Tracker**: Auto-detects the opening lap gate crossing. Configurable to trigger for the first pilot overall (`first_only`), an explicit target UID (`one_selected`), or ignored completely.
* **Custom Format Templates**: Format output text using reactive wildcards:
  * `{pilot}` - Resolves to the pilot callsign.
  * `{lap_number}` - Current lap integer.
  * `{lap_time}` - Formatted lap time string (accurate to two decimal positions).

### 4. Active Pilot Whitelist Grid
* **Targeted Monitoring**: A reactive data table showing active pilot profiles. Only pilots checked in the **Announce** column will trigger audio updates.
* **Configurable PBs**: Tracks separate personal best times dynamically per individual track name.
* **Manual Manipulation**: Add or remove pilots manually using inline inputs.

### 5. Configuration Profile Management
* **Persistent Storage**: Saves all interface fields, volume sliders, templates, and pilot records automatically inside the browser's local sandbox data cache (`localStorage`).
* **Importing Configuration**: Instantly load external `config.json` files. **Note: Importing a file completely overwrites all current browser profiles and pilots rather than merging.**
* **Exporting Configuration**: Downloads your live setup data as a cleanly formatted, portable `config.json` file for backups or sharing.

---

## 🛠️ Setup & Installation

No installations, Node servers, or terminal commands are required. The program runs entirely client-side inside any modern web browser.

1. Download or save the application file as `VD_Callout.html`.
2. Double-click or drag the file into your preferred internet browser (Google Chrome, Microsoft Edge, or Apple Safari are recommended for best Web Speech API voice selections).
3. Ensure Velocidrone is running on the same computer (or an accessible local network IP).
4. Launch a race mode in Velocidrone. Ensure the simulation setup has its external websocket data transmission active.
5. Click **Connect** on the dashboard. The status banner will flip to a green **Connected** alert, and the background log terminal will note tracking updates.

---

## 📂 Configuration Format (`config.json`)

The structure used for profile sharing is outlined below. The application generates this layout natively upon executing an **Export**:
