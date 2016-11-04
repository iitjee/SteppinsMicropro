#Timers and Counters

####Common usecases:
1. Counting the frequency of a pulse train
2. Generation of precise time delays

These can be accomplished using s/w techniques but it keeps the uc occupied. To relieve the processor of this burden
**two 16-bit UP-COUNTERS** named **T0 and T1** are provided for general use.

Each counter may be programmed to count internal clock pulses (-> Timer) or to count external pulses (-> Counter).








