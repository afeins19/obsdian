user mode -> kernel mode -> iosubsystem -> device driver -> interrupt handler -> device then back up the chain again

### Improving Performance for IO
- reduce number of context switches
- reduce data copying
- reduce interrupts by using large transfers 
- **DMA**

