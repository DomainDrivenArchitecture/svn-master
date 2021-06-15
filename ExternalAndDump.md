# Externals & Dumps

## SVN Dumps

Dumps sind Sicherungskopien des Repositories mit allen Revisionen.
Hooks werden dabei nicht mitgesichert.

Kann man auch verwenden um zu Git zu migrieren, bietet aber wenn der Server noch online ist keine Vorteile

`svnadmin dump /PfadZumRepository > svnexport.dump`

`git svn clone file:///path/to/svn/repo /path/to/empty/dir`

Vorteile:
* möglich wenn der SVN-Server nicht mehr online ist
Nachteile:
* funktioniert nur mit git-svn (andere Tools meistens nur für Server)
* gleiche Probleme wie die anderen Methoden (größe des Repos, Standardkonfiguration hilfreich, Benutzer manuell, ...)

## SVN Externals

Sind ähnlich zu Submodulen in Git oder Symlinks zu anderen Ordnern im Projekt

Ähnlichkeiten zu Submodulen:
* kann damit einen Ordner aus einem Repo in das eigene Repo einbinden.
* wenn sich der eingebundene Inhalt ändert und man Updatet erhält man den neuen Inhalt.

Nicht wie Submodule:
* Änderungen die im eingebundenen Ordner gemacht werden können mit dem normalen Projekt commited werden. 

https://tortoisesvn.net/docs/release/TortoiseSVN_en/tsvn-howto-common-projects.html#tsvn-howto-common-externals
