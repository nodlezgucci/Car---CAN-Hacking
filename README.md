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

7. I see that ID 19B corresponds to the doors with open doors having the data - #000000 and closed door having the data - #00000F 
   	Write a bash script in the linux cmd to lock and unlock the doors  
   
		while true do cansend vcan0 19B#00000F cansend vcan0 19B#000000 done
		
![314437872_661565698651571_7419970977940910151_n](https://user-images.githubusercontent.com/109030111/201494544-220d8860-2044-41ca-8fd4-f79a956f5180.png)

8. And finally I see that ID 244 corresponds to the speedometer with the speed of 95 having the data - #0000003894
	Write a bash script in the linux cmd to keep the speed at 95 

		while true do cansend vcan0 244#0000003894 done
   
![314445943_1172877640014528_1613940322642097491_n](https://user-images.githubusercontent.com/109030111/201494627-95e13746-8fce-4d2b-b71f-b69beede9c0a.png)

That pretty much wraps up my little CAN-sniffing adventure thank you for reading it and I hope you find it helpful!
By nodlezgucci!
