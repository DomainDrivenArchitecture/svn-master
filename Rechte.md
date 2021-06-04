# Rechte Management

Rechte Management funktioniert in Git nicht auf Dabei-Baum Ebene sonder nur auf der Ebene des gesamten Repositories. 

Git Repositories befinden sich nach einem clone komplett auf dem Entwickler-Rechner, ein feiner granulares RechteMgm macht hier kein Sinn mehr!

## Mögliche Lösung: Git mit Submodules

Um das Rechtemanagement abzubilden könnte wir auch mehrere verknüpfte Repositories (Git-Submodules) andenken: https://git-scm.com/book/en/v2/Git-Tools-Submodules

In unserem Bsp. sind das
* https://github.com/DomainDrivenArchitecture/svn-master
* https://github.com/DomainDrivenArchitecture/svn-sub1
* https://github.com/DomainDrivenArchitecture/svn-sub2

### UseCase1: Alle Repos clonen

### UseCase2: Ein Mitarbeiter A hat nur ein Submodul im Zugriff ändert etwas und Admin B hat alles im Zugriff und aktualisert Master so, dass ein clone "latest" möglich ist.

### UseCase3: Tag über alle Module im neuesten Stand


## Möglichkeit: Rechte auf SVN-Plattform-Ebene
* Einschränkung von Push / Trigger v. CI
* Rechte auf Azure-DevOps:
  -> entweder jem / Ansgar Schwarzer
* Rechte auf GitHub 
  -> zeigen: https://github.com/DomainDrivenArchitecture/dda-backup -> Settings
