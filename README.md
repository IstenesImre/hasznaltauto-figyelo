Powered by [icebob/hasznaltauto-figyelo](https://github.com/icebob/hasznaltauto-figyelo)
# hasznaltauto-figyelo
Ez az alkalmazás képes a hasznaltauto.hu oldalon beállított keresések találatainak figyelésére. Ha a találatok között megjelenik egy új elem, akkor arról e-mail értesítést küld a főbb adatokkal és az oldal linkjével.

## Telepítés
A telepítéshez vagy le kell klónozni ezt a tárolót
```
git clone https://github.com/istenesimre/hasznaltauto-figyelo.git
```
vagy letölteni [ZIP-ben](https://github.com/istenesimre/hasznaltauto-figyelo/archive/master.zip) és kicsomagolni.

Az alkalmazás NodeJS alapú, így szükséges [NodeJS telepítése](https://nodejs.org/en/download/package-manager/).

Telepítés után az alkalmazás mappájában ki kell adni az alábbi parancsot egy parancssorból a függőségek telepítéséhez:
```bash
npm install
```

Ha a parancs sikeresen lefutott akkor a program futtatható.

## Használat
A program futtatásához az alábbi parancsot kell kiadni parancssorban:
```bash
node index.js
```

## Konfigurálás
Az alkalmazás konfigurációja a `config.js` fájlban található.
A fájl szerkezete a következő:
```js
module.exports = {
	time: 10,
	dataDir: "./data",

	searches: [
		{
			id: "opel_caravan",
			name: "Opel Astra Caravan",
			url: "http://www.hasznaltauto.hu/talalatilista/auto/2G4ZLM6H4LHPDGMCKJQHZDH4T2PHATRPML46HMGZD5WYO4RCKTY1QY69R2S5GSOSA2LWHHFZA4RAMCAMTTFT3HQUMW3F0OZ9RMYDQRLYCCLDQW734RMFTH7Z2GZY31W1Y5WO6UISWJC1H9SOJT9Y8PY4YPLDTJ6905AHHT11QIF2HML0FAC2CIC9YEMGCW0W2EGOKOE9TEP0M1Q8PUF4C7FEJU22745MKGG2TY2F3F7HI5LR2EOTHH9UR2OQ499J2FM0DFAWMK9DQKHE3HZL7TG7LRAS8U1UE4II1IA5KLPZO0K6C1TS7G3ZUFOIUQK26WH61FY0Z7YT6JZRRIYE99KLOGY20WF3JJY6Y2KQAHKEJR6ZRUH970AUOMD/page1"
		}
	],

	telepulesID: 1843,
	maxDisance: 200,
	maxPrice: 2000000, 
	cookie: 'cookie=cookie; talalatokszama=100; results=100;',

	slackWebHook: "",

	email: {
		mailgunKey: "<PASTE HERE YOUR API KEY FROM MAILGUN.COM OR USE SMTP>",
		smtp: {
			host: 'smtp.yoursmtpserver.com',
			port: 465,
			secure: true, // secure:true for port 465, secure:false for port 587
			auth: {
				user: 'smtpmailaddress@example.com',
				cryptedPass: "19590f6521a29989569b3c5d718c4a1319b0f3054b"
			},
		},

		subject: "{0} új használtautó!",
		recipients: [
			"yourmail1@example.com",
			"yourmail2@example.com"
		]
	}
}
```

Beállítások leírása:

- **time**: a frissítési idő percekben. Ennyi időnként fut le a figyelés.
- **dataDir**: munkakönyvtár. Célszerű nem megváltoztatni.
- **searches**: a keresési linkeket tartalmazó tömb. Több elemet is tartalmazhat.
  - **id**: keresési azonosítója. Csak latin betűket és számokat tartalmazhat szóköz nélkül. Egy egyszerű név, a program a fájlnévként használja ezt az azonosítót. Lehet fantázianév, csak legyen **egyedi**.
  - **name**: a keresés beszédes fantázia neve (a parancssorban jelenik meg).
  - **url**: a keresés linkje. A hasznaltauto.hu oldalon összeállított kereséshez tartozó URL.
- **telepulesID** - a távolságszámításhoz használt település azonosító (hasznaltauto.hu oldalon lévő cookie-ból nyerhető id az adat).
- **maxDistance** - maximum távolság kilométerben, amin túl ignorálja a találatot.
- **maxPrice** - maximum ár, amin felül ignorálja a találatot.
- **cookie** - a kereséshez használt egyéb cookie mezők. Célszerű nem változtatni. 
- **email** - e-mail értesítéshez tartozó beállítások.
  - **mailgunKey** - a program az email küldéséhez a mailgun ingyenes szolgáltatását használja. Ehhez az oldalon be kell regisztrálni az ingyenes csomagra és az ott kapott `Secret API key`-t ide bemásolni.
  - **smtp** - email küldése SMTP szerveren keresztül.
   - **host** - SMTP szerver címe.
   - **port** - SMTP szerver portja. SSL/TLS: 465, nélküle 587.
   - **secure** - SSL/TLS: true, egyébként false.
   - **user** - SMTP felhasználónév.
   - **cryptedPass** - `Cryptr`-el titkosított jelszó.
  - **subject** - a levél fejléce. A `{0}` rész kicserélődik a talált új autók számára.
  - **recipients** - a címzettek e-mail címe. Több is megadható.

## License
[MIT license](https://tldrlegal.com/license/mit-license).
THX [icebob](https://github.com/icebob) Sensei!