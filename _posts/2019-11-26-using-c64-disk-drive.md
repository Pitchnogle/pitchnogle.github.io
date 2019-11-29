---
title: "Using C= Disk Drive"
categories:
  - c64
tags:
  - commodore 64
---

This is a brief guide on how to use the [1541 disk drive]({{ site.url }}/assets/pdf/Commodore_1541_Disk_Drive_Users_Guide.pdf) with a Commodore 64.

# Determine the DOS version

Commodore made a number of disk drives for their various computer models. To determine the DOS version used on a disk drive, enter and run the following program with no disk inserted.

```
10 REM READ THE ERROR CHANNEL
20 OPEN 15,8,15
30 INPUT#15,EN,EM$,ET,ES
40 PRINT EN,EM$,ET,ES
50 CLOSE 15
```

![C=64 check dos version]({{ site.url }}/assets/images/c64/check_dos_version.png)

# Formatting a new disk

On a real Commodore 64, a new disk named `BLOG DISK` with the id of `B0` can be formatted using the command:  

OPEN 15,8,15,"N0:BLOG DISK,B0":CLOSE 15
{: .notice--info}

If using the Vice emulator, select 'File->Create and attach an empty disk image ...'. The name in the upper part of the window refers to the disk name on Windows; in this example, the file created would be named `blog_disk.d64`. 

The lower part of the window refers to the C64 side. In this case the disk is given the name `BLOG DISK` with an id of `B0`. *Make sure to use lower case. It will be upper case within Vice. If upper case is used, then the name and id will be symbols.*

![vice create new disk]({{ site.url }}/assets/images/c64/vice_new_disk.png)

If a disk has already been created, select 'File->Attach disk image->Drive #8' or shortcut key Alt-8 to load a disk in Vice. This opens a dialog similar to the file creation window. Navigate to the location of the saved disk image then click 'Open'.
{: .notice--info}

# Listing the disk directory

Once the disk is present, `LOAD"$",8` command followed by `LIST` will display the contents.

![C=64 list directory]({{ site.url }}/assets/images/c64/vice_disk_list.png)

This is an empty disk so there are no programs present.

# Saving a new program

One nice feature of Vice is the ability to copy-paste a program. _Make sure the program is written in lower case before pasting into Vice._ If a Basic program is copied onto the clipboard, select 'Edit->Paste' or alt-insert to paste the program to the emulator. This is handy for source control of Basic programs.
{: .notice--info}

In this section we will create some simple programs to change the border, the screen color and the text color. The code is the same for each *look* except for the first two lines.

This program changes the screen color to resemble a VIC20.
```
10 rem vic20 look
20 bc=14:sc=1:tc=6
30 poke53280,bc
40 poke53281,sc
50 poke646,tc
60 end
```

To save the program to the disk drive, type:
```
SAVE"VIC20 LOOK",8
```

When this program is run, the system colors will change.

With the program listed we use the cursor keys to edit lines 10-20 to make the colors look like other old computers. Several more *looks* were saved using this idea.
{: .notice--success}

# Loading a program

Now, if we list the directory again, we should see our new programs.

![C=64 VIC20 look]({{ site.url }}/assets/images/c64/vice_disk_list2.png)

We can load a particular program by using its name directly.

```
LOAD"APPLE LOOK",8
```

![C=64 load apple look]({{ site.url }}/assets/images/c64/load_apple_look.png)

If we `LIST` again, the Basic program will be shown in memory.

![C=64 list apple look]({{ site.url }}/assets/images/c64/run_apple_look.png)

There is another way to load a program using the cursors. This time, we'll load the CoCo look program. Use the cursor keys to navigate to the line with the CoCo look program, type `LOAD` over the program number, then `,8` after the program name. Keep hitting spacebar to clear the `PRG` part of the line. 
{: .notice--info}

![C=64 load coco look]({{ site.url }}/assets/images/c64/load_coco_look.png)

# Updating a saved program

Line 10 in the listing is incorrect -- the `REM` comment wasn't updated properly. If we update the line, and save the file like before, it won't take since the file already exists. In order to revise the file, the syntax for saving the file changes somewhat.

We need to add a `@0:` before the filename. *Internally, this is essentially creating a new file, deleting the old file, then renaming the new file to the old file, but this way involves much less typing!*
{: .notice--success}

![C=64 view coco look]({{ site.url }}/assets/images/c64/update_coco_look.png)

# Deleting a saved program

So far, we've been able to create files, load files, and revise files. Next, we will delete (or 'scratch') a file.

The syntax is similar to the previous section, but this time `S0:` is added before the filename. For our example, we will delete the "APPLE LOOK" program.

![C=64 delete apple look]({{ site.url }}/assets/images/c64/del_apple_look.png)

In order to verify the program has been deleted enter `LOAD"$",8` then `LIST` again.
{: .notice--warning}
