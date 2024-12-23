# What this repo contains
NTGameFramework.xxx and Engine.xxx are debug menu files

fovedit coalesced

original code - AspectRatioAxisConstraint=AspectRatio_MaintainXFOV

changed code to - AspectRatioAxisConstraint=AspectRatio_MaintainYFOV

~~also this is the chase camera fov changes (fov when moving) original code - m_useSpeedFoV=false  Change code to m_useSpeedFoV=trueput fov  to m_speedFoVNewValue=120 this should give a wider fov similar to dmc4~~

! removed this because its annoying and difficult to adjust

coalesced_int.bin is the original for the international english

# How I Got Access to the Debug Menu in *DmC: Devil May Cry*

This little guide could work for other Unreal Engine 3 games that have a debug menu.

<details>
  <summary>Step-by-Step Guide</summary>

  1. **Use UE Explorer**
     - Download and open UE Explorer.

  2. **Find `IsNTGoldMaster` in `NTGameFramework`**
     - Look for this function in either the `NTWorldExec` or `NTWorldInfo` class (I forgot which one).

  3. **Collapse the Class**
     - Collapse the class.

  4. **Collapse Functions**
     - Next, collapse the functions to locate `IsNTGoldMaster`.

  5. **Right-Click `IsNTGoldMaster`**
     - Choose **View Table Buffer** to inspect the function's bytecode.

  6. **Edit the Bytecode**
     - Look for the sequence at the end:  
       ```
       01 25 02 00
       ```
       This indicates `true` in Unreal Script.

     - Change it to:  
       ```
       04 28 00 00
       ```
       This indicates `false`.

  7. **Save Changes**
     - Save the modified buffer.

</details>

---

The `IsNTGoldMaster` function asks, "Is this the final release?" By modifying it to always output `false`, you successfully trick the game into thinking it's a developer build, granting access to the debug menu.


# Guide How to Replace Files from your PS4 PKG Game

Step 1: Unpacking your game (fake pkgs only) (skip if your game is already dumped)
-
Begin going to the release tab of [PS4-PKG-TOOL](https://github.com/pearlxcore/PS4-PKG-Tool) download and extract the latest zip

Then download [fake-pkg-tools](https://github.com/CyB1K/PS4-Fake-PKG-Tools-3.87)

Extract the fake pkg tools to the PS4PKGToolTemp folder

now we have ps4 pkg tool ready to extract our files

open ps4 pkgtool set your directory to where your ps4 pkg is placed

you should see your pkg file and info about it listed click on it to select it

now you want to go to the view and extract tab and extract full pkg to a folder of your choice

Step 2: Setting up files for repack
-
You should have two folders named Sc0 and Image0 within a folder named after your game

Move the files in Sc0 over to the folder in Image0 named sce_sys then delete the Sc0 folder

Now you want to rename the folder with your game name after the Title ID of your game with a -app at the end

![image](https://github.com/user-attachments/assets/a419d7e8-f1bc-4c4e-9549-8d0fe7b9401c)

this is what it should look like (folder will just contain your Image0 folder with all the game files)

Drag and drop the coalesced here and replace

![image](https://github.com/user-attachments/assets/6e7fec38-e320-4e97-a684-7393ce715d53)

Step 3: repacking our game with fake-pkg-tools
-
Go back to your ps4-pkg-tool directory and go to the PS4PKGToolTemp folder 

you need to generate a gp4 project file with geng4_app.exe from CUSAXXXXX-app of your dump and save it.

![image](https://github.com/user-attachments/assets/d35589db-f9fc-40a9-aefa-3d61a9c90cbf)

selected image0 as our folder to generate our gp4

![image](https://github.com/user-attachments/assets/b8b92256-6673-44d6-8a16-a2f08f6a94e4)

save it wherever but i put it aside image0

now we are ready to pack our files back into a pkg (this requires about 30 gbs of space for temp files on your C: drive so clear up space and 17 gbs on the drive you are storing the pkg)

in our PS4PKGToolTemp folder open orbis-pub-gen.exe

go to file at the top left then press open and then go to the directory to where our gp4 file is at and doubleclick on it to open it 

![image](https://github.com/user-attachments/assets/4c249d3f-85b0-4613-afae-398dec6663c1)

now press build and choose your output path and you should be done after this takes an hour to compress into a pkg

![image](https://github.com/user-attachments/assets/5cfeaf22-79ea-4109-a10f-68abf7bb1580)

Step 4: Install our pkg
-
My preferred way is using [ps4remotepkgsenderv2](https://github.com/Gkiokan/ps4-remote-pkg-sender)

congrats now you should have increased fov for DmC Definitive Edition

How to make your own config edits
---
Download and extract [MELE_quickIniEditor](https://github.com/AYasinAkalin/MELE_quickIniEditor)

all we really want is LECoal folder here as i havent actually ran this program to see what it does

go to the LECoal folder open your terminal there or change directory to the lecoal folder

copy and paste the original or your edited coalesced_xxx.bin file to the le coal folder

now you want to make an unpacked folder within that folder

**!!!! ALWAYS BACKUP COALESCED BEFORE TWEAKS INCASE YOUR CHANGES BREAK YOUR GAME!!**

**there is a original coalesced_int.bin here incase with zero edits**

![image](https://github.com/user-attachments/assets/1b6e6563-c6f2-495c-a392-cc7f2b1ce01e)

so everything should look like this at this point

open terminal/powershell whatever you use that gives you access to your command line 

**windows instructions** 

cd -path "yourLECoaldirectory"

The command to unpack is:
.\LECoal.exe unpack Coalesced_XXX.bin "your Unpacked folder directory”

your unpacked folder should contain your ini files now

make your changes to your inis 

Go back into PowerShell, Type:

.\LECoal.exe pack "Your Unpacked directory" Coalesced_XXX.bin

**linux instructions (requires wine)**

cd (your LECoal directory)

wine LECoal.exe unpack Coalesced_XXX.bin YourUnpackedDirectory/

make your changes

wine LECoal.exe pack YourUnpackeddirectory/ Coalesced_XXX.bin

now you should have our new coalesced bin 

replace it in your unpacked game files and repack your game and enjoy!
