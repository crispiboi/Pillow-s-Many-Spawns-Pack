The contents of this folder are all of Pillow's Random Spawns spawnpoint files copied and renamed.
Every file beginning with "spawnpoints_" is a different series of spawn points.
The servertest_spawnregions file contains a reference to each of these spawnpoints files.
Copy all of these files to your /Zomboid/Server directory.
Review and modify the servertest_spawnregions file for your preferred setup.
The line must be uncommented by removing the preceding hyphens "--" 
You can rename the selection as it appears for clients by changing the contents between the apostrophes "" which follow the "name=" 
EX { name = "My Super Cool Server Random Spawn Across the Entire Map", serverfile = "spawnpoints_MP_All_Reduced.lua" },

You do not have to distribute this to your clients, it can remain server-side in your Zomboid/Server directory which contains the .ini and sandboxvars.lua files. 