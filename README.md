## Home Assistant - Gestion de bout en bout du chauffage

This repository contains the files of a post in HACF french forum, adapted to fit my personal setup.

It is the complete implementation of a heating management system for home assistant: 
- Proportional thermostat
- Heating modes
- Time schedule
- Override mode 

Please see https://forum.hacf.fr/t/gestion-de-bout-en-bout-du-chauffage/4897 for the original resources

## Setup

### Helpers

A few helpers are needed : 

- Input numbers:
  - room target temperature
  - Override duration
  - power target for the heater (computed by the proportionnal thermostat)
- Input select for selecting the heating mode 
- Timer for the override duration 

```yaml
input_number:
  target:  # The target temperature of the room
    name: Target temperature
    min: 15
    max: 25
    step: 0.2
    mode: slider 
    unit_of_measurement: °C
    icon: mdi:thermometer-check
  power:  # The power value for the heater
    name: heater power
    min: 0
    max: 100
    step: 1
    mode: box
    unit_of_measurement: %
    icon: mdi:lightning-bolt-circle
  override:  # The override duration
    name: Override duration
    min: 0
    max: 12
    step: 1
    mode: slider
    unit_of_measurement: Hours
    icon: mdi:timer-sand
input_select:
  heater_mode:
    name: heater mode
    options:
      - Stop       # for the Summer 
      - Hors-gel   # Avoid freezing 
      - Absent     # Out of the house
      - Dérogation # Override
      - Auto       # Will use the temperature set by the scheduler
    icon: mdi:heat-wave
timer:
  heater_derog:
    name: Heater override duration
    icon: mdi:timer
```