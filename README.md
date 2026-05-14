# Random Numbers Generator (Flask + Socket.IO)

A lightweight real-time web application that continuously generates random numbers on the server and streams them to connected clients using WebSockets.

## Overview

This project serves a simple dashboard where users can watch random numbers update live every second.  
It is built with:

- **Flask** for the web server and template rendering
- **Flask-SocketIO** for real-time communication
- **Eventlet/Gunicorn** for production deployment

> Note: The repository name mentions FastAPI, but the current implementation uses Flask + Flask-SocketIO.

## Features

- Real-time number broadcasting via Socket.IO
- Server-generated random integer values from **1 to 100**
- Auto-updating dashboard without manual refresh
- Minimal codebase, easy to understand and extend

## Project Structure

```text
.
├── app.py                  # Main Flask app and Socket.IO event handling
├── random_number.py        # Random number generation logic
├── templates/
│   └── index.html          # Frontend dashboard
├── requirement.txt.txt     # Python dependencies
└── Procfile                # Production startup command
```

## How It Works

1. A client opens `/` and loads `templates/index.html`.
2. The browser establishes a Socket.IO connection.
3. On each client connection, the server starts a background task.
4. The background task emits a `new_number` event every second.
5. The frontend listens for `new_number` and updates the UI in real time.

## Prerequisites

- Python 3.9+ (recommended)
- pip

## Installation

```bash
git clone https://github.com/ArokiyaNithish/Random-Numbers-Generator-using-Fastapi.git
cd Random-Numbers-Generator-using-Fastapi
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirement.txt.txt
```

## Run Locally

```bash
python app.py
```

Then open your browser at:

```text
http://127.0.0.1:5003/
```

## Production Run

The repository includes this `Procfile` command:

```bash
gunicorn -k eventlet -w 1 app:app
```

## Socket Event Contract

- **Event name:** `new_number`
- **Payload format:**

```json
{
  "number": 42
}
```

## Configuration Notes

- Default development port: `5003` (set in `app.py`)
- CORS for Socket.IO is currently open: `cors_allowed_origins="*"`

## Troubleshooting

- If dependencies fail to install, upgrade pip:
  ```bash
  python -m pip install --upgrade pip
  ```
- If the app starts but numbers do not update, check browser console logs and server logs for Socket.IO connection issues.

## Future Improvements

- Prevent multiple background tasks per client connection
- Add automated tests
- Add environment-based configuration for host/port/CORS
- Add CI checks (lint/test)

## License

No license file is currently included.  
If you plan to open-source this project publicly, add a license such as MIT.

