ThreeSearch library program for Colobot Gold Edition. This library program is shared across all missions on the 9 planets, from Earth to Terranova.

Usage:

1. Copy and paste following files from https://github.com/Three-Search/Colobot-Program to the Colobot\data\ai folder
SatCom.cbot
Grabber.cbot
Shooter.cbot
Builder.cbot

2. Load  the SatCom.cbot library program for each mission by editing the scene.txt file in the Colobot\data\levels\missions\chapterXXX\levelXXX folder and add script1="SatCom.cbot" to object Me under BeginObject section.

For example, the scene.txt file for chapter003\level003 with title "On the Offensive" will look like the example below after adding script1="SatCom.cbot" to object Me under BeginObject section:

BeginObject
CreateObject pos= 0.00; 0.00 dir=0.0 type=SpaceShip run=1
CreateObject pos= 0.00;-3.25 dir=1.5 type=Me script1="SatCom.cbot"

3. In the bot Program Editor, declare an instance of the SatCom class, and you can call any function in the SatCom.cbot library program,. For example:
extern void object::Tropica3()
{
	SatCom com();
	
	Message("Please start a program of Winged Grabber bot to call Mission() function of this bot");
	waitForAvailable(RepairCenter);
	
	Build(ResearchCenter);
	Build(BotFactory);
	Build(WingedShooter,"Mission()");
	
	go(SpaceShip);
	missionComplete();
	camerafocus(radar(WingedGrabber));
}

public void object::Mission()
{
	checkEnergyCell();
	
	if (category == WingedGrabber)
	{
		GrabMission();
	}
	else
	{
		ShootMission();
	}
}
