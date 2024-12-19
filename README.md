# Function

The smart alarm clock not only has the functionality of a traditional alarm clock, such as displaying the time and setting alarm intervals, but it also allows the alarm time to be set remotely via a host computer. When setting the alarm, the user can choose to use an ultrasonic sensor to detect whether the roommate has gotten out of bed. Once the roommate is detected as awake, the alarm will automatically turn off the buzzer.

# Requirements
- Hi3861/Hi3881
- Shanghai HiSilicon HiSpark Pegasus T1 loT Development Kit
- Buzzer, ultrasonic sensor
- HUAWEI DevEco Device Tool (DevEco Device Tool)

# Microcontroller Section

## Timer
Check if the input time is valid, and assign the input clock cycle to the timer's interval attribute.
Call the `LOS_SwtmrStart` function, passing the timer ID to start the timer.

## Buzzer
An active buzzer is used in the experiment. When the output is set to a high level, the buzzer sounds, and the status is recorded as `g_beeStatus=0`. `Beeon()` is used to turn on the buzzer, and `Beeoff()` is used to turn it off.

## Ultrasonic Distance Measurement
The ultrasonic sensor receives a high-level signal of at least 10μs on an IO pin (TRIG) as the trigger signal for distance measurement. 
The ultrasonic module needs to connect J19-J1.

## How to Calculate the Change in Distance Between This Moment and the Last Moment?
In a loop, the distance value (data2) is retrieved at regular intervals (FEED_DELAY) and compared with the previous distance value (data1). The distance change (distance_delta) is then calculated. If the distance change is greater than 500, it indicates that the roommate is awake, and the buzzer will be turned off (BeeOff) and the loop will exit. Otherwise, `data1` is updated with `data2`, and the loop continues until the total time (`total_time`) is reached.

## Button
The `ButtonControl` function is a loop that continuously reads the button status from the IO expansion chip.

# MQTT Cloud Connectivity
**"Cloud" Communication Principle**: The "alarm clock" connects to the Huawei Cloud server via Wi-Fi. Since the "alarm clock" needs to connect to the existing Wi-Fi network, it is set to STA mode. 
The "alarm clock" needs to connect to another AP device to access the internet.
