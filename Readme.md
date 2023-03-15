# IoT Energy Exercise

Todays goal is to utilize some of the techniques you heard about in the lecture to reduce the energy consumption of your device. You need to reduce it as much as possible while still being responsive.
We will use the same code you worked on last time. The use case is still you measuring what you're being told to measure by the server.

Concretely the goal is to implement deep sleep between send intervals. 

Since energy, and regulations, require us to reduce the communication we do, the server will now not respond with what you need to measure every time. Only when it wants you to chance sensor. That means you have to remember the last sensor you used, and send that.

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

## useful links
https://docs.pycom.io/firmwareapi/pycom/machine/#power-functions

<!---
## TODO:
IoT-lab setup

Goal: get code to IoT-lab. Set up consumption monitoring. run code. Evaluate.
-->

## Questions for thought
- Roughly much power do you think you save now compared to the code you started with?
- If you where to design a data collection system like this yourself are there things you would do that we haven't done to save power? Client-side? Server-side?