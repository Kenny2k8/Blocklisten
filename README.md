# Schutz vor Malware, Phishing, Werbung und Tracking.

Diese Listen sperren bekannte schädliche und unerwünschte Domains in deinem Netz. Pi-hole und Technitium laden sie als Hosts-Dateien und beantworten die Namen lokal.

Kenny2k8 holt die Domains aus öffentlichen Quellen, sortiert sie nach Thema und streicht Doppelungen. Jede Domain steht nur in einer Datei. Wächst ein Thema über eine Million Einträge, teilt er es in nummerierte Dateien.

> [!NOTE]
> Die Adressen zum Kopieren stehen in [blocklisten.md](blocklisten.md).
> Woher die Domains kommen, steht in [Quellen.md](Quellen.md).

## Was du hier findest

| Datei | Inhalt |
| --- | --- |
| [blocklisten.md](blocklisten.md) | Alle Listen-Adressen, gesamt und nach Thema |
| [listen/](listen) | Die Hosts-Dateien selbst |
| [Quellen.md](Quellen.md) | Die Herkunft, jedes Repository nur einmal |

Eine Zeile in den Hosts-Dateien sieht so aus: `0.0.0.0 example.com`. Zeilen mit `#` am Anfang sind Hinweise. Pi-hole und Technitium übergehen sie.

## Pi-hole: Listen importieren

1. Öffne die Weboberfläche deines Pi-hole.
2. Gehe zu **Group Management → Adlists**.
3. Öffne [blocklisten.md](blocklisten.md) und kopiere die Adressen.
4. Füge jede Adresse als eigene Adlist ein und speichere.
5. Lade die Listen neu: **Tools → Update Gravity**, oder auf dem Pi der Befehl `pihole -g`.

> [!TIP]
> Du musst nicht jedes Thema nehmen. In [blocklisten.md](blocklisten.md) liegen die Adressen nach Thema getrennt. Werbung allein ist eine andere Wahl als Malware und Phishing zusammen.

Pi-hole speichert die Adresse. Beim nächsten Gravity-Lauf lädt es die aktuelle Datei von GitHub. Die Adresse in Pi-hole bleibt gleich, solange der Dateiname gleich bleibt.

## Technitium: Listen importieren

1. Öffne die Weboberfläche deines Technitium DNS Servers.
2. Gehe zu **Settings → Blocking**.
3. Trage unter **Block List URLs** dieselben Adressen ein, eine pro Zeile.
4. Speichere. Technitium lädt die Listen beim nächsten Abruf.

Technitium nimmt höchstens 255 Listen-Adressen. In [blocklisten.md](blocklisten.md) stehen 52. Jede Adresse darf 255 Zeichen lang sein. Die Adressen hier bleiben darunter.

Technitium sperrt einen Namen und alles darunter. Steht `example.com` in der Liste, fallen dort auch `www.example.com` und `shop.example.com` weg. Pi-hole sperrt in einer normalen Hosts-Datei nur genau den eingetragenen Namen.

## Themen

| Thema | Was dort landet |
| --- | --- |
| Malware | Schadsoftware, Stalkerware, Cryptojacking |
| Phishing | Phishing und nachgebaute Bank-Domains |
| Fakeshops | Falsche Shops und unseriöse Angebote |
| Jugendschutz | Pornografie, Glücksspiel, Dating, Proxies |
| Tracking | Tracker und Telemetrie |
| Werbung | Werbenetze und Adserver |
| Dienste | Einzelne Anbieter, etwa Amazon, Google, Samsung |
| Diverse | Quellen, die in kein einzelnes Thema fallen |
| Standard | Die zusammengefasste Liste von StevenBlack |
| Overblock | Wenige sehr breite Domains |

Die genauen Adressen zu jedem Thema stehen in [blocklisten.md](blocklisten.md).

## Overblock

> [!WARNING]
> `listen/overblock.txt` sperrt wenige sehr breite Namen, darunter `baidu.com` und `buff.ly`. Auf Technitium fällt damit der ganze Dienst aus, nicht nur eine einzelne Seite. Lass diese eine Adresse weg, wenn du das nicht willst.

## Nutzung

Diese Zusammenstellung steht unter [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/). Du darfst sie privat nutzen, kopieren und weitergeben, auch in Pi-hole, Technitium und anderen DNS-Sperren. Kommerzielle Nutzung ist nicht erlaubt. Als Namensnennung gilt der Verweis auf dieses Repository und auf [Quellen.md](Quellen.md).

Die Domains stammen aus den Quellen in [Quellen.md](Quellen.md). Deren eigene Lizenz bleibt an den Ursprungsdaten. Der Lizenztext liegt in [LICENSE](LICENSE).

## Wenn sich die Listen ändern

Kenny2k8 baut die Listen neu, wenn sich die Quellen ändern, und legt die neuen Dateien nach `listen/`. Die Adressen in Pi-hole und Technitium bleiben dieselben. Neu einfügen musst du nur, wenn eine Datei hinzukommt oder wegfällt. Das steht dann in [blocklisten.md](blocklisten.md).

> [!IMPORTANT]
> Dieses Repository gehört nicht zu Pi-hole. Pi-hole findest du auf [pi-hole.net](https://pi-hole.net/). Die Dateien hier sind Listen, die du in Pi-hole oder Technitium importierst.
