# Migration von SVN
## Manuelle Migration (git-svn)

Vorteile:
* "aktueller", weil von git selbst
Nachteile:
* funktioniert schlechter bei nicht-standard Layout SVN Repositories
* SEHR langsam bei großer Migration (ca. 4 Tage bei 15.000 Revisions)

1. Commit Username -> First and Last Name + Email
   `svn log -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2">"}' | sort -u > authors-transform.txt`
   Dann manuell Namen auf der rechten Seite durch Vorname und Nachname ersetzen und in die Klammern die Email schreiben.
2. Remove SVN metadata
3. Clone in ein Git-Repo
  Diese Schritte werden mit einem Command gemacht (`--stdlayout` flag, falls das SVN repo das Standardlayout? benutzt, sonst nicht)
   `git svn clone [SVN repo URL] --no-metadata --authors-file=authors-transform.txt --stdlayout your_project`
4. Migrate svn:ignore to .gitignore
   `git svn show-ignore > .gitignore`
5. Convert SVN tags to git tags
   `for t in $(git for-each-ref --format='%(refname:short)' refs/remotes/tags); do git tag ${t/tags\//} $t && git branch -D -r $t; done`
6. Migrate branches to Git remote
   `for b in $(git for-each-ref --format='%(refname:short)' refs/remotes); do git branch $b refs/remotes/$b && git branch -D -r $b; done`
7. Set Git Remote
8. Push branches and tags
    `git push origin --all`
    `git push origin --tags`

### Automatisierte Alternativen

Vielleicht bietet sich auch alternativ svn2git als Tool an
https://github.com/svn-all-fast-export/svn2git

Dann mit Anleitung von https://techbase.kde.org/Projects/MoveToGit/UsingSvn2Git
und Tipps von https://smartbear.com/blog/migrating-from-subversion-to-git-lessons-learned/

Vorteile:
* deutlich schneller als git-svn
* kommt mit nicht-standard konfigurationen klar
Nachteile:
* nicht von git, evlt. Probleme mit aktuellen git Versionen
* man muss eigene, auf das Repository angepasste Regel Dateien schreiben (vlt. auch Vorteil?)
* relativ viel Doku zum einlesen


## Bekannte Probleme

* Tool von Git zur Migration ist sehr langsam bei großen Repositories: ca. 4 Tage bei 15.000 Revisions
* Größe des Repository: Git braucht viel Speicher, wenn es große Dateien gibt, die sich oft verändern und wird größer, je mehr Nutzer es gibt. Es gibt aber tools, die dieses Problem lösen (git-lfs)  
* Merge History ist nicht richtig, wenn sich der Trunk verschiebt: Lösung siehe https://stackoverflow.com/questions/12938189/how-do-i-keep-svn-history-in-git-when-trunk-has-moved

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

## Referenzen

* git-svn: https://git-scm.com/docs/git-svn
* Azure-Devops: 
  * https://docs.microsoft.com/de-de/azure/devops/repos/git/perform-migration-from-svn-to-git?view=azure-devops
* Github / Linux: 
  * https://blog.axosoft.com/migrating-git-svn/
  * https://sysadmin.compxtreme.ro/migrate-from-svn-to-git-step-by-step-tutorial/
  * https://john.albin.net/git/convert-subversion-to-git
  * https://git-scm.com/book/de/v2/Git-Tools-Submodule
* Migrationsprobleme
  * https://smartbear.com/blog/migrating-from-subversion-to-git-lessons-learned/
  * https://dalzhim.github.io/2017/05/13/svn-to-git-transition-problems/
