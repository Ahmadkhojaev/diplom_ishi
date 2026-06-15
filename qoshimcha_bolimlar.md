# Diplom ishiga qo'shimcha bo'limlar (yetishmayotgan mavzular)

> Quyidagi matnlar diplom uslubida, xalqaro standartlar (NIST FIPS, RFC, ISO/IEC)
> va klassik akademik manbalarga asoslanib yozilgan. Har bir qism mos bo'limga
> (1.1 va 1.2) qo'shilishi mumkin. Iqtiboslar [raqam] ko'rinishida berilgan;
> ularni adabiyotlar ro'yxatidagi tartibingizga moslab qayta raqamlang.

---

## 1.1-bo'limga qo'shimcha: Kriptografik himoyalash usullarining tasnifi

Zamonaviy kriptografiyada axborotni himoyalash usullari kalitlardan foydalanish
prinsipiga ko'ra ikkita asosiy sinfga bo'linadi: **simmetrik (maxfiy kalitli)
kriptografiya** va **asimmetrik (ochiq kalitli) kriptografiya**. Bundan tashqari,
ma'lumotlar yaxlitligini ta'minlovchi **xesh funksiyalar** mustaqil yo'nalish
sifatida ajratiladi. Ushbu uchta yo'nalish birgalikda axborot xavfsizligining
asosiy maqsadlari — maxfiylik (confidentiality), yaxlitlik (integrity),
autentifikatsiya (authentication) va rad eta olmaslik (non-repudiation) ni
ta'minlaydi [1, 2].

### 1.1.1. Simmetrik (maxfiy kalitli) shifrlash usullari

Simmetrik kriptografiyada shifrlash va deshifrlash uchun bitta umumiy maxfiy
kalitdan foydalaniladi. Jo'natuvchi va qabul qiluvchi oldindan bir xil kalitga
ega bo'lishlari shart, shuning uchun bu usulning asosiy muammosi — kalitni
xavfsiz almashtirish (key distribution) hisoblanadi [1].

Simmetrik shifrlar ikkita asosiy turga bo'linadi:

1. **Blokli shifrlar (block ciphers):** ma'lumotni belgilangan o'lchamdagi
   bloklarga (masalan, 64 yoki 128 bit) bo'lib shifrlaydi. Eng mashhur misollar:
   - **DES (Data Encryption Standard)** — 1977-yilda AQSh standarti sifatida
     qabul qilingan, 64-bitli blok va 56-bitli kalitdan foydalanadi. Kalit
     uzunligi qisqaligi sababli, bugungi kunda qo'pol kuch (brute-force)
     hujumlariga zaif hisoblanadi va eskirgan deb tan olingan [3].
   - **AES (Advanced Encryption Standard, FIPS 197)** — 2001-yilda NIST
     tomonidan Rijndael algoritmi asosida qabul qilingan. AES 128-bitli
     bloklar bilan ishlaydi va 128, 192 yoki 256-bitli kalitlardan foydalanadi.
     U substitution-permutation network (SPN) tuzilishiga asoslangan bo'lib,
     hozirgi kunda eng keng tarqalgan simmetrik shifr hisoblanadi [4].

2. **Oqimli shifrlar (stream ciphers):** ma'lumotni bit yoki bayt darajasida,
   psevdotasodifiy kalit oqimi (keystream) bilan XOR amali orqali shifrlaydi.
   Misollar: RC4 (eskirgan), ChaCha20 (zamonaviy, RFC 8439).

Simmetrik shifrlashning afzalligi — yuqori tezlik va kam hisoblash resursi
talab qilishi. Shu sababli katta hajmdagi ma'lumotlarni shifrlashda asosan
simmetrik algoritmlar ishlatiladi. Kamchiligi — kalitni xavfsiz almashtirish
muammosi va foydalanuvchilar soni ko'paygan sayli kalitlar sonining keskin
oshishi (n ta foydalanuvchi uchun n(n-1)/2 ta kalit) [1, 2].

### 1.1.2. Asimmetrik (ochiq kalitli) kriptografiya

Ochiq kalitli kriptografiya 1976-yilda Whitfield Diffie va Martin Hellman
tomonidan taklif etilgan bo'lib, simmetrik tizimning kalit almashtirish
muammosini hal qiladi [5]. Bu yondashuvda har bir foydalanuvchi matematik
jihatdan o'zaro bog'liq bo'lgan ikkita kalitga ega bo'ladi:

- **Ochiq kalit (public key)** — hammaga oshkor qilinadi va xabarni shifrlash
  yoki imzoni tekshirish uchun ishlatiladi;
- **Maxfiy kalit (private key)** — faqat egasida saqlanadi va deshifrlash yoki
  imzo qo'yish uchun ishlatiladi.

Ochiq kalit yordamida shifrlangan ma'lumotni faqat mos maxfiy kalit egasi
ocha oladi. Bu tizimlarning xavfsizligi yechilishi qiyin bo'lgan matematik
masalalarga asoslanadi:

- **RSA (Rivest–Shamir–Adleman, 1977)** — katta sonlarni tub
  ko'paytuvchilarga ajratish (integer factorization) masalasining
  murakkabligiga tayanadi. RSA shifrlash va raqamli imzo uchun ishlatiladi
  hamda RFC 8017 (PKCS #1) va FIPS 186-5 standartlarida rasmiylashtirilgan [6, 7].
- **Diffie–Hellman kalit almashinuvi** — diskret logarifm masalasiga
  asoslanib, ikki tomonga ishonchsiz kanal orqali umumiy maxfiy kalit hosil
  qilish imkonini beradi [5].
- **Elliptik egri chiziqlar kriptografiyasi (ECC)** — elliptik egri
  chiziqlardagi diskret logarifm masalasiga asoslanadi. ECC RSA bilan bir xil
  xavfsizlik darajasini ancha kichik kalit uzunligida ta'minlaydi (masalan,
  256-bitli ECC ≈ 3072-bitli RSA), shu sababli resurslari cheklangan
  qurilmalar uchun samaralidir. NIST SP 800-186 da egri chiziq parametrlari
  belgilangan [7, 8].

Asimmetrik kriptografiyaning afzalligi — kalit almashtirish muammosini hal
qilishi va raqamli imzo imkoniyatini berishi. Kamchiligi — simmetrik
algoritmlarga nisbatan ancha sekin ishlashi. Amaliyotda ko'pincha
**gibrid sxema** qo'llaniladi: katta ma'lumot simmetrik kalit (masalan, AES)
bilan shifrlanadi, simmetrik kalitning o'zi esa qabul qiluvchining ochiq
kaliti (RSA/ECC) bilan shifrlanib uzatiladi [1, 2].

---

## 1.2-bo'limga qo'shimcha: Axborot butunligini ta'minlovchi kriptografik usullar

Axborot butunligi (data integrity) deganda ma'lumot uzatish yoki saqlash
jarayonida ruxsatsiz yoki tasodifiy o'zgartirilmaganligiga ishonch hosil qilish
tushuniladi. Kriptografiyada butunlikni ta'minlashning to'rtta asosiy mexanizmi
mavjud: **kriptografik xesh funksiyalar**, **xabar autentifikatsiyasi kodlari
(MAC)**, **HMAC** va **elektron raqamli imzo (ERI)**. Bu mexanizmlar nafaqat
ma'lumotning o'zgartirilmaganligini, balki ba'zi hollarda uning manbasini
(autentifikatsiya) va kelib chiqishini (rad eta olmaslik) ham tasdiqlaydi [1, 2].

### 1.2.1. Kriptografik xesh funksiyalar yordamida butunlik

Kriptografik xesh funksiya H ixtiyoriy uzunlikdagi xabarni belgilangan
uzunlikdagi qiymatga (dayjest) aylantiradi: H: {0,1}* → {0,1}^n. Butunlikni
tekshirish uchun xabar uzatishdan oldin va keyin uning xesh qiymati hisoblanadi;
agar ikkala qiymat mos kelsa, ma'lumot o'zgartirilmagan deb hisoblanadi.

Bu mexanizmning ishonchliligi xesh funksiyaning quyidagi xususiyatlariga
bog'liq: birinchi obrazga chidamlilik (preimage resistance), ikkinchi obrazga
chidamlilik (second-preimage resistance) va to'qnashuvga chidamlilik (collision
resistance) [1]. SHA-2 (FIPS 180-4) va SHA-3 (FIPS 202) bugungi kunda tavsiya
etilgan standart xesh funksiyalardir [9, 10].

Biroq, oddiy xesh funksiyaning o'zi faqat **tasodifiy** xatolarni aniqlaydi:
agar tajovuzkor ham xabarni, ham uning xesh qiymatini birga o'zgartira olsa,
buni aniqlab bo'lmaydi. Shu sababli **qasddan qilingan** o'zgartirishlardan
himoyalanish uchun maxfiy kalitga asoslangan mexanizmlar (MAC, HMAC) yoki
ochiq kalitli imzo (ERI) qo'llaniladi [1, 2].

### 1.2.2. Xabar autentifikatsiyasi kodi (MAC)

Xabar autentifikatsiyasi kodi (Message Authentication Code, MAC) — bu xabar va
maxfiy kalitdan hisoblanadigan qisqa teg bo'lib, u bir vaqtning o'zida ham
butunlikni, ham manba autentifikatsiyasini ta'minlaydi. Jo'natuvchi va qabul
qiluvchi umumiy maxfiy kalitga ega bo'ladi: jo'natuvchi MAC = MAC(K, M) ni
hisoblab xabar bilan birga yuboradi, qabul qiluvchi esa o'zida qayta hisoblab,
qiymatlar mos kelishini tekshiradi [1, 11].

MAC qurishning bir necha usuli mavjud:
- **Xesh funksiyaga asoslangan MAC:** masalan, HMAC (quyida batafsil).
- **Blokli shifrga asoslangan MAC:** masalan, CMAC (NIST SP 800-38B) yoki
  CBC-MAC. ISO/IEC 9797 standarti blokli shifrga asoslangan MAC algoritmlarini
  belgilaydi [11].

MAC ning raqamli imzodan asosiy farqi shundaki, u **simmetrik** kalitdan
foydalanadi. Shu sababli MAC rad eta olmaslik (non-repudiation) xususiyatini
ta'minlamaydi — chunki kalit ikkala tarafda ham mavjud bo'lgani uchun, qabul
qiluvchi ham xuddi shunday teg yarata oladi [1].

### 1.2.3. HMAC (Keyed-Hash Message Authentication Code)

HMAC — bu kriptografik xesh funksiya va maxfiy kalit kombinatsiyasidan
foydalanadigan MAC turi. U dastlab Bellare, Canetti va Krawczyk tomonidan
taklif etilgan (RFC 2104, 1997) va keyinchalik NIST tomonidan FIPS 198-1
(2008) standarti sifatida qabul qilingan [12, 13].

HMAC quyidagi formula bo'yicha hisoblanadi:

    HMAC(K, M) = H( (K ⊕ opad) ‖ H( (K ⊕ ipad) ‖ M ) )

bu yerda H — xesh funksiya (masalan, SHA-256), K — maxfiy kalit, M — xabar,
ipad va opad — oldindan belgilangan to'ldiruvchi konstantalar, ‖ —
konkatenatsiya, ⊕ — XOR amali.

HMAC ning afzalliklari: ixtiyoriy iterativ xesh funksiya bilan ishlay olishi,
xeshga asoslangan sodda sxemalarni buzadigan uzunlik-kengaytma
(length-extension) hujumlariga bardoshli bo'lishi va xavfsizligi matematik
jihatdan isbotlanganligi [12]. HMAC bugungi kunda TLS, IPsec, JWT kabi ko'plab
protokollarda keng qo'llaniladi.

### 1.2.4. Elektron raqamli imzo (ERI)

Elektron raqamli imzo (Digital Signature) — ochiq kalitli kriptografiyaga
asoslangan mexanizm bo'lib, u bir vaqtning o'zida uchta xizmatni ta'minlaydi:
**butunlik**, **autentifikatsiya** va **rad eta olmaslik (non-repudiation)** [7].

Imzo jarayoni quyidagicha amalga oshiriladi:
1. Jo'natuvchi xabarning xesh qiymatini hisoblaydi: h = H(M).
2. Ushbu xesh qiymatini o'zining **maxfiy kaliti** bilan shifrlaydi (imzolaydi):
   S = Sign(privKey, h).
3. Xabar M va imzo S birga uzatiladi.
4. Qabul qiluvchi jo'natuvchining **ochiq kaliti** yordamida imzoni tekshiradi:
   xabardan qayta hisoblangan xesh qiymati imzodan tiklangan qiymatga mos
   kelsa, imzo haqiqiy hisoblanadi.

ERI xeshlash bilan birgalikda ishlatilishi sababli, butun xabarni emas, balki
uning kichik, doimiy o'lchamdagi dayjestini imzolash kifoya qiladi — bu
samaradorlikni oshiradi [1, 7].

Raqamli imzoning MAC dan asosiy ustunligi — **rad eta olmaslik** xususiyati:
imzo faqat maxfiy kalit egasi tomonidan yaratilishi mumkin bo'lgani uchun,
jo'natuvchi keyinchalik imzodan voz kecha olmaydi. NIST FIPS 186-5 (2023)
standarti uchta raqamli imzo algoritmini belgilaydi: **RSA**, **ECDSA**
(elliptik egri chiziqlarga asoslangan) va **EdDSA** (Edwards egri chiziqlari,
masalan Ed25519) [7].

### 1.2.5. Usullarning qiyosiy tahlili

| Mexanizm | Kalit turi | Butunlik | Autentifikatsiya | Rad eta olmaslik |
|----------|-----------|----------|------------------|------------------|
| Xesh funksiya | Kalitsiz | Faqat tasodifiy xatolar | Yo'q | Yo'q |
| MAC / HMAC | Simmetrik (umumiy) | Ha | Ha | Yo'q |
| Raqamli imzo (ERI) | Asimmetrik | Ha | Ha | Ha |

Jadvaldan ko'rinib turibdiki, mexanizm tanlash xavfsizlik talablariga bog'liq:
faqat tasodifiy buzilishlarni aniqlash uchun xesh kifoya; ishonchli tomonlar
o'rtasida tezkor autentifikatsiya uchun HMAC mos; huquqiy ahamiyatga ega,
rad etib bo'lmaydigan tasdiqlash zarur bo'lganda esa raqamli imzo qo'llaniladi
[1, 2].

---

## Foydalanish mumkin bo'lgan akademik va standart manbalar

**Klassik darsliklar (har qanday universitet diplomida iqtibos qilsa bo'ladi):**

1. A. J. Menezes, P. C. van Oorschot, S. A. Vanstone. "Handbook of Applied
   Cryptography". CRC Press, 1996. (Bepul onlayn: cacr.uwaterloo.ca/hac)
2. W. Stallings. "Cryptography and Network Security: Principles and Practice".
   Pearson. (Simmetrik/asimmetrik shifrlash, MAC, imzo bo'limlari uchun)
3. J. Katz, Y. Lindell. "Introduction to Modern Cryptography". CRC Press.
4. B. Schneier. "Applied Cryptography". Wiley.

**Rasmiy standartlar (eng ishonchli birlamchi manbalar):**

5. W. Diffie, M. Hellman. "New Directions in Cryptography". IEEE Transactions
   on Information Theory, 1976.
6. R. Rivest, A. Shamir, L. Adleman. "A Method for Obtaining Digital Signatures
   and Public-Key Cryptosystems". Communications of the ACM, 1978.
   (RSA — RFC 8017 / PKCS #1 da rasmiylashtirilgan)
7. NIST FIPS 186-5. "Digital Signature Standard (DSS)". 2023.
   (https://csrc.nist.gov/pubs/fips/186-5/final)
8. NIST SP 800-186. "Recommendations for Discrete Logarithm-Based Cryptography:
   Elliptic Curve Domain Parameters". 2023.
9. NIST FIPS 180-4. "Secure Hash Standard (SHS)" — SHA-2 oilasi.
10. NIST FIPS 202. "SHA-3 Standard: Permutation-Based Hash and Extendable-Output
    Functions". 2015.
11. NIST SP 800-38B. "Recommendation for Block Cipher Modes of Operation: The
    CMAC Mode for Authentication"; ISO/IEC 9797 (MAC algoritmlari).
12. H. Krawczyk, M. Bellare, R. Canetti. "HMAC: Keyed-Hashing for Message
    Authentication". RFC 2104, 1997. (https://www.rfc-editor.org/rfc/rfc2104)
13. NIST FIPS 198-1. "The Keyed-Hash Message Authentication Code (HMAC)". 2008.
14. NIST FIPS 197. "Advanced Encryption Standard (AES)". 2001.
    (https://csrc.nist.gov/pubs/fips/197/final)
