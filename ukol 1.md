**Prvni krok: musime najit christmas special z roku 2014.**

Pri normalnim vyhledavani nic nenajdeme, protoze uz byl smazan. 

Ovsem pokud pouzijeme sql trik, muzeme zobrazit i uz smazane produkty.
```code
/rest/products/search?q=qwert%27))%20UNION%20SELECT%20id,name,description,price,deluxePrice,image,createdAt,updatedAt,deletedAt%20FROM%20Products--"
```
pokud toto zadame do url vyjede nam stranka se vsemi produkty, i temi smazanymi.

Zjistime ze vanocni special ma id 10,coz je velka vec.

<img width="1755" height="890" alt="Screenshot 2026-10-16 at 10 08 30" src="https://github.com/user-attachments/assets/092b5e95-a406-46e8-b402-6c0ea0ac3197" />

**Druhy krok: musime vanocni special vlozit do kosiku**

standartni cestou to nejde, ale muzeme ho pomoci nastroje burp

muzeme do kosiku vlozit libovolny produkt, zastavit pozadavek POST a zmenit productId na hodnotu 10

<img width="1589" height="868" alt="Screenshot 2026-10-16 at 10 31 02" src="https://github.com/user-attachments/assets/722f590c-074e-45d6-840e-b4532042eb20" />

Nasledne v kosiku uvidime vanocni special

<img width="1074" height="377" alt="Screenshot 2026-10-16 at 10 33 27" src="https://github.com/user-attachments/assets/b0eb1013-b727-417b-8627-3c2b1ac9dc61" />

**Treti krok: padelani kuponu**
Juice shop zverejnil prispevek, ve kterem poskytuje slevovy kod:

<img width="601" height="120" alt="Screenshot 2026-10-16 at 10 41 17" src="https://github.com/user-attachments/assets/f205672d-a156-46b5-8302-d8e1445cfe51" />

Tento kod neni nahodny, ale je zakodovany pomoci Z85(ZeroMQ) 

Pokud ho rozsifrujeme, dostaneme text OCT26-40

<img width="1750" height="676" alt="Screenshot 2026-10-16 at 10 42 37" src="https://github.com/user-attachments/assets/518143e1-3c07-441c-934a-b2dd8173dd6b" />

Z toho je videt struktura kuponu: prvni tri pismena mesice, rok a procentni sleva za pomlckou

Pokud teda ze 40 udelame 50, dostaneme kod novy: pEw8phz3^u

<img width="1760" height="740" alt="Screenshot 2026-10-16 at 10 44 31" src="https://github.com/user-attachments/assets/25a9fd13-195b-4802-9753-c068ad6bef6d" />

Tento kod potom muzu pouzit v kosiku

<img width="1045" height="750" alt="Screenshot 2026-10-16 at 10 45 16" src="https://github.com/user-attachments/assets/627210e9-4df7-406c-aa55-88a59b5c0eeb" />

Vzali ho jako 50% slevu

<img width="1763" height="895" alt="Screenshot 2026-10-16 at 10 45 55" src="https://github.com/user-attachments/assets/4caa6199-25be-4736-a70a-eb05493afce0" />

Finalni screenshot jako dukaz uspesne objednavky

Tento text jsem psal vlastnima rukama



