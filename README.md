logic-comparator
================

This implementation of the Logic Comparator has a design flaw that I intended to fix any day. But it hasn't happened yet. Do not use the current design. 

Logic Comparator

This project aims to create a modern version of the obsolete [HP10529A](http://www.keysight.com/en/pd-1000000984%3Aepsg%3Apro-pn-10529A/logic-comparator?cc=SE&lc=eng)

The [HP10529](https://dl.dropboxusercontent.com/u/96935524/Datormusuem/HP10529%20Operating%20and%20Service%20Manual.pdf) is a rather simple device manufactured by HP in the early seventies. Although its simplicity it is quite powerful to find malfunctioning TTL ICs.

The basic idea with the HP10529A is that you have a reference IC on a small board inserted into the HP10529A Logic Comparator. Then you pu an IC clipon onto the IC that needs testing.
The HP10529A will then compare the outputs of the reference and the DUT. If there is a difference a LED will light. 


![Principal schematics](http://i.imgur.com/PQQRCGe.png "Principal schematics")

The HP10529A uses a 74L86 comparator and also a open collector driver to drive the LED. There is a capacitor on the output of the 74L86 to smear out the signal timewise.
and also a low pass filtering circuit on the open collector output so that the LED will stay on longer if there is a short pulse that is in error. When the output of the open collector NOR goes to it discharge the capacitor and also create a low level on the input of the 74L04 inverter. Thus the NOR still will have a low output for some longer time.

If the signal on the reference board is an input the signal from the DUT si connected to both the reference chip and the both of the inputs of the 74LS86. If the signal is an output the reference chip is connected to the upper input signal of the 74LS86 and the DUt connected to the lower input of the 74LS86 in the schematics above.

The first problem with the HP10529 is that it is obsolete. There are ones sold on Ebay at quite high prices. But if you get one, it only includes maybe a few adapter boards. There are shall also be a variant with ZIF socket available, but I have never seen one on Ebay.

The solution would be to make me my own one. It would be cheaper than buying an of Ebay in the US and have it shipped to Sweden.

### PCB layout

![PCB layout](http://i.imgur.com/FQjtUaC.png "PCB layout")

This is the PCB layout. The idea is to put the reference IC in the ZIF socket and then program the inputs by inserting ajumper at the aproriate position in the two rows of pin headers. I am looking into the option of creacting a small PCB that could be pushed over the PIN headers and thus can be similar to the ones used with the HP10529: A library of reference boards for common types of TTL ICs. 

The pulse stretching circuit is less advanced in that I motted the feedback signal via the capacitor that would stretch the signal. This mainly due to lack of space and possibility to route that many wires on the board.

Unfortunately there is a small annoying fault in the current layout. The electrolytic capacitor is connected to the LED directly instead of the output of the open collector driver. This is to be fixed in the layout, but the oredered boards are wrong and had to be fixed by small wires and cuts...
