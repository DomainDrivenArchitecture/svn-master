# Fragen

1. Migration von SVN nach Git: [MigrateFromSvn.md](MigrateFromSvn.md)
   1. Wie werden denn die externals konkret genutzt?
2. Mails versenden: [Hooks.md](Hooks.md)
3. Einbinden von Repositories / Externals: s. Rechte
4. Rechtemanagement: [Authorization.md](Authorization.md)
5. Management v. Secrets für Deployments / DB Migrationen o.ä.: [Secrets.md](Secrets.md)
5. Authentifizierung:
   1. git direkt: per http - Benutzername und Passwort möglich
   2. git direkt: per ssh - private / publick key möglich
   3. auf der Plattform: Benutzername / Passwort und mfa möglich
6. Backup: ein cron mit `git pull` reicht aus.
7. Artifacts: siehe Azure-DevOps Artifacts