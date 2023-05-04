Download Link: https://assignmentchef.com/product/solved-csci-2500-assignment-4-carry-lookahead-adder
<br>
For this assignment you will implement a <em>carry lookahead adder </em>as described in <a href="https://piazza.com/class_profile/get_resource/j6fema68yeu70x/j8xw7ie3agh5lt">cla.pdf</a>. This adder improves upon the partial adder that you implemented in <a href="https://piazza.com/class_profile/get_resource/j6fema68yeu70x/j8wzjyd4916df">Lab</a> <a href="https://piazza.com/class_profile/get_resource/j6fema68yeu70x/j8wzjyd4916df">7</a>. In that lab you constructed a 4-bit ripple carry adder. Now you must build a 64-bit carry lookahead adder. This can be achieved by building a “hierarchy” of progressively larger groups, sections, etc. See the PDF for more information. Additional details may be found starting on page B-38 in your textbook. Your CLA must also support the subtraction operation. This is discussed on page B-29 of your textbook. To summarize, recall that in order to negate a number in two’s complement we have to invert all of the bits and then add 1. This can be achieved by setting the initial carry-in to 1 instead of 0. Your program must support <a href="https://en.wikipedia.org/wiki/Hexadecimal">hexadecimal</a> (base 16) input. C natively supports hexadecimal; see the documentation for the %x specifier for printf()/scanf(). You should also be using the bitwise operations C exposes as mentioned in Lab 7.

I recommend that you start with a simple ripple carry adder so you can check your answers. It will also be helpful to quickly enable debugging output to check that your <em>generates </em>and <em>propagates </em>(see the PDF) are what you expect. Sample output below.

<h1><a name="_Toc2862"></a>bash-3.2$ ./cla</h1>

Enter A (hex):

1

Enter B (hex):

2

Add (0) or subtract (1): 1

<h1><a name="_Toc2863"></a>A is 0000000000000001 or 1</h1>

B is 0000000000000002 or 2

Inverting 2

B (bin) : 1111111111111111111111111111111111111111111111111111111111111101 Calculate sum, S:

<ul>

 <li>(bin) : 0000000000000000000000000000000000000000000000000000000000000001</li>

 <li>(bin) : 1111111111111111111111111111111111111111111111111111111111111101</li>

</ul>

S (bin) : 1111111111111111111111111111111111111111111111111111111111111111 S is ffffffffffffffff or -1

bash-3.2$ ./cla Enter A (hex):

1

Enter B (hex):

1

Add (0) or subtract (1): 0

A is 0000000000000001 or 1

<h1><a name="_Toc2864"></a>B is 0000000000000001 or 1</h1>

Calculate sum, S:

<ul>

 <li>(bin) : 0000000000000000000000000000000000000000000000000000000000000001</li>

 <li>(bin) : 0000000000000000000000000000000000000000000000000000000000000001</li>

</ul>

S (bin) : 0000000000000000000000000000000000000000000000000000000000000010 S is 0000000000000002 or 2

<a href="#_Toc2862">bash-3.2$ ./cla Enter A (hex):                                                </a>

<a href="#_Toc2863">A is 0000000000000001 or                                                     1</a>

<a href="#_Toc2864">B is 0000000000000001 or                                                     1</a>

<a href="#_Toc2865">InvertingB (bin) : 1111111111111111111111111111111111111111111111111111111111111110 Calculate sum, S:                                                                      1</a>




1

Enter B (hex):

1

Add (0) or subtract (1): 1

<ul>

 <li>(bin) : 0000000000000000000000000000000000000000000000000000000000000001</li>

 <li>(bin) : 1111111111111111111111111111111111111111111111111111111111111110</li>

</ul>

S (bin) : 0000000000000000000000000000000000000000000000000000000000000000 S is 0000000000000000 or 0

bash-3.2$ ./cla Enter A (hex):

15

Enter B (hex):

3

Add (0) or subtract (1): 0

<ul>

 <li>is 0000000000000015 or 21</li>

 <li>is 0000000000000003 or 3</li>

</ul>

Calculate sum, S:

<ul>

 <li>(bin) : 0000000000000000000000000000000000000000000000000000000000010101</li>

 <li>(bin) : 0000000000000000000000000000000000000000000000000000000000000011</li>

</ul>

S (bin) : 0000000000000000000000000000000000000000000000000000000000011000 S is 0000000000000018 or 24

bash-3.2$ ./cla Enter A (hex):

15

Enter B (hex):

3

Add (0) or subtract (1): 1

<ul>

 <li>is 0000000000000015 or 21</li>

 <li>is 0000000000000003 or 3</li>

</ul>

Inverting 3

B (bin) : 1111111111111111111111111111111111111111111111111111111111111100 Calculate sum, S:

<ul>

 <li>(bin) : 0000000000000000000000000000000000000000000000000000000000010101</li>

 <li>(bin) : 1111111111111111111111111111111111111111111111111111111111111100</li>

</ul>

S (bin) : 0000000000000000000000000000000000000000000000000000000000010010 S is 0000000000000012 or 18

bash-3.2$ ./cla Enter A (hex): deadbeef Enter B (hex):

123abc

Add (0) or subtract (1):

0

A is 00000000deadbeef or 3735928559 B is 0000000000123abc or 1194684

Calculate sum, S:

<ul>

 <li>(bin) : 0000000000000000000000000000000011011110101011011011111011101111</li>

 <li>(bin) : 0000000000000000000000000000000000000000000100100011101010111100</li>

</ul>

S (bin) : 0000000000000000000000000000000011011110101111111111100110101011 S is 00000000debff9ab or 3737123243

bash-3.2$ ./cla Enter A (hex): deadbeef Enter B (hex):

123abc

Add (0) or subtract (1):

1

<ul>

 <li>is 00000000deadbeef or 3735928559</li>

 <li>is 0000000000123abc or 1194684</li>

</ul>

Inverting 1194684

B (bin) : 1111111111111111111111111111111111111111111011011100010101000011 Calculate sum, S:

<ul>

 <li>(bin) : 0000000000000000000000000000000011011110101011011011111011101111</li>

 <li>(bin) : 1111111111111111111111111111111111111111111011011100010101000011</li>

</ul>

S (bin) : 0000000000000000000000000000000011011110100110111000010000110011 S is 00000000de9b8433 or 3734733875

bash-3.2$ ./cla Enter A (hex): de1ec7ab1ebeef Enter B (hex):

5ca1ded

Add (0) or subtract (1):

0

A is 00de1ec7ab1ebeef or 62521287748009711 B is 0000000005ca1ded or 97132013

Calculate sum, S:

<ul>

 <li>(bin) : 0000000011011110000111101100011110101011000111101011111011101111</li>

 <li>(bin) : 0000000000000000000000000000000000000101110010100001110111101101</li>

</ul>

S (bin) : 0000000011011110000111101100011110110000111010001101110011011100 S is 00de1ec7b0e8dcdc or 62521287845141724

bash-3.2$ ./cla Enter A (hex): de1ec7ab1ebeef Enter B (hex):

5ca1ded

Add (0) or subtract (1):

1

<ul>

 <li>is 00de1ec7ab1ebeef or 62521287748009711</li>

 <li>is 0000000005ca1ded or 97132013</li>

</ul>

Inverting 97132013

B (bin) : 1111111111111111111111111111111111111010001101011110001000010010 Calculate sum, S:

<ul>

 <li>(bin) : 0000000011011110000111101100011110101011000111101011111011101111</li>

 <li>(bin) : 1111111111111111111111111111111111111010001101011110001000010010</li>

</ul>

S (bin) : 0000000011011110000111101100011110100101010101001010000100000010

S is 00de1ec7a554a102 or 62521287650877698