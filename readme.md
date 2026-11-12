<!-- !/usr/bin/env markdown
-*- coding: utf-8 -*-
region header
Copyright Torben Sickert (info["~at~"]tsickert.com) 16.12.2012

License
-------

This library written by Torben Sickert stands under a creative commons naming
4.0 international license.
See https://creativecommons.org/licenses/by/4.0/deed.de
endregion -->


<!--|deDE:Projektstatus-->
<!--|frFR:État du projet-->
Project status
--------------

[![website](https://img.shields.io/website-up-down-green-red/https/tsickert.com/maintenancewebsite.svg?label=website&style=for-the-badge)](https://tsickert.com/maintenancewebsite)

<!--|deDE:Einsatzmöglichkeiten-->
<!--|frFR:Cas d'utilisation-->
Use case
--------

Maintenance-Website is a single self-contained HTML page you serve instead of
your real website while it is down for maintenance. It tells visitors that
the site will be back soon and still shows contact details and a legal
disclaimer. Styles are inlined, so it works even when every other service
behind your website is offline.
<!--deDE:
    Maintenance-Website ist eine einzelne, eigenständige HTML-Seite, die Sie
    anstelle Ihrer eigentlichen Webseite ausliefern, solange diese wegen
    Wartungsarbeiten nicht erreichbar ist. Sie teilt Besuchern mit, dass die
    Seite bald wieder verfügbar ist, und zeigt weiterhin Kontaktdaten und
    einen Haftungsausschluss. Die Stile sind eingebettet, sodass sie auch
    funktioniert, wenn alle anderen Dienste hinter Ihrer Webseite offline
    sind.
-->
<!--frFR:
    Maintenance-Website est une page HTML unique et autonome que vous servez
    à la place de votre véritable site pendant une maintenance. Elle informe
    les visiteurs que le site sera bientôt de retour et affiche toujours les
    coordonnées et un avertissement juridique. Les styles sont intégrés,
    elle fonctionne donc même lorsque tous les autres services derrière votre
    site sont hors ligne.
-->

See it live at
[tsickert.com/maintenancewebsite](https://tsickert.com/maintenancewebsite).
The page is available in American English, German and French. It picks the
visitor's browser language and offers links to switch manually. The switch is
done by
[web-internationalization](https://tsickert.com/web-internationalization)
loaded from a CDN. If it can not be loaded, the English version is shown.
<!--deDE:
    Live ansehen unter
    [tsickert.com/maintenancewebsite](https://tsickert.com/maintenancewebsite).
    Die Seite ist auf amerikanischem Englisch, Deutsch und Französisch
    verfügbar. Sie wählt die Browsersprache des Besuchers und bietet Links
    zum manuellen Umschalten. Das Umschalten übernimmt
    [web-internationalization](https://tsickert.com/web-internationalization),
    geladen von einem CDN. Kann es nicht geladen werden, wird die englische
    Version angezeigt.
-->
<!--frFR:
    Voir en ligne sur
    [tsickert.com/maintenancewebsite](https://tsickert.com/maintenancewebsite).
    La page est disponible en anglais américain, en allemand et en français.
    Elle choisit la langue du navigateur du visiteur et propose des liens
    pour changer manuellement. Le changement est assuré par
    [web-internationalization](https://tsickert.com/web-internationalization),
    chargé depuis un CDN. S'il ne peut pas être chargé, la version anglaise
    est affichée.
-->

<div class="wd-table-of-contents">
    <h2 id="content">Content<!--deDE:Inhalt--><!--frFR:Contenu--></h2>
    <!--wd-table-of-contents-->
</div>

Installation
------------

Pick whichever way fits your server. Both give you the same "index.html".
<!--deDE:
    Wählen Sie den Weg, der zu Ihrem Server passt. Beide liefern dieselbe
    "index.html".
-->
<!--frFR:
    Choisissez la méthode adaptée à votre serveur. Les deux fournissent le
    même "index.html".
-->

- On Arch Linux via the included "PKGBUILD": the file is installed to
  "/usr/lib/maintenanceWebsite.html".<!--deDE:Unter Arch Linux über das enthaltene "PKGBUILD": Die Datei wird nach "/usr/lib/maintenanceWebsite.html" installiert.--><!--frFR:Sous Arch Linux via le "PKGBUILD" fourni: le fichier est installé dans "/usr/lib/maintenanceWebsite.html".-->
- As plain download from GitHub.<!--deDE:Als einfacher Download von GitHub.--><!--frFR:Par simple téléchargement depuis GitHub.-->

```bash
# Arch Linux
git clone https://github.com/thaibault/maintenancewebsite.git
cd maintenancewebsite
makepkg --install

# Plain download
curl --output /usr/lib/maintenanceWebsite.html \
    https://raw.githubusercontent.com/thaibault/maintenancewebsite/main/index.html
```

<!--|deDE:Verwendung-->
<!--|frFR:Utilisation-->
Usage
-----

Answer every request with HTTP status "503 Service Unavailable" and this page
as body. The status code tells search engines and monitoring that the outage
is temporary. With nginx you can toggle maintenance mode by creating or
removing a flag file, without touching your configuration:
<!--deDE:
    Beantworten Sie jede Anfrage mit dem HTTP-Status "503 Service
    Unavailable" und dieser Seite als Inhalt. Der Statuscode signalisiert
    Suchmaschinen und Überwachungsdiensten, dass der Ausfall nur
    vorübergehend ist. Mit nginx schalten Sie den Wartungsmodus durch Anlegen
    oder Löschen einer Markierungsdatei um, ohne Ihre Konfiguration anzufassen:
-->
<!--frFR:
    Répondez à chaque requête avec le statut HTTP "503 Service Unavailable"
    et cette page comme contenu. Ce code indique aux moteurs de recherche et
    à la supervision que l'interruption est temporaire. Avec nginx, vous
    activez le mode maintenance en créant ou supprimant un fichier témoin,
    sans modifier votre configuration:
-->

```Nginx
server {
    # ...

    error_page 503 /maintenanceWebsite.html;

    location = /maintenanceWebsite.html {
        root /usr/lib;
        internal;
    }

    location / {
        if (-f /etc/nginx/maintenance) {
            return 503;
        }

        # Your regular configuration.
    }
}
```

```bash
touch /etc/nginx/maintenance # Enable maintenance mode.
rm /etc/nginx/maintenance    # Disable maintenance mode.
```

<!--|deDE:Anpassung-->
<!--|frFR:Personnalisation-->
Customization
-------------

The page is plain HTML without a build step. Copy "index.html" and adjust the
contact details, texts and the inline styles in its "head" to your needs.
Translations are written as HTML comments after each text, see
[web-internationalization](https://tsickert.com/web-internationalization).
<!--deDE:
    Die Seite ist einfaches HTML ohne Build-Schritt. Kopieren Sie
    "index.html" und passen Sie Kontaktdaten, Texte und die eingebetteten
    Stile im "head" nach Bedarf an. Übersetzungen stehen als HTML-Kommentare
    hinter jedem Text, siehe
    [web-internationalization](https://tsickert.com/web-internationalization).
-->
<!--frFR:
    La page est du HTML simple sans étape de build. Copiez "index.html" et
    adaptez les coordonnées, les textes et les styles intégrés dans son
    "head" selon vos besoins. Les traductions sont écrites sous forme de
    commentaires HTML après chaque texte, voir
    [web-internationalization](https://tsickert.com/web-internationalization).
-->
