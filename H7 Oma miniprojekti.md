# Oma miniprojekti
Projekti on loppuhuipennus Palvelinten Hallinta - kurssille ja kaikki tehtävänannot löytyvät oheisesta linkistä: https://terokarvinen.com/2024/configuration-management-2024-spring/

Projekti on tehty Windows 11 - Home - käyttöjärjestelmällä, päivitykset ajettu 13/05/2024 asti.

AMD Ryzen 5 4500U, RAM 8 Gt.

Aika: Itä-Euroopan normaaliaika Aikavyöhyke: Suomi (UTC+2)

Powershell + Vagrant + DigitalOcean

Projektin tekeminen aloitettu 13.05.2024 klo 16.00

# Projektin idea ja tarkoitus

Kuvitteellisessa tilanteessa, sain työkutsun Amsterdamiin. En saa ottaa mukaani tietokonetta tai puhelinta kotioloista ja saan sieltä kaksi tietokonetta käyttööni, jotka molemmat pyörivät Linuxilla.
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

## DigitalOcean valmistelu
- Jokaisella palveluntarjoajalla on vähän omat nimet näille, mutta täällä se on Droplet.

<img width="750" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/944e895e-e489-449d-945a-9a4e813ee42e">

- Sitten valitaan serveri. Tästä paras ottaa se, mihin on pienin latenssi eli lähin mahdollinen. Sattumalta työpaikkakin sijaitsee Amsterdamissa, joten mennään sillä.

<img width="685" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/8d2640ac-d7ca-4c5d-a047-564a864e59da">

- Imagesta voi valita haluamansa, itse käytän Debian 12

<img width="605" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/e4212a82-96c6-40f2-b992-fbc05d56f384">


- Tilauksesta Basic- älä maksa siitä, mistä et mitään tiedä. 1GB/25GB Disk, sillä se riittää mainiosti tähän tilanteeseen muutenkin, koska ei puhuta mistään massiivisista tiedonsiirroista. 6$ kuukaudessa ei ole paha investointi siinä mielessä, että säästän huomattavasti työtunteja tämän avulla.
 
<img width="739" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/67836a3b-e687-4535-94d6-8712eaa11d65">

- Koska nyt on kyse vain päivän keikasta ja ajattelin ehkä deaktivoida tuon pilvipalvelun, valitsen nyt vain salasanan SSH - avaimen sijasta authentication - methodiksi. Syy on myös siinä, etten saanut ottaa mitään mukaan ja salasana on helppo muistaa. Tehdään siitä kuitenkin vaikea!!!

- Tähän hetkeen ei tarvita mitään ylimääräistä lisäpalveluita - Host name on hyvä olla joku julkisuuteen kelpaava, joka ei paljasta mitään ylimääräistä. Sitten menee noin 30s, kun se aktivoituu.



