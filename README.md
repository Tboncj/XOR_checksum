XOR_checksum

Checksums created using XOR are quite common in AIS and GPS serial communication.

XOR or exclusive OR as it is properly called only produces a 1 if there is a difference between the respective bits of two bytes.

Example:
1010 and 0111 produces 1101 because, from the left, bits 1, 2 and 4 are different.

How do we get a checksum of 106 in the sketch, for the word "arduino"?

Chr	ASCII	Binary
a	97	01100001
r	114	01110010
xor =	19	00010011
d	100	01100100
xor =	119	01110111
u	117	01110101
xor =	2	00000010
i	105	01101001
xor =	107	01101011
n	110	01101110
xor =	5	00000101
o	111	01101111
xor =	106	01101010

<table>
  <tr>
    <th>Chr</th>
    <th>ASCII</th> 
    <th>Binary</th>
  </tr>
  <tr>
    <td>a</td>
    <td>97</td> 
    <td>01100001</td>
  </tr>
  <tr>
    <td>r</td>
    <td>114</td> 
    <td>01110010</td>
  </tr>
</table>
