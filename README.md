# Reduce-InputLag-PS4-Datafrog-Wireless-Controller-On-Linux


On Terminal :

bluetoothctl
power on
agent on
default-agent
scan on

Press PS buttom (HOME) + Share

You will see something like this:

[NEW] Device A2:5B:5D:C8:F8:3D Wireless Controller

On terminal write:

connect A2:5B:5D:C8:F8:3D

You will see something like this:
[CHG] Device A2:5B:5D:C8:F8:3D Connected: yes
[CHG] Device A2:5B:5D:C8:F8:3D Modalias: usb:v054Cp05C4d0100
[CHG] Device A2:5B:5D:C8:F8:3D ServicesResolved: yes
[CHG] Device A2:5B:5D:C8:F8:3D Paired: yes
[CHG] Device A2:5B:5D:C8:F8:3D WakeAllowed: yes

On terminal write:
trust A2:5B:5D:C8:F8:3D

cat /proc/bus/input/devices

You will see something like this:
I: Bus=0005 Vendor=054c Product=09cc Version=8100
N: Name="Wireless Controller Touchpad"
P: Phys=
S: Sysfs=/devices/virtual/misc/uhid/0005:054C:09CC.000B/input/input40
U: Uniq=A2:5B:5D:C8:F8:3D
H: Handlers=event16 mouse3 
B: PROP=5
B: EV=b
B: KEY=2420 10000 0 0 0 0
B: ABS=260800000000003

sudo touch /etc/udev/rules.d/99-gk-low-latency-protocol.rules

echo 'ACTION=="add", SUBSYSTEM=="hid", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="09cc", MODE="0660", GROUP="input", ATTR{bt_poll_interval}="1"' | sudo tee /etc/udev/rules.d/99-gk-low-latency-protocol.rules > /dev/null


