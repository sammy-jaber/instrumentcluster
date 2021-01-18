# Identifying register addresses on CAN bus-controlled instrument clusters

This is particularly useful for DIY EV conversions where the engine ECU has been removed but still want to utilise the original instrument cluster.

Firstly you need to identify the pin assignment for the instrument cluster you want to control because you have to know which pins are used for the CAN BUS data transfer.

Then you'll need the syntax of sending the CAN Broadcast over the CAN Bus Shield/Adaptor (here's what I used):
unsigned char stmp[8] = {0, 1, 2, 3, 4, 5, 6, 7};
CAN.sendMsgBuf(0x00, 0, 8, stmp);
You will need to find the correct register addresses. This method uses ‘brute-force’ technique using a simple "for loop".
Something like:
for (int i = 0; i < 4096; i++) {
    unsigned char stmp[8] = {128,128,128,128,128,128,128,128};
    CAN.sendMsgBuf( i, 0, 8, stmp);
    serial.println( i ); //Print out the actual register address
    delay(100); //wait to check if there happened something on the dash  
    }
You should try to vary the values. Most of it worked with 128, 0, 64 or 255. The loop only has to go to 4095, because this is the maximum value for an 3 digit hexadecimal
register address (register reaches from 0x000 to 0xFFF).
