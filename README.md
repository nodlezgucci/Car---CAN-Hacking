# Car_CAN-Hacking
!!! DISLAIMER - THIS PROJECT IS NOT INTENDED TO BE USED IN A BAD WAY AND IS INTENDED ONLY FOR EDUCATIONAL PURPOSES I NEITHER CONDONE NOR TAKE RESPONSIBILITY FOR SOMEONE
ELSE'S ACTIONS !!!

PREVIEW - ICSim is a simulator of how an actual car computer would work with visuals of a speedometer, blinkers and locked/unlocked doors, which is later on in the
file said as a dashboard

!!! Every command is done in a terminal and would probably need sudo privileges - sudo su !!!

1. Install ICSim

  [Clones the ICSim directory from github into an ICSim directory on your machine]
  - git clone https://github.com/zombieCraig/ICSim
  
2. Setup ICSim 

  [Changes the active directory of the terminal to ICSim's directory]
  - cd ICSim 
  
  [Runs the ICSim setup file]
  - ./setup_vcan.sh
  
3. Run ICSim
  
  [Runs the visual represantation of a car's dashboard with the interface for CAN communacation - vcan0]
  - ./icsim vcan0 (done in one terminal)
  
  [Runs the controls window which would need to be active(selected) in order to control the car using the same interface - vcan0]
  - ./controls vcan0 (done in a second terminal)
  
4. Run cansniffer
  
  [cansniffer is a tool used to sniff CAN packets]
  
  [Runs the cansniffer using the -c tag to helf identify changing data and using the same interface - vcan0]
  - cansniffer –c vcan0 (done in a third terminal)
  
5. Play around with the controls and try to spot what action corresponds to what ID in the cansniffer and how the data changes

6. I see that ID 188 corresponds to the blinkers with left blinker having the data - #010000 and the right blinker having the data - #020000
  Write a bash script in the linux cmd to make hazard lights (couldn't manage to take a screenshot with both lights on) -
  
		while true do cansend vcan0 188#010000 cansend vcan0 188#020000 done
    
![314419579_1745801909127820_5795919229665972963_n](https://user-images.githubusercontent.com/109030111/201494211-9c4eac66-79f8-4b52-9c28-1ae59e2c5f35.png)
