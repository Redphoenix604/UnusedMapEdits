# UnusedMapEdits
Previously used map edits for DayZ

* Biathlon Arena trader
* Dubrovka gas station trader

## Instructions (Not Expansion)
* Inside "dayzOffline.chernarusplus" folder, Create a new folder called "Map_addons".
* Paste "Traders.c" into the newly created Map_Addons folder.
* Open your "Init.c" with Notepad++, or VisualStudio.
* Copy the line below and paste at the TOP of your Init.c

` #include "$CurrentDir:\\mpmissions\\dayzoffline.chernarusplus\\Map_addons\\Traders.c"
  void SpawnObject(string objectName, vector position, vector orientation)
    {
        Object obj;
        obj = Object.Cast(GetGame().CreateObject(objectName, "0 0 0"));
        obj.SetPosition(position);
        obj.SetOrientation(orientation);
        
        // Force update collisions
        if (obj.CanAffectPathgraph())
        {
            obj.SetAffectPathgraph(true, false);
            GetGame().GetCallQueue(CALL_CATEGORY_SYSTEM).CallLater(GetGame().UpdatePathgraphRegionByObject, 100, false, obj);
        }
    }`
    
