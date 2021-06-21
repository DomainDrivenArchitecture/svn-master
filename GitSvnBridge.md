## Subgit

https://subgit.com/

Ermöglicht das Konvertieren von svn zu git oder zu einer 2-way bridge zwischen beiden.
* Ist ein kommerzielles Projekt und kostet dementsprechend.
* Es gibt die Möglichkeit für eine kostenlose Lizenz für 1 Open-Source Projekt für 1 Jahr die immer wieder erneuert werden kann.
* Die einmalige Umwandlung von SVN zu Git kostet nichts, aber Bridge ohne Lizenz nicht möglich.

## git-svn-bridge

https://github.com/mrts/git-svn-bridge

Verbindet SVN mit git und ermöglicht gleichzeitiges arbeiten mit beidem.
* Commits in das Git-Repository werden über Cron-Job automatisch mit SVN synchronisiert.
* Blockiert Commits aus git, falls in SVN verändert
* hat Tools zur Authentifizierung in SVN beim Push in git
* nutzt außerdem Hooks zur Synchronisation
* gute Doku

Schritte:
* Bridge User erstellen
* Initialisiere und Starte svnserve
* Erstelle ein Git-Repo für die Entwicklung und eins für die Bridge
* Erstelle einen Git-Hook der Commits blockiert und einen der synchronisiert
* Initialisiere den Auth-Manager
* Teste Synchronisierung