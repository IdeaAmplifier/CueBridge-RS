<p align="center">
  <img src="docs/figures/icon.png" width="104" alt="CueBridge RS">
</p>

<h1 align="center">CueBridge RS</h1>

<p align="center"><b>SSL Live ↔ REAPER, for live multitrack recording.</b><br>
Every console scene becomes a named marker. The console's own transport drives REAPER.<br>
One network cable, no ipMIDI driver, no counting scenes by hand.</p>

<p align="center"><b>SSL Live ↔ REAPER，為現場多軌錄音而做。</b><br>
控台每個 scene 都變成具名 marker，控台自己的 transport 直接控制 REAPER。<br>
一條網路線，不需要 ipMIDI 驅動，也不用手動數 scene。</p>

<p align="center">
  <img alt="Coming soon" src="https://img.shields.io/badge/status-coming_soon-orange?style=for-the-badge">
  <img alt="Version" src="https://img.shields.io/badge/version-0.2.8-informational?style=flat-square">
  <img alt="Price" src="https://img.shields.io/badge/free-no_account-brightgreen?style=flat-square">
</p>

> **Coming soon · 即將公開.** The installer is not available yet. Downloads will appear under [Releases](https://github.com/IdeaAmplifier/CueBridge-RS/releases) at public release.<br>
> 安裝包尚未開放，公開後會放在 [Releases](https://github.com/IdeaAmplifier/CueBridge-RS/releases)。

> **For** live sound engineers who record a multitrack from an SSL Live console into REAPER — and want the console's scenes, transport and channel list to line up with the DAW.<br>
> **給**用 SSL Live 控台把多軌錄進 REAPER，並希望控台的 scene、transport、channel list 與 DAW 對得上的現場工程師。

[Manual · 手冊](#documentation--手冊)

---

## What it does · 功能

| | |
|---|---|
| **SESSION BUILDER** | Turn the SSL channel list into a REAPER project: tracks named and ordered like the console, record inputs and hardware outputs patched in recorder order, stereo channels split to 2 × mono or linked.<br>用 SSL 的 channel list 建好 REAPER 專案：軌道名稱與順序和控台一致，錄音輸入與硬體輸出依 recorder 順序接好，立體聲可拆成 2 × mono 或連結。 |
| **AUTO-MARKING** | Every SSL scene fires a MIDI message; CueBridge drops a named marker in REAPER while it records — no clicking, no counting.<br>每個 SSL scene 送出一則 MIDI，CueBridge 在錄音時自動打上具名 marker，不用點也不用數。 |
| **SSL DAW CONTROL** | The console's own DAW transport (DAW 1 popout, User Keys, Events) drives REAPER over ipMIDI (HUI): Rec / Stop / Play / Loop / Rtz / Prev / Next / Goto Marker 1. REAPER's state lights the buttons on the console.<br>控台自己的 DAW transport（DAW 1 popout、User Keys、Events）透過 ipMIDI（HUI）控制 REAPER：Rec／Stop／Play／Loop／Rtz／Prev／Next／Goto Marker 1。REAPER 的狀態會點亮控台按鍵。 |

![SESSION BUILDER](docs/figures/session.png)

![AUTO-MARKING](docs/figures/marking.png)

## Requirements · 系統需求

- **macOS 13 (Ventura) or later** — Apple Silicon and Intel<br>**macOS 13（Ventura）或更新版本**，支援 Apple Silicon 與 Intel
- **REAPER**
- **SSL Live V5.2 or later**<br>**SSL Live V5.2 或更新版本**
- One Ethernet cable from the Mac to the SSL **Connectivity port**, on a subnet that is **not** shared with Dante<br>一條網路線從 Mac 接到 SSL 的 **Connectivity 埠**，網段**不可**與 Dante 共用
- No ipMIDI driver, no third-party libraries<br>不需要 ipMIDI 驅動，也不需要第三方函式庫

## Five-minute setup · 五分鐘設定

**On the SSL · 在 SSL 上**

- **Options › Network** — Connectivity port on a non-Dante subnet; Mac on the same subnet.<br>Connectivity 埠設在非 Dante 網段，Mac 接同一網段。
- **Options › DAW** — **DAW 1 = HUI** on an ipMIDI port (e.g. 2). Tick **Transport Master** if User Keys should drive the transport.<br>把 **DAW 1 設為 HUI**，指定一個 ipMIDI port（例如 2）。要用 User Keys 控制 transport 時勾選 **Transport Master**。
- **Scene Output Action** — make the MIDI action to the local MIDI port **and** an ipMIDI port (e.g. 1). Use a different ipMIDI port for DAW Control.<br>把 MIDI action 同時送到本機 MIDI port **和**一個 ipMIDI port（例如 1）。DAW Control 要用另一個 ipMIDI port。

**In REAPER (once per Mac) · 在 REAPER（每台 Mac 一次）**

- Quit REAPER → open CueBridge → **AUTO-MARKING** → **Set Up Reaper OSC…**<br>先關閉 REAPER，打開 CueBridge，到 **AUTO-MARKING** 按 **Set Up Reaper OSC…**
- This adds one OSC control surface (`CueBridge_RS`) and a lean OSC pattern. `reaper.ini` is backed up first. Nothing else is changed.<br>這會新增一個 OSC control surface（`CueBridge_RS`）和一份精簡的 OSC pattern。`reaper.ini` 會先備份，其他設定不動。

**In CueBridge · 在 CueBridge**

- `SCENES IN` — the ipMIDI port used for scene messages.<br>接收 scene 訊息的 ipMIDI port。
- `SSL DAW CONTROL` — the network card connected to the console, and the same ipMIDI port as SSL **DAW 1**.<br>選接到控台的網卡，以及與 SSL **DAW 1** 相同的 ipMIDI port。

The first console heard is locked in; after changing venue, press **Re-detect**.<br>
第一台收到的控台會被鎖定，換場地後請按 **Re-detect**。

## Documentation · 手冊

- **[User Manual, English (PDF)](docs/manual-en.pdf)**
- **[使用說明書，繁體中文（PDF）](docs/manual-zh.pdf)** · [Markdown](docs/manual-zh.md)

## Known limitations · 已知限制

- Only the first console sending HUI is listened to; other ipMIDI senders are ignored.<br>只聽第一台送出 HUI 的控台，其他 ipMIDI 來源會被忽略。
- `reaper.ini` is only supported at its standard location (no REAPER portable install).<br>只支援標準位置的 `reaper.ini`，不支援 REAPER 可攜版。
- No auto-update — install new versions manually.<br>沒有自動更新，新版要手動安裝。
- SESSION BUILDER assumes SSL recorder I/O follows the Console Config order 1:1 (SSL Live V5.2+ Make All).<br>SESSION BUILDER 假設 SSL recorder I/O 與 Console Config 順序 1:1 對應（SSL Live V5.2 以上的 Make All）。
- Scene MIDI actions must be configured on the console; CueBridge does not change console settings.<br>Scene 的 MIDI action 要在控台上設定，CueBridge 不會更改控台設定。

## License · 授權

**Free to download and use. Source code is not published.** See [LICENSE.md](LICENSE.md).<br>
**免費下載與使用，不公開原始碼。** 詳見 [LICENSE.md](LICENSE.md)。

You may redistribute the unmodified installer. You may not modify and redistribute it under the CueBridge RS name, or sell it.<br>
未經修改的安裝包可以轉發；不得修改後以 CueBridge RS 名義散布，也不得販售。

## Contact · 聯絡

Questions, bug reports, or a show you want to try it on: **ideaamp.support@icloud.com**<br>
有問題、要回報 bug，或想在演出上試用，請寄到 **ideaamp.support@icloud.com**

---

<p align="center"><sub>CueBridge RS v0.2.8 · macOS 13+ · Coming soon · by <a href="https://github.com/IdeaAmplifier">ideaAmplifier</a></sub></p>
