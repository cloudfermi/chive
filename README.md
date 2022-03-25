# cHive MQTT Broker
A plug-n-play on-chip MQTT broker for IoT rapid deployment based on ESP32
# Overview
- Target to no setup time, no maintenance, 24/7 reliable operation, low power and very small size.
- For rapid deployment of IoT projects in data collection and distributed control.
- Based on ESP32 wifi dual core chip, 240MHz.
- Up to 80 MQTT clients.
- The firmware ready run on ESP32-WROOM-32. So it's ready for any ESP32 dev kits using that module.
- Having reference to https://github.com/martin-ger/uMQTTBroker during our design of MQTT broker.
# Features
- Written in C++ with Arduino ESP-IDF v3.3.5. Embedded with custom-built MicroPython v1.16 ESP32, as a task running on core 1.
- Up to 80 MQTT clients. Support MQTT version v3.1 (v3) and v3.1.1 (v4) simultaneously.
- Retained messages. LWT. QoS level 0. Username / password authentication.
- Port could be customized. Default port 1883.
- Username / password could be changed. Default “admin” / “admin”. Customed authentication could be
made at MicroPython side.
- Access to broker API via topic $DEV/ by device authentication. Default “admin” / “admin”.
- Support callbacks: connect, tcpconnect, disconnect, data, publish at MicroPython side.
- Local subscribe/publish at MicroPython side.
- Support device/group/broadcast publish from broker (local) to other clients following EXT API defined by
CloudFERMI.
- TLS, non-clear sessions, other QoS (1, 2) not supported.
- Support Wifi AP/STA. STA with dynamic (DHCP) and static IP assignment.
- cBoot Manager embedded to support remote firmware upgrade and other provisioning.
# Recommendations & Limitations
- Message length < 4096 bytes.
- Topic levels < 20. Topic length < 256 bytes.
- KeepAlive <= 4000s
- Client Id as short as possible to save RAM. But make sure keep it unique among clients.
- Topic, Topic subscription as short as possible. Too many clients with the same topic subscriptions should
be avoided. 16 clients subscribed on the same topic are fine.
- Reconnect period should be long enough, ex 30s+. KeepAlive should be long enough, ex 1200s. If possible,
clients should use random keepalive, ex 1200s – 3600s to avoid keepalive messages arriving to broker at
the same time.
- Message payload should be short to save RAM. When not enough RAM, the broker will drop messages or
disconnect clients.
- Number of subscriptions limited by RAM. RAM resource is limited on the broker.
- Limit usage of LWT, retained messages to save RAM.
- Running MicroPython code is slow. Avoid using it too much in broker processing flow.
# Required GPIOs
- EN reset, input.
- IO34 (SYS button) active low, input.
- IO32 (SPEAKER), active high, output. Driving piezo speaker, required driver circuit. 
- IO2 (SYS Led), active low, output.
- IO15 (ACTIVITY Led), active low, output.
# User Guide
- Please refer to https://drive.google.com/file/d/18Kykagh5T9F9ALrh75DmNdfSj6Xic4-4/view
- and https://drive.google.com/file/d/1hgYMJvaeOWBA8W5PGBhrbFi8se1-KYuu/view
# License
- This is our completely proprietary firmware design based on our cThings IoT platform, ready to run in production. Require some fee per firmware downloading to your ESP32 chip for our efforts of code design, maintenance, and support.
- Please contact us for more details of remote provisioning cHive firmware on your own hardware, and others.
# Contacts
- Please email to info@cloudfermi.com, or cloudfermi@gmail.com
