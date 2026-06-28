# QR Codes — Demo Props (5 Assets)

**Owner:** Track 4 (Pitch) · **Status:** Ready to print
**Use:** Print these for the live scan demo. Hero asset is `meeting-4f`.
**Related:** [[pitch/logistics]] · [[pitch/script]]

---

## Print spec

- **Size:** At least **8×8 cm** per code (larger is better for stage scanning).
- **Contrast:** Black on white only — no logos, gradients, or colored backgrounds.
- **Material:** Card stock or laminated paper; tape to asset cards or table props.
- **Test:** From the **presenter phone**, scan each code from **~30 cm** before leaving for the venue.
- **Fallback:** Bookmark each full URL on the phone in case the camera will not focus live.

Generate QR images from any of:

- [QR Code Generator](https://www.qr-code-generator.com/) — paste URL, download PNG
- macOS **Quick Actions** or **Preview** after generating
- Terminal (if `qrencode` installed): `qrencode -o meeting-4f.png "https://fridson.lovable.app/r/meeting-4f"`

---

## Asset table (copy URLs into your QR generator)

| # | Asset ID | Label (for prop card) | Full URL | Role |
|---|----------|----------------------|----------|------|
| 1 | `printer-3f` | Printer · 3rd floor East | `https://fridson.lovable.app/r/printer-3f` | Backup prop |
| 2 | `bathroom-2f` | Bathroom · 2nd floor | `https://fridson.lovable.app/r/bathroom-2f` | Backup hero ("Leak") |
| 3 | `meeting-4f` | Meeting room · 4th floor | `https://fridson.lovable.app/r/meeting-4f` | **Hero — live scan ("Projector broken")** |
| 4 | `pump-basement` | Pump room · Basement | `https://fridson.lovable.app/r/pump-basement` | Backup prop |
| 5 | `kitchen-1f` | Kitchen · Ground floor | `https://fridson.lovable.app/r/kitchen-1f` | Backup prop |

---

## Ready-to-print checklist (🧑 human)

1. Open a QR generator; for each row above, paste the **Full URL** and download a PNG.
2. Print all **5** codes on one sheet (or 5 separate cards) at **≥8×8 cm**.
3. Write the **Label** under each code so props are identifiable on the table.
4. Place **`meeting-4f`** closest to the presenter — it drives the full agent flow.
5. On the presenter phone: scan all 5 from ~30 cm; fix size/contrast if any fail.
6. Bookmark all 5 URLs as scan-fallback tabs (see [[pitch/dry-run-checklist]]).

---

## Scan → tap flow (rehearsal reminder)

1. Scan opens asset page with location confirmation.
2. Presenter taps **"Projector broken"** on `meeting-4f` (or **"Leak"** on `bathroom-2f` backup).
3. Success screen shows **"Sent."** — projection feed picks up from there.
