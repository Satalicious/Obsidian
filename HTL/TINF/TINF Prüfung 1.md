

#### 1-2 kleine Codebeispiele ~ Hälfte der Prüfung
- Interrupts
- Callback
- Timer

- DigitalOut, DigitalIn umgehen können
- BusOut (wie man definiert und ein Lauflicht macht)

### ZUM ÜBEN: https://simulator.mbed.com


```cpp
#include "mbed.h"

PwmOut led5(p5);
PwmOut led6(p6);
Analogin ponti(p15);

BusOut myleds(LED1, LED2, LED3, LED4);

int main() {
    while(1) {
        led5 = led5 +0.1;
        led6 = led5;
        printf("LED is now %.2f\n",led5.read());
        
        for(int i = 0; i < 16; i++) {
            myleds = i;
            wait(0.5);
        }
        if (led5 == 1)
            led5 = 0;
    }
}

```