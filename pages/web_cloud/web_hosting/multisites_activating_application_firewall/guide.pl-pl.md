---
title: "Aktywacja zapory systemowej"
excerpt: "Hosting www: Aktywacja zapory systemowej"
updated: 2021-04-26
---

> [!primary]
> Tłumaczenie zostało wygenerowane automatycznie przez system naszego partnera SYSTRAN. W niektórych przypadkach mogą wystąpić nieprecyzyjne sformułowania, na przykład w tłumaczeniu nazw przycisków lub szczegółów technicznych. W przypadku jakichkolwiek wątpliwości zalecamy zapoznanie się z angielską/francuską wersją przewodnika. Jeśli chcesz przyczynić się do ulepszenia tłumaczenia, kliknij przycisk "Zgłóś propozycję modyfikacji" na tej stronie.
>

## Wprowadzenie 

*ModSecurity* to uzupełniający moduł Apache, który filtruje wszystkie zapytania kierowane do serwera WWW. Wzmacnia bezpieczeństwo przed znanymi podatnościami poprzez przechwytywanie i filtrowanie wniosków, zanim zostaną one przetworzone przez skrypty.

Wstępnie skonfigurowany zbiór podstawowych zasad, takich jak "Core Rule Set" (CRS), *ModSecurity* chroni Twoje strony WWW przed najczęstszymi atakami, na przykład:

- Trojany,
- Wstrzykiwanie e-maili,
- Luka w plikach PDF,
- Włamania do plików na hostingu,
- wtrysk typu SQL lub XSS
- itd.

**Niniejszy przewodnik wyjaśnia, jak aktywować zaporę aplikacyjną w Panelu klienta OVHcloud, aby uzyskać lepszą ochronę.**

## Wymagania początkowe

- Posiadanie [hostingu OVHcloud](https://www.ovhcloud.com/pl/web-hosting/){.external}.
- Posiadanie co najmniej jednej [domeny](https://www.ovhcloud.com/pl/domains/){.external} przypisanej do hostingu
- Dostęp do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl){.external}.

## W praktyce

Zaloguj się do swojego [panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl){.external} i wybierz `Web Cloud`{.action}. Kliknij sekcję `Hosting`{.action}, a następnie nazwę odpowiedniego hostingu.

### Włącz firewall aplikacyjny w konfiguracji PHP

Następnie przejdź do zakładki `Informacje ogólne`{.action}. Aktualna `wersja globalna PHP` wyświetla się w strefie **Konfiguracja**. Kliknij przycisk `...`{.action} i wybierz `Zmień konfigurację`{.action}. W oknie, które się otworzy wybierz element `Zmień bieżącą`{.action} konfigurację i kliknij przycisk `Dalej`{.action}.

![managephpconfig](images/application-firewall-step-2.png){.thumbnail}

W nowym oknie upewnij się, że **Aplikacja firewall** jest ustawiona na `Włącz`{.action}. Aby potwierdzić konfigurację, kliknij przycisk `Potwierdź`{.action}.

### Włącz firewall aplikacyjny dla poszczególnych domen na stronie podpiętej w opcji MultiSite

Kliknij zakładkę `MultiSite`{.action} w Twoim pakiecie hostingowym. Kliknij przycisk `...`{.action} po prawej stronie wybranej domeny i wybierz opcję `Zmień domenę`{.action}.

![zapalenie skóry](images/modify-a-domain.png){.thumbnail}

W oknie konfiguracji zaznacz kratkę `Włącz firewall`{.action}. Możesz również włączyć subdomenę `www` do tej konfiguracji, zaznaczając kratkę na górze.

Kliknij `Dalej`{.action}, a następnie `Zatwierdź`{.action}, aby zmienić ustawienia MultiSite.

![modyfydomain](images/modify-a-domain-enable-firewall-step-1.png){.thumbnail}

### Sprawdź stan zadania aktywacji

![zarządzanie w trakcie](images/firewall-planned.png){.thumbnail}

Zadania związane z aktualizacją konfiguracji MultiSite zostaną wymienione w zakładce `Operacje w toku`{.action} (status początkowy to "Zaplanowany"). Firewall będzie aktywny, gdy jego zadanie aktualizacji nie pojawi się już na liście.

### Weryfikacja domen, dla których zapora jest aktywna

Zakładka `MultiSite`{.action} w Twoim pakiecie hostingowym zawiera informacje o domenach, dla których aktywowana jest opcja firewalla.

![gerageenabled](images/firewall-enabled.png){.thumbnail}

Wyświetlana tabela zawiera wszystkie nazwy domen dodanych do Twojego hostingu. W kolumnie "Firewall" wyświetla się status aktywacji każdej domeny.

## Sprawdź również

W przypadku wyspecjalizowanych usług (pozycjonowanie, rozwój, etc.) skontaktuj się z [partnerami OVHcloud](https://partner.ovhcloud.com/pl/directory/).

Jeśli chcesz otrzymywać wsparcie w zakresie konfiguracji i użytkowania Twoich rozwiązań OVHcloud, zapoznaj się z naszymi [ofertami pomocy](https://www.ovhcloud.com/pl/support-levels/).

Dołącz do społeczności naszych użytkowników na stronie <https://community.ovh.com/en/>.