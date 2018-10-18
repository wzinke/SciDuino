# Matlab TTL trigger

Tektronix TDS 1002B

Series A: On 10 ms, Off 100 ms (25 ms bin)
Series B: On 100 ms, Off 100 ms (50 ms bin)

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

chanstr = ['D', num2str(chan)];
    
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
