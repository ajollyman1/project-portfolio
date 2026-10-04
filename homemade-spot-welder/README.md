# Homemade Spot Welder

During the process of making my battery pack for my 3kW go-kart, I needed a spot welder. After a bit of research, I realised I could make one myself from a car battery and a super simple circuit with basic MOSFETs. It would be unreliable, as the timing depended purely on my click speed, but it would get the job done.

I didn't document much of this build, but essentially:

- I made two copper probes and siliconed them to a stick.
- I wired the two probes to the positive and negative outputs of the MOSFETs.
- I added a mechanical switch that activated a side circuit, which then activated the main circuit, shorting out the car battery through the MOSFET for a few seconds.

That was enough to weld two very thin nickel strips together. Unfortunately, it was also enough to blow the four MOSFETs I used, and it never worked reliably. Since it didn't work, I found a similar design on AliExpress for $25 and decided to bite the bullet and buy that instead. The AliExpress one worked perfectly.

I got the MOSFETs from a broken e-bike motor controller.

I also 3D printed a breadboard-style jig with a bunch of small holes in it. It's the only photo I have of the project: TODO add photo.
