# Teleham
A system for telemetry and control of a computer remotely over cheap VHF/UHF FM ham portables.

# Disclaimer
If you get in trouble with the FCC, that is not my problem. I expect you to understand the legality of this. I believe this is entirely legal, but I could be wrong. I AM NOT RESPONSIBLE FOR YOU.

# Purpose
Teleham lets you control and get information and warnings from a computer using cheap ham portables (like Baofeng or Quansheng).<br>
You can use the keypad on most ham radios while pressing PTT to send DTMF tones, this project takes advantage of that.

# Legality
The big part of this not being allowed under normal part 97 rules is that the computer is transmitting without a person involved.<br>
I believe this to still be legal. Here is why:<br>
<ul>
<li>47 CFR §97.221(b) permits automatically controlled amateur stations to transmit data emissions on the 6-meter and shorter-wavelength bands.</li>
<li>Teleham transmits telemetry and telecommand using FM on VHF/UHF. Under §97.3(c)(2), telemetry, telecommand, and computer communications are explicitly included in the definition of a data emission.</li>
<li>Because VHF and UHF are shorter than 6 meters, Teleham's automatically generated data transmissions fall within the frequency range specified by §97.221(b).</li>
</ul>
If anyone wants to prove me wrong though, please tell me.

# DTMF codes
As some ham radios cannot transmit A, B, C, or D in DTMF tones, our commands only use 0-9, *, and #.<br>
Here are some example commands:<br>
<ul>
<li>*#123: Reception check. Just echo back *#123.</li>
<li>*#456: Do I have any warnings?</li>
<li>*#789: Quick status like "OK" or "BAD".</li>
<li>*#159: In depth status.</li>
</ul>
There is one thing: how do you understand the computer's response, as it is just DTMF tones?<br>
<br>
Introducing...

# DTMF ASCII
A map to convert DTMF tones into ASCII.<br><br>
This generally requires firmware modifications to understand DTMF tones and display them with the map applied.<br>
This usually needs something like a Quansheng UV-K5, or another portable with easily modifiable firmware.<br>
I personally have a Quansheng UV-K5(8) with a firmware modification available <i>soon™</i> to display DTMF ASCII to the screen.<br>
<br>
All DTMF ASCII messages start with "A#" (or ">" in DTMF ASCII) as a magic number to signify that this is a DTMF ASCII encoded message.<br>
The encoding is that each DTMF tone encodes 4 bits. The map between each DTMF tone and 4 bits is below
<ul>
<li>1: 0000</li>
<li>2: 0001</li>
<li>3: 0010</li>
<li>A: 0011</li>
<li>4: 0100</li>
<li>5: 0101</li>
<li>6: 0110</li>
<li>B: 0111</li>
<li>7: 1000</li>
<li>8: 1001</li>
<li>9: 1010</li>
<li>C: 1011</li>
<li>*: 1100</li>
<li>0: 1101</li>
<li>#: 1110</li>
<li>D: 1111</li>
</ul>
This basically translates into the following keypad, read left->right, top->bottom as increasing binary:<br>
1 2 3 A<br>
4 5 6 B<br>
7 8 9 C<br>
* 0 # D<br>
