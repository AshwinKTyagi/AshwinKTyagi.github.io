---
title: "TinyChip"
summary: "Duration: September 2023 - December 2023 | Github: **(https://github.com/AshwinKTyagi/TinyChip)**"
date:  2023-12-16T20:48:26-08:00
# weight: 1
aliases: ["/tinychip"]
tags: ["Projects", "TinyChip"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: true
draft: false
hidemeta: true
comments: false
description: "Duration: September 2023 - December 2023"
canonicalURL: "https://canonical.url/to/Projects/TinyChip"
disableHLJS: false # to disable highlightjs
disableShare: false
disableHLJS: true
hideSummary: false
searchHidden: true
ShowReadingTime: false
ShowBreadCrumbs: false
ShowPostNavLinks: false
ShowWordCount: false
ShowRssButtonInSectionTermList: false
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/AshwinKTyagi/AshwinKTyagi.github.io/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
Github: https://github.com/AshwinKTyagi/TinyChip

## Project Desciption

I partnered with a team member to design and implement a microprocessor with a MIPS-like architecture using SystemVerilog.

### Design Constraints

The main restriction we faced was dealing with 9-bit wide instructions, which prevented us from directly copying MIPS instructions.
However, we found the most essential instructions that we will need for our programs and integrated them into our 4-register architecture.

## Instruction Format

Due to the 9 bit design constraint, we decided to split our instructions into two types. By using the 1st bit to define the "bit type",
we were able to design up to 24 different operations(We only used 19).

- Register 
    - By splitting the last 3 bits into 2 bits for the src register and 1 for the function bit, we can make use of a 4 bit opcode that derives from `{1 bit funct code, 3 bit opcode}`. 
    As a result, we can use 16 different operations using the register bit type.
```
(type bit)_(3 bit opcode)_(2 bit destination register)_(2 bit source register)_(function bit)
```
- Immediate
    - Frees up the last bit to allow us to use immedate values ranging from 0-7 instead of 0-3. 
```
(type bit)_(3 bit opcode)_(2 bit destination register)_(3 bit immediate value)
```
- EXCEPTIONS: For some commands, we decided to repurpose the 9 bits so as to provide more flexibility
| Commands       | 9 bit modification                                       |
| -------------- | -------------------------------------------------------- |
| `beq` and `bne`| `(type bit)_(3 bit opcode)_(5 bit address)`              |


## Operation Codes

| Opcode | Bit | Name |  Description | Usage    |
| ------ | --- | ---- | ------------ | -------- |
| `000`  | R   | and  | Does a logical AND on two registers.  | `and r1 r0` |
|        | F   | jump | Unique command that takes the middle 6 bits as a jump target | `j #63` |
|        | I   | andi | Does a logical AND on register and immediate  | `andi r1 #5` |
| `001`  | R   | add  | Does an arithmetic ADD on two registers | `add r1 r0` |
|        | I   | addi | Does an arithmetic ADD on register and immediate | `addi r1 #7` |
| `010`  | R   | sub  | Does an arithmetic SUB on two registers | `add r1 r0` |
|        | F   | sub0 | Used in conjunction with branching, feed result to next cycle to help determine branch condition | `sub0 r1 r0` | 
|        | I   | beq  | Paired with sub0 to do a Branch if the two values are not equal to each other. (branch value defines index in the Program Counter LUT handled by instruction memory) | `beq #12` |
| `011`  | R   | or   | Does a logical OR on two registers | `add r1 r0` |
|        | I   | bne  | Paired with sub0 to do a Branch if the two values are equal to each other. | `beq #15` |
| `100`  | R   | xor  | Does a logical OR on two registers | `add r1 r0` |
|        | I   | ldr  | Loads Word from data memory. The Data Memory address is defined by last 5 bits stored in second register.| `ldr r1 r0` |
| `101`  | R   | mult | Does a multiply on two registers | `mult r1 r0` |
|        | F   | clr  | Clear the register by doing a multiply by 0 | `clr r1` | 
|        | I   | str  | Stores word from second register into data memory at the address defined by last 5 bits of data stored in 1st register  | `sw r1 r0` |
| `110`  | R   | div  | Does arithmetic division on two registers | `div r1 r0` |
|        | I   | srr  | Does an logical shift right on data in register by an immediate | `srr r1 #7` |
| `111`  | R   | slt  | For two registers, output the one with the smaller value | `slt r1 r0` |
|        | I   | srl  | Does an logical shift left on data in register by an immediate | `srl r1 #7` |

## Optimizations

Since we were not constrained by area in this certain project, we decided to design our chip to use solely combinational logic.
As a result, our program executes one instruction every cycle, allowing for a much faster chip only limited by the propogation delay of the worstcase combinational logic.

Whereever applicable, our modules make use of two always blocks; one driven by the clock and the other driven by changes in the input values.
This design pattern allows for any change in the instructions to automatically return an output without relying on the clock.

In our Instruction Memory Module, we have the clock-driven always block update the address to be read and store the previous address in `last_addr`:
```
always @(posedge clk or posedge reset) begin
    if (reset) begin
        last_addr <= '0;
        done = 1;
    end
    else begin
        last_addr <= addr;
        done <= (mem[addr] == 'bx);
    end
end
```
The `always_comb` block then detects a change in the last_address and updates the instruction.
```
always_comb begin
    if(addr != last_addr) 
        instruct <= mem[addr];
    else
        instruct <= mem[addr];
end
```
