## Compile local changes into esphome project

Playing with inverters and energy-meters I faced the problem that esphome was not compiling my local code changes using the yaml file given by the repo [esphome-soyosource-gtn-virtual-meter](https://github.com/syssi/esphome-soyosource-gtn-virtual-meter) 

According to this [manual](https://esphome.io/components/external_components.html) the yaml file had to be changed to use local sources.

### Add local sources to yaml file:
 
```
external_components:
  - source: ${external_components_source}
    refresh: 0s
  - source:
      type: local
      path: components
    components: [ soyosource_virtual_meter ]
```

At the end I used [this file](esp8266-wifi-dongle-limiter-Web.Local.yaml) for building the firmware for my inverter wifi dongle. 
It has a web server, uses mqtt for publishing inverter data factoring my local changes to the project.
