# CRM BizHub

A small Flask-based demo app for checkout and Lightning-style payments.

This repository contains a lightweight web app (Flask) that serves a simple storefront/checkout flow and includes helpers for integrating with Lightning Network Daemon (LND) and generating QR codes.

## Features

- Simple product listing and checkout UI (templates in `templates/`).
- QR code generation for payments (uses `qrcode` and `Pillow`).
- LND helper code in `lnd_client.py` to interact with a Lightning node (project-specific — configure before using).
- A small detection utility in `polar_detect.py` (project-specific usage).

## Requirements / Dependencies

This project uses the Python packages listed in `requirements.txt`. At time of writing these include:

- flask
- requests
- qrcode
- Pillow

Install them with:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Quick start (development)

1. Create and activate a virtual environment and install dependencies (see above).
2. Run the app:

```bash
# Option 1: run with python
python app.py

# Option 2: with flask if you prefer
export FLASK_APP=app.py
flask run
```

3. Open a browser at http://127.0.0.1:5000

Note: The project may rely on additional configuration (LND credentials, certs, environment variables). See the "LND / configuration" section below.

## LND / Configuration notes

This project includes `lnd_client.py` which is intended to interface with an LND node. The repository does not include credentials or certs. To use Lightning features:

- Configure `lnd_client.py` or provide environment variables / configuration files with the host, macaroon, and TLS certificate paths for your LND node.
- Ensure your node and credentials are secured and not committed to source control.

If you're not using LND locally, the rest of the app (product page, checkout UI, QR generation) should still work.

## Project structure

- `app.py` — Flask application entry point and route handlers.
- `lnd_client.py` — helper(s) to connect to an LND node (Lightning Network).
- `polar_detect.py` — detection utility used by the app (project-specific logic).
- `products.json` — example product data used by the storefront.
- `requirements.txt` — Python dependencies.
- `templates/` — Jinja2 templates (index, checkout, success, error, base).
- `static/` — static assets (CSS, images).

## How it works (short)

The app serves a product listing (from `products.json`). The checkout flow calls into server-side code which may create payment requests or QR codes. QR images are generated using the `qrcode` package and served to the client where appropriate.

## Troubleshooting

- Missing dependency errors: confirm your virtualenv is active and `pip install -r requirements.txt` completed successfully.
- LND connection failures: verify your host, macaroon, and TLS certificate paths; check firewall and that your LND node is accessible.
- Template or static file errors: check that the `templates/` and `static/` folders exist and contain the expected files.

## Contributing

Small improvements, bug fixes, or documentation additions are welcome. Please open an issue or a pull request with a short description of the change.

## License

This repository has no license file included. If you want a permissive license, consider adding an `MIT` license file. Until then, assume default copyright.

---

If you'd like, I can:

- add an example `.env` or sample config for `lnd_client.py` (non-sensitive placeholders),
- add a minimal `Procfile` or Dockerfile for deployment, or
- add a LICENSE file (MIT) and commit it.

Tell me which follow-up you'd like and I'll implement it.