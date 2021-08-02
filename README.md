# UnusedMapEdits
Previously used map edits for DayZ

* Biathlon Arena trader
* Dubrovka gas station trader

## Instructions (Not Expansion)
* Inside "dayzOffline.chernarusplus" folder, Create a new folder called "Map_addons".
* Paste "Traders.c" into the newly created Map_Addons folder.
* Open your "Init.c" with Notepad++, or VisualStudio.
* Copy the lines below and paste at the TOP of your Init.c

``` 
#include "$CurrentDir:\\mpmissions\\dayzoffline.chernarusplus\\Map_addons\\Traders.c"
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
    }
```
* Copy the below line and paste right after "DATE RESET AFTER ECONOMY INIT". Example Below
```
Traders();	
//GetCEApi().ExportProxyData( "7500 0 7500", 10000 ); //Unhash on server startup for loot generation
```

```
//DATE RESET AFTER ECONOMY INIT-------------------------
	int year, month, day, hour, minute;
	int reset_month = 9, reset_day = 20;
	GetGame().GetWorld().GetDate(year, month, day, hour, minute);

	if ((month == reset_month) && (day < reset_day))
	{
		GetGame().GetWorld().SetDate(year, reset_month, reset_day, hour, minute);
	}
	else
	{
		if ((month == reset_month + 1) && (day > reset_day))
		{
			GetGame().GetWorld().SetDate(year, reset_month, reset_day, hour, minute);
		}
		else
		{
			if ((month < reset_month) || (month > reset_month + 1))
			{
				GetGame().GetWorld().SetDate(year, reset_month, reset_day, hour, minute);
			}
		}
	}
	
	//CUSTOM BUILDING FILES GO HERE
	Traders();	
	//GetCEApi().ExportProxyData( "7500 0 7500", 10000 ); //Unhash on server startup for loot generation
}
```
* Save and start the server.
