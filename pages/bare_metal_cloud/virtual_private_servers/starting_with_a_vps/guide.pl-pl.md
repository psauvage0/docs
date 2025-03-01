---
title: Pierwsze kroki z serwerem VPS
excerpt: Dowiedz się, jak zarządzać serwerem VPS w Panelu klienta i poznaj pierwsze kroki korzystania z niego, w tym zdalne połączenia i środki bezpieczeństwa
updated: 2024-01-10
---

> [!primary]
> Tłumaczenie zostało wygenerowane automatycznie przez system naszego partnera SYSTRAN. W niektórych przypadkach mogą wystąpić nieprecyzyjne sformułowania, na przykład w tłumaczeniu nazw przycisków lub szczegółów technicznych. W przypadku jakichkolwiek wątpliwości zalecamy zapoznanie się z angielską/francuską wersją przewodnika. Jeśli chcesz przyczynić się do ulepszenia tłumaczenia, kliknij przycisk "Zgłóś propozycję modyfikacji" na tej stronie.
>
 
## Wprowadzenie

Prywatny serwer wirtualny (VPS) to wirtualny serwer dedykowany. W przeciwieństwie do rozwiązań hostingowych OVHcloud, którymi zarządza OVHcloud, konfiguracja i konserwacja systemu VPS należy do Twoich kompetencji jako administratora systemu.

**Poznaj informacje niezbędne do rozpoczęcia pracy z serwerem VPS.**


## Wymagania początkowe

- Posiadanie serwera [VPS](https://www.ovhcloud.com/pl/vps/) w Panelu klienta OVHcloud
- Dostęp do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl)

## W praktyce

Zaloguj się do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl), przejdź do sekcji `Bare Metal Cloud`{.action} i wybierz Twój serwer w sekcji `Prywatne serwery wirtualne`{.action}.

### Panel klienta

Karta `Strona`{.action} główna zawiera ważne informacje o Twojej usłudze i umożliwia przeprowadzenie najważniejszych operacji.

![VPS Home](images/vpshome.png){.thumbnail}

#### Twój VPS <a name="yourvps"></a>

W tej sekcji wyświetlane są podstawowe informacje o serwerze VPS i o stanie usługi.

##### **Nazwisko**

Jeśli klikniesz `...`{.action}, a następnie wybierzesz `Zmień nazwę`{.action}, będziesz mógł wprowadzić osobną nazwę dla tego VPS. Funkcja ta jest przydatna w przypadku zarządzania kilkoma usługami VPS. Nazwa wewnętrznej usługi jest zapisana w formacie *vps-XXXXXXX.vps.ovh.net*.

##### **Boot**

Wyświetlony tutaj tryb uruchamiania działa w trybie "normalnym", w którym system ładuje zainstalowany system operacyjny (*LOCAL*) lub w **trybie rescue** dostarczonym przez OVHcloud w przypadku rozwiązywania problemów. Użyj przycisku `...`{.action} aby [zrestartować serwer VPS](#reboot-current-range) lub uruchomić go w trybie Rescue.

Więcej informacji na ten temat znajdziesz w naszym przewodniku o [trybie Rescue](/pages/bare_metal_cloud/virtual_private_servers/rescue).

##### **OS / Dystrybucja**

Jest to aktualnie zainstalowany system operacyjny. Użyj przycisku `...`{.action} aby [ponownie zainstalować ten sam system operacyjny lub wybrać inny z dostępnych](#reinstallvps) opcji.

Pamiętaj, że reinstalacja usunie wszystkie dane aktualnie hostowane na serwerze VPS (z wyjątkiem dodatkowych dysków).

> [!primary]
>
> Jeśli zamówiłeś VPS **Windows**, możesz wybrać do reinstalacji tylko jeden OS Windows. Podobnie, jeśli system Windows nie został wybrany podczas zamówienia, nie może zostać zainstalowany po zainstalowaniu serwera VPS.
>

Po zainstalowaniu systemu wykonaj aktualizacje zabezpieczeń. Więcej informacji znajdziesz [poniżej](#reinstallvps) i w naszym przewodniku [Zabezpiecz serwer VPS](/pages/bare_metal_cloud/virtual_private_servers/secure_your_vps).

##### **Strefa** / **Lokalizacja**

W tych sekcjach znajdziesz informacje o lokalizacji serwera VPS. Może to być przydatne na przykład do identyfikacji skutków dla Twojej usługi wymienionych w [status reports](https://bare-metal-servers.status-ovhcloud.com/).

#### Twoja konfiguracja

##### **Model**

Ten element wskazuje model biznesowy identyfikujący model serwera VPS odpowiadający [ofertom VPS na naszej stronie](https://www.ovhcloud.com/pl/vps).

##### **vCores** / **Pamięć** / **Przestrzeń dyskowa**

Tutaj wyświetlają się bieżące zasoby Twojego serwera VPS. Możesz je zaktualizować osobno, klikając odpowiedni przycisk. Aktualizacje są ograniczone wybranym modelem VPS i mogą być dostępne tylko po przejściu na wyższą [gamę](https://www.ovhcloud.com/pl/vps).

#### Adresy IP

##### **IPv4**

Główny publiczny adres IPv4 serwera VPS jest konfigurowany automatycznie podczas instalacji. Więcej informacji na temat zarządzania adresami IP znajdziesz w przewodniku [Konfiguracja IP aliasing](/pages/bare_metal_cloud/virtual_private_servers/configuring-ip-aliasing).

##### **IPv6** / **Gateway**

W tej części można zobaczyć publiczny adres IPv6 i adres przypisanej bramy. Są one automatycznie dołączane do serwera VPS podczas instalacji. Więcej informacji zawiera [ten przewodnik](/pages/bare_metal_cloud/virtual_private_servers/configure-ipv6).

##### **DNS secondary**

Funkcja ta jest przydatna przy instalowaniu usług DNS. Szczegółowo opisany jest [w przewodniku dotyczącym konfigurowania DNS secondary OVHcloud na serwerze VPS](/pages/bare_metal_cloud/virtual_private_servers/adding-secondary-dns-on-vps).

#### Podsumowanie opcji

Opcje te dotyczą dodatkowych usług VPS, które można zamówić w Panelu klienta.

- Opcja `Snapshot` pozwala na utworzenie ręcznego snapshota jako pojedynczego punktu przywracania.
- Opcja `Zautomatyzowany backup` zapasowych pozwala na zachowanie kilku snapshotów serwera VPS (z wyłączeniem dodatkowych dysków).
- Opcja `Dodatkowe dyski` pozwala na podłączenie przestrzeni dyskowej do Twojego serwera VPS, na przykład w celu przechowywania danych kopii zapasowych.

Wszystkie informacje na temat dostępnych dla Twojej usługi rozwiązań do tworzenia kopii zapasowych można znaleźć na [stronie produktu](https://www.ovhcloud.com/pl/vps/options/) oraz w odpowiednich [przewodnikach](/products/bare-metal-cloud-virtual-private-servers-backups).

#### Abonament

W tych sekcjach znajdują się najważniejsze informacje dotyczące fakturowania usługi. Wszystkie informacje na ten temat znajdziesz w odpowiedniej [dokumentacji](/products/account-and-service-management-managing-billing-payments-and-services).

### Funkcje VPS dostępne w zakładce "Strona główna"

> [!warning]
>
> OVHcloud udostępnia Ci usługi, ale to użytkownik ponosi odpowiedzialność za zarządzanie nimi oraz ich konfigurację. Do Twoich obowiązków należy zatem upewnienie się, że działają one prawidłowo.
>
> Celem niniejszego przewodnika jest pomoc w jak najbardziej optymalnym wykonywaniu bieżących zadań. Niemniej jednak, w przypadku trudności lub wątpliwości związanych z administrowaniem, użytkowaniem lub wdrażaniem usług na serwerze, zalecamy skontaktowanie się z [wyspecjalizowanym](https://partner.ovhcloud.com/pl/directory/) dostawcą usług lub [naszą społecznością](https://community.ovh.com/en/).
>

### Reinstalacja serwera VPS <a name="reinstallvps"></a>

Reinstalacja jest możliwa po zalogowaniu się do panelu klienta. Kliknij `...`{.action} obok **OS / Dystrybucja**, a następnie `Reinstalacja serwera VPS`{.action}.

![Reinstalacja serwera VPS](images/2023panel_01.png){.thumbnail}

W oknie, które się pojawi, wybierz system operacyjny z rozwijanej listy. Proponowane opcje to obrazy [kompatybilne z serwerem VPS OVHcloud](/pages/public_cloud/compute/image-life-cycle) i są gotowe do użytku natychmiast po instalacji.

Możesz również wybrać **klucz SSH** do zainstalowania w systemie, jeśli wcześniej przechowywałeś go w Panelu [klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl). Więcej informacji na ten temat znajdziesz w przewodniku Tworzenie i [używanie kluczy SSH](/pages/bare_metal_cloud/dedicated_servers/creating-ssh-keys-dedicated).

> [!primary]
>
> **Licencje**
>
> Niektóre zastrzeżone systemy operacyjne lub platformy, takie jak Plesk lub cPanel, wymagają licencji, które generują dodatkowe koszty. Licencjami można zarządzać w Panelu klienta: przejdź do sekcji `Bare Metal Cloud`{.action} , a następnie na pasku nawigacji po lewej stronie kliknij `Licencje`{.action}.
>
> Aby posiadać system operacyjny **Windows** działający na serwerze VPS, należy **wybrać w procesie zamówienia**. Na serwerze VPS z innym zainstalowanym systemem operacyjnym nie można zainstalować systemu Windows w sposób opisany powyżej.
>

W Panelu klienta wyświetli się pasek postępu instalacji. Operacja ta może potrwać do 30 minut.

### Restart serwera VPS <a name="reboot-current-range"></a>

Ponowne uruchomienie może być konieczne w celu zastosowania zaktualizowanych konfiguracji lub rozwiązania problemu. Jeśli to możliwe, wykonaj "restart oprogramowania" w graficznym interfejsie serwera (Windows, Plesk, ...) lub za pomocą wiersza poleceń:

```bash
sudo reboot
```

Jednak w każdej chwili możesz wykonać "reboot sprzętowy" w Panelu [klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl). W zakładce `Strona`{.action} główna kliknij `...`{.action} obok `Boot` w sekcji **Twój VPS**. Wybierz `Restart serwera VPS`{.action} i w oknie, które się wyświetli kliknij `Zatwierdź`{.action}.

![Reboot](images/reboot-vps01.png){.thumbnail}

### Logowanie do serwera VPS (OS GNU/Linux)

Przy pierwszej instalacji lub podczas reinstalacji z Panelu sterowania automatycznie tworzony jest użytkownik z podwyższonym poziomem uprawnień. Ten użytkownik będzie nazwany w zależności od systemu operacyjnego, na przykład "ubuntu" lub "rocky".

Otrzymasz wówczas e-mail z nazwą użytkownika i hasłem niezbędnymi do zalogowania się do Twojego serwera VPS przez SSH. SSH to bezpieczny protokół komunikacyjny używany do ustanawiania szyfrowanych połączeń ze zdalnym hostem.

Większość obecnych stacjonarnych systemów operacyjnych będzie miała natywnie zainstalowanego klienta **Open SSH**. Oznacza to, że dane dostępowe umożliwiają szybkie nawiązanie połączenia z Twoim serwerem VPS w odpowiedniej aplikacji wiersza polecenia (`Terminal`, `Command prompt`, `Powershell`, etc.). Wprowadź następujące polecenie:

```bash
ssh username@IPv4_VPS
```

Przykład:

```bash
ssh ubuntu@169.254.10.250
```

Możesz również korzystać z dowolnej aplikacji innej firmy, która jest kompatybilna z **Open SSH**.

Po zalogowaniu możesz zmienić predefiniowane hasło standardowego użytkownika na silne hasło, używając tego polecenia:

```bash
passwd
```

```console
Changing password for ubuntu.
Current password:
New password: 
Retype new password: 
passwd: password updated successfully
```

**Wykonaj następujące czynności**:

- Zapoznanie się z połączeniami SSH w przewodniku [Wprowadzenie do SSH](/pages/bare_metal_cloud/dedicated_servers/ssh_introduction).
- Rozważ użycie kluczy SSH jako zaawansowanej i wygodnej metody zdalnego połączenia za pomocą naszego przewodnika [Tworzenie i używanie kluczy SSH](/pages/bare_metal_cloud/dedicated_servers/creating-ssh-keys-dedicated).
- Zapoznaj się z przewodnikiem [Zabezpiecz serwer VPS](/pages/bare_metal_cloud/virtual_private_servers/secure_your_vps), aby chronić Twój system przed automatycznymi atakami typu *brute force* i innymi typowymi zagrożeniami.

> [!primary]
>
Należy pamiętać, że w przypadku wyboru **dystrybucji z aplikacją** (Plesk, cPanel, Docker) ogólne środki bezpieczeństwa mogą nie mieć zastosowania do Twojego systemu. Zapoznaj się z przewodnikami Pierwsze [kroki z wstępnie zainstalowanymi](/pages/bare_metal_cloud/virtual_private_servers/apps_first_steps) aplikacjami i [wdrażaj cPanel na serwerze VPS](/pages/bare_metal_cloud/virtual_private_servers/cpanel), a także z oficjalną dokumentacją producenta.
>

#### Aktywacja połączeń root

> [!warning]
>
> Połączenie z użytkownikiem "root" jest domyślnie wyłączone ze względów bezpieczeństwa. Jeśli chcesz zezwolić na te połączenia, zapoznaj się z instrukcjami zawartymi w [tym przewodniku](/pages/bare_metal_cloud/virtual_private_servers/root_password#enable-root-login).
>

#### Aktualizacja hasła root

Aby zmienić lub zaktualizować hasło "root", zapoznaj się z instrukcjami zawartymi w [tym przewodniku](/pages/bare_metal_cloud/virtual_private_servers/root_password).

### Łączenie z serwerem VPS Windows

Po zainstalowaniu VPS Windows otrzymasz wiadomość e-mail z nazwą domyślnego użytkownika `Windows user`.

Następnie należy dokończyć instalację systemu Windows, ustawiając język wyświetlania, układ klawiatury i hasło administratora.

W tym celu skorzystaj z konsoli KVM: kliknij `...`{.action} obok nazwy serwera VPS w sekcji [Twój VPS](#yourvps) i wybierz `KVM`{.action}. Więcej informacji na temat tego narzędzia znajdziesz w naszym [przewodniku KVM](/pages/bare_metal_cloud/virtual_private_servers/secure_your_vps).

Aby zakończyć instalację serwera VPS Windows za pomocą narzędzia KVM, wykonaj kroki opisane w przewodniku [Konfigurowanie nowej instalacji systemu Windows Server](/pages/bare_metal_cloud/virtual_private_servers/windows_first_config).

Na lokalnym sprzęcie z systemem Windows możesz połączyć się z serwerem VPS za pomocą aplikacji klienckiej `Remote Desktop Connection`.

![Windows Remote](images/windows-connect-03.png){.thumbnail}

Wprowadź adres IPv4 Twojego serwera VPS, następnie identyfikator i hasło. Zazwyczaj pojawia się komunikat ostrzegawczy z prośbą o potwierdzenie logowania z powodu nieznanego certyfikatu. Kliknij przycisk `Tak`{.action}, aby się zalogować.

Możesz również używać dowolnych aplikacji innych firm kompatybilnych z RDP. Jest to wymagane, jeśli system Windows nie jest zainstalowany na urządzeniu lokalnym.

> [!primary]
>
W przypadku wystąpienia problemów z tą procedurą sprawdź, czy na urządzeniu są dozwolone połączenia zdalne (RDP), sprawdzając ustawienia systemu, reguły zapory i możliwe ograniczenia sieciowe.
>

### Zabezpiecz Twój serwer VPS

Jako administrator serwera VPS jesteś odpowiedzialny za bezpieczeństwo przechowywanych na nim aplikacji i danych.

Zapoznaj się z naszym przewodnikiem [Zabezpieczanie VPS](/pages/bare_metal_cloud/virtual_private_servers/secure_your_vps), aby uzyskać ważne wskazówki dotyczące ochrony systemu.

> [!primary]
>
Należy pamiętać, że w przypadku wyboru **dystrybucji z aplikacją** (Plesk, cPanel, Docker) ogólne środki bezpieczeństwa mogą nie mieć zastosowania do Twojego systemu. Zapoznaj się z przewodnikami Pierwsze [kroki z wstępnie zainstalowanymi](/pages/bare_metal_cloud/virtual_private_servers/apps_first_steps) aplikacjami i [wdrażaj cPanel na serwerze VPS](/pages/bare_metal_cloud/virtual_private_servers/cpanel), a także z oficjalną dokumentacją producenta.
>

### Przypisz domenę

Aktywacja Twojego serwera VPS w Internecie zwykle polega na przypisaniu domeny i skonfigurowaniu DNS. Jeśli zarządzasz domeną w OVHcloud, zapoznaj się z naszym przewodnikiem [Edycja strefy DNS](/pages/web_cloud/domains/dns_zone_edit) OVHcloud, aby uzyskać instrukcje.

### Zabezpieczenie domeny za pomocą certyfikatu SSL

Po skonfigurowaniu Twojego serwera VPS, masz możliwość zabezpieczenia nazwy Twojej domeny oraz Twojej strony WWW. W tym celu potrzebujesz certyfikatu SSL, który umożliwi dostęp do Internetu Twojego serwera VPS za pośrednictwem protokołu *HTTPS* zamiast *niezabezpieczonego HTTP*.

Certyfikat SSL można zainstalować ręcznie, bezpośrednio na serwerze VPS. Zapoznaj się z oficjalną dokumentacją dotyczącą Twojej dystrybucji VPS.

W przypadku bardziej zautomatyzowanego procesu OVHcloud oferuje również rozwiązanie SSL Gateway. Więcej informacji znajdziesz na [stronie produktu](https://www.ovh.pl/ssl-gateway/) lub w [przewodniku](/products/web-cloud-ssl-gateway) OVHcloud.

## Sprawdź również

[VPS FAQ](/pages/bare_metal_cloud/virtual_private_servers/vps-faq)

[Wprowadzenie do protokołów SSH](/pages/bare_metal_cloud/dedicated_servers/ssh_introduction)

[Zabezpieczenie serwera VPS](/pages/bare_metal_cloud/virtual_private_servers/secure_your_vps)

[Konfigurowanie nowej instalacji systemu Windows Server](/pages/bare_metal_cloud/virtual_private_servers/windows_first_config)

Dołącz do społeczności naszych użytkowników na stronie <https://community.ovh.com/en/>.
