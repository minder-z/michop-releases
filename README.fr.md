<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Prêtez le micro de ce Mac à un autre Mac.</b><br>
  Vous parlez sur celui-ci, et l’autre se comporte comme s’il avait un micro branché ; en réseau local ou via Tailscale.<br>
  <sub>Lend your Mac's microphone to another Mac — live and encrypted, over LAN or Tailscale.</sub>
</p>

---

## À quoi ça sert

Je travaille d’habitude sur un MacBook et je me connecte à un Mac mini avec un logiciel de bureau à distance (UU Remote, Sunlogin, ToDesk, etc.) pour y travailler : faire écrire du code à Claude Code, monter des vidéos, entretenir des sites web…

Le problème : **le Mac mini n’a pas de micro, et le logiciel de bureau à distance ne transmet pas celui du MacBook**. Impossible donc d’utiliser la saisie vocale dans le bureau à distance.

C’est précisément ce que résout MicHop. Installez une app sur chacun des deux ordinateurs :

- **L’ordinateur sur lequel vous parlez** (par exemple le MacBook) : installez « MicHop »
- **L’ordinateur sur lequel vous travaillez** (par exemple le Mac mini) : installez « MicHop Receiver »

```
MacBook (vous parlez)                        Mac mini (vous travaillez)

Micro ────── 🔊 son ──────────────►  Micro virtuel (MicHop Audio intégré)
                                      → Dictée / WeChat Input Method / mode vocal de Claude Code

              via le réseau local ou Tailscale
```

Le son du micro du MacBook arrive en temps réel sur le Mac mini et devient le micro du Mac mini. Toutes les apps du Mac mini qui ont besoin d’un micro peuvent s’en servir : la Dictée du système, la saisie vocale de WeChat Input Method, le mode vocal de Claude Code, etc.

- Le récepteur intègre son propre périphérique audio virtuel, **MicHop Audio** : il propose de l’installer à la première ouverture (le mot de passe administrateur est demandé une seule fois), sans rien télécharger d’autre. Si vous aviez déjà installé [BlackHole](https://github.com/ExistentialAudio/BlackHole), vous pouvez continuer à l’utiliser.
- Deux façons de parler, disponibles à tout moment : appuyez une fois sur **⌃⌥M** pour envoyer en continu, puis à nouveau pour arrêter ; ou **maintenez ⌃⌥** pendant que vous parlez et relâchez pour arrêter.
- L’annulation d’écho intégrée évite tout écho, même lorsque vous êtes connecté via un logiciel de bureau à distance.
- La touche Fn ne passe pas à travers le logiciel de bureau à distance : pensez à remplacer, sur le Mac mini, le raccourci de saisie vocale par une combinaison de touches de modification, par exemple Ctrl + Option. [Détails plus bas](#astuce--la-touche-fn-ne-passe-pas-en-bureau-à-distance-changez-de-raccourci).

### Comment relier les deux ordinateurs

- **Sur le même réseau local** : il suffit de saisir l’adresse IP locale du Mac mini.
- **S’ils ne sont pas au même endroit** : installez [Tailscale](https://tailscale.com) sur les deux ordinateurs pour créer un réseau virtuel, puis saisissez l’**adresse IP Tailscale** du Mac mini (elle commence par 100). Cela fonctionne de la même façon à la maison et à l’extérieur.
- La fenêtre du récepteur affiche l’adresse IP locale, l’adresse IP Tailscale et le code, chacun avec un bouton de copie.

### Autres points forts

- **Aucun service cloud** : le son circule directement entre vos deux ordinateurs, chiffré de bout en bout, par le réseau local ou via Tailscale.
- **Indépendant du logiciel de bureau à distance** : fonctionne avec UU Remote, Sunlogin, ToDesk ou le Partage d’écran.
- **Mises à jour automatiques** : l’app se met à jour d’elle-même quand une nouvelle version sort, sans qu’il faille réaccorder les autorisations.
- **Multilingue** : l’interface est disponible en 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português et Русский. Le chinois est la langue par défaut ; changez-la dans « Réglages… → Général → Langue / Language ».

## Téléchargement et installation

Téléchargez les fichiers depuis [Releases](../../releases/latest) :

| Fichier | Sur quel ordinateur l’installer | Icône de la barre des menus |
|---|---|---|
| `MicHop.zip` (MicHop) | L’ordinateur sur lequel vous parlez, par exemple le MacBook | Deux micros, comme l’icône de l’app |
| `MicHop-Receiver.zip` (MicHop Receiver) | L’ordinateur sur lequel vous travaillez, par exemple le Mac mini | Idem |

La couleur de l’icône de la barre des menus indique l’état : **gris** = non connecté, **vert** = connecté, **rouge** = envoi du son en cours.

> **Les deux apps s’articulent autour de leur fenêtre principale** : un clic sur l’icône du Dock ouvre la fenêtre principale, dont le haut affiche deux blocs d’état : « Connexion » (gris / bleu) et « Audio » (gris / rouge). Les actions courantes se trouvent dans la fenêtre ; les raccourcis, la langue, les mises à jour automatiques, etc. sont dans « Réglages… » (⌘,). L’icône de la barre des menus et le menu contextuel de l’icône du Dock ne gardent que les options les plus utilisées. Si la caméra (l’encoche) du MacBook masque l’icône de la barre des menus, passez par l’icône du Dock.

Nécessite macOS 13 ou une version ultérieure ; fonctionne sur les Mac à puce Apple comme sur les Mac Intel.

> **À la première ouverture, un message indique que le développeur ne peut pas être vérifié** : c’est parce que l’app n’a pas fait l’objet de la notarisation payante d’Apple. Ouvrez Réglages Système → Confidentialité et sécurité, puis cliquez sur « Ouvrir quand même » en bas de la page. Vous pouvez aussi exécuter cette commande dans Terminal pour lever la quarantaine, puis ouvrir l’app :
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. L’ordinateur sur lequel vous travaillez (récepteur)

1. Décompressez `MicHop-Receiver.zip`, faites glisser « MicHop Receiver » dans le dossier Applications, puis ouvrez-le.
   - Si une fenêtre vous demande d’accepter les connexions réseau entrantes, cliquez sur **Autoriser**.
2. À la première ouverture, l’app propose d’installer le périphérique audio virtuel intégré **MicHop Audio** : cliquez sur « Installer » et saisissez une fois le mot de passe administrateur. Pendant l’installation, le son du système se coupe une ou deux secondes. Vous pouvez aussi l’installer plus tard dans « Réglages… → Périphérique audio virtuel ».
3. Une fois l’installation terminée, suivez les indications pour choisir MicHop Audio comme **périphérique d’entrée du système** (le bouton « Corriger » est aussi disponible dans « Préparation », dans la fenêtre principale). Pour la **sortie** du système, gardez les haut-parleurs (ou le périphérique audio du logiciel de bureau à distance). MicHop Audio ne peut pas être choisi comme sortie système, si bien que le son du système ne s’y mélange pas.
4. La fenêtre principale affiche :
   - **Infos de connexion** : l’adresse locale de ce Mac, l’adresse Tailscale et le code, chacun avec un bouton de copie.
   - **Préparation** : quand le périphérique audio virtuel et l’entrée système portent tous deux une coche verte, tout est prêt. Si un élément affiche un avertissement jaune, un bouton pour le corriger apparaît directement à sa droite.
5. Par défaut, l’app s’ouvre automatiquement à l’ouverture de session ; si vous n’en voulez pas, désactivez cette option dans « Réglages… → Général ».

> **Vous aviez déjà installé BlackHole ?** Il fonctionne toujours : choisissez le périphérique voulu dans « Préparation → Lire dans ». Pour passer au périphérique intégré, cliquez sur « Installer » à côté de « Vous pouvez passer au périphérique virtuel intégré ». Avec BlackHole, veillez à ne pas le choisir comme sortie système ; en cas d’erreur, un avertissement « Sortie système » apparaît dans « Préparation » : il suffit de cliquer sur « Revenir aux haut-parleurs ».

### 2. L’ordinateur sur lequel vous parlez (émetteur)

1. Décompressez `MicHop.zip`, faites glisser « MicHop » dans le dossier Applications, puis ouvrez-le.
2. À la première ouverture, la fenêtre de réglages s’affiche : saisissez l’**adresse** et le **code** du récepteur, cliquez sur « Tester la connexion », puis, quand « Connecté — prêt » s’affiche en vert, cliquez sur « Enregistrer ».
   - Dans la fenêtre du récepteur, les boutons de copie à côté de l’adresse et du code permettent de copier chaque élément séparément.
   - Vous pouvez aussi cliquer sur « Tout copier » dans le récepteur, puis coller le bloc entier dans le champ « Adresse ». L’émetteur repère l’adresse tout seul (en privilégiant l’adresse Tailscale s’il y en a une) et remplit aussi le code.
   - Si une fenêtre demande l’autorisation de rechercher des appareils sur votre réseau local, cliquez sur **Autoriser**.
3. À la première utilisation, l’app demande l’accès au **micro** : autorisez-le. Elle demande aussi l’autorisation **Accessibilité** (pour détecter quand vous maintenez ⌃⌥) ; suivez les indications : Réglages Système → Confidentialité et sécurité → Accessibilité → activez « MicHop ».
4. À l’ouverture, l’app se connecte au récepteur. Quand « Connexion » passe au bleu dans la fenêtre principale et que l’icône de la barre des menus passe au vert, tout est prêt. Pour modifier plus tard l’adresse ou le code, cliquez sur « Modifier… » dans la rubrique « Récepteur » de la fenêtre principale, ou appuyez sur ⌘,.

## Utilisation

Commencez par cliquer, dans le bureau à distance, à l’endroit de l’ordinateur de travail où vous voulez utiliser la voix : le mode vocal de Claude Code, la Dictée du système ou la méthode de saisie. Ensuite, deux façons de parler sont disponibles à tout moment :

1. **Envoi continu** : appuyez une fois sur **⌃⌥M (Ctrl + Option + M)**, ou cliquez sur « Démarrer l’audio » dans la fenêtre principale ; le micro reste ouvert. Appuyez à nouveau pour arrêter.
2. **Maintenir pour parler** : **maintenez Ctrl + Option pendant que vous parlez, relâchez pour arrêter**. Le micro n’est ouvert que tant que les touches sont maintenues.

Pendant l’envoi, « Audio » dans la fenêtre principale et l’icône de la barre des menus passent au rouge ; côté récepteur, « Audio » passe aussi au rouge.

- Le logiciel de bureau à distance transmet aussi cette combinaison de touches à l’ordinateur de travail. Si, sur celui-ci, vous réglez aussi le raccourci vocal de la Dictée ou de la méthode de saisie sur Ctrl + Option (voir [l’astuce ci-dessous](#astuce--la-touche-fn-ne-passe-pas-en-bureau-à-distance-changez-de-raccourci)), **une seule pression suffit à la fois pour envoyer le son et pour lancer la dictée de l’autre côté**.
- Pendant que vous maintenez les touches pour parler, MicHop coupe temporairement le son de ce Mac, afin que le son de l’autre ordinateur, renvoyé par le logiciel de bureau à distance, ne soit pas repris par le micro et ne crée pas d’écho ; le son revient automatiquement environ 1 seconde après le relâchement. (L’envoi continu utilise l’annulation d’écho d’Apple.)

> **Les raccourcis sont modifiables** : dans « Réglages… → Raccourcis », cliquez sur le bouton, puis appuyez sur la nouvelle combinaison. « Commencer à parler » accepte toute combinaison comportant ⌃, ⌥ ou ⌘ ; « Maintenir pour parler » exige une combinaison d’au moins deux touches parmi ⌃ ⌥ ⇧ ⌘. Si la combinaison choisie est déjà utilisée par le système (par exemple, sur de nombreux Mac, ⌃⌥Espace correspond à « Sélectionner la source suivante du menu Saisie »), l’app affiche un avertissement orange : désactivez ce raccourci dans Réglages Système → Clavier → Raccourcis clavier, ou choisissez une autre combinaison.

> **Pourquoi y a-t-il de l’écho ?** Beaucoup de logiciels de bureau à distance (UU Remote, par exemple) capturent le son de l’ordinateur contrôlé avec le framework d’enregistrement d’écran d’Apple, qui enregistre **le son émis par toutes les apps** de cet ordinateur, quel que soit le périphérique audio sur lequel il est lu. Quand MicHop joue votre voix dans le périphérique audio virtuel, elle est elle aussi enregistrée, renvoyée vers votre ordinateur, diffusée par les haut-parleurs, puis captée de nouveau par le micro.
>
> C’est pourquoi l’**annulation d’écho** est activée par défaut sur l’émetteur (vous pouvez la désactiver dans « Options », dans la fenêtre principale). Elle s’appuie sur le traitement de la voix d’Apple, celui-là même qu’utilise FaceTime : elle retire du signal du micro le son renvoyé, atténue les autres sons pendant que vous parlez et réduit le bruit au passage. Le résultat est meilleur avec un casque ou des écouteurs.

### Astuce : la touche Fn ne passe pas en bureau à distance, changez de raccourci

Quand vous êtes connecté avec un logiciel de bureau à distance comme UU Remote, Sunlogin ou ToDesk, **la touche Fn pressée sur votre ordinateur n’arrive pas jusqu’à l’ordinateur contrôlé**. Elle n’y déclenche rien, que vous utilisiez la Dictée du système ou la saisie vocale de WeChat Input Method. Il y a deux raisons à cela : votre ordinateur intercepte d’abord la touche Fn (et lance la dictée en local) ; et même si le logiciel de bureau à distance la transmettait, ce ne serait qu’une « frappe simulée » sur l’ordinateur contrôlé, que le système et les méthodes de saisie ne reconnaissent généralement pas.

La solution : sur l’**ordinateur contrôlé** (par exemple le Mac mini), changez le raccourci de la saisie vocale :

- **Dictée du système** : Réglages Système → Clavier → Dictée → Raccourci → « Personnaliser ».
- **WeChat Input Method** : modifiez le raccourci de la saisie vocale dans les réglages de WeChat Input Method.

Privilégiez une **combinaison de touches de modification**, par exemple **Ctrl + Option de gauche**, ou Ctrl avec une autre touche de modification (Option, Maj, Commande).

**N’utilisez pas Ctrl avec un chiffre ou une lettre** (par exemple Ctrl+D). La saisie vocale demande généralement de maintenir la touche pendant que vous parlez, et une lettre ou un chiffre maintenu se répète sans arrêt, ce qui est très pénible. Une combinaison composée uniquement de touches de modification ne produit aucun caractère, même maintenue.

Choisissez MicHop Audio comme périphérique d’entrée de l’ordinateur contrôlé, maintenez le nouveau raccourci dans le bureau à distance pendant que vous parlez, et l’ordinateur contrôlé transcrit directement votre dictée.

## Récupérer le son du Mac mini (haut-parleur virtuel)

Le périphérique audio virtuel fourni avec le récepteur comprend aussi un **haut-parleur virtuel, MicHop Speaker** (depuis la 1.6.0). C’est un périphérique distinct de MicHop Audio, qui diffuse le son de votre micro : les deux sons ne se mélangent pas.

Sur le récepteur, activez « Envoyer le son de ce Mac vers MicHop Speaker » dans « Réglages… → Périphérique audio virtuel » :

- La sortie système du Mac mini passe sur MicHop Speaker : **ses haut-parleurs restent muets**, et aucun son ne surgit soudain dans la pièce.
- Les logiciels de bureau à distance ou d’enregistrement d’écran qui demandent de choisir un périphérique audio (par exemple Sunlogin, certaines versions de ToDesk, OBS) peuvent prendre MicHop Speaker comme source sonore pour renvoyer le son du Mac mini.
- Les touches de volume du clavier fonctionnent normalement, et le son capté suit le volume.
- Quand vous désactivez l’option, quittez le récepteur ou désinstallez le périphérique audio virtuel, la sortie système revient automatiquement sur le périphérique d’origine.

> Les logiciels de bureau à distance qui captent le son via l’enregistrement d’écran d’Apple, comme UU Remote, l’enregistrent quel que soit le périphérique de sortie ; pour eux, l’intérêt principal du haut-parleur virtuel est que « les haut-parleurs du Mac mini restent muets, mais on entend toujours le son à distance ».

Dans la fenêtre principale du récepteur, la dernière ligne de « Préparation », « Son de ce Mac », indique où part actuellement le son de cet ordinateur.

## Pas sur le même réseau ? Utilisez Tailscale

1. Installez [Tailscale](https://tailscale.com) sur les deux ordinateurs et connectez-vous avec le même compte.
2. Dans la fenêtre principale du récepteur, la ligne « Tailscale » des « Infos de connexion » affiche 100.x.x.x : saisissez cette adresse dans les réglages de l’émetteur. Le nom de machine affiché dans Tailscale fonctionne aussi.
3. Si « Introuvable » s’affiche, vérifiez d’abord que Tailscale est connecté sur l’ordinateur récepteur, puis cliquez sur le bouton d’actualisation de cette ligne pour relancer la détection. Si l’adresse n’est toujours pas détectée, saisissez celle qu’indique le menu Tailscale dans « Réglages… → Tailscale → Adresse manuelle » du récepteur.

L’adresse Tailscale fonctionne aussi bien à la maison qu’à l’extérieur, et lorsque les deux ordinateurs sont sur le même réseau local, la connexion se fait automatiquement en direct.

## Sécurité

- **Le son est chiffré de bout en bout** : chaque connexion commence par un échange de clés (X25519), puis chaque segment audio est chiffré avec ChaCha20-Poly1305. Cela protège contre quiconque écoute ou capture le trafic sur le même réseau : il ne peut ni entendre ce que vous dites, ni récupérer le code. Le code lui-même ne transite jamais sur le réseau.
- Chaque récepteur possède un code aléatoire à 6 chiffres, et toute connexion avec un code erroné est refusée ; après 5 erreurs de suite, le récepteur n’accepte plus de nouvelle connexion pendant 30 secondes et la fenêtre principale affiche « Quelqu’un essaie de deviner le code ». Pour le changer, cliquez sur « Nouveau » dans la ligne « Code » de la fenêtre principale du récepteur (il faudra ensuite le saisir à nouveau sur l’émetteur).
- **Ce qui n’est pas couvert** : quelqu’un qui détourne activement la connexion en se faisant passer pour le récepteur. Un code à 6 chiffres n’offre qu’un million de possibilités : avec une seule poignée de main interceptée, il peut le retrouver hors ligne. Utilisez donc MicHop uniquement sur votre réseau domestique ou via Tailscale, et n’exposez pas le port du récepteur (TCP **8766**) à Internet.
- L’émetteur et le récepteur doivent tous deux être en version 1.6.0 ou plus récente. Si l’un des deux est trop ancien, l’autre indique qu’il faut le mettre à jour.

## Questions fréquentes

- **Impossible de se connecter** : vérifiez que les deux ordinateurs sont sur le même réseau, ou qu’ils sont tous deux connectés à Tailscale. L’adresse IP locale peut changer : mieux vaut attribuer une IP fixe au récepteur dans votre routeur, ou utiliser directement l’adresse Tailscale.
- **Le récepteur indique qu’il ne peut pas ouvrir le port** : en général, un ancien récepteur ne s’est pas complètement fermé et occupe encore le port ; le récepteur l’arrête automatiquement. Si c’est un autre programme qui l’occupe, son nom figure dans le message, et le récepteur démarrera tout seul dès que le port sera libéré.
- **Maintenir ⌃⌥ ne fait rien** : l’émetteur a besoin de l’autorisation **Accessibilité**. Après une recompilation ou une mise à jour de l’app, macOS invalide parfois l’autorisation précédente : supprimez d’abord l’ancienne entrée de la liste Accessibilité, puis ajoutez-la de nouveau.

## Mises à jour automatiques

Les deux apps vérifient d’elles-mêmes la présence d’une nouvelle version sur GitHub : une première fois 30 secondes après le lancement, puis toutes les 6 heures. Lorsqu’une nouvelle version est disponible, elles la téléchargent, la mettent en place et se rouvrent automatiquement.

- Le numéro de la version actuelle figure en bas à gauche de la fenêtre principale ; dans « Réglages… → Général », cliquez sur « Rechercher des mises à jour » pour vérifier immédiatement.
- Si vous ne voulez pas d’installation automatique, désactivez « Installer les mises à jour automatiquement » dans « Réglages… → Général ». Par la suite, quand une nouvelle version sera disponible, un bouton « Mettre à jour vers x.y.z » apparaîtra dans les réglages, ainsi que la même option dans le menu de la barre des menus ; la mise à jour ne se fera que lorsque vous cliquerez dessus.
- Rien ne vous interrompt pendant l’utilisation : aucune mise à jour n’a lieu pendant l’envoi du son.
- Sécurité : la nouvelle version doit être signée avec **le même certificat** que la version actuelle, faute de quoi l’installation est refusée.
- Après la mise à jour, les autorisations Accessibilité, Micro, etc. sont conservées : inutile de les accorder de nouveau.

## License

[MIT](LICENSE)
