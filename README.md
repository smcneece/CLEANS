
# 🧼 CLEANS – Clothes Laundering Event Alert Notification System

**CLEANS** is a Home Assistant automation blueprint that monitors your washer or dryer using a vibration sensor. It prevents false alerts caused by the cat jumping on the washer, brief fill/drain pauses, or unloading, and alerts you only when a full cycle has truly ended.

---

## 🚀 Features

- 💥 Works with **any binary vibration sensor**
- 🧠 Uses **input_booleans and timers** for accurate tracking
- 📱 Sends notifications via **Mobile**, **Alexa**, and/or **Email**
- 🕵️‍♀️ Filters out:
  - Short bumps and unloading events
  - Fill and drain cycle pauses
  - Cheap sensor dropouts
- 🧺 Handles both **washer** and **dryer**
- 💡 Supports **blueprint import via URL** (no HACS needed!)

---

## 🧰 Required Helpers

To function correctly, you must create one **`input_boolean`** and one **`timer`** per device (washer/dryer):

### 🧼 Example `input_boolean.yaml`:
```yaml
washer_vibration_active:
  name: Washer Vibration Active
  initial: false

dryer_vibration_active:
  name: Dryer Vibration Active
  initial: false
```

### ⏱️ Example `timer.yaml`:
```yaml
washer_done_timer:
  duration: "00:05:00"

dryer_done_timer:
  duration: "00:05:00"
```

### 👇 In `configuration.yaml`:
```yaml
input_boolean: !include input_boolean.yaml
timer: !include timer.yaml
```

---

## 📥 Import This Blueprint

Click this button to import it directly into Home Assistant:
[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?repository_url=https://github.com/smcneece/CLEANS/blob/main/blueprints/automation/smcneece/cleans_blueprint.yaml)


---

## 🔧 Inputs & Configuration

| Input | Description |
|-------|-------------|
| `vibration_sensor` | Binary sensor that detects vibration |
| `friendly_name` | Name shown in notifications |
| `active_flag` | `input_boolean` used to track running state |
| `done_timer` | `timer` used to track post-cycle silence |
| `min_run_duration` | Minimum sustained vibration to consider a real cycle |
| `done_timeout` | Minutes of silence before sending notification |
| `mobile_notify_target` | Your notify service (e.g., `notify.mobile_app_yourdevice`) |
| `alexa_target` | Alexa notify service |
| `alexa_start_time` / `end_time` | Time range Alexa is allowed to speak |
| `email_notify_target` / `email_to_address` | Email options if enabled |

---

## 🧪 Tips

- Want to support both washer and dryer? Just create two automation instances and point each one at different helpers and sensors.
- Adjust `min_run_duration` if your machine vibrates weakly or starts with slow pulses.
- Adjust `done_timeout` based on how long your washer/dryer goes silent before actually finishing.

---

## 🤘 Credits

Crafted with sarcasm, soap, and sensor rage by Spicoli & Cletus.

---

