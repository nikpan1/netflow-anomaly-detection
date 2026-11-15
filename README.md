# Detekcja anomalii w ruchu sieciowym

Zbuduj detektor anomalii dla przepływów sieciowych (Tstat) z ośmiu sieci małych firm.
Dane: AIT Netflow Data Set (Zenodo 10.5281/zenodo.13168643, CC BY 4.0), przygotowane na potrzeby zajęć.

## Pliki

- `detector_notebook.ipynb` – notatnik do pracy (lokalnie albo w Google Colab),
- `train.csv.gz` – kilka dni **normalnego** ruchu wszystkich 8 sieci, bez etykiet,
- `test.csv.gz` – doba ataku w 5 z tych sieci, z etykietami: `label` (0/1), `phase` (faza ataku), `raw_label`.

Kolumny: `network`, `ts` (s, UTC), `duration` (s), `src_ip`, `src_port`, `dst_ip`, `dst_port`, `proto` (tcp/udp),
`state` (SF, S0, REJ, RSTO, RSTR, OTH), `bytes_out`, `bytes_in`, `pkts_out`, `pkts_in`, `sni`, `fqdn`.

W Colabie: prześlij notatnik, wrzuć `train.csv.gz` i `test.csv.gz` do plików sesji (ikona folderu po lewej),
*Środowisko wykonawcze → Uruchom wszystko*.

## Zadanie

Model ma dwie metody:

- `score(df)` – ryzyko dla każdego przepływu (im wyżej, tym bardziej podejrzany),
- `predict(df)` – decyzja dla każdego przepływu: 1 = alarm, 0 = brak alarmu.

Oddajesz plik **`model.pkl`** zapisany na końcu notatnika.

Fazy ataku w danych: `dns_brute_force`, `host_discovery`, `service_scan`, `web_scan`, `webshell`,
`online_cracking`, `dns_exfiltration`, `vpn_connect`.

## Zasady

- Tylko uczenie bez nadzoru: model uczy się na `train.csv.gz`. Etykiety z `test.csv.gz` służą wyłącznie do sprawdzania
  wyników – nie trenuj na nich modeli i nie wpisuj reguł wyczytanych z etykiet.
- Bez wpisanych na sztywno adresów, godzin czy nazw hostów.
- Biblioteki: numpy, pandas, scikit-learn, scipy, cloudpickle.
