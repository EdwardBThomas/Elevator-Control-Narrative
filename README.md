# Elevator-Control-Narrative
A control narrative for a hypothetical elevator

	1. By default, the elevator is in state 00, or idle and resting on floor 1
	2. Once a floor is called or entered, the elevator moves to State 01 and the called floor is added to Table 01
		a. Table 01 is the list of all floors to stop at before switching to State 10 and reading from Table 10
			i. If Table 10 is empty, the elevator automatically changes to State 00
		b. As a floor is stopped at and moved on from, it is removed from Table 01
		c. If a floor is added that is less than the current-lowest floor, it is placed into Table 10.
	3. Once the highest floor is 'read' from Table 01, the elevator switches to State 10 and reads from Table 10
		a. Table 10 is the list of all floors to stop at before switching to State 01 and reading from Table 01
			i. If Table 01 is empty, the elevator automatically changes to State 00
		b. As a floor is stopped at and moved on from, it is removed from Table 10
		c. If a floor is added that is more than the current-lowest floor, it is placed into Table 01
		
	4. Once Tables 01 and 10 are empty, the elevator changes to State 00 and reads from Table 00
		a. Table 00 is read-only with one entry: floor 1.
		b. Once a floor is called, the called floor is added to Table 01 and the elevator changes to State 01 again.
	
	5. State 11 is reserved for emergencies
		a. State 11 can be triggered manually 
			i. By someone pressing the corresponding button in the cabin
				1) See 5.b.i-iii
		b. Standard practice for elevator fail-safe mechanisms is strictly mechanical; in this case, once the tensioner is triggered and the plugs/cams fired, the control system switches to State 11 automatically
			i. Emergency lighting and other in-cabin alerts are turned on
			ii. Cabin is put into audio contact with the front desk and local first responders.
			iii. The front desk of the building is sent an immediate alert with a secondary alert to local first responders.
				1) If the front desk does not confirm a false alarm in one minute (or any other interval set by industry general practice), or confirms a positive alarm, the secondary alert is sent to local first responders.
				
	6. The correct distance to travel between stops uses two orthogonal and mutually complimentary methods.
		a. The distance between floors is a read-only variable, and the total distance to travel to the 'next' stop is calculated via multiplying the difference between the last stop and the next stop by the between-floor distance.
		b. In addition, the control system has a camera that scans barcodes or QR codes on the inside of the shaft.
			i. The control system thereby can make minor corrections by engaging the drive system until the 'stop here' graphical code aligns with the camera.
			ii. This is for correcting mechanical elasticity as machines wear over time, making sure the cabin opens as level as possible with the floor for wheelchairs, dollies, hospital beds, the blind, the infirm, &c.
	7. When the doors open--I imagine there's de facto standard code (available from the ISO, perhaps?) floating around for digitized elevator controls. But, for the sake of this exercise, let's hash it out…
		a. Once the control system reads the floor's QR code such it is level with the camera, the doors 'open until fully-open'.
		b. They stay open for 30 seconds before closing automatically.
		c. The doors use a mechanical system where, if anything jostles their inside surface, they re-run the 'open until fully-open' routine.
			i. The doors can also use a digital system of laser tripwires to accomplish the same purpose, or provide a complimentary and orthogonal failsafe.
![image](https://user-images.githubusercontent.com/81997990/124364341-be3be980-dbf5-11eb-8ecf-2b1a83a46cd8.png)
