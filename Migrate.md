Antworten am 20.5.

Rechte Management

Rechte Management funktioniert in Git nicht auf Dabei-Baum Ebene sonder nur auf der Ebene des gesamten Repositories. 

Git Repositories befinden sich nach einem clone komplett auf dem client, ein feiner granulares RechteMgm macht hier kein Sinn mehr!

Git mit Submodules
Um das Rechtemanagement abzubilden könnte wir auch mehrere verknüpfte Repositories (Git-Submodules) andenken: https://git-scm.com/book/en/v2/Git-Tools-Submodules
-> 3 Repos anlegen, sync mit Github, sync mit AzureDevops
     Eines ist der Master, 2 Sub
     clone von alle / mit Master [inkl. 2 Subs]
     Änderungen in einem Sub-Module und commit
     tag über alle / mit Master [inkl. 2 Subs]

Einschränkung von Push / Trigger v. CI
Rechte auf Azure-DevOps:
  -> entweder jem / Ansgar Schwarzer
Rechte auf GitHub 
  -> zeigen: https://github.com/DomainDrivenArchitecture/dda-backup -> Settings


Migration von SVN

* Azure-Devops
   * https://docs.microsoft.com/de-de/azure/devops/repos/git/perform-migration-from-svn-to-git?view=azure-devops
* Github / Linux
  * Anleitung?
  * Limits ?
    -> evtl ist eine Migration von einem SVN-Repo in ein Git-Repo möglich, müssen wir aber testen. Ich habe schon Probleme bei sehr großen Repositories (> 50GB) erlebt
  * Mix von https://blog.axosoft.com/migrating-git-svn/
      und https://sysadmin.compxtreme.ro/migrate-from-svn-to-git-step-by-step-tutorial/
      oder alternativ https://john.albin.net/git/convert-subversion-to-git (alles bis auf die Autoren, schon bisschen älter 2010)
  * Schritte:
  - Commit Username -> First and Last Name + Email
  
        `svn log -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2">"}' | sort -u > authors-transform.txt`
        
    Dann manuell Namen auf der rechten Seite durch Vorname und Nachname ersetzen und in die Klammern die Email schreiben.
  - Remove SVN metadata
  - Clone in ein Git-Repo
    Diese Schritte werden mit einem Command gemacht (`--stdlayout` flag, falls das SVN repo das [Standardlayout](http://svnbook.red-bean.com/en/1.5/svn.branchmerge.maint.html) benutzt, sonst nicht)
    
    `git svn clone [SVN repo URL] --no-metadata --authors-file=authors-transform.txt --stdlayout your_project`
    
  - Migrate svn:ignore to .gitignore
  
    `git svn show-ignore > .gitignore`
    
  - Convert SVN tags to git tags
  
    `for t in $(git for-each-ref --format='%(refname:short)' refs/remotes/tags); do git tag ${t/tags\//} $t && git branch -D -r $t; done`
    
  - Migrate branches to Git remote
  
    `for b in $(git for-each-ref --format='%(refname:short)' refs/remotes); do git branch $b refs/remotes/$b && git branch -D -r $b; done`
    
  - Set Git Remote
  - Push branches and tags
    `git push origin --all`
    `git push origin --tags`

Vielleicht bietet sich auch alternativ svn2git als Tool an um die Schritte von `git svn clone ...` bis `for b ...` zu automatisieren
https://github.com/nirvdrum/svn2git
funktioniert sehr ähnlich zu den Schritten oben, aber ein bisschen automatischer
Dann mit Anleitung auf https://docs.gitlab.com/ee/user/project/import/svn.html#cut-over-migration-with-svn2git

Interaktion von Tortoise-Clients mit GIT
Vielleicht ist https://tortoisegit.org/ schon gut genug?

Hook

Git kennt Hooks auf mehreren Ebenen:
-> Client Commit / Push-Hooks: lint läuft bei push od. commit

Ebene Entwickler: vor einem commit kann z.B. die Formatierung als hook integriert werden
Ebene Plattform:
als Pipeline Trigger -> Build
als sync Trigger -> Zeigen: https://github.com/DomainDrivenArchitecture/dda-backup und https://gitlab.com/domaindrivenarchitecture/dda-backup/-/settings/integrations
Sync. Hooks auf Azuer-DevOps: ?

Secrets

Organisations-Secrets in Pipelines: https://github.com/DomainDrivenArchitecture/dda-devops-build -> Settings und Actions
Secrets auf Azure-DevOps: ? / Evtl. Key-Vault Integration?

