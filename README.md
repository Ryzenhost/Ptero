# RYZENNC Panel

Made by ryzennc

## Quick Automated Setup (Recommended)

Run the automated management script:

```bash
bash install.sh
```

Menu options:

1. **Initialize Main Panel** – installs Node.js, Docker, PM2, dependencies, builds & starts on port 6767
2. **Initialize Dev Panel** – developer mode on port 3000
3. **Update & Auto-Repair**
4. **Create / Reset Owner**
5. **System & Service Status**
6. **Cloudflare Tunnel** – paste the Debian command from Cloudflare to run a tunnel
7. **Uninstall RYZENNC Panel**
0. **Exit**

Shortcuts: `bash install.sh main`, `bash install.sh dev`, `bash install.sh cloudflare`

---

## Cloudflare Tunnel

`bash install.sh` → **[6] Cloudflare Tunnel** → **[1] Tạo / chạy tunnel**

1. Vào https://one.dash.cloudflare.com → Networks → Tunnels → **Create a tunnel** → Cloudflared.
2. Đặt tên tunnel, chọn **Debian** (64-bit).
3. Copy dòng lệnh `cloudflared service install eyJ...` và dán vào menu. Script tự cài cloudflared và chạy tunnel (systemd, hoặc PM2/nohup nếu không có systemd).
4. Trong dashboard, tab **Public Hostname**: chọn domain, Service = `HTTP`, URL = `localhost:6767`.

Menu còn có xem trạng thái và gỡ tunnel. Trạng thái chạy lưu trong `.cloudflare.env` (git-ignored).

---

## GitHub Build

`.github/workflows/build.yml` runs on every push / PR to `main`, on tags `v*`, and manually (Actions → *Build ryzennc* → *Run workflow*):

- installs dependencies, runs `npm run build`, verifies `dist/server.cjs` + `dist/index.html`
- uploads `ryzennc-dist.tar.gz` as an artifact
- on tag `v*` → publishes a GitHub Release with the archive
- on push → builds & pushes the Docker image to `ghcr.io/<owner>/<repo>`

Release example:

```bash
git tag v3.0.1 && git push origin v3.0.1
```

---

## Manual Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/Ryzenhost/ryzenhost.git
   cd ryzennc
   ```
2. Install dependencies: `npm install`
3. Build: `npm run build`
4. Create an admin user: `npm run createuser`
5. Start (port 6767): `npm run start`

## Development

```bash
npm run dev   # port 3000
```
