### Jak zbudować przyzwoity monitoring sieci i serwerów 

Na potrzeby monitoringu różnych usług sieciowych oraz serwerowych można zastosować różne narzędzia do monitoringu popularne z nich to : zabbix, nagios, elastic-stack, telegraf, prometheus, fluentd i wiele innych. 

Ja zdecydowałem się na monitoring oparty na zabbix-ie który jest darmowy oraz posiada dużo modułów oraz gotowych dashboardów. Zabbix posiada możliwośc monitoringu np przez sntp oraz swojego agenta który jest dostępny na bardzo wiele dystrybucji linuxowych i windowsowych. 

Niestety przynajmniej dla mnie wykresy które są rysowane w zabbixie nie przypadły mi do gustu i trzeba było poszukać innego rozwiązania które może prezentować dane i jest takim agregatorem dla róznych systemów które mogą monitorować i zbierać dane. Wybór padł na Grafane która umożliwia wyświetlanie wykresów i danych z wielu róznych źródeł.

Do zarządzania logami wybór padł na stack elastic'a, jest to bardzo dobre narzędzie do zarządzania nimi. Obecnie cały stack zapewnia też SIEM, monitoring i wiele innych rzeczy. Dane logi, metryki są zbierane za pomocą beatsów (małe programy w Go wydawane przez elastica do monitorowania).


Więc mój stack do monitorwania wygląda nastepująco Zabbix + ELK + Grafana

### 1. Elasticstack

Wykożystałem obraz dockerowy z https://github.com/deviantony/docker-elk 


1. Pobieramy z gita obraz dla dockera :
```markdown
git clone https://github.com/deviantony/docker-elk.git
```
2. W pliku .env możemy wybrać wersję która ma się ściągnąć
3. Odpalamy docker-compose up -d
4. Następnie odpalamy skrypt który poustawia hasła do całego stacka 
```markdown
docker-compose exec -T elasticsearch bin/elasticsearch-setup-passwords auto --batch
```
5. Podmieniamy hasła które zostały wygenerowane 
```markdown
elasticsearch.username: kibana_system w kibana/config/kibana.yml

xpack.monitoring.elasticsearch.username: logstash_system w logstash/config/logstash.yml

podmieniamy hasło dla usera elastic w logstash/pipeline/logstash.conf
```

6. Resetartujemy ELK
```markdown
docker-compose restart kibana logstash
```
