# Schutz vor Malware, Phishing, Werbung und Tracking.

Diese Listen sperren bekannte schädliche und unerwünschte Domains in deinem Netz. Es gibt drei Fassungen, weil Pi-hole die volle Menge tragen kann und Technitium und AdGuard nicht.

Kenny2k8 holt die Domains aus öffentlichen Quellen, sortiert sie nach Thema und streicht Doppelungen. Jede Domain steht nur in einer Datei. Wächst ein Thema über eine Million Einträge, teilt er es in nummerierte Dateien.

> [!NOTE]
> Die Adressen zum Kopieren stehen in [blocklisten.md](blocklisten.md).
> Woher die Domains kommen, steht in [Quellen.md](Quellen.md).

## Was du hier findest

| Ordner | Für wen | Umfang |
| --- | --- | --- |
| [listen/pihole/](listen/pihole) | Pi-hole | Alle Themen, etwa 45 Millionen Domains |
| [listen/technitium/](listen/technitium) | Technitium | Nur Themen mit höchstens einer Million Domains |
| [listen/adguard/](listen/adguard) | AdGuard Home | Dieselben Domains wie Technitium, als Adblock-Regeln |

In der kleinen Fassung liegen Malware, Werbung, Fakeshops, Standard, Dienste und Overblock, zusammen etwa 1,55 Millionen Namen. Phishing, Jugendschutz, Tracking und Diverse bleiben bei Pi-hole. Die vier Themen sind zusammen etwa 44 Millionen Einträge.

Technitium hält jeden Namen im Arbeitsspeicher. Der Hersteller rechnet mit etwa 300 MB je Million Namen, und beim Aktualisieren liegt die neue Liste zusätzlich im Speicher, also grob das Doppelte. 1,55 Millionen Namen sind damit etwa 450 MB, beim Aktualisieren etwa 1 GB. Die 45 Millionen der Pi-hole-Fassung brauchen weit mehr als 8 GB. Der Server sitzt dann stundenlang am Speicherlimit.

## Pi-hole

1. Öffne die Weboberfläche deines Pi-hole.
2. Gehe zu **Group Management → Adlists**.
3. Öffne in [blocklisten.md](blocklisten.md) den Abschnitt **Pi-hole** und kopiere die Adressen.
4. Füge jede Adresse als eigene Adlist ein und speichere.
5. Lade die Listen neu: **Tools → Update Gravity**, oder auf dem Pi der Befehl `pihole -g`.

Eine Zeile sieht so aus: `0.0.0.0 example.com`. Zeilen mit `#` am Anfang sind Hinweise. Pi-hole übergeht sie und sperrt nur genau den eingetragenen Namen.

> [!TIP]
> Du musst nicht jedes Thema nehmen. Phishing allein sind über 30 Millionen Namen. Werbung oder Malware sind eine kleinere Wahl.

## Technitium

1. Öffne die Weboberfläche deines Technitium DNS Servers.
2. Gehe zu **Settings → Blocking**.
3. Trage unter **Block List URLs** die Adressen aus dem Abschnitt **Technitium** in [blocklisten.md](blocklisten.md) ein, eine pro Zeile.
4. Speichere. Technitium lädt die Listen beim nächsten Abruf.

Technitium nimmt höchstens 255 Listen-Adressen. Die kleine Fassung bleibt darunter. Technitium sperrt einen Namen und alles darunter. Steht `example.com` in der Liste, fallen dort auch `www.example.com` und `shop.example.com` weg. Solche längeren Namen stehen in der Technitium-Fassung nicht noch einmal.

> [!WARNING]
> Trag in Technitium nur die Adressen aus dem Abschnitt **Technitium** ein. Die Adressen aus **Pi-hole** laden die 45 Millionen Namen. Dafür reichen 8 GB nicht. Alte Adressen unter `listen/pihole/` in den Block List URLs löschen, speichern, und die schon heruntergeladenen Dateien im Ordner `blocklists` der Technitium-Konfiguration entfernen. Sonst lädt der nächste Abruf die große Fassung wieder.

## AdGuard Home

1. Öffne die Weboberfläche von AdGuard Home.
2. Gehe zu **Filters → DNS blocklists**.
3. Füge die Adressen aus dem Abschnitt **AdGuard** in [blocklisten.md](blocklisten.md) ein.
4. Speichere und lade die Filter neu.

Eine Regel sieht so aus: `||example.com^`. AdGuard sperrt den Namen und alles darunter. Die Domains sind dieselben wie in der Technitium-Fassung. Die Adressen aus **Pi-hole** gehören auch hier nicht hinein.

## Themen

| Thema | Was dort landet | Fassung |
| --- | --- | --- |
| Malware | Schadsoftware, Stalkerware, Cryptojacking | Pi-hole, Technitium, AdGuard |
| Phishing | Phishing und nachgebaute Bank-Domains | nur Pi-hole |
| Fakeshops | Falsche Shops und unseriöse Angebote | Pi-hole, Technitium, AdGuard |
| Jugendschutz | Pornografie, Glücksspiel, Dating, Proxies | nur Pi-hole |
| Tracking | Tracker und Telemetrie | nur Pi-hole |
| Werbung | Werbenetze und Adserver | Pi-hole, Technitium, AdGuard |
| Dienste | Einzelne Anbieter, etwa Amazon, Google, Samsung | Pi-hole, Technitium, AdGuard |
| Diverse | Quellen, die in kein einzelnes Thema fallen | nur Pi-hole |
| Standard | Die zusammengefasste Liste von StevenBlack | Pi-hole, Technitium, AdGuard |
| Overblock | Wenige sehr breite Domains | Pi-hole, Technitium, AdGuard |

## Overblock

> [!WARNING]
> `overblock.txt` sperrt wenige sehr breite Namen, darunter `baidu.com` und `buff.ly`. Auf Technitium und AdGuard fällt damit der ganze Dienst aus, nicht nur eine einzelne Seite. Lass diese eine Adresse weg, wenn du das nicht willst.

## Nutzung

Diese Zusammenstellung steht unter [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/). Du darfst sie privat nutzen, kopieren und weitergeben, auch in Pi-hole, Technitium, AdGuard Home und anderen DNS-Sperren. Kommerzielle Nutzung ist nicht erlaubt. Als Namensnennung gilt der Verweis auf dieses Repository und auf [Quellen.md](Quellen.md).

Die Domains stammen aus den Quellen in [Quellen.md](Quellen.md). Deren eigene Lizenz bleibt an den Ursprungsdaten. Der Lizenztext liegt in [LICENSE](LICENSE).

## Wenn sich die Listen ändern

Kenny2k8 ergänzt neue Domains und legt sie in denselben Ordner. Die Adressen bleiben gleich, solange der Dateiname gleich bleibt. Neu einfügen musst du nur, wenn eine Datei hinzukommt oder wegfällt. Das steht dann in [blocklisten.md](blocklisten.md).

> [!IMPORTANT]
> Dieses Repository gehört nicht zu Pi-hole, Technitium oder AdGuard. Die Dateien hier sind Listen, die du dort importierst.
