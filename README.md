<b>XOR Checksums - sounds complicated but it really isn't</b>

Checksums created using XOR are standard in AIS and GPS serial communication.

Most of us are aware of GPS but AIS (Automatic Identification System) is less well known. This is a transponder system used by commercial shipping vessels to broadcast information including, but not limited to, vessel name, MMSI, position, course over ground, speed over ground and rate of turn. Most sailing vessels don't have this transponder but may have an AIS receiver that can show the data superimposed on a digital radar or GPS plotter.

A GPS data string example:-
$GPGGA,092750.000,5321.6802,N,00630.3372,W,1,8,1.03,61.7,M,55.2,M,,*76

NOTE: the checksum 76 at the end, is the hexadecimal representation of decimal 118 i.e. binary 01110110.<br>
01110110 is the result of the last XOR calculation.

The actual data to be processed is enclosed between "$"(a marker for the beginning of the data string) and "*"(a marker for the end of the data string), and hexadecimal 76 is the XOR checksum. <b>Important</b>, this is NOT an array, the commas are part of the serial stream. Once the data string has been extracted and it's checksum has been confirmed as correct, the string may be converted to an array for further use.

<b>Now the theory</b>

XOR or exclusive OR as it is properly called, produces a 1 if there is a difference between the respective bits of two bytes and zero(0) if the respective bits have the same value.

Example:
1010 and 0111 results in 1101 because, from the left, bits 1, 2 and 4 are different, and bits 3 the same.

So, how do we get a checksum of 6A in the demo sketch, for the word "arduino"?

The binary values of "a" and "r" are compared to get the first xor result value, then the binary value of "d" is compared to the xor result. This is repeated until the binary value of "o" is compared to the previous xor result. The final xor result is then output as hexadecimal 6A (decimal 106).

<table>
  <tr>
    <th>Char</th>
    <th>ASCII</th>
    <th>bit 8</th>
    <th>bit 7</th>
    <th>bit 6</th>
    <th>bit 5</th>
    <th>bit 4</th>
    <th>bit 3</th>
    <th>bit 2</th> 
    <th>bit 1</th>
    <th>Hex</th>
  </tr>
  <tr>
    <td>a</td>
    <td>97</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>61</td>
  </tr>
  <tr>
    <td>r</td>
    <td>114</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>72</td>
  </tr>
  <tr>
    <td>xor result</td>
    <td>19</td> 
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>13</td>
  </tr>
  <tr>
    <td>d</td>
    <td>100</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>0</td>
    <td>64</td>
  </tr>
  <tr>
    <td>xor result</td>
    <td>119</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>77</td>
  </tr>
  <tr>
    <td>u</td>
    <td>117</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>75</td>
  </tr>
  <tr>
    <td>xor result</td>
    <td>2</td> 
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>2</td>
  </tr>
  <tr>
    <td>i</td>
    <td>105</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>69</td>
  </tr>
  <tr>
    <td>xor result</td>
    <td>107</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>6B</td>
  </tr>
  <tr>
    <td>n</td>
    <td>110</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>6E</td>
  </tr>
  <tr>
    <td>xor result</td>
    <td>5</td> 
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>5</td>
  </tr>
  <tr>
    <td>o</td>
    <td>111</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>6F</td>
  </tr>
  <tr>
    <td>xor result</td>
    <td>106</td> 
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>6A</td>
  </tr>
</table>

<b>Practical uses</b>

Communication between two Arduinos either using RX/TX, USB or Radio comms (e.g. 433MHz modules etc).

Finally, if you want to transmit the word "arduino" in GPS style, the output to the serial port would be <b>$arduino*6A</b>

<b>TIP: </b>You don't have to use $ or *, any two characters will do, but you cannot have these characters in the data string!

<b>That's all folks! Hope you find this useful.</b>
