# Migration von SVN
## Schritte im Einzelnen

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
Vielleicht bietet sich auch alternativ svn2git als Tool an um die Schritte von `git svn clone ...` bis `for b ...` zu automatisieren
https://github.com/nirvdrum/svn2git
funktioniert sehr ähnlich zu den Schritten oben, aber ein bisschen automatischer
Dann mit Anleitung auf https://docs.gitlab.com/ee/user/project/import/svn.html#cut-over-migration-with-svn2git


## Bekannte Probleme
* https://dalzhim.github.io/2017/05/13/svn-to-git-transition-problems/

## Referenzen

* Azure-Devops: https://docs.microsoft.com/de-de/azure/devops/repos/git/perform-migration-from-svn-to-git?view=azure-devops
* Github / Linux: 
  * https://blog.axosoft.com/migrating-git-svn/
  * https://sysadmin.compxtreme.ro/migrate-from-svn-to-git-step-by-step-tutorial/
  * https://john.albin.net/git/convert-subversion-to-git

