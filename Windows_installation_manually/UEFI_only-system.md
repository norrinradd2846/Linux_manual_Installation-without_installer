[DISKPART]

[Shift - F10 to open Command Prompt]
diskpart
sel disk 0
clean
convert gpt

create par efi size=500
format fs=fat32

assign letter W
create par pri
format fs=ntfs quick
assign letter C
exit

[Windows DISM]
cd /d D:\Sources (i didn't mention this but this is optional)


(FOR PEOPLE WHO DOWNLOADED WINDOWS ISO FROM THE INTERNET)
dism /get-wiminfo /imagefile:D:\Sources\install.wim
dism /apply-image /imagefile:D:\Sources\Install.wim /index:1 /applydir:C:\

(FOR THOSE WHO DOWNLOADED WINDOWS FROM MEDIA CREATION TOOL)
dism /get-wiminfo /imagefile:D:\Sources\Install.esd
dism /apply-image /imagefile:D:\Sources\Install.esd /index:1 /applydir:C:\

[FOR BOOT COMMANDS]
bootrec /scanos
bcdboot C:\Windows /s W:
bootrec /scanos (repeat)


[COMMAND PROMPT RESTART]
wpeutil reboot



