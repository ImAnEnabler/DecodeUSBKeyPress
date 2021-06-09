# DecodeUSBKeyPress

## Decode HID USB key

Python3 script to decode HID USB data.
Read from a file containing values (hex format 8 bytes) per line

Run the script using the following command: 
```
python3 .\decodeusbkeypress.py file_to_decode.txt
```

### Data model
AABBCCDDEEFFGGHH

AA => Modifier keys status  
BB => Reserved field  
CC => keypress #1  
DD => keypress #2  
EE => keypress #3  
FF => keypress #4  
GG => keypress #5  
HH => keypress #6  

### Modifier keys status
This byte is a bitfield, where each bit corresponds to a specific modifier key. When a bit is set to 1, the corresponding modifier key is being pressed. Unlike PS/2 keyboards, USB keyboards don't have "scancodes" for modifier keys. 

0x01 => Left Ctrl.  
0x02 => Left Shift.  
0x03 => Left Alt.  
0x04 => Left GUI (Windows/Super key.)  
0x05 => Right Ctrl.  
0x06 => Right Shift.  
0x07 => Right Alt.  
0x08 => Right GUI (Windows/Super key.)  

When software receives an interrupt and, for example, one of the Shift modifier keys are set to 1, software should use the scancode table for the shift modification to get the key from the scancode. 

### Reserved field
This byte is reserved by the USB HID specification, and thus software should ignore it. 

### Keypress
One keyboard report can indicate up to 6 keypresses. All these values are unsigned 8-bit values (unlike PS/2 scancodes, which are mostly 7-bit) which indicate the key being pressed. A reference on the USB scancode to ASCII character conversion table is in the bottom of the article. 

## References
https://wiki.osdev.org/USB_Human_Interface_Devices
https://www.win.tue.nl/~aeb/linux/kbd/scancodes-14.html

## Use case
Decoding a usb pcap

## Keywords
usb hid tshark pcap usbpcap wireshark scancode decode
