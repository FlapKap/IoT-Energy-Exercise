# IoT Energy Exercise

Todays goal is to utilize some of the techniques you heard about in the lecture to reduce the energy consumption of your device. You need to reduce it as much as possible while still being responsive.
We will use the same code you worked on last time. The use case is still you measuring what you're being told to measure by the server.

Concretely the goal is to make your device sleep between send intervals. 

Since energy, and regulations, require us to reduce our communication, the server will now not respond with what you need to measure every time. Only when it wants you to chance sensor. That means you have to remember the last sensor you used.

In addition to the sensor, the server also sends two numbers:
1.  An interval. This you should use to filter your measurements, such that you dont send data that falls within the previous sent measurement +- interval.
2.  Seconds until next measurement. We want the next measurement x seconds from now.

An example:

```
       ┌──────────────────┐                                    ┌────────────────┐
       │                  │           Hi there                 │                │
       │                  ├───────────────────────────────────►│                │
       │                  │                                    │                │
       │                  │           CO2 50 10                │                │
       │                  │◄───────────────────────────────────┤                │
       │                  │                                    │                │
       │                  │          1100                      │                │
       │                  ├───────────────────────────────────►│                │
       │                  │                                    │                │
       │                  │          1010                      │                │
       │   PYCOM          ├───────────────────────────────────►│     SERVER     │
       │                  │                                    │                │
       │                  │          1070                      │                │
       │                  ├───────────────────────────────────►│                │
       │                  │                                    │                │
       │                  │         Humidity 2 30              │                │
       │                  │◄───────────────────────────────────┤                │
       │                  │                                    │                │
       │                  │          34                        │                │
       │                  ├───────────────────────────────────►│                │
       │                  │                                    │                │
       │                  │          37                        │                │
       │                  ├───────────────────────────────────►│                │
       │                  │                                    │                │
       └──────────────────┘                                    └────────────────┘


```

As last time, I will run the 

## Notes
There are 2 forms of sleep. Light and deep sleep.
For deep sleep, the board basically resets when it is woken, so you need to save anything you want to remember when you wake up.

## useful links
https://docs.pycom.io/tutorials/basic/sleep/

https://docs.pycom.io/firmwareapi/pycom/machine/#power-functions

https://docs.micropython.org/en/v1.11/esp8266/tutorial/filesystem.html : While this is for the ESP8266, working with the filesystem is pretty much the same. This is useful for saving and loading values across sleep.

<!---
## TODO:
IoT-lab setup

Goal: get code to IoT-lab. Set up consumption monitoring. run code. Evaluate.
-->

## Questions for thought
- Roughly much power do you think you save now compared to the code you started with?
- If you where to design a data collection system like this yourself are there things you would do that we haven't done to save power? Client-side? Server-side?