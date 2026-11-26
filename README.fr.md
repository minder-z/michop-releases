<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Prêtez le micro de ce Mac à un autre Mac.</b><br>
  En audio ou en texte, sur le réseau local ou via Tailscale.<br>
  <sub>Lend your Mac's microphone to another Mac — as live audio or as text, over LAN or Tailscale.</sub>
</p>

---

## À quoi ça sert

Je travaille d'habitude sur un MacBook et j'utilise un logiciel de bureau à distance (UU Remote, Sunlogin, ToDesk, etc.) pour me connecter à un Mac mini et y travailler : faire écrire du code à Claude Code, monter des vidéos, maintenir des sites web…

Le problème : **le Mac mini n'a pas de micro, et le logiciel de bureau à distance ne transmet pas le micro du MacBook**. Impossible donc d'utiliser la saisie vocale dans le bureau à distance.

C'est exactement ce que résout MicHop. On installe une app sur chaque ordinateur :

- **L'ordinateur dans lequel vous parlez** (par exemple le MacBook) : installez « MicHop »
- **L'ordinateur qui travaille** (par exemple le Mac mini) : installez « MicHop Receiver »

### Deux modes d'envoi, à changer à tout moment depuis la fenêtre principale

```
MacBook (vous parlez)                        Mac mini (il travaille)

Micro ────── 🔊 Envoyer l'audio ──────►  Micro virtuel (MicHop Audio intégré)
                                      → Dictée / WeChat Input Method / mode vocal de Claude Code

Dictée ───── 📝 Envoyer du texte ─────►  Collé à l'emplacement du curseur, Retour automatique en option

              via le réseau local ou Tailscale
```

**🔊 Envoyer l'audio : le Mac mini vous « entend » directement**

Le son du micro du MacBook est transmis en temps réel au Mac mini et devient le micro du Mac mini. Toute app du Mac mini qui a besoin d'un micro peut l'utiliser : la Dictée du système, la saisie vocale de WeChat Input Method, le mode vocal de Claude Code, etc.

- Le Receiver intègre son propre périphérique audio virtuel, **MicHop Audio** : son installation vous est proposée au premier envoi audio (le mot de passe administrateur est demandé une fois), sans rien télécharger d'autre. Si vous aviez déjà installé [BlackHole](https://github.com/ExistentialAudio/BlackHole), vous pouvez continuer à l'utiliser.
- L'annulation d'écho est intégrée : pas d'écho, même connecté via un logiciel de bureau à distance.
- La touche Fn ne passe pas à travers le logiciel de bureau à distance : pensez à remplacer le raccourci de saisie vocale par une combinaison de touches de modification, par exemple Ctrl + Option. [Voir plus bas](#astuce--la-touche-fn-ne-passe-pas-en-connexion-à-distance-changez-de-raccourci).

**📝 Envoyer du texte : reconnaissance sur le MacBook, envoi des mots**

Sur le MacBook, appuyez sur ⌃⌥Espace (Ctrl + Option + Espace) et utilisez la Dictée du système pour transformer votre voix en texte. Le texte est envoyé au Mac mini et collé automatiquement à l'emplacement du curseur ; il peut même appuyer automatiquement sur Retour pour l'envoyer directement à Claude.

- Aucun pilote audio à installer ni réglage audio à faire sur le Mac mini : c'est la solution la plus simple et la plus fiable.
- C'est le mode par défaut de l'app.

| | 🔊 Envoyer l'audio | 📝 Envoyer du texte |
|---|---|---|
| Où la voix est reconnue | Mac mini (avec sa propre dictée ou méthode de saisie) | MacBook (avec la Dictée du système) |
| Ce qu'il faut sur le Mac mini | Receiver + son périphérique audio virtuel intégré (installé à la première utilisation) | Uniquement le Receiver |
| Idéal pour | Utiliser la méthode de saisie, la dictée ou le mode vocal de Claude du Mac mini | Simplement transformer ce que vous dites en texte saisi |

### Connecter les deux ordinateurs

- **Sur le même réseau local** : il suffit de saisir l'IP locale du Mac mini.
- **À des endroits différents** : installez [Tailscale](https://tailscale.com) sur les deux ordinateurs pour former un réseau local virtuel, puis saisissez l'**IP Tailscale** du Mac mini (qui commence par 100). **L'audio comme le texte peuvent passer par Tailscale** : ça marche pareil à la maison ou en déplacement.
- La fenêtre du Receiver affiche l'IP locale, l'IP Tailscale et le code, chacun avec son propre bouton de copie.

### Autres points forts

- **Aucun service cloud** : l'audio et le texte circulent directement entre vos deux ordinateurs, sur le réseau local ou par le tunnel chiffré de Tailscale.
- **Indépendant du logiciel de bureau à distance** : fonctionne avec UU Remote, Sunlogin, ToDesk et le Partage d'écran.
- **Mises à jour automatiques** : l'app se met à jour toute seule quand une nouvelle version sort, sans avoir à redonner les autorisations.
- **Multilingue** : l'interface est disponible en 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português et Русский. Le chinois est la langue par défaut ; changez-la dans « Réglages… → Général → Langue / Language ».

## Téléchargement et installation

Téléchargez depuis [Releases](../../releases/latest) :

| Fichier | Sur quel ordinateur | Icône de la barre des menus |
|---|---|---|
| `MicHop.zip` (MicHop) | L'ordinateur dans lequel vous parlez, p. ex. MacBook | Un carré arrondi, comme l'icône de l'app |
| `MicHop-Receiver.zip` (MicHop Receiver) | L'ordinateur qui travaille, p. ex. Mac mini | Idem |

La couleur de l'icône de la barre des menus indique l'état : **gris** = non connecté, **vert** = connecté, **rouge** = envoi en cours (vous parlez / son reçu).

> **Les deux apps s’articulent autour de leur fenêtre principale** : cliquez sur l’icône du Dock pour l’ouvrir. En haut, l’état s’affiche en deux blocs : « Connexion » (gris / bleu) et « Audio » (gris / rouge) ; les actions courantes se trouvent dans la fenêtre ; la langue, les mises à jour automatiques, etc. sont dans « Réglages… » (⌘,). L’icône de la barre des menus et le clic droit sur l’icône du Dock ne gardent que les options les plus utilisées. Quand l’encoche de la caméra du MacBook masque l’icône de la barre des menus, passez simplement par l’icône du Dock.

Nécessite macOS 13 ou version ultérieure ; fonctionne sur les Mac à puce Apple comme sur les Mac Intel.

> **Au premier lancement, le message « impossible de vérifier le développeur » s'affiche** : c'est parce que l'app n'a pas fait l'objet de la notarisation payante d'Apple. Ouvrez Réglages Système → Confidentialité et sécurité, puis cliquez sur « Ouvrir quand même » en bas de la page. Vous pouvez aussi exécuter cette commande dans le Terminal pour lever la mise en quarantaine, puis ouvrir l'app :
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. L'ordinateur qui travaille (Receiver)

1. Décompressez `MicHop-Receiver.zip`, faites glisser « MicHop Receiver » dans « Applications », puis ouvrez-la.
2. Suivez les instructions pour activer l'autorisation **Accessibilité** : Réglages Système → Confidentialité et sécurité → Accessibilité → activez « MicHop Receiver ». Elle en a besoin pour appuyer sur ⌘V à votre place.
   - Si le message « Voulez-vous que l'application accepte les connexions réseau entrantes ? » s'affiche, cliquez sur **Autoriser**.
3. Cliquez sur l'icône « MicHop Receiver » dans le Dock ; la fenêtre principale affiche :
   - **Infos de connexion** : l'adresse locale de ce Mac, l'adresse Tailscale et le code, chacun avec son bouton de copie.
   - **Préparation** : la ligne « Autorisation d’accessibilité » doit afficher une coche verte. Pour toute ligne marquée d'un avertissement jaune, un bouton de correction apparaît directement à droite.
4. « Ouvrir à la connexion » est activé par défaut ; vous pouvez le désactiver dans « Réglages… → Général » si vous n'en avez pas besoin.

### 2. L'ordinateur dans lequel vous parlez (émetteur)

1. Décompressez `MicHop.zip`, faites glisser « MicHop » dans « Applications », puis ouvrez-la.
2. Au premier lancement, la fenêtre des réglages s'ouvre : saisissez l'**adresse** et le **code** du Receiver, cliquez sur « Tester la connexion », puis, une fois « Connecté — prêt » affiché en vert, cliquez sur « Enregistrer ».
   - Dans la fenêtre du Receiver, les boutons de copie à côté de l'adresse et du code permettent de copier chaque valeur séparément.
   - Vous pouvez aussi cliquer sur « Tout copier » dans le Receiver et coller le tout dans le champ « Adresse du récepteur ». L'émetteur extrait automatiquement l'adresse (en privilégiant l'adresse Tailscale s'il y en a une) et remplit aussi le code.
   - Si le message « Autoriser la recherche d'appareils sur le réseau local » s'affiche, cliquez sur **Autoriser**.
3. Vérifiez que la Dictée du système est activée : Réglages Système → Clavier → Dictée.
4. Dès que le haut de la fenêtre principale affiche « Connecté au récepteur », c'est prêt. Pour changer plus tard l'adresse ou le code, cliquez sur « Modifier… » dans la section « Récepteur » de la fenêtre principale, ou appuyez sur ⌘,.

## Utilisation

1. D'abord, dans le bureau à distance, cliquez dans un champ de saisie de l'ordinateur qui travaille, par exemple Claude Code.
2. Appuyez sur **⌃⌥Espace (Ctrl + Option + Espace)** : une petite fenêtre apparaît en bas de l'écran et la dictée démarre automatiquement. Si elle ne démarre pas d'elle-même, appuyez une fois sur Fn.
3. Parlez, puis appuyez sur **Retour** : le texte apparaît sur l'autre ordinateur.

| Touche | Action |
|---|---|
| Retour / ⌃⌥Espace à nouveau | Envoyer |
| Maj + Retour | Nouvelle ligne |
| Échap | Annuler |

Le haut de la petite fenêtre indique vers quel ordinateur le texte sera envoyé. En bas à gauche se trouve l'option « Appuyer sur Entrée après l’envoi », cochée par défaut : le texte est directement envoyé à Claude. Si vous préférez le relire avant de l'envoyer vous-même, décochez-la (le même interrupteur se trouve aussi dans « Options » de la fenêtre principale).

Si le logiciel de bureau à distance intercepte cette combinaison et que la petite fenêtre n'apparaît pas, cliquez sur le grand bouton « Parler » de la fenêtre principale, ou sur l'icône de la barre des menus → « Parler ».

> **Les raccourcis sont modifiables** : dans « Réglages… → Raccourcis », cliquez sur le bouton, puis appuyez sur la nouvelle combinaison. Sur certains Mac, ⌃⌥Espace est déjà pris par le raccourci système « Sélectionner la source suivante du menu Saisie » : l'appui change alors de source de saisie. Dans ce cas, l'app affiche un avertissement orange : désactivez cet élément dans Réglages Système → Clavier → Raccourcis clavier → Sources de saisie, ou choisissez une autre combinaison dans MicHop.

## Deux modes d'envoi

Changez de mode dans la section « Envoyer en » de la fenêtre principale, en cliquant sur la carte « Texte » ou « Audio » ; le menu de l'icône de la barre des menus le permet aussi. **Le mode par défaut est Envoyer du texte.**

| | Envoyer du texte (par défaut) | Envoyer l'audio |
|---|---|---|
| Où la voix est reconnue | Sur ce Mac, avec la Dictée du système | Sur l'autre ordinateur, avec sa propre dictée ou le mode vocal de Claude Code |
| Rôle de ⌃⌥Espace | Ouvre la petite fenêtre de dictée | Démarre ou arrête le mode « Toujours actif » |
| Maintenir ⌃⌥ | — | Envoie tant que c’est maintenu, s’arrête au relâchement |
| Grand bouton de la fenêtre principale | « Parler » | « Démarrer l’audio » / « Arrêter l’audio » |
| Ce qu'il faut de l'autre côté | Uniquement le Receiver | Le Receiver, plus son périphérique audio virtuel intégré |

## Mode Envoyer l'audio

Utilisez ce mode quand vous voulez que l'ordinateur qui travaille **entende directement votre voix**, par exemple pour utiliser le mode vocal de Claude Code sur cet ordinateur, ou sa propre dictée.

```
Micro du MacBook ──audio──► Receiver ──► Périphérique audio virtuel MicHop Audio ──► toute app de ce Mac qui « écoute le micro »
```

**Au préalable, sur l'ordinateur du Receiver :**

1. Installez le périphérique audio virtuel intégré, **MicHop Audio** : au premier envoi audio depuis l'émetteur, le Receiver affiche une invite ; cliquez sur « Installer ». Vous pouvez aussi cliquer sur « Installer » dans « Réglages… → Périphérique audio virtuel » du Receiver. Le système demande une fois le mot de passe administrateur, et le son système se coupe une ou deux secondes à la fin de l'installation.
2. Une fois installé, suivez l'invite pour régler l'**entrée système** sur MicHop Audio (le bouton « Corriger » est aussi disponible dans « Préparation » de la fenêtre principale).
3. Laissez le périphérique de **sortie** du système sur les haut-parleurs (ou sur le périphérique audio du logiciel de bureau à distance). MicHop Audio ne peut de toute façon pas être choisi comme sortie système : le son du système ne s'y mélange donc pas.

> **Vous aviez déjà BlackHole ?** Il fonctionne toujours : choisissez le périphérique voulu dans « Préparation → Lire dans ». Pour passer au périphérique intégré, cliquez sur « Installer » à côté de « Vous pouvez passer au périphérique virtuel intégré ». Avec BlackHole, veillez à ne pas le choisir comme sortie système ; en cas d'erreur, un avertissement « Sortie système » apparaît dans « Préparation » : cliquez simplement sur « Revenir aux haut-parleurs ».

> **Pourquoi y a-t-il de l'écho ?** Beaucoup de logiciels de bureau à distance (UU Remote, par exemple) capturent le son de l'ordinateur distant via le framework d'enregistrement d'écran d'Apple, qui enregistre **le son de toutes les apps** de cet ordinateur, quel que soit le périphérique audio sur lequel il est joué. Quand MicHop joue votre voix dans le périphérique audio virtuel, elle est donc enregistrée elle aussi, renvoyée vers votre ordinateur, diffusée par les haut-parleurs, puis captée de nouveau par le micro.
>
> C'est pourquoi l'option **« Annulation d'écho »** est activée par défaut sur l'émetteur (vous pouvez la désactiver dans « Options » de la fenêtre principale). Elle utilise le traitement vocal d'Apple, le même que FaceTime : elle soustrait du micro le son renvoyé, atténue les autres sons quand vous parlez et réduit le bruit au passage. C'est avec un casque que le résultat est le meilleur.

**Utilisation :**

Dans la section « Envoyer en » de la fenêtre principale, choisissez « Audio » : l'émetteur se connecte au Receiver (la première fois, l'autorisation d'accès au micro est demandée), « Connexion » passe au bleu et l'icône de la barre des menus au vert. Vous avez ensuite deux façons de parler, disponibles à tout moment :

1. **Toujours actif** : appuyez une fois sur **⌃⌥Espace** (ou cliquez sur « Démarrer l’audio ») et le micro reste ouvert ; appuyez à nouveau pour arrêter.
2. **Maintenir pour parler** : **maintenez Ctrl + Option enfoncées pendant que vous parlez, relâchez pour arrêter**. Le micro n'est activé que tant que vous maintenez les touches : « Audio » passe au rouge dans la fenêtre principale, et l'icône de la barre des menus aussi ; quand vous relâchez, le micro se coupe et le volume de ce Mac n'est pas non plus atténué. La première fois, l'autorisation Accessibilité est demandée : elle sert à détecter cette combinaison de touches. Si elle n'est pas accordée, « Options » dans la fenêtre principale vous le signale : cliquez sur « Activer… ».
3. Le logiciel de bureau à distance transmet aussi la combinaison que vous maintenez à l'ordinateur qui travaille. Si, sur cet ordinateur, vous réglez aussi le raccourci vocal de la dictée ou de la méthode de saisie sur Ctrl + Option (voir [l'astuce ci-dessous](#astuce--la-touche-fn-ne-passe-pas-en-connexion-à-distance-changez-de-raccourci)), **une seule pression suffit à envoyer l'audio et à lancer la dictée de l'autre côté**.
4. Les deux raccourcis se modifient dans « Réglages… → Raccourcis ».

> Tant que vous maintenez les touches, MicHop coupe temporairement le son de ce Mac, pour que le son renvoyé par le logiciel de bureau à distance n'atteigne pas le micro et ne crée pas d'écho ; le son revient environ 1 seconde après avoir relâché. (Le mode Toujours actif utilise l'annulation d'écho d'Apple.)

### Astuce : la touche Fn ne passe pas en connexion à distance, changez de raccourci

Quand vous êtes connecté via un logiciel de bureau à distance comme UU Remote, Sunlogin ou ToDesk, **la touche Fn pressée sur votre Mac n'atteint pas l'ordinateur distant**. Que l'ordinateur distant utilise la Dictée du système ou la saisie vocale de WeChat Input Method, rien ne se déclenche. Il y a deux raisons : la touche Fn est d'abord interceptée par votre Mac (qui lance sa propre dictée) ; et même si le logiciel distant la transmettait, côté distant ce ne serait qu'une « frappe simulée », que le système et les méthodes de saisie ignorent en général.

La solution : sur l'**ordinateur distant** (par exemple le Mac mini), changez le raccourci de saisie vocale :

- **Dictée du système** : Réglages Système → Clavier → Dictée → Raccourci → « Personnaliser ».
- **WeChat Input Method** : modifiez le raccourci de saisie vocale dans les réglages de WeChat Input Method.

Nous recommandons une **combinaison de touches de modification**, par exemple **Ctrl gauche + Option**, ou Ctrl avec une autre touche de modification (Option, Maj, Commande).

**N'utilisez pas Ctrl avec une touche chiffre ou lettre** (comme Ctrl+D). La saisie vocale demande généralement de maintenir la touche enfoncée pendant que vous parlez, et maintenir une lettre ou un chiffre fait se répéter ce caractère : très pénible. Une combinaison composée uniquement de touches de modification ne tape aucun caractère quand on la maintient.

Cette astuce s'utilise avec le mode « Envoyer l'audio » : réglez le périphérique d'entrée de l'ordinateur distant sur MicHop Audio, maintenez le nouveau raccourci dans le bureau à distance pendant que vous parlez, et l'ordinateur distant peut dicter directement.

## Pas sur le même réseau ? Utilisez Tailscale

1. Installez [Tailscale](https://tailscale.com) sur les deux ordinateurs et connectez-vous au même compte.
2. Dans la fenêtre principale du Receiver, la ligne « Tailscale » des « Infos de connexion » affiche 100.x.x.x ; saisissez-la dans les réglages de l'émetteur. Vous pouvez aussi saisir le nom de machine affiché dans Tailscale.
3. Si « non détectée » s'affiche, vérifiez d'abord que Tailscale est connecté sur l'ordinateur du Receiver, puis cliquez sur le bouton d'actualisation de cette ligne pour relancer la détection. Si elle reste introuvable, allez dans « Réglages… → Tailscale → Adresse manuelle » sur le Receiver et entrez l'adresse affichée dans le menu de Tailscale.

L'adresse Tailscale fonctionne à la maison comme en déplacement ; lorsque les deux ordinateurs sont sur le même réseau local, la connexion directe se fait automatiquement.

## Sécurité

- Chaque Receiver possède un code aléatoire à 6 chiffres, et toute requête avec un code erroné est refusée. Pour le changer, cliquez sur « Nouveau » sur la ligne « Code » de la fenêtre principale du Receiver (il faudra ensuite le ressaisir dans l'émetteur).
- Le Receiver écoute sur deux ports TCP, **8765** (texte) et **8766** (audio), et la transmission n'est pas chiffrée. Utilisez-le uniquement sur le réseau local de votre domicile ou via Tailscale, et n'exposez pas ces ports sur Internet.
- Pour coller, l'app emprunte temporairement le presse-papiers et restaure son contenu d'origine au bout d'environ 1 seconde.

## FAQ

- **Impossible de se connecter** : vérifiez que les deux ordinateurs sont sur le même réseau, ou qu'ils sont tous deux connectés à Tailscale. L'IP locale peut changer : attribuez de préférence une IP fixe au Receiver dans votre routeur, ou utilisez directement l'adresse Tailscale.
- **Message indiquant que l'autorisation Accessibilité n'est pas activée** : après une recompilation ou une mise à jour de l'app, macOS peut invalider l'autorisation précédente. Supprimez d'abord l'ancienne entrée de la liste Accessibilité, puis ajoutez-la de nouveau.

## Mises à jour automatiques

Les deux apps vérifient d'elles-mêmes la présence de nouvelles versions sur GitHub : une fois 30 secondes après le lancement, puis toutes les 6 heures. Lorsqu'une nouvelle version est trouvée, elle est automatiquement téléchargée, remplacée et relancée.

- Le numéro de version actuel s'affiche en bas à gauche de la fenêtre principale ; dans « Réglages… → Général », vous pouvez cliquer sur « Rechercher des mises à jour » pour vérifier immédiatement.
- Si vous ne voulez pas d'installation automatique, désactivez « Installer les mises à jour automatiquement » dans « Réglages… → Général ». Dès lors, quand une nouvelle version sera disponible, un bouton « Mettre à jour vers x.y.z » apparaîtra dans les réglages (ainsi que la même option dans le menu de la barre des menus), et la mise à jour ne se fera que si vous cliquez dessus.
- Pas d'interruption en cours d'utilisation : l'émetteur ne se met pas à jour tant que la petite fenêtre de dictée est ouverte ; le Receiver non plus pendant la réception audio, ni dans la minute qui suit la réception d'un texte.
- Sécurité : la nouvelle version doit être signée avec **le même certificat** que la version actuelle, sinon l'installation est refusée.
- Après la mise à jour, les autorisations (Accessibilité, micro, etc.) sont conservées : inutile de les accorder à nouveau.

## License

[MIT](LICENSE)
