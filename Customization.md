# Introduction #

wifi-positioner has been designed to make it possible to you, to create your own methods based on the data structures that are given to you. For this purpose all necessary methods have been declared virtual, so all you need is an installed Visual C# IDE, like Visual C# 2010 Express Edition which is completly free.

# Insert your algorithm #

First you should create a new project, console or windowed. I think it is easier to take the console based one because you won't have to fight with the GUI, just concentrate on the topic right now.

The next step is to add a reference on the wifi-positioner. You can alternatively add all files from wifi-positioner into your project if it's easier for you. And finally have to create a reference on both DLL files which I included into the binaries package.

## Implement an Interface ##

Now you have to decide what you want to do. There are more possibilites than just insert the code of your desire. You can completly write a new core by creating a new class which implements the interface `Positionable`.
You can find the interface in the namespace `WiFiPositioner.Interfaces` and you will have to implement the following methods:

```
void start();
Position findPosition(WlanClient client);
bool createSectorAtPosition(int sector, int xSector, int ySector, WlanClient client);
Position printFinalResult(List<SectorDifference> list);
SortedDictionary<int, Sector> getAccessPointMap();
SortedDictionary<int, Sector> loadMap(string type, string mapName);
void saveMap(string mapName);
```

### start() method ###

I used it to create a kind of menue with while loops where you can hit enter to start creating a new sector and other things like interruptions for this to get into finding position mode.

### findPosition() method ###

This is where I implemented the calculation and the measurement for the position finding algorithm. All you have to overgive is a WlanClient object which is easy to create, as you can see it in my code. It's nothing special, just a handle on the WiFi system.

### createSectorAtPosition() method ###

I tried to implement the creation of the sectors in this method. All you have to overgive is the sector number, which should count up and the coordinates which you want to have for this specific sector, and actually also the WlanClient object to get access to the WiFi system.

### printFinalResult() method ###

I used to save all data results, in this case the signal strength difference between sectors (SectorDifference), in a specific datastrcture which is added to a list. Why a list? Well you can sort the list automatically by C#'s internal methods and then you can find the smallest difference which will be your resulting position.

### getAccessPointMap() method ###

Your complete map is stored in a SortedDictionary in this case here and this method should just return it because you'll probably need it somewhere else, too.

### loadMap() method ###

Here you can implement the XML or JSON loader.

### saveMap() method ###

Here you can implement the XML or JSON file saver.

You will have to include the following namespace into your class:

```
using NativeWifi;
using Newtonsoft.Json;

using WiFiPositioner.Interfaces;
using WiFiPositioner.Datastructures;
using WiFiPositioner.Utilities;
using WiFiPositioner;
```

And to give you a hint how to start, let's do it like this:

```
namespace MyWiFiPositioner
{
    class MyPositioning : Positionable
    {
        // implement methods here

        // and take a look at Positioning.cs for
        // any datastructures that you might need
        // defined in this class
    }
}
```

I suppose you are clever enough to know how to start the program from now on. You will need the main method and before you can find any positions you have to start creating the map, which can be saved in an XML file.

Note that you will have to implement everything by your own. If you don't want to do this, fill the methods with the code from the Positioning class or follow the steps from the next chapter.


---


## Inherit from Positioning class ##

An easier way of customizing the application to your needs is to inherit from the `Positioning` class and overwrite only the methods which you do not want to change. The rest of the methods can be used as they are used in the basic program.

Inherit like this:

```
class MyPositioning : Positioning
{
   // most basic constructor. would need you to 
   // set all the expected internal data fields
   // as you can see them in the code of Positioning
   public MyPositioning() : base()
   {
        // your own stuff
   }    
}
```

Try to figure out which constructor would fit your needs best.

If you want to overwrite any methods, let's say that you like all methods but you want to have another type of calculation (the core) you can only change that for your needs by the following example:

```
...

public override Position findPosition(WlanClient client)
{
     // your own implementation
}

...
```

Be careful, not all methods could be overwritten. All getters and setters won't be able to be overwritten by your own methods, because it wouldn't make any sense at all.

At least the start() method is empty. There is only a bunch of commented code which I used some day to test the application in console mode. Feel free to use it, or to leave the method as you wish. If you go by creating a new GUI you won't have to use start().