# Lancez Vos Programmes Windows

![Screenshot](assets/Wine_4.0.jpg)

Vous pensiez que Linux et Windows sont des plateforms complètement différentes qui ne peuvent jamais être compatibles? Vous n'avez pas réellement tort. Toutefois, les développeurs de Linux sont arrivés à exécuter les applications de Windows dans un système d'exploitation GNU/Linux, et cela en ayant recours à une application très intéressante qui s'appelle Wine.

Contrairement à ce que la plupart des gens pensent, Wine n'est pas un emulateur. Le nom de l'application semble indiquer qu'il est une abréviation de (WIN-dows Emulator), mais en réalité c'est absolument le contraire. Les développeurs de Wine disent toujours: "Wine is not an emulator", ce qui lève le doute sur sa nature.

## Comment ça fonctionne?

Wine est une couche de compatibilité, ce qui signifie qu'elle fait marcher les applications Windows exactement comme Windows la plupart du temps. Les développeurs de Wine ont trouvé une bonne façon pour décrire Wine: "Wine est un emulateur Windows exactement comme Windows Vista est un emulateur de Windows XP." Les développeurs de Wine ont une base de données riche sur les applications Windows connues et qui ont été testées. Donc tout problème reporté par la communauté est réglé dans la mise à jour qui suit.

## Installation et utilisation

Actuellement, Wine a deux versions, une qui est stable et l'autre dédiée au développement. La version stable 1.6.2 est disponible sur Ubuntu, Arch Linux et Fedora. Elle est suffisante pour le lancement des applications Windows, mais si vous voulez quelque chose de plus récent, vous devez installer la version dédiée au développement.

La version de développement est quelque fois nécessaire, surtout pour les nouvelles applications et les nouveaux jeux de Windows parce qu'elle est mise à jour périodiquement pour régler certains problèmes. Malheureusement ceci veut dire qu'elle est plus sensible aux bugs et aux plantages.

On a testé Wine (les deux versions) sur Ubuntu 14.04 Beta 2 LTS et ils ont marché très bien. Vous pouvez télécharger Wine depuis "Ubuntu Software Center" mais vous ne trouverez que l'ancienne version. Pour avoir la dernière version, tout ce que vous avez besoin de faire est de lancer les commandes suivantes dans un terminal (en mode root):

```bash
sudo add-apt-repository ppa:ubuntu-wine/ppa
sudo apt update
sudo apt install wine
```

Si vous voulez avoir la version de développement, vous devez remplacer la dernière commande par celle là:

```
sudo apt install wine1.7
```

Lorsque vous ouvrez le "Dash" et cherchez le mot "Wine", vous allez trouver une entrée nommée "Configure Wine".

L'utilisateur peut changer beaucoup de choses dans l'application Wine, mais l'entrée la plus importante est l'onglet "Applications" ou vous pouvez choisir quel système Windows à "imiter". C'est la fonctionnalité la plus importante et la première à consulter lorsque quelque chose ne marche pas bien.

Il ne faut pas toucher aux autres options que si vous suivez un tutoriel qui traite un problème précis.

Aussi, le répértoire Wine peut être trouvé dans le chemin: `~/home/.wine`. C'est le répértoire dans lequel vous trouverez aussi les applications Windows téléchargées.

**L'inconvenient** majeur de cette applications c'est que certaines applications et certains jeux vidéos nécessitent un ordinateur puissant pour pouvoir les lancer par Wine même si ces applications peuvent bien se lancer dans Windows avec la même configuration hardware.

**L'avantage** c'est qu'on sait tous que Windows propose des centaines d'applications de bonne qualité et le fait qu'on peut les lancer par Linux est un miracle.

Le travail fait pour atteindre ce but est très appréciable.
