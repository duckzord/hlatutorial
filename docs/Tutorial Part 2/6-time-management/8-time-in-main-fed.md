---
sidebar_position: 8
---

# Implementing HLA Time Management in the Master Federate

There is one more thing we need to do to get the best flexibility out of HLA Time Management. We will use the Master federate to control the speed of all other federates. We will thus take away any code from the CarSims that makes them run at a particular wall clock time speed, namely the “sleep” function in the main loop. The Master federate will do the pacing, i.e. controlling how fast the simulation speed runs in relation to the wall clock time. Only the Master federate will sleep before moving to the next time step. Instead of sleeping, the CarSim federates will simply be waiting to be granted to the next time step.

In the main loop of the Master federate we thus need to do the following:

1.	Save the wall clock time before the starting the loop (frame).
2.	Perform the regular calculations for the simulation. In case of the Master application, not much is simulated, but this is still shown for clarity.
3.	Sleep until the end of the frame, which is the saved wall clock time from the start plus the size of the time step in wall clock time. Remember that when simulating at real-time speed, one second of logical time equals one second of wall clock time!
4.	Save the wall clock time for another round.
5.	Advance logical time. Since we may now receive and process messages this may take some time.
6.	Repeat from step 2.

This is what the main loop may look like:

 
```cpp
mainLoop()
     
{
_startOfCurrentFrameMillis = currentTimeMillis();
    while (true) {

   // Perform the simulation calculations
calculateNextFrame();

   // Determine the starting point in milliseconds for next frame and then wait
      _startOfNextFrameMillis = _startOfCurrentFrameMillis + _frameSizeMillis;       
       sleepUntilWallClockTime(_startOfNextFrameMillis);

// Save a new wall clock time value for the start of the next frame
  _startOfCurrentFrameMillis = currentTimeMillis();

   // Do the Logical Time Advance
_grant = false;
HLAinteger64Time tNext = _tCurrent.add(_step)
_rtiAmbassador.timeAdvanceRequest(tNext);
    while (!_grant) {
        // Process incoming messages
    Thread.sleep(10);
    }
    // Time has now been advanced
  }
}
```

No other federate will be granted to a new time step unless the Master federate is finished with that time step and requests to be granted to the new time. 

Be careful how you sleep. Use a proper sleep function, for example:

- In C++: Windows Sleep, Unix usleep or Boost thread sleep 
- In Java: Thread.sleep

A beginner may be tempted to do a “busy wait” by performing meaningless computations to keep the CPU busy for some time. This approach will waste CPU resources, slowing down other processes, so it must be avoided.
