# Ubuntu 18.04 + Nobreak Ts shara USB
![tsshara](https://github.com/rbernardes/tsshara-ubuntu-server/blob/master/tsshara.jpg?raw=true)


### Install required packages:
```
# apt install nut-client nut-server
```

### Configure
```
# cat >> /etc/nut/ups.conf << EOF
[ups]

        driver = blazer_ser
        port = /dev/ttyACM0 # or change port to auto
        desc = "TS Shara"
EOF

# echo "LISTEN 127.0.0.1 3493" >> /etc/nut/upsd.conf
```

### Configure NUT client
```
# echo "MODE=standalone" >>  /etc/nut/nut.conf
```

### Testing
```
# /lib/nut/blazer_ser -a ups
Network UPS Tools - Megatec/Q1 protocol serial driver 1.57 (2.7.4)
Duplicate driver instance detected! Terminating other driver!
Supported UPS detected with megatec protocol
Vendor information unavailable
No values provided for battery high/low voltages in ups.conf

Using 'guestimation' (low: 10.400000, high: 13.000000)!
Battery runtime will not be calculated (runtimecal not set)

# /etc/init.d/nut-server restart

# netstat -tnlp | grep ups
tcp        0      0 127.0.0.1:3493          0.0.0.0:*               LISTEN      22646/upsd
```

### Testing nut-client > nut-server
```
# upsc ups
Init SSL without certificate database
battery.charge: 100
battery.voltage: 13.00
battery.voltage.high: 13.00
battery.voltage.low: 10.40
battery.voltage.nominal: 12.0
device.type: ups
driver.name: blazer_ser
driver.parameter.pollinterval: 2
driver.parameter.port: /dev/ttyACM0
driver.parameter.synchronous: no
driver.version: 2.7.4
driver.version.internal: 1.57
input.current.nominal: 100.0
input.frequency: 60.0
input.frequency.nominal: 60
input.voltage: 224.0
input.voltage.fault: 224.0
output.voltage: 116.0
ups.beeper.status: enabled
ups.delay.shutdown: 30
ups.delay.start: 180
ups.load: 32
ups.status: OL
ups.temperature: 29.0
ups.type: offline / line interactive
```

### phpsysinfo
![ups](https://github.com/rbernardes/tsshara-ubuntu-server/blob/master/ups.png?raw=true)
