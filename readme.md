# Robocode "Catslayer" von Matteo Jakob

## Aufgabenstellung
Aus persönlichem Intresse, aber auch als Auftrag, habe ich ein Roboter auf "Robocode" programmieren. Diesen Roboter wurde in Einzelarbeit programmiert. Bei diesem Portfolio gehe ich mehr in Richtung wie alles Funktioniert und wie ich meinen ersten Roboter programmiert habe.
- Der Leser erfährt, was "Robocode" ist
- Der Leser lernt, wie man ein Roboter kann programmieren
- Der Leser lernt, was die Strategie meines Roboters ist

## Inhalt 🧠
### Robocode und ein Roboter
Robocode ist ein Programm, wo sich Roboter auf einem Spielfeld bekämpfen können. Roboter kann man selber in java programmieren, jedoch gibt es auch weitere Roboter im Netz, welche man brauchen kann.
Das Ziel im Spiel ist es, die meisten Punkten in einem Spiel zu holen, man bekommt Punkte indem man anderen Robotern schaden macht, als längster überlebt und weitere kleinere Faktoren.

Ich habe meinen Bot (CatSlayer69) mit Java im Source-Editor programmiert. Man öffnet den Editor indem man das Spiel startet, auf "Robot" geht und "Source Editor" auswählt.
Nun kann man einen Roboter öffnen oder kreieren, es gibt API's vom Hersteller zur Hilfestellung der Programmierung.

Nach vielen Versionen, habe ich die Strategie meines Roboters "Sway" gennant. Das Ziel ist es, immer nach vorne und nach hinten zu bewegen, sodass man immer in Bewegung ist und alle Schüsse so gut wie möglich ausweicht. Man kann auch dank dieser Bewegung sehr zielsicher sein, da wenn man einmal anvisiert ist, nicht gross die Waffe drehen muss. Mein Roboter macht zwischendurch auch Scans mit ``turnGunRight(360);`` und wenn er einen Gegner gescannt hat, zielt er mit seiner Waffe auf diese Richtung und schiesst. Als Zusatz habe ich auch eine Funktion gemacht, welche schaut, ob der Roboter in der Nähe eine Ecke ist oder in der Nähe eines Randes und sich dann davon wegbewegt.

### Code
```java
package JakobMatteo;
import robocode.*;

// 	https://robocode.sourceforge.io/docs/robocode/robocode/JuniorRobot.html



// CatSlayer69 - a robot by Matteo Jakob



public class CatSlayer69 extends JuniorRobot
{
	public int firingMode = 0;

	public void run() {
		// Parts: Body, gun, radar, bullet, scan_arc
		setColors(black, black, white, red, red);
		
		int x = fieldWidth;
		int y = fieldHeight;

		while(true) {
			if (firingMode == 0){
				ahead(100);
				turnGunRight(360); }
				else if (firingMode ==1){
					ahead(120);
					back(110);
					turnGunRight(360); }
					

		// Gets Pos and reacts correspondingly
		if (isNearWall() == true){
			out.println("Ich bin in der Nähe einer Wand *w*");
			
			if (robotX < 100 && robotY < 100){ // if bottom left
				turnTo(45);
				ahead(200);
				out.println("unten links ich bin *w*");
				}else if (robotX > x-100 && robotY > y-100){ // if top right
					turnTo(-135);
					ahead(200);
					out.println("oben rechts ich bin *w*");
					}else if (robotX < 100 && robotY > y-100){ // if top left
					turnTo(135);
					ahead(200);
					out.println("oben links ich bin *w*");
						}else if (robotX > x-100 && robotY < 100){ // if bottom right
						turnTo(-45);
						ahead(200);
						out.println("unten rechts ich bin *w*");
						
						}	// if not in a corner
							else if(robotX < 100){
							turnTo(85);
							ahead(200);
								}else if(robotX > x-100){
									turnTo(-85);
									ahead(200);
									}else if(robotY < 100){
										turnTo(-5);
										ahead(200);
										}else if (robotY>y-100){
											turnTo(200);
											ahead(200);
										}
			}
		}
	}
	
	public void onScannedRobot() {
		firingMode = 1;
		turnGunTo(scannedAngle);
		smartFire(scannedDistance, scannedAngle);
	}
	
	public void onHitRobot(){
		if(scannedBearing < 90 && scannedBearing > -90){
			ahead(100);
		}else{
			back(100);
		}
		
	}
	public void onHitByBullet() {
		firingMode = 1;
	}
	
	public boolean isNearWall() {
	int x = fieldWidth;
	int y = fieldHeight;
	int chooseDistance = 150;
		if (robotX < chooseDistance && robotY < chooseDistance ||
				robotX > x-chooseDistance && robotY > y-chooseDistance|| 
					robotX < chooseDistance && robotY > y-chooseDistance || 
						robotX > x-chooseDistance && robotY < chooseDistance ||
						
							robotX < chooseDistance ||
								robotX < x-chooseDistance||
									robotY < chooseDistance||
										robotY < y-chooseDistance	){
							return true;
								}
						else{
							return false;
								}
	}
	
	public void smartFire(int distance, int angle) {
		if (gunReady) {
			if(distance > 500 ||energy < 10){
				turnTo(angle);
				ahead(50);
				turnRight(45);
				ahead(50);
				turnLeft(45);
				ahead(50);				
			}	
				else if (distance > 200 || energy < 15) {
					fire(1);
					} else if (distance > 150) {
						fire(2);
						} else {
							fire(3);
			}
		}
		
	}	
}

```

### Gif vom Spiel
Der Roboter mit rotem Laser ist meiner.
![](https://media1.giphy.com/media/kJnUZH9p5oc7OCcMSt/giphy.gif)

## Reflexion ✨
Ich fand es gut, dass ich nicht zu viele Probleme hatte mit anderen Programmiersprachen. Zuvor hatte ich mehr Angst, andere Sprachen asuzuprobieren.
Im Robot-Editor habe ich auch die Farben des Hintergrunds gewechselt, da es meinen Augen viel besser ging, nach stundenlangem Schauen.
Ich fand nicht so gut dass ich mir nicht eine konkrete Idee am Anfang erstellt habe, da ich somit viel mehr Zeit brauchte, eine Idee auf dem Weg zu entwickeln. Da ich nicht eine konkrete Idee hatte, hatte ich auch Probleme mit dem Programmieren, weil sich die einzelnen Funktionen zuerst immer gegeneinander gewirkt haben und somit mein Roboter sich zum Teil nicht mehr bewegen oder schiessen konnte.
Als Verbesserung könnte man, bevor man anfängt zu programmieren, ein kleines Word-Dokument auf Word oder eine Mindmap auf XMind zu machen und die Ideen zusammenzuführen, analysieren und ausführen. Im Falle einer Mindmap, kann man auf XMind


Beim letztem Portfolio war der Verbersserungsvorschlag, dass ich

## Verifikation ✅
Man lernt was Robocode ist im Inhalt und dann Text ganz oben. 
Man findet heraus, wie man einen Roboter programmiert im Inhalt, Tetxt und dann der Teil in der Mitte, jecoch kann man auch den Code anschauen. Um die Strategie herauszufinden, kann man zum Inhalt nochmal gehen, Text und dann der untere Teil.
