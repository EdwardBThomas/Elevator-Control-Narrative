# Elevator-Control-Narrative
A control narrative for a hypothetical elevator

	1. By default, the elevator is in state 0, or idle and resting on floor 1
	2. Once a floor is called or entered, the elevator moves to State 1 and the called floor is added to Table Delta F.
		a. Table Delta F is the list of all floors to stop at before the drive shifts to the opposite gear and the contents of Table Anti-Delta F are moved to Table Delta F.
		b. As a floor is stopped at and moved on from, it is removed from Table Delta F
		c. If an addition to Table Delta F would make the rate-of-change from the current floor to the next floor less than or equal to zero, that addition is added to Table Anti-Delta F.
		d. When both Tables are empty, the elevator automatically changes to State 0
			i. State 0 has read-only Table 0, containing Floor 1.
	
	3. Emergencies are independent of the control narrative--it is reasonable to say the mechanism is entirely mechanical to reduce possibility of error.
		a. Can be triggered manually 
			i. By someone pressing the corresponding button in the cabin
				1) See 3.b.i-iii
		b. Standard practice for elevator fail-safe mechanisms is strictly mechanical; in this case, once the tensioner is triggered and the plugs/cams fired, the control system switches to State 11 automatically
			i. Emergency lighting and other in-cabin alerts are turned on
			ii. Cabin is put into audio contact with the front desk and local first responders.							
	4. The correct distance to travel between stops uses two orthogonal and mutually complimentary methods.
		a. The distance between floors is a read-only variable, and the total distance to travel to the 'next' stop is calculated via multiplying the difference between the last stop and the next stop by the between-floor distance.
		b. In addition, the control system has a camera that scans barcodes or QR codes on the inside of the shaft.
			i. The control system thereby can make minor corrections by engaging the drive system until the 'stop here' graphical code aligns with the camera.
			ii. This is for correcting mechanical elasticity as machines wear over time, making sure the cabin opens as level as possible with the floor for wheelchairs, dollies, hospital beds, the blind, the infirm, &c.
	5. When the doors open--I imagine there's de facto standard code (available from the ISO, perhaps?) floating around for digitized elevator controls. But, for the sake of this exercise, let's hash it out…
		a. Once the control system reads the floor's QR code such it is level with the camera, the doors 'open until fully-open'.
		b. They stay open for 30 seconds before closing automatically.
		c. The doors use a mechanical system where, if anything jostles their inside surface, they re-run the 'open until fully-open' routine.
			i. The doors can also use a digital system of laser tripwires to accomplish the same purpose, or provide a complimentary and orthogonal failsafe.
			
5 instances of change:
	1. A1: A floor is input into the control script.
		a. Since there isn't another floor in either table, the rate of change is positive and the entry automatically goes into table Delta F.
	2. A2: A floor is input into the control script.
		a. The script checks the new entry: if it would maintain a positive rate of change with the current floor (or the most-recent floor), the entry goes into table Delta F. If the rate of change would be negative, it would go into table Anti-Delta F.
	3. B: Delta F is null > change to Anti-Delta F
		a. Once table Delta F no longer contains any entries, the drive system of the elevator changes gears and either of two things can happen:
			i. The contents of table Anti-Delta F are moved to table Delta F
			ii. The labels of the two tables are switched.
		b. The point is, with the drive's gear switched, the entries that would have previously created a negative rate of change would instead create a positive rate of change. The elevator can then use the same logic.
	4. C1: Delta F and Anti-Delta F are null
		a. The system itself enters floor 1 or automatically calls floor 1
			i. If the elevator was moving down previously, adding floor 1 maintains a positive rate of change
			ii. If the elevator was moving up previously, the entry goes into table Anti-Delta F
				1) With table Delta-F empty, the tables are switched, the drive reverses, and the script just reads off floor 1.
	5. C2: Delta F and Anti-Delta F are null
		a. The system itself enters floor 1 or automatically calls floor 1
			i. The script does not actually remember it's on floor 1--the camera inside the shaft scans the QR code, reads floor 1, engages the drive as necessary (which is not at all), and opens the door as necessary (which is not at all, as it is already open).
![image](https://user-images.githubusercontent.com/81997990/126216934-811ac08f-0b55-4f92-9958-d3031dd40051.png)
	
![image](https://user-images.githubusercontent.com/81997990/126215997-f0a98242-fa0f-41a3-8514-deb9d5ef1790.png)
