# Exp 5 Physical Design of a 4-Bit Up-Down Counter

## Aim:

Execute floorplanning, power planning, and placement for the synthesised 4-bit up-down counter design.

## Tool Required:

Physical Design: Innovus

## Mandatory Inputs for PD: 

1. Gate Level Netlist [Output of Synthesis]
   
2. Block Level SDC [Output of Synthesis]
   
3. Liberty Files (.lib)
   
4. LEF Files (Layer Exchange Format)
   
## Procedural Steps:

Ensure the Synthesis for the target design is complete, and then open a terminal from the corresponding workspace. 

• Initiate the Cadence tools and cmd:innovus (Press Enter) 

• For Innovus tool, a GUI opens, and the terminal also enters the Innovus command prompt, where the tool commands can be entered. 

After importing the Design, Perform the following Physical Design stages:

→ Floor Planning 

→ Power Planning

→ Placement
Note : Check the paths to properly read in the input files. 

•	Else, if you would like to import your design using GUI, open the Innovus tool and from the GUI, go to File → Import Design.

o	A new pop-up window appears. 

o	First, load the netlist. You can browse for the file and select “Top cell : Auto Assign”.

•	Similarly, select your LEF files from the specified path.

•	Once LEF Files are loaded, Next step is to create the power supply pins both VDD and VSS

•	In order to load the Liberty File and SDC, create delay corners and analysis view, select the “Create Analysis Configuration” option at the bottom.

o	An MMMC browser Pops Up.

<img width="819" height="670" alt="image" src="https://github.com/user-attachments/assets/12b66c0e-44d0-437e-878e-7620932e7edd" />

The order of adding the MMMC Objects is as follows. 

1. Library Sets
   
2. RC Corners
 
3. Delay Corners
   
4. Constraints (SDC)
   
Once all of them are added, Analysis Views are created and assigned to Setup and Hold. 

In order to add any of the objects, make a right click on the corresponding label → Select New. 

Adding Liberty Files (slow.lib, fast.lib) under “Library Sets

• add slow.lib with a label Slow or any identifier of your own.
<img width="1920" height="1080" alt="Screenshot (221)" src="https://github.com/user-attachments/assets/891b2626-e926-473c-9c8a-c210d0fe3f02" />


### Fig.1 Add slow Library set

• add fast.lib with a label Fast or any identifier of your own.
<img width="1920" height="1080" alt="Screenshot (222)" src="https://github.com/user-attachments/assets/a6c93196-1f84-43a0-8431-ae17456fbad7" />
### Fig.2 Add fast Library set

• Adding RC Corners can also be done in a similar process. The temperature value can be found under the corresponding liberty file. Also, cap table and RC Tech files can be added from Foundry where available.
<img width="1920" height="1080" alt="Screenshot (223)" src="https://github.com/user-attachments/assets/aee858ce-0b0b-4d5f-9d84-4d3772766ffd" />

### Fig.3 Add RC corner

• Delay Corners are formed by combining Library Sets with RC Corners.
<img width="1920" height="1080" alt="Screenshot (224)" src="https://github.com/user-attachments/assets/21f2e1fd-a686-4888-bea7-3615ad046eee" />
<img width="1920" height="1080" alt="Screenshot (225)" src="https://github.com/user-attachments/assets/af8e0019-9054-44e3-9357-dcc1181fcb9c" />

### Fig.4 Add Delay corner Max_delay & Min_delay

• Similarly, SDC can be read under the MMMC Object of “Constraints”.
<img width="1920" height="1080" alt="Screenshot (226)" src="https://github.com/user-attachments/assets/4ca92cd7-25f4-4219-9dcf-5ece0efec513" />

### Fig.5 SDC Constraint file

• Analysis Views are formed from combinations of SDC and Delay Corner.
<img width="1920" height="1080" alt="Screenshot (227)" src="https://github.com/user-attachments/assets/2bd2be0c-d0ad-4e27-a724-ebdaa143320c" />
<img width="1920" height="1080" alt="Screenshot (228)" src="https://github.com/user-attachments/assets/cd0cd7ff-6624-4d61-a42f-2556895b2142" />

### Fig.6 Add Analysis View Worstcase & Bestcase

• Once “Best” and “Worst” Analysis views are created, assign them to Setup and Hold.
<img width="1920" height="1080" alt="Screenshot (229)" src="https://github.com/user-attachments/assets/50fa33f4-617a-4771-93dd-6a5142f518f5" />
<img width="1920" height="1080" alt="Screenshot (230)" src="https://github.com/user-attachments/assets/d6254178-5b33-4623-ad79-b715521ca6b2" />

### Fig.7 Add Setup Analysis View & Hold Analysis View

• Once all the process is done, Click on “Save&Close” and save the script generated with any name of your choice. 

• Make sure the file extension remains .view or .tcl 

• After saving the script, go back to Import Design window and Click “OK” to load your design.

<img width="829" height="504" alt="image" src="https://github.com/user-attachments/assets/9daa96ae-ee07-42a3-804a-58f68763fd55" />

In the Import Design window click the save option to save the Default.globals file

• A rectangular or square box appears in your GUI if and only if all the inputs are read properly.
<img width="1920" height="1080" alt="Screenshot (232)" src="https://github.com/user-attachments/assets/8d99f2e1-ecfe-4ab8-9640-c75e7dbb36a9" />

### Fig.8 Core area

• The internal area of the box is called “Core Area”. 

• The horizontal lines running along the width of Core are “Standard Cell Rows”. Every alternate of them are marked indicating alternate VDD and VSS rows. 

• This setup is called “Flipped Standard Cell Rows”.

### → Floorplan 

#### Steps under Floorplan : 

1. Aspect Ratio [Ratio of Vertical Height to Horizontal Width of Core]

2. Core Utilisation [The total Core Area % to be used for Floor Planning]
 
3. Channel Spacing between Core Boundary to IO Boundary
 
• Select Floorplan → Specify Floorplan to modify/add concerned values to the above Factors. On adding/modifying the concerned values, the core area is also modified.
<img width="1920" height="1080" alt="Screenshot (233)" src="https://github.com/user-attachments/assets/9b11a9ab-f1d1-4bd5-96db-faa5194bcfa5" />

### Fig.9 Specify Floorplan 

• The Yellow patch on the Left Bottom are the group of “Unassigned pins” which are to be  placed along the IO Boundary along with the Standard Cells [Gates].

#### → Power Planning

#### Steps under Power Planning : 

1. Connect Global Net Connects
   
2. Adding Power Rings
   
3. Adding Power Strings
   
4. Special Route

Under Connect Global Net Connects, we create two pins, one for VDD and one for VSS connecting them to corresponding Global Nets as mentioned in Globals file / Power and Ground Nets.

1. Select Power → Connect Global Nets.. to create “Pin” and “Connect to Global Net” as shown and use “Add to list”.
   
2. Click on “Apply” to direct the tool in enforcing the Pins and Net connects to Design and then Close the window.
   
• In order to tap in Power from a distant Power supply, Wider Nets and Parallel connections improve efficiency. Moreover, the cells that would be placed inside the core area are expected to have shorter Nets for lower resistance. 

• Hence Power Rings [Around Core Boundary] and Power Stripes [Across Core Boundary] are added which satisfies the above conditions.

• Select Power → Power Planning → Add Rings to add Power rings ‘around Core Boundary’.

• Select the Nets from Browse option OR Directly type in the Global Net Names separated by a space being Case and Spelling Sensitive. 

• Select the Highest Metals marked ‘H’ [Horizontal] for Top and Bottom and Metals marked ‘V’ [Vertical] for Right and Bottom. This is because Highest metals have Highest Widths and thus Lowest Resistance. 

• Click on Update after the selection and “Set Offset : Centre in Channel” in order to get the Minimum Width and Minimum Spacing of the corresponding Metals and then Click “OK”. 

• Similarly, Power Stripes are added using similar content to that of Power Rings.

• On adding Power Stripes, The Power mesh setup is complete as shown. However, There are no Vias that could connect Metal 9 or Metal 8 directly with Metal 1 [VDD or VSS of Standard Cells are generally made up of Metal 1]. 

• The connection between the Highest and Lowest Metals is done through Stacking of Vias done using “Special Route”. 

• To perform Special Route, Select Route → Special Route → Add Nets → OK. 

• After the Special Route is complete, all the Standard Cell Rows turn to the Color coded for Metal 1 
<img width="1920" height="1080" alt="Screenshot (244)" src="https://github.com/user-attachments/assets/105397ec-20ee-4a8a-a4ae-f2bd163dfe4f" />

### Fig.10 Power plan 

The complete Power Planning process makes sure Every Standard Cell receives enough power to operate smoothly.

#### → Placement 

1. The Placement stage deals with Placing of Standard Cells as well as Pins.
    
2. Select Place → Place Standard Cell → Run Full Placement → Mode → Enable ‘Place I/O Pins’ → OK → OK .
   
• All the Standard Cells and Pins are placed as per the communication between them, i.e., Two communicating Cells are placed as close as possible so that shorter Net lengths can be used for connections as Shorter Net Lengths enable Better Timing Results.
<img width="1920" height="1080" alt="Screenshot (245)" src="https://github.com/user-attachments/assets/dffc89d2-e488-49f5-b2a2-78afc9c57a82" />

### Fig.11 Placement of standard Cells 
<img width="1920" height="1080" alt="Screenshot (247)" src="https://github.com/user-attachments/assets/59834424-d598-4399-bfee-8c612cecfce6" />
• You can toggle the Layer Visibility from the list on the Right. The List of Layers available are shown on the right under “Layer” tab with colour coding.

## Result

Thus, the physical design stages up to placement for the 4-bit up-down counter were completed and verified.
