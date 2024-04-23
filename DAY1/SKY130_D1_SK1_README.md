#  SKY130_D1_SK1 - How to talk to computers
##  Introduction to QFN-48 Package, Chip, pads, core, die and Ips 

### 	• Fundamental Terminologies:-
1. **Wire bonds** 

     wire bonds are thin wires that connect the semiconductor die (chip) to the leads of the package, enabling electrical signals to travel between the chip and the external world. So that we will be able to transfer the signals between chip and outside the world.
![image](/DAY1/assets/07R01.jpg)

2.	**Pads**

    Pads are the metal areas on the surface of an integrated circuit (IC) where external connections, such as wires or solder balls, are attached. These pads serve as contact points for connecting the IC to other components or circuitry, facilitating the transfer of electrical signals or power.By using this pads we can send the signals through the pads inside the chip.

3.	**Foundry IP's**
   
    Foundry - It is a place with set of machines, where the actual chips get manufactured.
    Generally we will give the whole design layout (Tapeout or GDS file) to the foundry, Foundry will manufacture the chip for us.

  	Foundry IPs (Intellectual Properties) are pre-designed and pre-verified components provided by semiconductor foundries to their customers. These components are essential building blocks for designing integrated circuits (ICs) and include standard functions such as memory blocks, input/output interfaces, and various analog and digital circuitry. Foundry IPs help designers by providing a a set of building blocks that can use to create Digital circuit designs without having to design every logic function from scratch.
  	
      **Examples** :-	Memory blocks (e.g., SRAM, ROM), interface IPs (e.g., USB, PCIe, HDMI), and analog IPs (e.g., PLLs, ADCs, DACs).

    Companies will take these foundry IP's and design their own design with some extra things and then they will send it to foundry , foundry will manufacture the IC.

4.  **Macro**
   
    A pre-designed and pre-verified functional block that performs a specific task within an integrated circuit (IC). Macros are typically larger than standard cells and can include complex functions such as arithmetic units, memory blocks, or interface controllers. Integrating macros into a chip design allows designers to save time and effort by using pre-designed and thoroughly tested functional blocks, rather than designing these functions from scratch.
    
    Examples :- Graphics Processing Unit (GPU), Digital Signal Processor (DSP), Image Signal Processor (ISP) .. etc.
				
    #### The key difference is that a macro is a specific function within a chip design, while foundry IP encompasses pre-designed components provided by semiconductor foundries for general use in various chip designs.

5. **Die**

     A die, is a small, rectangular piece of semiconductor material (usually silicon) on which the integrated circuit (IC) is fabricated. A die can contain any number of cores.

  ![image](/DAY1/assets/die.png)

  #### A Typical chip consists below parts as shown in fig.
  
  ![image](/DAY1/assets/fondary%20ips.png)

  **what is QFN-48?**

  The QFN (Quad Flat No-leads) 48 package is a type of surface-mount integrated circuit (IC) package that is widely used in the semiconductor industry. It is characterized by its flat, rectangular shape and the absence of traditional leads or pins extending from the package.


## Introduction to RISC - V
  RISC-V is an open-source instruction set architecture (ISA) based on the Reduced Instruction Set Computing (RISC) principles. It is designed to be modular, extensible, and customizable, allowing for a wide range of implementations across various applications and industries. RISC-V has gained significant attention and adoption in recent years due to its openness, flexibility, and potential for innovation in the semiconductor industry.

  If the user is giving the specifications or instructions to the computer in the C language , the computer will not be able to understand the c language. we have to make this c program needs to be run on particular layout (Hardware). For this we need to pass this c program to particular hardware in certain terms.

  The steps that follow is :-
  
  C program is first compiled in it's assembly language which is nothing but RISC-V assembly language.  
  Then it is converted into machine language also known as binary language(1's & 0's) which is understood by the hardware of the computer (Layout).  
  Finally this 1's & 0's gets executed in the particular layout. We will get the required output.

  ![image](/DAY1/assets/Screenshot%202024-04-15%20122606.png)


  There will be another interface required that needs to be present between RISC-V and Layout That is known as Hardware description language.
  This means we need to create or implement this RISC-V specifications in terms of RTL. This RTL output will fed to the Hardware(Layout).

  ![image](/DAY1/assets/implementation.png)


  ### From Software applications to Hardware

  Applications(Apps) which we are used in day do day life. These apps are actually run in Mobile or Laptop.  
  How these applications are working?

  Example :- Suppose we are using the stopwatch. Whenever we click on start button it will start working and if we click stop button it will stop. How is it possible? 
  
  The steps that follow to give requird output is :-

  First The application software enters into a system software. This system software will convert into machine language.  
  The flow of system software works as 

**OS (Operating System)**'  
**Compiler**  
**Assembler**  

  The output of OS is small functions in the C, C++, JAVA.  
  These will taken by the respective compiler and converted into instructions.  
  The syntax of this instructions will depend upon the Hardware we used. This Hardware belongs to anything like Intelx86,  RISC-V, MIPS.  
  If the hardware belong to RISC-V then the instructions format also belongs to RISC-V.  
  Then the Assembler will take the instructions and converted into binary or machine language.  
  That machine language will fed into the hardware (Layout) ,then It will give the required output.  

  ![image](/DAY1/assets/application.png)

  ![image](/DAY1/assets/assembler.png)