# Velocidrone_Callout - hear holeshot times, lap times and race times for pilots racing in Velocidrone, using system Text-to-Speech voices and languages.

A lightweight, high-performance browser-based dashboard that connects to the **Velocidrone FPV Simulator** via WebSockets to provide real-time, text-to-speech (TTS) voice announcements for race timing events. 

Designed for FPV drone pilots and race coordinators, this application monitors incoming telemetry feeds, filters data based on an adjustable pilot whitelist, tracks personal records across tracks, and queues spoken announcements seamlessly.

---

## 🚀 Features

### 1. Telemetry WebSocket Layer
* **Live Connection Tracker**: Connects to Velocidrone's broadcast address (eg `192.168.0.1:60003`). Websocket requires the actual IP address, not localhost or 127.0.0.1

### 2. Audio Announcement Engine
* **Web Speech TTS Integration**: Detects and exposes native browser voice targets available on your operating system, with real-time adjustment sliders to change the voice, volume and speed.
* **Smart Audio Queueing Options**:
  * **Speak Everything**: Safe sequential layout spacing announcements 1.8 seconds apart.
  * **Skip Low Priority**: Drops normal lap updates if more than 2 high-priority callouts (like Personal Bests) accumulate.
  * **Latest Only**: Drops lagging queue rows to immediately state the absolute newest telemetry milestone.

### 3. Directives & Dynamic Templates
* **Toggle Options**: Separately toggle announcements for normal Lap Times, Personal Bests (PBs), Race Fastest Laps, and Race Finishes.
* **Holeshot Tracker**: Auto-detects the opening lap gate crossing. Configurable to trigger for the first pilot overall (`first_only`), an explicit target UID (`one_selected`), or ignored completely.
* **Custom Format Templates**: Format output text using reactive wildcards, for example:
  * `{pilot}` - Resolves to the pilot callsign.
  * `{lap_number}` - Current lap integer.
  * `{lap_time}` - Formatted lap time string (accurate to two decimal positions).

### 4. Active Pilot Whitelist Grid
* **Autoupdate Pilot List**: Updates Pilot List from pilots in active races.
* **Targeted Monitoring**: A reactive data table showing active pilot profiles. Only pilots checked in the **Announce** column will trigger audio updates.
* **Configurable PBs**: Tracks separate personal best times dynamically per individual track name (awaiting Velocidrone to implement tracknames over Websocket).
* **Manual Manipulation**: Add or remove pilots manually using inline inputs.

### 5. Configuration Profile Management
* **Persistent Storage**: Saves all interface fields, volume sliders, templates, and pilot records automatically inside the browser's local sandbox data cache (`localStorage`).
* **Importing Configuration**: Instantly load external `config.json` files. **Note: Importing a file completely overwrites all current browser profiles and pilots rather than merging.**
* **Exporting Configuration**: Downloads your live setup data as a cleanly formatted, portable `config.json` file for backups or sharing.

---

## 🛠️ Setup & Installation

No installations, Node servers, or terminal commands are required. The program runs entirely client-side inside any modern web browser.

1. Change directory to application folder - can be on same computer as Velocidrone or another, or an accessible local network IP.
2. Download or save the application file as `VD_Callout.html` into the application folder.
3. Double-click or drag the file into your preferred internet browser (Google Chrome, Microsoft Edge, or Apple Safari are recommended for best Web Speech API voice selections).
4. Ensure Velocidrone is running on the same computer, or an accessible local network IP.
5. Launch a race mode in Velocidrone. Ensure the simulation setup has its external websocket data transmission active (in Velocidrone Options General Menu).
6. In **Terminal** run the command **python -m http.server 8000** (or python3 -m http.server 8000).
7. The application will attempt to auto-connect and the status banner will flip to a green **Connected** alert if successful. 
8. The background log terminal will note tracking updates and Websocket packets.

---

## 📂 Troubleshooting

1. Examine the Websocket log shown on the webpage for possible clues.
2. Refreshing the browser webpage will force a reload and restart.
3. Closing the python thread will force the application to halt.
