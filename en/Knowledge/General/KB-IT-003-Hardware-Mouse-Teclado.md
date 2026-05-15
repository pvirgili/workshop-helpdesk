# KB-IT-003: Mouse or keyboard not working

**Category:** Hardware  
**Impact:** Medium  
**Estimated resolution time:** 5–15 minutes

---

## Problem description

The mouse or keyboard is unresponsive, works intermittently, or behaves unexpectedly (double-clicking, stuck keys, jumping cursor).

---

## Most common causes

1. Low battery in wireless devices.
2. USB receiver (dongle) disconnected or making poor contact.
3. Outdated or corrupt device driver.
4. USB conflict (too many devices on a USB hub without enough power).
5. Active accessibility settings (filter keys, slow keys, or mouse keys enabled).
6. Physical device failure.

---

## Diagnostic and resolution steps

### For wireless mouse or keyboard

#### Step 1 — Check the battery
- Replace the batteries even if they seem new.
- For rechargeable devices: charge for at least 30 minutes before testing again.

#### Step 2 — Check the USB receiver (dongle)
1. Unplug the USB dongle from the device.
2. Plug it into a different USB port (preferably directly on the computer, not a hub).
3. Wait 10 seconds for Windows to recognize it.

#### Step 3 — Re-pair the device
- Turn the mouse/keyboard off and back on.
- Press the pairing button (usually on the bottom of the device).
- If it's a Logitech device with a Unifying receiver: use Logitech Unifying Software to re-pair.

### For wired USB mouse or keyboard

#### Step 1 — Try a different USB port
- Unplug and reconnect to a different USB port.
- Prefer USB ports directly on the computer over ports on a hub or docking station.

#### Step 2 — Test on another computer
- Connect the device to another computer to determine whether the issue is with the device or the port.

### For any type of device

#### Step 3 — Reinstall the driver

1. Open **Device Manager**.
2. Expand **Mice and other pointing devices** or **Keyboards**.
3. Right-click the device → **Uninstall device** (check "Delete the driver software for this device").
4. Disconnect the device → reconnect → Windows will install the driver automatically.

#### Step 4 — Check accessibility settings

1. Go to **Settings → Accessibility → Keyboard**.
2. Verify that **Filter Keys**, **Slow Keys**, and **Toggle Keys** are disabled.
3. Go to **Accessibility → Mouse** → verify that **Mouse Keys** (cursor control with numpad) is disabled.

#### Step 5 — Check for Windows updates

Some mouse/keyboard drivers are delivered via Windows Update:
1. **Settings → Windows Update → Check for updates**.
2. Check for driver updates in **Advanced options → Optional updates**.

---

## When to escalate to the help desk (hardware request)

- The device doesn't work on any computer (confirmed hardware failure → replacement needed).
- The mouse double-clicks persistently (microswitch failure → warranty replacement or new hardware request).
- The docking station doesn't recognize any connected device.

**To request a new mouse or keyboard**, use the hardware request process (see KB-IT-009-Equipment-Renewal).

**Suggested priority when escalating:** Low–Medium (user can use the laptop keyboard or a spare mouse).

---

## Information to gather when escalating

- Device brand and model.
- Connection type: USB, wireless RF, Bluetooth.
- Whether the issue also occurs on another computer.
- How long the issue has been occurring.
