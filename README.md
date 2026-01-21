# Security System Retrofit

Using ESP32 and [ESPHome](https://esphome.io) for new Security System

## The Backstory

Upon moving into my home, I discovered an abandoned HoneyWell security system. While the keypads had been removed, and the panel abandoned, the infrastructure was still in place. I found that there were 7 zones of doors and windows that were pre-wired with magnetic reed switches and a buzzer. Instead of letting it go to waste, I decided to build my own security system.

What I did: 
Replaced the legacy panel with an ESP32, and developed a custom configuration using ESPHome for Home Assistant.

## Software Setup

1. Setup using **ESPHome** [Getting Started with ESPHome and Home Assistant](https://esphome.io/guides/getting_started_hassio.html).
2. Created a new device configuration in the **ESPHome Dashboard** 
3. Defined the hardware pins using 'substitutions' and imported the logic from GitHub using 'packages':

```yaml
substitutions:
  garage_door: GPIO
  front_door: GPIO
  back_door: GPIO
  kitchen_window: GPIO
  living_room_window: GPIO
  bedroom_window: GPIO
  laundry_window: GPIO
  buzzer: GPIO

packages:
  security: github://emily-weeks/security-system/security.yaml@main
```

4. Flashed the firmware to the ESP32 and set up the dashboard display in Home Asssitant.

## The Result

The system provides a veiw of real time changes for every entry point to the house.
Here is the dashboard view in Home Assistant:

![Home Assistant Entity](https://github.com/emily-weeks/security-system/blob/main/images/home-assistant-entity.jpg?raw=true)

When a door or window is opened and the magnetic circuit is broken, the ESP32 registers the event and triggers the logic to log, beep, or set off the alarm.

![Entity Changes](https://github.com/emily-weeks/security-system/blob/main/images/entity-activity.jpg?raw=true)

