# Hook

Git kennt Hooks auf mehreren Ebenen:

## Hook auf git-client Ebene

Ebene Entwickler: vor einem commit kann z.B. die Formatierung als hook integriert werden
-> Client Commit / Push-Hooks: lint läuft bei push od. commit


## Hook auf Platform Ebene

Ebene Plattform:
als Pipeline Trigger -> Build
als sync Trigger -> Zeigen: https://github.com/DomainDrivenArchitecture/dda-backup und https://gitlab.com/domaindrivenarchitecture/dda-backup/-/settings/integrations
Sync. Hooks auf Azuer-DevOps: ?
