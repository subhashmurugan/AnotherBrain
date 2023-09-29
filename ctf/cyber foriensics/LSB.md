
Least significant bits(Lsb) in the left lowest  bit or right lowest bits it depends on the architecture of the system . If the LSB is on the right, the architecture is called "little-endian" If the LSB is on the left, the architecture is called "big-endian."

The number of image pixels in a **PNG** file is generally composed of **RGB** three primary colors (red, green, and blue). Each color occupies 8 bits, and the value ranges from 0x00 to 0xFF, that is, there are 256 colors, which contain a total of 256 to the third power. Thus there are 16777216 color in total.

The human eye can distinguish about 10 million different colors, which means that the human eye can't distinguish the remaining 6 million colors. LSB steganography is to modify the lowest binary bit (LSB) of RGB color  components, each color will have 8 bits, LSB steganography is to modify the lowest bit in the number of pixels, and human eyes will not notice before and after this change, each pixel can carry 3 bits of information.


zsteg tool is used to find the flag in the picture
https://github.com/zed-0xff/zsteg



