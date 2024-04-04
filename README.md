# HADysonOscillate

Home Assistant Automation to handle Dyson Fan Oscillating

## Prerequisite

Create some helpers in Home Assistant:

-   An `Input Number` to handle Fan Angle
    -   Set the range to fit your fan's min & max (In my case is `5` to `355`)
    -   Called `input_number.dyson_angle` in example code
-   An `Input Select` to handle Fan oscillating range
    -   Set options that you would like to use (Don't have to match the preset Dyson provided on their app)
    -   Make sure there is option `0` in the list
    -   Called `input_select.dyson_oscillating` in example code

## Propose of automations

-   `Set Fan Angle` - Apply angle change to fan
-   `Set Oscillating & Angle` - Apply oscillating range to fan & update angle accordingly

## Additional

If you want to make a preset angle for fan to stay at, Don't call dyson's set angle service directly. Call `input_number.set_value` to update the value of the helper created above instead.

The following is an example automation for that:

```yaml
alias: Fan to Bed
description: ''
trigger:
    - platform: state
      entity_id:
          - input_button.fan_to_bed
      from: null
      to: null
condition: []
action:
    - service: input_number.set_value
      target:
          entity_id: input_number.dyson_angle
      data:
          value: 270
mode: single
```
