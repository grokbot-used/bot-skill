---
name: Enable OpenAPI PAYG on JusTrack
description: >-
  Use when enabling PAYG (pay-as-you-go) for an OpenAPI app on JusTrack
  Application Management (开通 PAYG).
---
# Enable OpenAPI PAYG on JusTrack

Enable pay-as-you-go for one OpenAPI application via **Open Platform → Application Management**.

## Inputs
- `{base_url}` — Web root ending before hash, e.g. `http://183.36.245.58:9080/gpstrack/test/index/`
- `{app_name}` — Application Name shown in the table (demo used `123`)
- `{payg_sku}` — PAYG SKU label or code to pick in the dropdown (demo used `ping-payg-0.01` / `PAYG_ozpdsrtM`)
- `{effective_time}` — usually **Now**; otherwise a concrete datetime the picker accepts

## Assumptions
- Signed-in Chrome session already has permission to enable PAYG (demo used dealer account「解放双手」).
- Do not enter or store passwords in this skill; sign-in lives in the browser profile.
- At most one PAYG may be active per application; if already Opened, stop and report instead of forcing another enable.
- UI language may be English or Chinese; match visible labels (`Enable PAYG` / 开通按量付费, `Confirm Activation` / 确认开通, `Got it` / 知道了).

## Steps
1. Open `{base_url}#/charge-ops/app-manage` (Open Platform → Application Management).
2. Locate the row for `{app_name}`. Note current **PAYG Status**. If already **Opened**, report and stop.
3. Click **Enable PAYG** in that row’s Operation column.
4. In the **Enable PAYG** modal:
   - Confirm **Application** is `{app_name}` (pre-filled when opened from the row).
   - Open **PAYG SKU** and select `{payg_sku}` (Unit Price should populate from the SKU).
   - Set **Effective time** to `{effective_time}` (demo: open the picker → **Now** → **OK**).
5. Click **Confirm Activation**. Do not click Confirm until Application, SKU, and Effective time are filled.
6. Wait for **Activation successful**. Click **Got it**.
7. Refresh/verify the table row: **PAYG Status** = **Opened**; package summary includes **PAYG**.

## Report back
- App name, SKU chosen, unit price shown, effective time used
- Before/after PAYG Status and resource-package summary
- Exact toast/modal text on success or failure
- If SKU missing, permission denied, or status already Opened: stop with the UI text — do not invent another path
