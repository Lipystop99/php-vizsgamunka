# Követelményspecifikáció

## 1. Áttekintés
Ez a dokumentum egy cipőket árusító weboldal követelményeit tartalmazza. A weboldal három fő részből áll: a főoldal (vásárlóknak), az adminisztrációs felület (adminisztrátoroknak) és a regisztrációs oldal (új felhasználók számára).

## 2. Funkcionális követelmények

### 2.1. Főoldal
- **Terméklista megjelenítése**:  
  A főoldalon az elérhető cipők listája jelenik meg, amelyekhez a következő információk tartoznak:  
  - Név  
  - Ár  
  - Méretek  
  - Rövid leírás  
  - Képek  
  - Mennyiség

- **Kosár funkció**:  
  - A vásárlók hozzáadhatják a kiválasztott termékeket a kosarukhoz.
  - A kosár tartalma bármikor megtekinthető, módosítható (pl. darabszám változtatása, elem eltávolítása).

- **Vásárlási folyamat**:  
  - A vásárlók eldönthetik, hogy:  
    1. Bejelentkeznek-e a vásárláshoz.  
    2. Vendégként adják meg a szükséges adatokat (név, cím, elérhetőség).  
  - A vásárlás végén a vásárló a fizetési oldalon választja ki a fizetési módot és befejezheti a tranzakciót.

### 2.2. Adminisztrációs felület
- **Bejelentkezés adminisztrációs felületre**:  
  Az admin felülethez külön bejelentkezési folyamat szükséges.
  - Ahoz hogy be tudjon lépni kelleni fog egy hitelesítő kód is! 
  - Kód: (159753)  --> 2FA hitelesítési kód
  
- **Termékek kezelése**:  
  - Új termék hozzáadása: név, ár, méretek, leírás, képek feltöltése, raktáron lévő mennyiség megadása.  
  - Meglévő termékek szerkesztése (pl. ár módosítása, méretek frissítése, készlet frissítése).  
  - Termékek törlése.

### 2.3. Regisztrációs oldal
- **Felhasználói regisztráció**:  
  A felhasználóknak meg kell adniuk:  
  - E-mail cím 
  - Teljes név 
  - Felhasználónév  
  - Jelszó (hash-elve tárolva).

- **Adatbiztonság**:  
  - A jelszavakat megfelelő algoritmussal (pl. bcrypt) hash-eljük.

## 3. Nem funkcionális követelmények
- **Adatvédelem**:  
  Az ügyfelek és adminisztrátorok adatai biztonságosan tárolva legyenek. 
  
- **Rendszer teljesítmény**:  
  - A weboldal gyorsan betöltődjön, és a vásárlási folyamat ne legyen késleltetett.  
  
- **Skálázhatóság**:  
  A rendszer képes legyen egyszerre több felhasználó kiszolgálására.

- **Keresőoptimalizálás (SEO)**:  
  A főoldal optimalizált legyen a keresőmotorok számára.

## 4. Technikai követelmények
- **Frontend**:  
  - HTML, CSS, JavaScript (React).

- **Backend**:  
  - PHP és MySQL.

- **Szerver**:  
  - Linux alapú (pl. Ubuntu), Docker támogatással.

- **Adatbázis**:  
  - MySQL/MariaDB.

## 6. Dokumentáció

### **Felhasználói útmutató**:
A felhasználói útmutató célja, hogy segítse a vásárlókat és adminisztrátorokat az oldal használatában. A következő területek lefedése szükséges:

- **Regisztráció**:
  - A felhasználó hogyan regisztrálhat az oldalon, és hogyan hozzon létre fiókot.
    - A felhasználónak meg kell nyitni a <u>Regisztráció</u> fület, majd hiteles, érvényes adatokkar regisztrálni
    - Késöbbiekben lesz küldve egy email hitelesítő link is, amivel hitelesíteni tudja fiókját. 
        - Mindaddig, amíg ezt meg nem teszi a fiókja hitelesítettlen állapotban lesz feltüntetve.
  - A jelszó erőssége és a jelszó megújítása.
    - A felhasználónak egy legalább __10__ karakterekből összeálló jelszót kell kiválasztania, amely tartalmaz:
        - <u>Kis -és Nagy betűket
        - 0-9 -ig számokat
        - </u>-és <u>Írásjeleket</u> 
    - ezek után mi ezt a jelszót le _hash_-eljük, és úgy tároljuk az adatbázisban.

- **Bejelentkezés**:
  - Hogyan lehet bejelentkezni az oldalra a felhasználónév és jelszó segítségével.
    - A bejelentkezés egyszerű!
    - A felhasználó megkeresi a <u>Bejelentkezés</u>i menüpontot és megadja a regisztrálásnál használt adatokat.
  - Az elfelejtett jelszó visszaállítása.
    - Elfelejtett jelszó visszaállítása esetében egy külön oldalra visszük át az illetőt, ahol meg kell adnia az email címét és az ehez a fiókhoz megadott nevét.
    - Ha az adatok hitelesek, akkor engedélyt kap, hogy új jelszót állítson be.

- **Vásárlás**:
  - Hogyan adhatja hozzá a vásárló a termékeket a kosárhoz?
    - Ahoz hogy a termék a kosárba kerüljön rá kell nyomni a <u>__Kosárba__</u> gombra.
  - A rendelés véglegesítése és fizetési lehetőségek.
    - A rendelés véglegesítése úgy történik meg, hogy a felhasználó rákattint a __<u>Megrendelés</u>__ gombra. Ezzel le is zártuk a rendelést, és elkezdjük az összekészítést.
    - Fizetési lehetőségek:
        - A felhasználó képes fizetni a helyszínen: ___-készpénzzel, -kártyával, -utalvánnyal___
        - A felhasználó képes fizetni a kiszállított címen: ___-készpénzzel, -kártyával___
  - Az adatok megadása a szállításhoz (név, cím, elérhetőség).

- **Megrendelés kezelése**:
  - Hogyan nyomon követhető a megrendelés állapota és a vásárlás részletei.
    - A rendelések úgy követhetőek nyomon, hogy az illető kap róla egy email-t, a megrendelés pillanataban, majd kap még egy email-t, amikor átadtuk a futárszolgálatnak a csomagját.
        - Hogyha olyan eset lép érvénybe, hogy mi visszük ki a megrendelt csomagot, akkor az érkezés előtt felvesszük a kapcsolatot a megrendelővel telefonon.
  - A rendelés törlésének vagy módosításának lehetőségei.
    - A rendelés törlését két féle módon tudjuk megoldani:
    1. A megrendelő _Vendég_ -ként rendelte a csomagot:
        - Az email-ban küldött megrendelési szám alapján tudjuk törölni a rendelés, hogyha személyazonosságát igazolta.
    2. A megrendelő _Felhasználó_ -ként rendelte a csomagot:
        - A menüpontok között található egy olyan, hogy rendlések.
        - Abban megtalálja a felhasználó, amelyiket ki szeretné törölni, és egy egyszerű __Törlés__ gombra kattintással ez meg is oldható
        - __!!! A felhasználó csak a megrendelés leadását követő 6 órában tudja törölni rendelését !!!__
            - _Hogyha ez után szeretné törölni a megrendelését, ahoz sajnos <u>törlési felárat</u> kell felszámolnunk, melynek díja: **2.500 HUF** !!_

- **Adminisztrációs felület**:
  - Hogyan lehet bejelentkezni az adminisztrátori felületre.
    - Admin felületre ugyan úgy be lehet jelentkezni, mint egy sima felhasználó!
    - Annyi különbség van, hogy a sima felhasználó az "user" rangot kap, az admin 'felhasználó' pedig "admin" rangot kap, így nem lehet összekeverni a kettőt.
  - A termékek hozzáadásának, módosításának és törlésének folyamata.
    - A termékek hozzáadása külön oldalon történik, az ott bekért adatok hiteles, -és valós értékének megadásával.
    - A termékek módosítása is külön oldalon történik,
        - meg kell adnunk egy cikkszámot, az alapján a rendszer lekéri az adatokat, majd tudjuk módosítani.
        - a módosításról egy .log fájlban feljegyzés készül, így hogyha valaki nem jól rögzített valamit, azt vissz tudjuk keresni.
    - A termékek törlése, a __Termék Törlése__ menüpontra kattintva történik.
        - Itt szintén meg kell adnunk annak a terméknek a cikkszámát, amelyiket törölni szeretnénk, majd az oldal lekéri automatikusan az adatokat -és megjelníti számunkra.
        - Hogyha meggyőződtünk az adatok hitelességéről, hogy biztos ezt szeretnénk törölni, akkor a __Törlés__ gombra kattintva tehetjük ezt meg.
  - Megrendelések és felhasználók kezelése.
    - A megrendelések és felhasználók külön-külön táblában vannak eltárolva.
  - A jelszó módosítása és felhasználói jogosultságok kezelése.
    - A jelszó módoítást szintén ugyan úgy kell elvégezni mint egy normális Felhasználónál, ugyan azon a felületen.
    - A felhasználói jogosultságok kezelése is kapott egy külön menüpontot
        - Ebben a menüpontban ( __Jogosultságok kezelése__ ) latjuk az összes eddigi felhasználó felhasználó nevét, ID -ját, jogosultságát.
        - Ha egy felhasználónak ilyen joga van:
            1. _"user"_ (Felhasználó) -> Az ő jogát az "admin" is tudja módosítani
            2. _"admin"_ (Adminisztrátor) -> Az ő jogát csak is kizárólag a tulajdonos tudja módosítani.
            3. _"owner"_ (Tulajdonos) -> Az ő jogát csak a szerver üzemeltetője tudja módosítani terminálban!
