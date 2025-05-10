My notes for alternatives to nice!nano V2

Link with the list of alternatives and comments https://github.com/joric/nrfmicro/wiki/Alternatives
I used `SuperMini NRF52840` from Tenstar Robot with a success.

**Important:** nice!nano docs warn against using high soldering temperatures:
> "When soldering the nice!nano, avoid using high iron temperatures, as you could damage the main nRF52840 chip. A
> temperature around 270°C-300°C should be hot enough. The higher the temperature, the more likely you are to damage the
> board."  
[Source](https://nicekeyboards.com/docs/nice-nano/getting-started/)

**Important:** The nice!nano v2 does not have ESD (Electrostatic Discharge) protection, so it's possible to damage it if
you touch the pins or components with static electricity (you are not grounded), or if you 'shock' controller when you
connect USB cable.
Controller after such shock may work but not properly (eg some keys may not work only from time to time or keys can be
repeated from time to time). It always good to ground yourself before touching controller and you should cover
controller to not touch it when you connect USB cable.
Such problems can be caused also by bad soldering so sometimes it is hard to find the reason of the problem.
Keep in mind that you can always switch controllers with second half (and flash it accordingly) to check if the problem
is with the controller or with the soldering.
