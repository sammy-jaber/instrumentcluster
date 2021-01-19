# Identifying register addresses on CAN bus-controlled instrument clusters

This is particularly useful for DIY EV conversions where the engine ECU has been removed but still want to utilise the original instrument cluster.

Firstly you need to identify the pin assignment for the instrument cluster you want to control because you have to know which pins are used for the CAN BUS data transfer.

Then you'll need the syntax of sending the CAN Broadcast over the CAN Bus Shield/Adaptor. In the data for each ID there are 8 bytes. Labeled Byte 0,1,2,3,4,5,6,7
You will need to find the correct register addresses. This method uses ‘brute-force’ technique using a simple "for loop".

You should try to vary the values. Most of it worked with 128, 0, 64 or 255. The loop only has to go to 4095, because this is the maximum
value for an 3 digit hexadecimal register address (register reaches from 0x000 to 0xFFF).
