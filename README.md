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
				1) See 5.b.i-iii
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
![image](https://user-images.githubusercontent.com/81997990/124364341-be3be980-dbf5-11eb-8ecf-2b1a83a46cd8.png)
