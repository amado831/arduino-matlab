# arduino-matlab

For Ubuntu users:
Matlab may have difficulty finding attaching a serial port to your USB drive. The reason why was found here:
https://www.mathworks.com/matlabcentral/answers/25323-using-serial-to-connect-to-an-arduino

The solution is pasted below

You can use /dev/ttyACM0 but you need to let the library know that you will be using it. 
To specify the ports on your system, create a java.opts file in the directory 
you start MATLAB from with the following line in it:

-Dgnu.io.rxtx.SerialPorts=/dev/ttyS0:/dev/ttyS1:/dev/USB0:/dev/ttyACM0


After you restart MATLAB, the port should be found:

>> instrhwinfo('serial')

ans =
       AvailableSerialPorts: {2x1 cell}
             JarFileVersion: 'Version 2.7.0'
      ObjectConstructorName: {2x1 cell}
                SerialPorts: {2x1 cell}

>> ans.AvailableSerialPorts
ans =
      '/dev/ttyS0'
      '/dev/ttyACM0'

Another option is to create a symbolic link from /dev/ttyS101 to 
/dev/ttyACM0. The port should be enumerated as ttyS101 then.

You may also need to change permissions or add yourself to the dialout group to access /dev/ttyACM0. Instructions are provided hereL
https://www.arduino.cc/en/Guide/Linux
