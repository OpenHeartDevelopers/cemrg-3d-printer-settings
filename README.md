# 3D Printing at CEMRG
We need PrusaSlicer.
## PrusaSlicer (instructions for linux)
Install flatpak, which is like snap in that it's a package manager.
```shell
sudo apt update -y 
sudo apt install flatpak gnome-software-plugin-flatpak -y 
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

Now we actually install PrusaSlicer
```shell
flatpak install flathub com.prusa3d.PrusaSlicer
```
Run with: 
```shell
flatpak run com.prusa3d.PrusaSlicer
```
> You can put this on a script. 

## Instructions to print
### Convert your mesh to obj for printing
To print you’ll need a surface mesh in `obj` format (you can convert it using meshtool)
```shell
meshtool extract surface -msh=[PATH_TO_MESH] -ifmt={vtk,carp_txt} -ofmt=obj
``` 
In the installer, when it ask you to select the printer, scroll down and select **Original Prusa i3 MK3S & MK3S+**, with the nozzle options of **0.4, 0.6 and 0.8 mm**

### Setup printer settings 
+ Select “Normal” or “advanced” mode (yellow mode) 
+ The setup is simple to do manually: 
  + The main things are the extruder is 0.8mm, 
  + Nozzle temperature 220 degrees, and 
  + the support is 5% and organic. 
+ Alternatively, load the environment `ready_to_print_config.ini` (File > Import... > Import Config Bundle) 

### Setup mesh on plate
+ Drag your obj file to the UI of PrusaSlicer. You can use the controls to rotate, move and 
+ Set the scaling to 0.1 (if it looks too bigm play aroung with this parameter)
+ When placing the object in the bed of the printer (the flat surface), I’d recommend to either: 
  + place it hovering a little bit. This will create the organic, tree-like supports that are really easy to snap; OR
  + rotate it in a way there's the smallest amount of contact with the bed of the printer.
+ **Ready to print:** Select “Slice” to generate the rendered/final version of the file. You’ll see the amount of material used, and the approximate time it will take to print. You can play around with the position of the object to find out how to print it more efficiently. 
+ When exporting, always export both the gcode and the session. So each case should always have 3 files: obj, gcode, and 3fm 