---
title: "Single light switch"
categories:
  - blog
---
# Toggling all lights at home with a single switch using Home Assistant, ESPHome, and ESP8266s

I have a bunch of cool lights or decorations at home that need power to function. I would love to have these on more often but for whatever reason I barely ever go through the effort of turning them on. Thus, I would love to be able to toggle all of these using a single switch! So this is what I'm trying to do here.

The general plan is to hook all my things to be toggled up to home assistant, as well as the single switch or button that will toggle all of the things. Then I'd set up an automation which would toggle all the things when the switch or button is pressed.

To hook up my things and the switch I used ESPHome, for no other reason than that this is what I found and seemed to work upon testing.

1. I used the following instructions to install ESPHome and add devices: [Getting Started with ESPHome and Home Assistant &#8212; ESPHome](https://esphome.io/guides/getting_started_hassio.html)
  
2. Then I configured my button to be a binary sensor based on this documentation: [GPIO Binary Sensor &#8212; ESPHome](https://esphome.io/components/binary_sensor/gpio.html)

![Wiring up the button, which is an old train door button in this case]({{site.url}}/assets/images/train_switch.jpg)

```yaml
binary_sensor:
  - platform: gpio
    name: "train_blue"
    pin: D2
  - platform: gpio
    name: "train_yellow"
    pin: D5
```

3. And configured my LED strip based on the following documentation: [NeoPixelBus Light — ESPHome](https://esphome.io/components/light/neopixelbus.html)

![Wiring up the LED strip controller]({{site.url}}/assets/images/led_strip_controller.jpg)  

```yaml
light:
  - platform: neopixelbus
    type: GRB
    variant: WS2812
    pin: D1
    num_leds: 89
    name: "Window LED strip"
```

4. Then I added the devices to Home Assistant
  
5. And finally, I made an automation that would toggle the LED strip when the button was pressed.

![]({{site.url}}/assets/images/automation.png)

Ta-da! Done.

[Demo video](https://www.youtube.com/watch?v=Z4dOUPHXtsM)
