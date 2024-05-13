# Oma miniprojekti
Projekti on loppuhuipennus Palvelinten Hallinta - kurssille ja kaikki tehtävänannot löytyvät oheisesta linkistä: https://terokarvinen.com/2024/configuration-management-2024-spring/

Projekti on tehty Windows 11 - Home - käyttöjärjestelmällä, päivitykset ajettu 13/05/2024 asti.

AMD Ryzen 5 4500U, RAM 8 Gt.

Aika: Itä-Euroopan normaaliaika Aikavyöhyke: Suomi (UTC+2)

Powershell + Vagrant + DigitalOcean

# Projektin idea ja tarkoitus

Kuvitteellisessa tilanteessa, sain työkutsun Keniaan. En saa ottaa mukaani tietokonetta tai puhelinta kotioloista ja saan sieltä kaksi tietokonetta käyttööni, jotka molemmat pyörivät Linuxilla.
Työtehtävät liittyvät Linuxin parissa toimimiseen ja minulla on yksi päivä aikaa tehdä lähtövalmistelut. 

Ajattelin siis tekeväni lähtövalmisteluita varten valmiit asennukset ohjelmille, joita tarvitsen, jotta siirtymä onnistuu mahdollisimman sujuvasti. 
Tässä hyödynnän pilvipalvelun vuokraamista DigitalOcean - palvelusta, jotta pystyn yhdistämään sen ja asentamaan sitä kautta ilman omaa, fyysistä läppäriäni.

Teen siis Pilvipalvelusta master - koneen, jolla asentelen orjille seuraavat ohjelmat hyödyntäen herra-orja-arkkitehtuuria, jotka ainakin aluksi ovat tarpeellisia itselleni:

- Micro
- Apache
- Firefox
- Spotify
- Thunderbird
- Git
- Wireshark


## Suoritus

Koska pääsen käsittääkseni DigitalOceaniin kiinni käytännössä mistä vain, teen alkuvalmisteluina PowerShellin ja Vagrantin yhteistyölle kansion 'omaprojekti', johon VagrantFile tulee. 
Pitää tehdä vielä toinen kone, joka toimii sitten orjana testaamiseen.
Powerhsellin kotihakemistoon ```mkdir -p omaprojekti; cd omaprojekti ```
Tämä luo kansion, johon ```vagrant init debian/bullseye64```
Tämän jälkeen käynnistellään vagrant ```vagrant up``` - komennolla

- Käytän hyväkseni aikaisempaa Linux Palvelimet kurssia ja GitHubin Student - pakettia, jonka ansiosta käytössäni on jo valmiiksi DigitalOcean ja sinne muistaakseni 200€ crediittejä.
- Tuosta löytyy ohjeet, joita noudattelen samalla: https://github.com/NicoSaario/Linux_Palvelimet/blob/main/h4%20Maailma%20kuulee.md
- 

