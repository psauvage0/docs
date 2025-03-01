---
title: 'IP-Adresse als Alias konfigurieren'
excerpt: 'Erfahren Sie hier, wie Sie Additional IPs in Ihre VPS-Konfiguration einbinden'
updated: 2023-08-15
---

> [!primary]
> Diese Übersetzung wurde durch unseren Partner SYSTRAN automatisch erstellt. In manchen Fällen können ungenaue Formulierungen verwendet worden sein, z.B. bei der Beschriftung von Schaltflächen oder technischen Details. Bitte ziehen Sie im Zweifelsfall die englische oder französische Fassung der Anleitung zu Rate. Möchten Sie mithelfen, diese Übersetzung zu verbessern? Dann nutzen Sie dazu bitte den Button "Beitragen" auf dieser Seite.
>

> [!primary]
>
> Seit dem 6. Oktober 2022 heißt unser Dienst "Failover-IP" nun [Additional IP](https://www.ovhcloud.com/de/network/additional-ip/). Die Namensänderung hat keine Auswirkungen auf dessen technische Funktionen.
>

## Ziel

Bei *IP Aliasing* handelt es sich um eine spezielle Netzwerkkonfiguration für bestimme OVHcloud Dienste, mit der Sie mehrere IP-Adressen über ein einziges Netzwerkinterface verbinden können.

**Diese Anleitung erklärt, wie Sie Additional IPs zu Ihrer Netzwerkkonfiguration hinzufügen.**

> [!warning]
> OVHcloud stellt Ihnen Dienstleistungen zur Verfügung, für die Sie die alleinige Verantwortung tragen. Da wir keinen Zugriff auf diese Dienste haben, können wir hierfür keinerlei Administrator-Aufgaben übernehmen oder sonstige Hilfeleistung anbieten. Es liegt daher in Ihrer Verantwortung, das Softwaremanagement und die tägliche Sicherheit zu gewährleisten.
>
> Wir stellen Ihnen diese Anleitung zur Verfügung, um Ihnen bei der Bewältigung alltäglicher Verwaltungsaufgaben zu helfen. Wir empfehlen Ihnen jedoch, sich an einen [spezialisierten Dienstleister](https://partner.ovhcloud.com/de/directory/) zu wenden, wenn Sie Schwierigkeiten oder Zweifel hinsichtlich der Verwaltung, Nutzung oder Sicherheit eines Servers haben. Sie können sich auch jederzeit an unsere [Community](https://community.ovh.com/en/) wenden, um sich mit anderen Benutzern auszutauschen.
>

## Voraussetzungen

- Sie haben einen [VPS](https://www.ovhcloud.com/de/vps/) in Ihrem OVHcloud Account.
- Sie verfügen über eine [Additional IP](https://www.ovhcloud.com/de/bare-metal/ip/)-Adresse.
- Sie haben administrativen Zugriff (Root) auf Ihren VPS über SSH oder GUI. 
- Sie haben Grundkenntnisse in Administration und Netzwerkkonfiguration.

## In der praktischen Anwendung

Die folgenden Abschnitte enthalten die Konfigurationen für die am häufigsten verwendeten Distributionen/Betriebssysteme. Der erste Schritt ist immer die Anmeldung an Ihrem Server über SSH oder einen GUI-Login (RDP für einen Windows-VPS). Die folgenden Beispiele setzen voraus, dass Sie als Benutzer mit erhöhten Berechtigungen (Administrator/sudo) angemeldet sind.

> [!primary]
>
Bitte beachten Sie, dass sich bei unterschiedlichen Distributionen die korrekte Vorgehensweise zur Konfiguration Ihrer Netzwerkschnittstelle sowie die Dateinamen geändert haben können. Wir empfehlen Ihnen, bei Problemen die Dokumentationen und Wissensressourcen der jeweiligen Betriebssystemversionen zu konsultieren. 
>

**Bitte beachten Sie die Terminologie, die in den nachfolgenden Codebeispielen und Anweisungen dieser Anleitung verwendet wird:**

|Bezeichnung|Beschreibung|Beispiele|
|---|---|---|
|ADDITIONAL_IP|Ihrem Dienst zugewiesene Additional IP|169.254.10.254|
|NETWORK_INTERFACE|Name des Netzwerkinterfaces|*eth*, *ens3*|
|ID|ID der Alias-IP, beginnend mit *0* (abhängig von der Anzahl der zu konfigurierenden zusätzlichen IP-Adressen)|*0*, *1*|

### Debian 10/11

#### Schritt 1: Automatische Netzwerkkonfiguration deaktivieren

Öffnen Sie diesen Dateipfad mit einem Texteditor:

```bash
sudo nano /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg
```

Fügen Sie die folgende Zeile ein, speichern Sie und schließen Sie dann den Editor.

```bash
network: {config: disabled}
```

Die Erstellung dieser Konfigurationsdatei verhindert die automatische Ausführung von Änderungen an der Konfiguration Ihres Netzwerks.

#### Schritt 2: Netzwerkkonfigurationsdatei bearbeiten

Um den Namen Ihres Netzwerkinterfaces zu überprüfen, verwenden Sie folgenden Befehl:

```bash
ip a
```

Öffnen Sie die Netzwerkkonfigurationsdatei zur Bearbeitung:

```bash
sudo nano /etc/network/interfaces.d/50-cloud-init
```

Fügen Sie folgende Zeilen hinzu:

```bash
auto NETWORK_INTERFACE:ID
iface NETWORK_INTERFACE:ID inet static
address ADDITIONAL_IP
netmask 255.255.255.255
```

#### Schritt 3: Interface neu starten

Wenden Sie die Änderungen mit folgendem Befehl an:

```bash
sudo systemctl restart networking
```

### Ubuntu 20.04 & Debian 12

Die Konfigurationsdatei für Ihre Additional IPs befindet sich in `/etc/netplan/`. In diesem Beispiel heißt sie "50-cloud-init.yaml". Bevor Sie Änderungen vornehmen, überprüfen Sie am besten den tatsächlichen Dateinamen in diesem Ordner. Jede Additional IP benötigt in der Datei eine eigene Zeile.

#### Schritt 1: Automatische Netzwerkkonfiguration deaktivieren

Öffnen Sie diesen Dateipfad mit einem Texteditor:

```bash
sudo nano /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg
```

Fügen Sie die folgende Zeile ein, speichern Sie und schließen Sie dann den Editor.

```bash
network: {config: disabled}
```

Die Erstellung dieser Konfigurationsdatei verhindert die automatische Ausführung von Änderungen an der Konfiguration Ihres Netzwerks.

#### Schritt 2: Konfigurationsdatei bearbeiten

Um den Namen Ihres Netzwerkinterfaces zu überprüfen, verwenden Sie folgenden Befehl:

```bash
ip a
```

Öffnen Sie die Netzwerkkonfigurationsdatei zur Bearbeitung:

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

Ändern Sie nicht die vorhandenen Zeilen in der Datei; fügen Sie Ihre Additional IP in einem zweiten Block für das öffentliche Interface wie folgt hinzu:

```yaml
network:
    version: 2
    ethernets:
        NETWORK_INTERFACE:
            dhcp4: true
            match:
                macaddress: fa:xx:xx:xx:xx:63
            set-name: NETWORK_INTERFACE            
        NETWORK_INTERFACE:
            dhcp4: true
            match:
                macaddress: fa:xx:xx:xx:xx:63
            set-name: NETWORK_INTERFACE
            addresses:
            - ADDITIONAL_IP/32
```

> [!warning]
>
> Es ist wichtig, dass die Zeilenausrichtung jedes Elements dieser Datei, wie im Beispiel dargestellt, eingehalten wird. Verwenden Sie nicht die Tabulationstaste, um den Abstand zu erzeugen.
>

Speichern und schließen Sie die Datei.

#### Schritt 3: Neue Netzwerkkonfiguration anwenden

Sie können Ihre Konfiguration mit folgendem Befehl testen:

```bash
sudo netplan try
```

Ist die Änderung korrekt, verwenden Sie folgenden Befehl, um sie anzuwenden:

```bash
sudo netplan apply
```

Wiederholen Sie diesen Vorgang für jede Additional IP.

### Windows Server 2016

#### Schritt 1: Netzwerkkonfiguration überprüfen

Klicken Sie mit der rechten Maustaste auf das `Startmenü`{.action} und öffnen Sie `Ausführen`{.action}.

Geben Sie `cmd` ein und klicken Sie auf `OK`{.action}, um die Kommandozeilenanwendung zu öffnen.

![cmdprompt](images/vps_win07.png){.thumbnail}

Um die aktuelle IP-Konfiguration anzuzeigen, geben Sie `ipconfig` in der Eingabeaufforderung ein.

![IP-Konfiguration überprüfen](images/image1-1.png){.thumbnail}

#### Schritt 2: IPv4 Eigenschaften ändern

Die IP-Eigenschaften müssen nun zu einer statischen Konfiguration geändert werden.

Öffnen Sie die Adaptereinstellungen in der Windows-Systemsteuerung und öffnen Sie die `Eigenschaften`{.action} von `Internet Protocol Version 4 (TCP/IPv4)`{.action}.

![IP-Konfiguration ändern](images/image2.png){.thumbnail}

Wählen Sie in den IPv4-Eigenschaften `Folgende IP-Adresse verwenden`{.action}. Geben Sie die IP-Adresse ein, die Sie im ersten Schritt ausgelesen haben, und klicken Sie dann auf `Erweitert`{.action}.

#### Schritt 3: Die Additional IP in "Erweiterte TCP/IP Einstellungen" hinzufügen

Klicken Sie im neuen Fenster auf `Hinzufügen...`{.action} unter "IP-Adressen". Geben Sie Ihre Additional IP und die Subnetzmaske (255.255.255.255) ein.

![Konfiguration](images/image4-4.png){.thumbnail}

Bestätigen Sie, indem Sie auf `Hinzufügen`{.action} klicken.

![Konfiguration Additional IP](images/image5-5.png){.thumbnail}

#### Schritt 4: Netzwerk-Interface neu starten

Wieder in der Systemsteuerung (`Netzwerkverbindungen`{.action}), klicken Sie mit der rechten Maustaste auf Ihr Netzwerkinterface und wählen Sie `Deaktivieren`{.action}.

![Netzwerkdeaktivierung](images/image6.png){.thumbnail}

Um es neu zu starten klicken Sie mit der rechten Maustaste darauf und wählen Sie `Aktivieren`{.action}.

![Netzwerkaktivierung](images/image7.png){.thumbnail}

#### Schritt 5: Überprüfung der neuen Netzwerkkonfiguration

Öffnen Sie die Eingabeaufforderung (cmd) und geben Sie `ipconfig` ein. Die Konfiguration sollte nun die neue Additional IP enthalten.

![Aktuelle Netzwerkkonfiguration überprüfen](images/image8-8.png){.thumbnail}

### cPanel (CentOS 7) / RedHat Derivate

#### Schritt 1: Netzwerkkonfigurationsdatei bearbeiten

Um den Namen Ihres Netzwerkinterfaces zu überprüfen, verwenden Sie folgenden Befehl:

```bash
ip a
```

Öffnen Sie die Netzwerkkonfigurationsdatei zur Bearbeitung:

```bash
sudo nano /etc/sysconfig/network-scripts/ifcfg-NETWORK_INTERFACE:ID
```

Fügen Sie folgende Zeilen hinzu:

```bash
DEVICE=NETWORK_INTERFACE:ID
BOOTPROTO=static
IPADDR=ADDITIONAL_IP
NETMASK=255.255.255.255
BROADCAST=ADDITIONAL_IP
ONBOOT=yes
```

#### Schritt 2: Interface neu starten

Wenden Sie die Änderungen mit folgendem Befehl an:

```bash
sudo systemctl restart networking
```

### Plesk

#### Schritt 1: Auf die IP-Verwaltung von Plesk zugreifen

Wählen Sie im Plesk Konfigurationspanel `Tools & Settings`{.action} im linken Menü aus.

![Zugang zur Verwaltung der IP-Adressen](images/pleskip1.png){.thumbnail}

Klicken Sie auf `IP Addresses`{.action} unter **Tools & Resources**.

#### Schritt 2: Die zusätzliche IP-Information hinzufügen

Klicken Sie in diesem Abschnitt auf den Button `Add IP Address`{.action}.

![IP-Informationen hinzufügen](images/pleskip2-2.png){.thumbnail}

Geben Sie Ihre Additional IP in der Form `xxx.xxx.xxx.xxx/32` in das Feld "IP address and subnet mask" ein und klicken Sie dann auf `OK`{.action}.

![IP-Informationen hinzufügen](images/pleskip3-3.png){.thumbnail}

#### Schritt 3: Aktuelle IP-Konfiguration überprüfen

Überprüfen Sie im Bereich "IP Addresses" ob die Additional IP korrekt hinzugefügt wurde.

![aktuelle IP-Konfiguration](images/pleskip4-4.png){.thumbnail}

### Diagnose

Starten Sie zunächst Ihren Server über die Kommandozeile oder dessen Benutzeroberfläche neu. Wenn Sie dann immer noch keine Verbindung zwischen dem öffentlichen Netzwerk und Ihrer Alias-Adresse herstellen können und ein Netzwerkproblem vermuten, ist es notwendig, den Server im [Rescue-Modus neu zu starten](/pages/bare_metal_cloud/virtual_private_servers/rescue). Anschließend können Sie die Additional IP direkt auf dem Server konfigurieren.

Wenn Sie über SSH mit Ihrem Server verbunden sind, geben Sie folgenden Befehl ein:

```bash
ifconfig ens3:0 ADDITIONAL_IP netmask 255.255.255.255 broadcast ADDITIONAL_IP up
```

Um die Verbindung zu testen senden Sie einfach von außerhalb einen Ping an Ihre Additional IP. Wenn sie im Rescue-Modus antwortet, bedeutet dies wahrscheinlich, dass ein Konfigurationsfehler vorliegt. Wenn die IP jedoch noch nach wie vor nicht funktioniert, informieren Sie bitte unsere Support-Teams, indem Sie ein Support-Ticket über Ihr [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) erstellen.

## Weiterführende Informationen

[VPS Rescue-Modus aktivieren](/pages/bare_metal_cloud/virtual_private_servers/rescue)

Für den Austausch mit unserer User Community gehen Sie auf <https://community.ovh.com/en/>
