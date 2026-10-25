# Thermostat as a Service

An IoT (Internet of Things) project where an ESP32-C6 microcontroller reads temperature from an LM75 module and publishes temperature readings to an MQTT topic.
A web service subscribes to the MQTT topic, consuming messages and persisting sensor recordings.

<img width="742" height="700" alt="taas-architecture" src="https://github.com/user-attachments/assets/25feceb6-bda4-4c38-9970-911f47e3b97f" />

Each components full functionality is summarised as follows:

Web Service:
  - Subscribe to topic for temperature recordings and persist in DB
  - Query temperature recordings over HTTP
  - Set a temperature threshold over HTTP
  - Publish MQTT message with new temperature threshold
  - Subscribe to MQTT topic for temperature crossing threshold, persist in DB

LM75:
  - Detect ambient temperature
  - Store temperature threshold
  - Trigger interrupt for the microcontroller when temperature passes above threshold

ESP32-C6:
  - Read current temperature from LM75
  - Publish temperature in MQTT message
  - Subscribe to MQTT topic for setting temperature threshold
  - Write temperature threshold to LM75
  - Respond to interrupt from LM75 when temperature crosses threshold, publish message
