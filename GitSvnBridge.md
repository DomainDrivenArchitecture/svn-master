## Projekt erstellen
* Neues Projekt mit erstellen, dabei Import auswählen
* svn repo importieren 

## Nutzer Setup
* git-Benutzer clonen das Projekt über https oder ssh und können dann normal arbeiten
* update mit `git fetch`

* svn-Benutzer machen einen Checkout mit der https URL auf Github
* unter Settings -> Developer Settings -> Personal access tokens -> Generate new token -> repo auswählen -> generate Token
* Token kopieren und speichern
* wenn bei commits nach dem Passwort gefragt wird access token verwenden
* update mit `svn up trunk`

## Quellen
* https://docs.github.com/en/github/importing-your-projects-to-github/working-with-subversion-on-github/support-for-subversion-clients
* https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories