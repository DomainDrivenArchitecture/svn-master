# Git-Svn Bridge
Erlaubt Benutzern ein git repository auch mit einem svn-Client zu nutzen.

## Authentifizierung
Nutzer (die MFA nutzen) müssen zur Authentifizierung einen personal access token anlegen
* Auf Github unter Settings -> Developer Settings -> Personal access tokens -> Generate new token -> repo auswählen -> generate Token
* Token kopieren und speichern
* wenn svn Authentifizierung verlangt username und personal access token verwenden

## Nutzer Setup
* svn-Benutzer machen einen Checkout mit der https URL auf Github
* checkout mit `svn co [URL]`
* update mit `svn up trunk`

## Quellen
* https://docs.github.com/en/github/importing-your-projects-to-github/working-with-subversion-on-github/support-for-subversion-clients
* https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories