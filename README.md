# 🏢 SlothLite - Sistem za upravljanje kompanijom

**SlothLite** je informacioni sistem za upravljanje kompanijom koji pokriva osnovne tokove od upravljanja zaposlenima i projektima, preko praćenja realizacija i odsustva, do upravljanja klijentima i timovima. Cilj je centralizacija poslovnih procesa, poboljšanje transparentnosti i efikasniji menadžment resursa.

---

## 📚 Sadržaj
- [Domen, cilj i motivacija](#domen-cilj-i-motivacija)
- [Opis sistema](#opis-sistema)
- [Entiteti i odnosi (sažetak)](#entiteti-i-odnosi-sažetak)
- [Obim projekta](#obim-projekta)
- [Obavezni EER koncepti](#obavezni-eer-koncepti)
- [Plan kontrolnih tačaka](#plan-kontrolnih-tačaka)
- [CASE alat i dijagrami](#case-alat-i-dijagrami)
- [Licenca i autori](#licenca-i-autori)

---

## 🎯 Domen, cilj i motivacija
- **Domen:** upravljanje kompanijom (zaposleni → projekti → realizacije → odsustva → klijenti → timovi).
- **Problem:** fragmentovani procesi, nedostaje jedinstveno mesto za praćenje rada zaposlenih, realizacija projekata, upravljanje odsustvima i komunikacije sa klijentima. Ručno vođenje evidencija dovodi do grešaka i neefikanosti.
- **Cilj:** centralizovan IS koji omogućava kompletno upravljanje poslovnim procesima kroz jedinstvenu platformu sa jasno definisanim ulogama i pravima pristupa.

---

## 🔍 Opis sistema

U sistemu postoje **zaposleni** koji se identifikuju po jedinstvenom broju zaposlenog. Svaki zaposleni ima osnovne informacije kao što su ime, prezime, email, pozicija i datum zapošljavanja. Zaposleni mogu biti **menadžeri** ili **izvršioci**, gde menadžeri imaju dodatne privilegije kao što je odobravanje odsustva i pristup izveštajima.

Svaki zaposleni pripada jednom ili više **timova**. Tim ima naziv, opis i **team leadera** koji je odgovoran za koordinaciju rada. Timovi rade na različitim **projektima** za **klijente**. 

**Klijent** se karakteriše nazivom kompanije, kontakt osobom, emailom i adresom. Jedan klijent može imati više projekata, a svaki projekt pripada tačno jednom klijentu.

**Projekat** ima naziv, opis, datum početka, planirani datum završetka i status (aktivan, pauziran, završen). Na projektu može raditi više timova, a svaki tim može biti angažovan na više projekata istovremeno.

Zaposleni beleže svoja dnevna **ostvarenja** (realizacije) gde specificiraju na kom projektu su radili, koliko vremena su utrošili, opis aktivnosti i datum. Ostvarenje pripada jednom zaposlenom i vezano je za jedan projekat.

Sistem takođe vodi evidenciju o **odsustvima** zaposlenih. Postoje različiti **tipovi odsustva** kao što su godišnji odmor, bolovanje, neplaćeno odsustvo, službeni put. Svako odsustvo ima datum početka, datum završetka, tip odsustva, razlog i status (zatraženo, odobreno, odbačeno). Odsustvo zatražuje zaposleni, a odobrava menadžer.

Sistem takođe vodi evidenciju o **sastancima** gde se beleži datum, učesnici (zaposleni), tema, zaključci i povezanost sa projektom.

Za potrebe izveštavanja, sistem generiše **izveštaje** o ostvarenjima zaposlenih, napredovanju projekata, iskorišćenosti timova i analizi odsustva.

---

## 🧩 Entiteti i odnosi (sažetak)
**Entiteti:** Zaposleni, Tim, Projekat, Klijent, Ostvarenje, Tip odsustva, Odsustvo, Tim-Projekt (*gerund*), Sastanak (*slabi*), Izveštaj, Menadžer (IS-A), Izvršilac (IS-A), Kategorija projekta (*kategorizacija*).

**Ključni odnosi:**
- **Zaposleni** ↔ **Tim** preko **Članstvo** (*M:N*, Članstvo nosi atribute kao što je uloga u timu).
- **Tim** ↔ **Projekat** preko **Tim-Projekt** (*M:N*, gerund nosi datum pridruživanja i ulogu tima).
- **Klijent** → **Projekat** (*1:M*).
- **Zaposleni** → **Ostvarenje** (*1:M*), **Ostvarenje** → **Projekat** (*M:1*).
- **Zaposleni** → **Odsustvo** (*1:M*), **Odsustvo** → **Tip odsustva** (*M:1*).
- **Zaposleni** → **Zaposleni** (rekurzivni *1:M*, nadređen–podređen).
- **Zaposleni** IS-A **Menadžer**, **Izvršilac**.
- **Projekat** → **Kategorija projekta** (*M:1*, kategorizacija).
- **Projekat** → **Sastanak** (*1:M*, slabi ID-zavisan entitet).

---

## 📏 Obim projekta
Obim je planiran na **≈15 tipova entiteta** sa odgovarajućim tipovima poveznika. IS-A hijerarhija se računa kao **jedan** tip entiteta u ukupnom obimu.

---

## 🧠 Obavezni EER koncepti
- **Gerund**: *Tim-Projekt* (povezuje Tim i Projekat, nosi atribute kao što su datum pridruživanja i uloga).
- **Rekurzivni TP**: Zaposleni —nadređen→ Zaposleni (*1:M*).
- **Slabi ID-zavisni TE**: *Sastanak* (identifikujuća veza sa Projektom).
- **IS-A hijerarhija**: Zaposleni → Menadžer, Izvršilac.
- **Kategorizacija**: Projekat → Kategorija projekta.

*Svi ovi koncepti su obavezni i moraju se pojaviti u finalnoj šemi.*

---

## 🗺️ Plan kontrolnih tačaka
- **KT1 – Specifikacija** (ovaj dokument).  
- **KT2 – ER dijagram + opis TE/TP** (SQL Developer Data Modeler).  
- **Final – Relacioni model + SQL skripte + implementacija i test podaci.**

---

## 🛠️ CASE alat i dijagrami
- Za modeliranje koristi se **SQL Developer Data Modeler**.
- Voditi računa o čitljivosti dijagrama (izbegavati preklapanja linija).
- ER dijagram služi kao osnova za generisanje relacionog modela.

---

## 📄 Licenca i autori
- **Licenca:** MIT  
- **Autor:** _Marko Sladojević_ — _SV33/2025_.  
- **Predmet/Asistent:** Baze podataka — _Jelena Hrnjak_.
