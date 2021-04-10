# Ardupilot

cd /home/idr/courseRoot/apm/ardupilot
cd $apm

# lists the boards we can compile for
./waf list_boards

# sim_vihicle is located in
ardupilot/Tools/autotest/sim_vehicle.py

# start sym vehicle
cd /home/idr/courseRoot/apm/ardupilot/ArduCopter && sim_vehicle.py --map --console

# all params 
# http://ardupilot.org/copter/docs/parameters.html
/home/idr/courseRoot/apm/ardupilot/ArduCopter/mav.param

# mavproxy show params
param show rtl_alt
param set sim_gps_disable 1

# mavproxy light ground control station
# win gateway 10.0.2.2
mavproxy.py --master tcp:127.0.0.1:5760 --baudrate 115200 --out udp:127.0.0.1:14550

# start manual sitl
cd /home/idr/courseRoot/apm/ardupilot/build/sitl/bin && ./arducopter -S -I0 --home -35.363261,149.165230,584,353 --model "+" --speedup 1 --defaults $apm/ardupilot/Tools/autotest/default_params/copter.parm

# mavproxy commands
# https://ardupilot.github.io/MAVProxy/html/modules/index.html

# lift commands
Mode GUIDED
arm throttle
takeoff 5

# guided mode movement
velocity 0 -10 0
setyaw 30 5 1

# install dronekit
sudo -H pip install dronekit
sudo -H pip install dronekit-sitl

# check install
pip freeze | grep dronekit
