# COA-Lab_task-5
Write an assembly language program to perform division of 8-bit and 16-bit data.
### README for Assembly Code

---

#### Overview:
This program demonstrates how to perform basic arithmetic operations (division) and hexadecimal digit extraction using x86 assembly language. It converts both the quotient and remainder from a division into their hexadecimal representations and prints them as characters. Additionally, the second section of the code does division and prints both quotient and remainder in hexadecimal format using the interrupt `int 21h` to print characters on the screen.

---

#### Prerequisites:
- You should be familiar with x86 architecture, 16-bit registers, and basic assembly operations like shifting, masking, and interrupt handling.
- You should be using EMU8086 or any compatible assembler and emulator that supports 16-bit DOS interrupts.

---

#### Instructions:

1. **First Program Segment:**
   - The code starts at address `org 100h` and performs division of `AL` (96h) by `BL` (10h).
   - The quotient and remainder are extracted, converted into hexadecimal format, and printed character by character.
   - The program then moves on to convert both the quotient and remainder into their ASCII representations for printing.

2. **Second Program Segment:**
   - Initializes AX and BX registers with `1980h` and `1000h` respectively.
   - It divides `AX` by `BX` and stores the quotient in `AX` and the remainder in `DX`.
   - Both the quotient and remainder are printed in hexadecimal format using similar masking and shifting techniques as in the first segment.

---

#### Key Sections:

1. **Division and Printing (First Section):**
   - **Division**: The instruction `idiv bl` divides the contents of `AL` by `BL`. After this:
     - Quotient is in `AL`, and remainder is in `AH`.
   - **Quotient Conversion**: 
     - The code uses `shr` and `and` to separate the higher and lower nibbles of the quotient for conversion into ASCII.
     - These nibbles are compared with `39h` (ASCII for '9') to determine whether they need to be converted into a digit (0-9) or a letter (A-F).
   - **Remainder Conversion**:
     - Similar operations are performed for the remainder, stored in `BH`.
     - The nibbles are converted and printed using interrupts.

2. **Division and Printing (Second Section):**
   - **Division**: The instruction `div bx` divides `AX` by `BX`. The quotient is stored in `AX` and the remainder in `DX`.
   - **Printing Quotient and Remainder**:
     - The quotient and remainder are processed in chunks, extracting the higher and lower nibbles, converting them to their ASCII equivalents, and printing using `int 21h`.

---

#### Breakdown of Key Operations:

1. **Division**:
   - `idiv` and `div` are used to divide the contents of `AX` or `AL` by another register (BL or BX), which stores the quotient and remainder in separate registers.

2. **Nibble Extraction**:
   - The higher nibble is extracted by masking with `0f0h` and shifting right by 4 bits.
   - The lower nibble is extracted by masking with `0fh`.

3. **ASCII Conversion**:
   - Digits (0-9) are directly converted by adding `30h` (ASCII for '0').
   - Letters (A-F) are converted by adding `7` after checking if the value exceeds `9` using `cmp`.

4. **Printing**:
   - Each character is printed using DOS interrupt `int 21h` with `ah = 02h` (print character) and the character stored in `dl`.

---

#### How to Run:
1. Load the code into EMU8086 or a compatible x86 assembler.
2. Assemble and run the program.
3. The program will print the quotient and remainder in hexadecimal after performing the division operations.

---

#### Example Output:
- For the first section, dividing `96h` by `10h` will result in a quotient of `9` and remainder `6`, both printed as hexadecimal characters.
  ![image](https://github.com/user-attachments/assets/63f666db-23d3-4089-9b54-b86fc1ee54a2)

- For the second section, dividing `1980h` by `1000h` will yield the hexadecimal quotient and remainder which will be printed.
![image](https://github.com/user-attachments/assets/128feb08-2ff2-4d90-ab8d-e87db8f5dbce)

---

#### Notes:
- The program makes use of DOS interrupts for printing, which works on legacy systems or emulators supporting DOS.
- Ensure that the numbers being divided do not exceed the capacity of the registers involved (8-bit or 16-bit).

---

#### Author:
- **Sruthi Vihitha Potluri**
  
