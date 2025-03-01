---
title: 'DNS-Server eines OVHcloud Domainnamens ändern'
excerpt: 'Erfahren Sie hier, wie Sie DNS-Server im OVHcloud Kundencenter bearbeiten'
updated: 2023-08-25
---

> [!primary]
>
> Diese Übersetzung wurde durch unseren Partner SYSTRAN automatisch erstellt. In manchen Fällen können ungenaue Formulierungen verwendet worden sein, z.B. bei der Beschriftung von Schaltflächen oder technischen Details. Bitte ziehen Sie beim geringsten Zweifel die englische oder französische Fassung der Anleitung zu Rate. Möchten Sie mithelfen, diese Übersetzung zu verbessern? Dann nutzen Sie dazu bitte den Button "Beitragen" auf dieser Seite.
>

## Ziel

### DNS verstehen 

**D**omain **N**ame **S**ystem bezeichnet einen Satz von Elementen (DNS-Server, DNS-Zonen, etc.), mit denen ein Domainname IP-Adressen zugeordnet werden kann.

### DNS-Server 

Die **DNS-Server** enthalten DNS-Konfigurationsdateien für Domainnamen, die als **DNS-Zonen** bezeichnet werden.

Eine DNS-Zone enthält technische Informationen, die als DNS-Einträge bezeichnet werden.

Sie können beispielsweise Folgendes angeben:

- Die IP-Adresse (DNS-Einträge vom Typ *A* und *AAAA*) Ihres Hostings muss in der Zone eingetragen sein, damit Ihre Webseite angezeigt wird, wenn der Domainnamenname in einen Browser eingegeben wird.
- Die E-Mail-Server (DNS-Einträge vom Typ *MX*), die E-Mails erhalten sollen, die an Adressen mit diesem Domainnamen versendet wurden. Wenn Sie die MX-Einträge Ihres Domainnamens konfigurieren, können Sie E-Mails über Ihre personalisierten E-Mail-Adressen empfangen.
- Informationen zur Sicherheit/Authentifizierung von Diensten (Webhosting, Webserver, E-Mail-Server, etc.), die mit Ihrem Domainnamen verbunden sind (DNS-Einträge vom Typ *SPF*, *DKIM*, *DMARC*, etc.).

Weitere Informationen zu den DNS-Zonen finden Sie in unserer [Dokumentation zu DNS](/pages/web_cloud/domains/dns_zone_edit).

Aus diesem Grund müssen die **DNS-Server** beim Domainnamen angemeldet sein, um die von ihnen gehostete DNS-Zone verwenden zu können. 

![DNS](images/dnsserver.png){.thumbnail}

**DNS-Server** werden üblicherweise in Paaren eingesetzt:

- *Primärer* DNS-Server: Er leitet die vom Domainnamen empfangenen Anfragen auf die von ihm gehostete DNS-Zone. Damit wird die *DNS-Auflösung* durchgeführt, um eingehenden Traffic auf die passenden Dienste (Server, Website, E-Mails, etc.) zu leiten.
- *Sekundärer* DNS-Server: Kann als *Backup*-Server verwendet werden, wenn der *Primäre* DNS-Server mit Anfragen überlastet ist, nicht verfügbar ist oder langsamer antwortet als der *Sekundäre* DNS-Server.

DNS-Provider können auch drei oder mehr **DNS-Server** einsetzen, die alle deklariert werden müssen, um die betroffene DNS-Zone zu aktivieren.

**Diese Anleitung erklärt, wie Sie die DNS-Server eines OVHcloud Domainnamens ändern.**

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/BvrUi26ShzI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Voraussetzungen

- Sie verfügen über eine bei OVHcloud registrierten [Domainnamen](https://www.ovhcloud.com/de/domains/).
- Sie verfügen über die [entsprechenden Berechtigungen](/pages/account_and_service_management/account_information/managing_contacts){.external} für die Verwaltung des Domainnamens über Ihr [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de).
- Sie haben Zugriff auf Ihr [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de).

> [!primary]
>
> Ein Domainnamen-Registrar ist ein Diensteanbieter, der authorisiert ist, Domainnamen zur Registrierung seitens Privatpersonen, Unternehmen oder sonstigen Organisationen anzubieten. OVHcloud gehört zu diesen Registraren.
>
> Wenn Ihre Domain nicht bei OVHcloud registriert ist, müssen Sie die DNS-Server bei dem Registrar ändern, bei dem Ihr Domainname derzeit verwaltet wird.
>

## In der praktischen Anwendung

> [!warning]
>
> **Wir raten zur Vorsicht, wenn Sie die DNS-Server einer Domainnamen ändern.** Fehlkonfigurationen können dazu führen, dass Ihre Website nicht mehr erreichbar ist, oder dass Ihre E-Mail-Adressen keine neuen E-Mails mehr empfangen können. Im Folgenden erklären wir Ihnen die Auswirkungen von Konfigurationsänderungen, um Ihnen zu helfen, die Konsequenzen besser einzuschätzen.
>

Wenn Sie die DNS-Server Ihres Domainnamens ändern, ändern Sie dessen DNS-Konfiguration. Die neue DNS-Konfiguration ersetzt die alte und wird auf den neu hinterlegten DNS-Servern gespeichert. Technisch gesehen verwendet der Domainname dann eine neue DNS-Zone.

Bitte beachten Sie:

- Wenn neue DNS-Server deklariert werden (beispielsweise wenn OVHcloud DNS-Server externe ersetzen), wird die alte DNS-Konfiguration nicht automatisch in die neue repliziert. Stellen Sie sicher, dass Ihre neue DNS-Zone alle DNS-Einträge enthält, die erforderlich sind, damit die Dienste Ihres Domainnamens korrekt funktionieren (z.B. Ihre Website und Ihre E-Mail-Adressen).

- Wenn Sie nur einzelne Elemente Ihrer aktuellen DNS-Konfiguration ändern möchten (also einen DNS-Eintrag), empfehlen wir stattdessen, unsere [Anleitung zur Änderung der DNS-Zone](/pages/web_cloud/domains/dns_zone_edit) zu befolgen.

- Vereinzelt haben die Registrys, die Domainendungen verwalten, besondere Anforderungen an die DNS-Server (Anzahl der Namensserver, Wert der Einträge, etc.). Überprüfen Sie im Zweifelsfall die Regeln der zuständigen Registry des Domainnamens.

Stellen Sie sicher, dass Ihr Domainname aufgrund der Änderungen nicht unerreichbar wird. Wenn Sie sich nicht sicher sind, kontaktieren Sie die Person, die Sie um Änderungen ersucht.

### Zugang zur Verwaltung der OVHcloud DNS-Server

Loggen Sie sich in Ihr [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) ein und gehen Sie in den Bereich `Web Cloud`{.action}. Klicken Sie in der linken Spalte auf `Domainnamen`{.action} und wählen Sie den Domainnamen aus. Gehen Sie dann auf den Tab `DNS-Server`{.action}.

Die angezeigte Tabelle listet die DNS-Server auf, die derzeit von OVHcloud für Ihren Domainnamen definiert sind. Es werden möglicherweise mehrere DNS-Server angezeigt. Eine Tabellenzeile entspricht dabei jeweils einem Server.

> [!primary]
>
> Wenn Sie die regulären OVHcloud DNS-Server verwenden, haben die in den Servernamen enthaltenen Nummern keinen Bezug zu den von Ihnen verwendeten Diensten. Nur die Option [DNS Anycast](https://www.ovhcloud.com/de/domains/options/) verwendet bestimmte DNS-Server, die Ihnen automatisch zugewiesen werden. 

![dnsserver](images/edit-dns-server-ovh-step1.png){.thumbnail}

### DNS-Server ändern

Wenn Sie externe DNS-Server verwenden möchten, müssen die aktuellen OVHcloud Server **ersetzt** werden, anstatt sie der Konfiguration hinzuzufügen.

Klicken Sie rechts auf `DNS-Server ändern`{.action}.

Ersetzen Sie in den Textfeldern die aktuellen Werte der DNS-Server mit den Namen der neuen Server, die Sie hinterlegen möchten. Um weitere Server zur Liste hinzuzufügen, klicken Sie rechts neben der letzten Tabellenzeile auf `+`{.action}. Es wird eine neue Tabellenzeile angefügt, in die Sie die entsprechenden Informationen eintragen können.

> [!warning]
>
> Achten Sie darauf, eine Gruppe von DNS-Servern nicht mit einer anderen zu mischen. 
>
> Zum Beispiel entsprechen *dns19.ovh.net* und *ns19.ovh.net* einer Gruppe von OVHcloud DNS-Servern; diese sind aufeinander abgestimmt und werden synchronisiert. Wenn Sie externe DNS-Server zu OVHcloud Servern hinzufügen (oder die einer anderen Gruppe), erfolgt die DNS-Auflösung zufällig unter den OVHcloud DNS-Servern und den externen DNS-Servern.
>
> Bei OVHcloud können DNS-Servergruppen anhand der in den Servernamen angegebenen Nummer identifiziert werden, zum Beispiel gehören *dns19.ovh.net* und *ns19.ovh.net* zur selben Gruppe.
>

Wenn Sie die Server eingetragen haben, klicken Sie auf `Konfiguration anwenden`{.action}. Der Status der DNS-Server wird nun entsprechend der von Ihnen vorgenommenen Änderungen in der Tabelle aktualisiert.

![dnsserver](images/edit-dns-server-ovh-step2.png){.thumbnail}

> [!success]
>
> Die Änderung der DNS-Server eines Domainnamens führt zu einer Propagationsverzögerung von **24** bis **48** Stunden, bis diese Änderung wirksam wird.
>

### Sonderfall: DNS-Server zurücksetzen 

Mit dem Button `DNS-Server zurücksetzen`{.action} können Sie die aktuellen DNS-Server zurücksetzen, indem Sie diese automatisch durch die ursprünglichen OVHcloud DNS-Server ersetzen. Verwenden Sie diese Option **ausschließlich**, wenn Sie die OVHcloud DNS-Server (und die dazugehörige OVHcloud DNS-Zone) verwenden möchten. 

![dnsserver](images/edit-dns-server-ovh-step3.png){.thumbnail}

Nachdem die erforderlichen Änderungen vorgenommen wurden, dauert es eine gewisse Zeit, bis diese effektiv sind. Dabei sind zwei aufeinanderfolgende Vorgänge zu beachten:

- Die bei OVHcloud vorgenommene Änderung muss von der Registry, die Ihre Domainendung verwaltet, übernommen werden (z.B. der DENIC für *.de*). Sie können den Fortschritt dieser Operation in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) nachverfolgen, indem Sie im Bereich `Domainnnamen`{.action} auf `Laufende Vorgänge`{.action} klicken.
- Nachdem die Registry Ihrer Domainendung die Änderung angenommen hat, ist eine Propagationszeit von maximal 48 Stunden erforderlich, bis sie voll wirksam ist.

## Weiterführende Informationen

[Bearbeiten einer OVHcloud DNS-Zone](/pages/web_cloud/domains/dns_zone_edit).

Kontaktieren Sie für spezialisierte Dienstleistungen (SEO, Web-Entwicklung etc.) die [OVHcloud Partner](https://partner.ovhcloud.com/de/directory/).

Wenn Sie Hilfe bei der Nutzung und Konfiguration Ihrer OVHcloud Lösungen benötigen, beachten Sie unsere [Support-Angebote](https://www.ovhcloud.com/de/support-levels/).

Für den Austausch mit unserer User Community gehen Sie auf <https://community.ovh.com/en/>.