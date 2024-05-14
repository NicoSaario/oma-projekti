# Oma miniprojekti
Projekti on loppuhuipennus Palvelinten Hallinta - kurssille ja kaikki tehtävänannot löytyvät oheisesta linkistä: https://terokarvinen.com/2024/configuration-management-2024-spring/

Projekti on viimeinen osa tehtäviä - muut tehtävien suoritukset löytyvät täältä: https://github.com/NicoSaario/palvelinten-hallinta/blob/main/h6%20Benchmark.m

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

- Powerhsellin kotihakemistoon ```mkdir -p omaprojekti; cd omaprojekti ```
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

## Yhteydenotto
- Hypätään Windowssille ja tehtyyn vagranttiin
```vagrant ssh```
- Asennellaan ssh - palvelin
- Eipä tarvitse. Se on jo valmiina. Yritetään yhdistää juuri luotuun droplettiin
- ```ssh root@'dropletip'```
- Eipä tässä nyt mitään kauheen salaista oo, mutta piilotellaan nyt kuitenkin

- <img width="444" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/0b4948b5-9a54-4aad-8f1e-6df209f5029e">

- Laitellaan heti palomuuri, koska kyse on kuitenkin julkisesta pilvikoneesta

```sudo apt install ufw```

```systemctl status ufw```

<img width="425" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/e04961cf-fa05-4680-bc1e-8de8138fc0f2">

Jatketaan omia ohjeita:
- Lisätään käyttäjä ```sudo adduser nico```
- Lyödään se sudoryhmään
```sudo adduser nico sudo```
- Tsekataan, että se oikeesti toimii, ennenkö heitetään koko roottikäyttäjä ulos ```ssh nico@'dropletip'```
Siellähän se on, joten heitetään rootti ulos ```sudo usermod --lock root```

## Saltin asennus DigitalOcean - Master!

Kokeilin ensin peruskomentoa ```sudo apt-get install salt-master```, tämä ei kuitenkaan toiminut joten hyppään saltin omille sivuille ja katson nimenomaan Debian 12 - setuppia. https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/debian.html

- Jotta salt-päivitykset saadaan kiinnitettyä uusimpaan pakettiin Debian 12, pitää tehdä seuraava:

```
mkdir /etc/apt/keyrings

sudo curl -fsSL -o /etc/apt/keyrings/salt-archive-keyring-2023.gpg

https://repo.saltproject.io/salt/py3/debian/12/amd64/SALT-PROJECT-GPG-PUBKEY-2023.gpg

echo "deb [signed-by=/etc/apt/keyrings/salt-archive-keyring-2023.gpg arch=amd64] https://repo.saltproject.io/salt/py3/debian/12/amd64/latest bookworm main" | sudo tee /etc/apt/sources.list.d/salt.list

```

Tämän jälkeen ```sudo apt-get install salt-master```

- Sivuhuomio: Olisin varmaan voinut tehdä sen myös salt-cloudilla, mutta en vielä sen functiosta ole 100% varma, joten kokeillaan tätä ensin.

- Kuten näkyy, ```hostname -I``` - komennolla IP on sama, kuin DigitalOceanissa. Tämä pitää siis lyödä kiinni tuonne vagrantin tulevalle minionille

<img width="455" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/d3afe081-1a12-40ca-9a62-306b9c25cb69">


Minion (asennan nyt samalla myös micron, jotta säästän päänvaivaa. Onhan tämä vain kokeilu):

```
sudo apt-get update
sudo apt.get install micro
sudo apt-get install salt-minion
```

```sudoedit /etc/salt/minion```

Ja seuraava sisään: masterin osoite tulee siis edellä mainitusta esimerkistä hostname - I - kohdasta.

<img width="479" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/10d112e4-8c89-43ef-9887-e3ad897134bb">

Potkitaan demonia ```sudo systemctl restart salt-minion.service```

- Hyväksytään avain Digitalista: ```sudo salt-key -A ... Proceed y```
- Mitään ei tapahdu. Käyn katsomassa Teron Salt Quickstart - ohjeita ja https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/ lukee tuosta palomuuriasetuksista
- On siis avattava portit 4505/tcp ja 4506/tcp

```
sudo ufw allow 4505/tcp
sudo ufw allow 4506/tcp
```

Potkitaan sitäkin välillä: ```sudo sustemctl restart ufw```
Päällä on! 

<img width="427" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/0ba0bdd2-17ec-4957-b918-f77e040ef841">

- Hetken pohdiskelin, miksei avaimia tule näkyviin ja tarkistelin kaikki uudelleen. Kopion masterin IP-osoitteen uudelleen ja potkin salt-minionia, jolloin avain tuli näkyviin:

<img width="219" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/0ed1e199-c6ad-44f7-86d0-5bc8afb6769e">

- Tähän vain y ja avain on hyväksytty


# Testi
Tässä vaiheessa tärkeä testata, että orjan ja koneen välinen yhteys oikeasti toimii.

Luodaan kansio Digitalille ja hypätään sinne ```sudo mkdir -p /srv/salt/; cd /srv/salt/;```

- Sinne sisään: 

<img width="455" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/4d5d7560-e3b1-423b-82cf-34a3b8bb4e38">

Tehdään kansio ```sudo mkdir testi```
Sinne init.sls - tiedosto, jonka sisään:

<img width="478" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/3b858a02-0cf6-483d-a852-10fc7af327c6">

Ajetaan ja katsotaan, toimiiko: 

```sudo salt '*' state.apply```

Katsotaan vielä, että se tuli perille orjalle:

```cd /tmp```

<img width="387" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/28c15b86-621b-4d80-9b2c-3a983ebf0ce2">

Onnistuin siis juuri luomaan pilvipalvelun kautta Windowsin Vagrantille toimivan yhteyden joka ajaa tilan salt-call state.apply! Ihmettelen kyllä itsekkin vähän.

## Ohjelmien asenteluvaihe
- Luon lyhyen ja yksinkertaisen tiedoston kansioon /srv/salt/: ```sudo mkdir UsefulPrograms```
- Sinne sisään init.sls : micro init.sls


<img width="344" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/0b5e785d-6e78-4627-9025-264d1cd7494b">



- Muokataan myös top.sls - tiedostoa ja tehdään sinne lisäys UsefulPrograms, eli äsken luodun kansion nimi

<img width="474" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/83c579db-fd4c-4129-be3a-13476342c2ec">


Ajetaan ja kokeillaan: 

<img width="343" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/4f348b3b-0787-4fce-b564-448b6f648168">

Syy, miksi se näyttää pelkkää vihreätä valoa ja "All specified packages are already installed" johtuu siitä, että ajelin tuota useamman kerran testimielessä ja korjasin tämän sivun avulla https://www.debian.org/distrib/packages pakettien nimet, esimerkiksi firefox-esr

Kokeilin tehdä graafisen käyttöliittymän Vagrantille, mutta siitä ei nyt tullut mitään, mutta asentelen Debianin .iso - kuvakkeesta uuden virtuaalikoneen, koska haluan raporttia varten testata ne vielä GUI:n - kautta kuvankaappauksineen. Saapahan samalla testattua toimivuuden.

Kyseessä siis täysin puhtaan asennuksen jälkeen oleva kone. Tein ainoastaan edellämainitut salttikonfiguraatiot.

<img width="287" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/785794f3-13c6-45c4-9028-a84ecc1c8d23">

Siellä ollaan sisällä. Nyt lyödään state.apply päälle

<img width="278" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/3a45cbee-fd4c-4039-8d4b-99be7dcbd976">


<img width="327" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/9d1d5560-0846-48d0-832f-977bd213d466">


Wireshark:

<img width="637" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/9f87acd7-1693-44be-8300-32ffbbf816d9">

Microeditori:

<img width="629" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/18e215d3-22d0-4347-aa1f-1ee00dd28aa7">

Thunderbird: 

<img width="637" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/181387b1-c8b7-421e-a921-f7b2b79de9cd">

git:

<img width="449" alt="image" src="https://github.com/NicoSaario/oma-projekti/assets/156778628/8d792a77-cfc9-4d11-b0c3-7d53cde73844">


Salt install guide Debian, luettavissa: https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/debian.html (luettu 14.05.2024) 
https://www.debian.org/distrib/packages
