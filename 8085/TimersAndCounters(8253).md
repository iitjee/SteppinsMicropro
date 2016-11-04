#8253 Programmable Interval Timer (PIT)

1. 3 Timers (TM0, TM1, TM2) and 1 CWR
2. **Every CLK** pulse **decrements** the count by 1
3. Gate controls the start and stop of the timer.


Timer can be in 6 Modes:  <br/>
(000) **Mode 0:** Interrupt on Terminal Count <br/>
(001) **Mode 1:** Hardware Retriggable One-Shot <br/>
(x10) **Mode 2:** Baud Rate Generator aka Divide-by-N Counter <br/>
(x11) **Mode 3:** Square-Wave Generator <br/>
(100) **Mode 4:** Software triggered strobe <br/>
(101) **Mode 5:** Hardware triggered strobe <br/>


####Mode-0:
1. Only mode in which initial output is LOW.
2. When gate is high and Clock L-->H-->L, counting starts.
3. After N CLK pulses, counter becomes 0 i.e terminal count has reached => Output becomes high and stays hight
4. A L-->H interrupt is generated after count is terminated.
5. * OUT remains high until a NEW COUNT OR COMMAND WORD is loaded. (Counting need not start yet, OUT just becomes low)
6. Effect of Gate in middle of counting can be seen in the following table 






| Mode | Gate signal (Low or Going Low(H-->L))                                    | Gate signal Rising(L-->H)                                                                                   | Gate signal High                             | Notes                                                    |
|------|--------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|----------------------------------------------|----------------------------------------------------------|
| 0    | Counting is disabled & current value is freezed in the counting element. | Nothing happens  while rising                                                                               | Counting is progressed from the frozen value |                                                          |
| 1    | Nothing happens                                                          | Initiates counting (but doesn't yet start) and resets the output to initial value AFTER the next CLK pulse. | Nothing happens                              | It's EDGE RETRIGGERING everytime L->H transition happens |
| 2    | Counting is disabled and output is set HIGH                              | Reloads counter with initial value and just initiates counting                                              | Counting is progressed                       | This requires both L-->H and High to trigger the timer   |
| 3    | Counting is disabled and output is set HIGH                              | Counting is initiated and proceeds with previous value                                                      | Counting is progressed                       |                                                          |
| 4    | Counting is disabled                                                     | -                                                                                                           | Counting is enabled                          |                                                          |
| 5    |                                                                          |                                                                                                             |                                              |                                                          |
|      |                                                                          |                                                                                                             |                                              |                                                          |










####Usecases:
1. Real Time Clock
2. An Event Counter
3. Digital One-shot
4. Square-Wave Generator
