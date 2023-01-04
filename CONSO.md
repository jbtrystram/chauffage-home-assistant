## Energy consumption estimation

With this setup you can do an estimation of the electricity used by the radiator.

The idea is to check the state of the radiator every minute, and when it's ON
we count the used Wh.
As it runs every minute, the step of the counter should be:
`heater rated power / 60`.

Then we create a template sensor that pull the data from that counter.

A counter helper is needed : 

```yaml
counter:
  office_heater_conso_counter:
    initial: 0
    minimum: 0
    # Example for a 1000 W heater. 1000/60
    step: 16.6
```

The template sensor look like this:
```yaml
template:
  - sensor:
      - name: office_heater_conso
        unit_of_measurement: "Wh"
        device_class: energy
        state_class: total_increasing
        state: "{{ states('counter.office_heater_conso_counter') }}"
```

Once this is set up use the blueprint to create the automation.

TODO: have the blueprint create the counter and the sensor ?