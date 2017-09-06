Big Endian and Little Endian - read + write word
================================================
I thought sharing some code for accessing word from in little & big endian ways will be helpful for someone.


## READ

    int getWord(int address) {
      int i = address - from; //From is the start address of memory in the Linear Address Space

      if (CONSTANTS.BIG_ENDIAN) {
       return (((int) memory[i] << 24)
         | (((int) memory[i + 1] << 16) & 0x00ff0000)
         | (((int) memory[i + 2] << 8) & 0x0000ff00)
         | (((int) memory[i + 3]) & 0x000000ff));
      } else {
       return (((int) memory[i + 3] << 24)
         | (((int) memory[i + 2] << 16) & 0x00ff0000)
         | (((int) memory[i + 1] << 8) & 0x0000ff00)
         | (((int) memory[i]) & 0x000000ff));
      }
     }

## WRITE

     void setWord(int address, int data) {
      int i = address - from; //From is the start address of memory in the Linear Address Space

      if (CONSTANTS.BIG_ENDIAN) {
       memory[i] = (byte) (data >> 24);
       memory[i + 1] = (byte) ((data & 0x00ff0000) >> 16);
       memory[i + 2] = (byte) ((data & 0x0000ff00) >> 8);
       memory[i + 3] = (byte) (data & 0x000000ff);
      } else {
       memory[i + 3] = (byte) (data >> 24);
       memory[i + 2] = (byte) ((data & 0x00ff0000) >> 16);
       memory[i + 1] = (byte) ((data & 0x0000ff00) >> 8);
       memory[i] = (byte) (data & 0x000000ff);
      }
     }


## Useful Resource:
http://en.wikipedia.org/wiki/Endianness
