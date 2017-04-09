# Getting Started

## Repository
Beim Anlegen eines neuen Repositories wird ein Verzeichnis `.git` erzeugt. Alle Verzeichnisse und Dateien, die im gleichen Verzeichnis oder 
tiefer liegen, können dem Git-Repository hizugefügt werden. Im `.git`-Verzeichnis werden alle erforderlichen Dateien abgelegt. Dazu gehört 
auch, welche Unterverzeichnisse und welche Dateien unter Versionskontrolle stehen sollen. Anders als bei Versionsverwaltungssystemen wie 
Subveron müssen damit keine weiteren `.svn`-Dateien in Unterverzeichnissen angelegt werden.

## Mögliche Zustände eines Verzeichnisses/einer Datei in Git [1]:
* ![untracked](untracked.png) untracked: 
Alle Verzeichnisse und Dateien, die ausgehend vom `.git`-Verzeichnis im gleichen Verzeichnis oder tiefer liegen, sind bekannt 
aber noch nicht erfasst (not recorded). Sie stehen also noch nicht unter Versionskontrolle. Sie müssen dem Repository einmalig hinzugefügt 
werden ("Add" und anschließend "Commit", in Eclipse: "Team" -> "Add" und "Team" -> "Commit").
* ![added](added.png) added: 
Alle Verzeichnisse/Dateien, die in Git bekannt sind, aber noch nicht committed wurden. Sie sind also (immer) noch nicht gesichert, 
sondern lediglich dem Index (mehr Infos dazu siehe unten) hinzugefügt. Um sie endgültig unter Versionskontrolle zu bringen, ist ein Commit 
erforderlich (In Eclipse: "Team" -> "Commit")
* ![tracked](tracked.png) tracked: 
Alle Verzeichnisse/Dateien, die bekannt und zum Repository hinzugefügt wurden (recorded).
* ![dirty](dirty.png) dirty: 
Jede getrackte Datei mit Änderungen, aber noch nicht dem Index hinzugefügt wurde. Die Änderungen sind also ungesichert. Um dies 
zu ändern, müssen sie gestaged werden. (In Eclipse: "Team" -> "Add to Index")
* ![staged](staged.png) staged: 
Jede getrackte Datei mit Änderungen, die bereits zum Index hinzugefügt wurden.
* ![partially-staged](partiallyStaged.png) partially-staged: 
Jede getrackte Datei mit Änderungen, die bereits teilweise zum Index hinzugefügt wurden. Üblicherweise entsteht dies, 
wenn eine Datei verändert, anschließend zum Index hinzugefügt und danach noch einmal verändert wird. Es ist also wieder ein "Add to Index" 
erforderlich.
* ![conflicted](conflicted.png) conflicted: 
Alle Dateien, deren Änderungen nach einem Merge in Konflikt mit anderen Änderungen stehen. Diese Konflikte müssen von Hand 
aufgelöst werden (in Eclipse: "Team" -> "Merge Tool"), weil Git nicht ermitteln kann welche der Versionen die korrekte ist. Über die 
History (Eclipse: "Team" -> "Show in History") kann ermittelt werden, von wem die anderen Änderungen stammen um ggf. Rücksprache zu halten. 
Nach Auflösen des Konflikts kann die Datei dem Index hinzugefügt werden. Damit wird sie nicht mehr als "conflicted" markiert sondern als 
"staged". Ein Commit fügt die gemergte Datei dem Repository hinzu.
* ![removed](removed.png) removed:
Verzeichnisse/Dateien, die aus dem Repository entfernt werden sollen. Hierfür gibt es zwei Möglichkeiten: 1. In Eclipse: "Team" -> "Untrack" 2. Löschen der aus dem Eclipse-Workspace (einfach Datei über Tastatur oder Kontextmenü entfernen). Hier erscheint das Icon jedoch nicht da die Datei nicht mehr im Workspace existiert. Beim nächsten Commit wird die jeweilige Datei aber dennoch gelöscht. Dies ist auch in der Staging-Area in der Eclipse-Staging-View einzusehen.
Any file that should be removed from the repository. For this icon to appear Team => Untrack has to be performed. By deleting the file from the workspace, the file will disappear (and therefore no icon will appear). However, it will still be removed from the repository with the next commit.
* ![ignored](ignored.png) ignored: 
Manche Verzeichnisse/Dateien sollen nicht zum Repository hinzugefügt werden (Beispiel: `bin`-Verzeichnis von Eclipse). Diese 
Dateien können von der Versionskontrolle ausgeschlossen werden. Sie werden dazu in einer separaten Datei `.gitignore` gelistet und von Git 
als nicht existent behandelt. (In Eclipse: "Team" -> "Ignore")

## Index [1, 2]
Der Index, auch Staging Area genannt, ist eine Art Dateiverwaltung. Sie enthält Dateien, die verändert und später entweder ins lokale oder 
direkt ins lokale **und** remote Repository eingecheckt werden sollen. Der Index kann somit als Sammlung von zusammengehörigen 
Veränderungen an Dateien dienen, die als ein Commit eingecheckt werden sollen. 
Mit dem Hinzufügen einer Datei zum Index ändert sich ihr Status von „Verändert“ zu „Staged“. Eine gestagte Datei kann wieder verändert 
werden. Die veränderte Datei kann mit der gestagten Datei verglichen werden, ohne dass ein Commit nötig wäre. Die veränderte Datei kann 
wieder auf den Stand der gestagten Datei zurückgesetzt werden. Ebenso kann der Index zurückgesetzt werden.

## File-Menü-Übersicht in Eclipse [3]
* Add to Index:
Hinzufügen von Dateien zum Git Index.
„Team“ –> „Add to Index“
* Commit:
Erzeugen eines neuen Commits.
„Team“ -> „Commit...“
* Ignore:
Ausschließen einer Datei von der Versionskontrolle durch Hinzufügen zur .gitignore-Datei.
„Team“ -> „Ignore“
* Pull:
Änderungen vom remote Repository ins lokale Repository auschecken. Entspricht der Kombination aus „Fetch“ und „Merge“ mit teilweise etwas zusätzlicher „Magie“. Das Ausführend eines Fetch-Commands und eines anschließendes Merge-Commands ist leichter nachvollziehbar.
„Team“ -> „Pull“
* Fetch:
Update der Branches im remote Repository.
„Team“ –> „Fetch from Upstream“
* Switch:
Erzeugen eines neuen Branchs oder wechseln zu einem anderen, bereits existierenden Branch
„Team“ -> „Switch To“
* Push:
Übertragen der Änderungen/Commits aus dem lokalen Repository ins remote Repository.
„Team“ -> „Push to Upstream“
* Merge:
Mergen zweier Branches, um Dateiänderungen aus einem Branch in einen anderen Branch zu übertragen.
„Team“ -> „Merge...“
Zusammenführen von unterschiedlichen Versionen einer Datei, die in Konflikt zueinander stehen.
„Team“ -> „Merge Tool“

## Use Case: Bearbeiten eines neuen Defects/Requirements
![Branching Model [4]](gitflow.gif)
Branching Model [4]

1.	Wechsle in den Development-Branch über „Team“ -> „Switch“ -> „Development“
2.	Lege (ausgehend vom Development-Branch) einen neuen Feature-Branch an: „Team“ -> „Switch to“ -> „New Branch“ -> Benenne den neuen Branch nach dem Defect/Requirement.
3.	Implementierung
4.	„Team“ -> „Add to index“
5.	„Team“ -> „Commit“
6.	„Team“ -> „Push to Upstream“
Spätestens bevor der Feature-Branch wieder in den Development-Branch gemerged wird:
7.	Auschecken des neuesten Standes aus dem Development-Branch in den eigenen Feature-Branch: „Team“ -> „Fetch“ 
8.	Mergen der Änderungen mit eigenen: „Team“-> „Merge“
Es kann nun evtl. zu Merge-Konflikten kommen. Falls keine Merge-Knflikte auftreten, weiter mit 10. Ansonsten:
9.	„Team“ -> „Merge Tool“ starten und von Hand mergen (wie in SAVI).
10.	Testen
11.	Fall es Änderungen in durch das Auflösen von Merge-Konflikten gegeben hat, die betroffenen Dateien zum Index hinzufügen: „Team“ -> „Add to Index“. Ansonsten direkt weiter mit 12. 
12.	Team“ -> „Commit“
13.	„Team“ -> „Push to Upstream“
14.	Wechsle in den Development-Branch, um den Feature-Branch dort hinein zu mergen: „Team“ -> „Switch to“ -> „Development“
15.	„Team“ -> „Merge“.

**ACHTUNG: Besonderheit Hotfixes**
Falls es sich bei dem Defect um einen Hotfix handelt, muss der Branch in 2. vom master-Branch aus durchgeführt werden. In 6. und 7. wird mit dem master-Branch anstatt mit dem Development-Branch gearbeitet. Am Ende (14.) muss der Defect sowohl in den master-Branch, als auch in den Feature-Branch gemerged werden.

## Use Case: Mergen zweier Branches [3]
*	Checken den Branch A aus, in den ein anderer Branch B gemergt werden soll. Dazu: „Team“ -> „Switch Branch“
*	Starte den Merge-Dialog mit „Team“ -> „Merge...“
*	Wähle den Branch B aus, dessen Änderungen in den aktuellen Branch A gemerged werden sollen.
*	Selektiere in den Merge options „Commit“.
*	Selektiere in den Fast forward options „If a fast-forward, create a merge commit“.
*	Klicke auf „Merge“.



## Quellen:
   [1] Maximilian Koegel und Jonas Helming: EGit Tutorial. http://eclipsesource.com/blogs/tutorials/egit-tutorial/. Feb 19th, 2015. 
[Stand: 03.04.2017]   
   [2] Scott Chacon and Ben Straub: Pro Git. Apress 2014, 2nd Edition.   
   [3] Lars Vogel: Git version control with Eclipse (EGit) - Tutorial. http://www.vogella.com/tutorials/EclipseGit/article.html. 06.07.2016. 
[Stand: 03.04.2017]   
   [4] Vincent Driessen: Branching Model. http://nvie.com/posts/a-successful-git-branching-model/. January 05, 2010 [Stand: 03.04.2017]   
