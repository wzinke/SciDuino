# Matlab TTL trigger

Data acquired with Tektronix TDS 1002B (directly saved to USB stick).

The Arduino was controlled via Matlab; the main intention behind these timing tests was to check if the added lag caused by the USB communication would differ for different boards. In addition, I tried to get a better estimate, how long this lag is, and how consistent.

## Matlab Arduoni TTL series generater

https://www.mathworks.com/matlabcentral/fileexchange/47522-matlab-support-package-for-arduino-hardware

``` Matlab
function Test_Arduino_TTL(chan, Period)
% create a continous pulse series

if(~exist('chan','var') || isempty(chan))
    chan = 12;
end

if(~exist('Period','var') || isempty(Period))
    Period = [100, 100];
elseif(length(Period) == 1)
    Period = [Period, Period];
end

if(any(Period > 5))
    Period = Period ./ 1000;  % need the time in seconds
end

a = arduino;

chanstr = sprintf('D%d', chan);
    
while(~KbCheck)
    % On phase
    writeDigitalPin(a, chanstr, 1);
    WaitSecs(Period(1));
    
    % Off phase
    writeDigitalPin(a, chanstr, 0);
    WaitSecs(Period(2));
end

clear a;
```








## tested boards


* [**Arduino Uno**](https://store.arduino.cc/usa/arduino-uno-rev3)
![](https://store-cdn.arduino.cc/usa/catalog/product/cache/1/image/1000x750/f8876a31b63532bbba4e781c30024a0a/a/0/a000066_iso_3_1.jpg)

* [**Arduino Due**](https://store.arduino.cc/usa/arduino-due)
![](https://store-cdn.arduino.cc/usa/catalog/product/cache/1/image/1000x750/f8876a31b63532bbba4e781c30024a0a/A/0/A000062_iso_2.jpg)

* [**Sunfounder Mega**](https://www.sunfounder.com/mega-2560-compatible-with-arduino.html)

Correctly recognized by Matlab as Arduino Mega board.
![](https://www.sunfounder.com/media/catalog/product/cache/1/image/9df78eab33525d08d6e5fb8d27136e95/1/_/1_2_6.jpg)

* [**STEMtera**](https://stemtera.com/)

Recognized by Matlab as Arduino Uno and works as expected.
![](https://cdn.sparkfun.com//assets/parts/1/1/9/4/6/10483-02.jpg)

* [**Arduino 101**](https://store.arduino.cc/usa/arduino-101)

Matlab does not recognize the Arduino 101 board and hence it was not possible to test the TTL timings for this board.
![](https://store-cdn.arduino.cc/usa/catalog/product/cache/1/image/1000x750/f8876a31b63532bbba4e781c30024a0a/A/B/ABX00005_iso_2.jpg)


