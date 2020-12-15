### Jak zbudować przyzwoity monitoring sieci i serwerów 

Na potrzeby monitoringu różnych usług sieciowych oraz serwerowych można zastosować różne narzędzia do monitoringu popularne z nich to : zabbix, nagios, elastic-stack, telegraf, prometheus, fluentd i na pewno wiele innych. 

Ja zdecydowałem się na monitoring oparty na zabbix-ie który jest darmowy oraz posiada dużo modułów, gotowych dashboardów, programów ułatwiających tworzenie dashboardów. Zabbix posiada możliwośc monitoringu np przez sntp oraz swojego agenta który jest dostępny na bardzo wiele dystrybucji linuxowych i windowsowych. 

Niestety przynajmniej dla mnie graphy które są rysowane w zabbixie nie przypadły mi do gustu i trzeba było poszukać innego rozwiązania które może prezentować dane i jest takim agregatorem dla róznych narzędzi które moga monitorować i zbierać dane. Wybór padł na Grafane jest to narzędzie do prezentacji wykresów, obecnie też logów, posiada system alertów, no i rysuje ładne wykresy ;) 

Do zarządzania logami wybór padł na stack elastic'a, jest to bardzo dobre narzędzie do zarządzania logami, robienia z nich wykresów, obecnie cały stack rozrusł się bardzo mocno i zapewnia też SIEM, monitoring - realizowany za pomocą beatsów (małe programy w Go wydawane przez elastica do monitorowania wielu rzeczy).


Więc mój stack do monitorwania wygląda nastepująco Zabbix + ELK + Grafana

### 1. Elasticstack

Wykożystałem obraz dockerowy z https://github.com/deviantony/docker-elk 
