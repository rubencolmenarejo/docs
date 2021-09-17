---
title: "Gérer et accéder à ses mots de passe"
slug: gerer-et-acceder-a-ses-mots-de-passe
excerpt: Apprenez à modifier les mots de passe de vos services OVHcloud
section: Premiers pas
---

**Dernière mise à jour le 17/09/2021**

## Objectif

Il peut parfois être nécessaire, par exemple, suite à un cas de piratage, de modifier l'ensemble des mots de passe de vos services OVHcloud. Vous trouverez ici toutes les informations nécessaires.

**Découvrez comment modifier l'ensemble des mots de passe de vos services OVHcloud.**

> [!warning]
>
> OVHcloud met à votre disposition des services dont la configuration, la gestion et la responsabilité vous incombent. Il vous revient de ce fait d'en assurer le bon fonctionnement.
>
> Nous mettons à votre disposition ce guide afin de vous accompagner au mieux sur des tâches courantes. Néanmoins, nous vous recommandons de faire appel à un prestataire spécialisé et/ou de contacter l'éditeur du service si vous éprouvez des difficultés. En effet, nous ne serons pas en mesure de vous fournir une assistance. Plus d'informations dans la section [Aller plus loin](#aller-plus-loin) de ce guide.
>

## Prérequis

- Disposer d’un compte client et de services OVHcloud actifs.
- Connaître l'identifiant et le mot de passe de votre [espace client OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) ou avoir accès à l'adresse e-mail de récupération de votre compte.

> [!primary]
>
> Pour modifier les mots de passe de vos différents services OVHcloud, seuls les identifiants d'accès à votre [espace client](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) sont nécessaires.
>
> Une fois connecté à votre [espace](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), vous pourrez modifier les mots de passe de l'ensemble de vos services sans connaître les anciens mots de passe.
>

### Espace client OVHcloud

Pour modifier le mot de passe de votre [espace client OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), suivez les instructions de ce [guide](https://docs.ovh.com/fr/customer/gerer-son-mot-de-passe/).

### Accès FTP aux fichiers de votre hébergement

Pour modifier le mot de passe [d'accès FTP à l'espace de stockage de votre hébergement](https://docs.ovh.com/fr/hosting/connexion-espace-stockage-ftp-hebergement-web/), suivez les instructions de ce [guide](https://docs.ovh.com/fr/hosting/modifier-mot-de-passe-utilisateur-ftp/).

> [!primary]
>
> Si vous souhaitez retrouver le mot de passe FTP actuel, consultez les e-mails émanant de nos services. Lors de l'installation de votre [offre d'hébergement](https://www.ovh.com/fr/hebergement-web/), un message contenant l'identifiant FTP (login) et le mot de passe associé vous a en effet été envoyé.
>
> Vous pouvez retrouver cet e-mail à tout moment en haut à droite de votre [espace client OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) sur votre nom puis sur `E-mails de service`{.action}.
>
>![](images/.png){.thumbnail}
>
> Si vous avez par contre modifié le mot de passe indiqué dans ce message, vous devrez le modifier en suivant ces [instructions](https://docs.ovh.com/fr/hosting/modifier-mot-de-passe-utilisateur-ftp/).
>

### Base de données

#### Offre StartSQL

Pour modifier le mot de passe de votre [base de données StartSQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml) (il s'agit des bases de données livrées avec l'ensemble de nos [offres d'hébergement mutulisées](https://www.ovh.com/fr/hebergement-web/), à l'exception des offres gratuites [Start10M](https://docs.ovh.com/fr/hosting/activer-start10m/)), suivez les instructions de ce [guide](https://docs.ovh.com/fr/hosting/modifier-mot-de-passe-base-de-donnees/).

#### Serveur SQL privé

Pour modifier le mot de passe d'une base de données sur votre [serveur SQL privé](https://docs.ovh.com/fr/hosting/premiers-pas-avec-sql-prive/), rendez vous dans l'onglet Bases de données situé sur la gauche de votre écran puis choisissez l'offre concernée. Cliquez ensuite sur l'onglet `Utilisateurs et droits`{.action} puis sur le bouton `...`{.action} concerné et `Changer le mot de passe`{.action}.

La base de données n'est pas créée automatiquement suite à la commande d'un hébergement mutualisé. Vous devez créer celle-ci une fois votre offre installée. La procédure de création d'une base de données est décrite dans ce [guide](https://docs.ovh.com/fr/hosting/creer-base-de-donnees/){.ref}. Le mot de passe est personnalisé dès la création et celui-ci ne sera pas mentionné dans le mail de confirmation transmis suite à la création.

Si vous oubliiez le mot de passe de votre base de données :

- votre site est en ligne, il utilise la base de données : dans ce cas le mot de passe de la base de donnée est mentionné dans un fichier présent sur votre espace FTP (ex: pour WordPress ce fichier est nommé : wp-config.php).
- vous n'avez pas de site utilisant la base de donnée, ou vous souhaitez simplement modifier le mot de passe de la base de données : dans ce cas il faut modifier le mot de passe depuis l'espace client. La procédure de modification du mot de passe d'une base de données est décrite dans ce [guide](https://docs.ovh.com/fr/hosting/modifier-mot-de-passe-base-de-donnees/){.ref} .

> [!alert]
>
> Attention : modifier le mot de passe de la base de données n'est pas anodin.
> Cela peut entrainer une coupure du site ou des services utilisant cette base de
> données.
> Pensez à mettre à jour le fichier de configuration de votre site afin qu'il se
> connecte à la base de données avec le nouveau mot de passe si un site est
> présent sur l'hébergement lors de la modification.
> 

### Adresse E-mail OVHcloud

Lorsque vous créez une adresse e-mail, vous personnalisez directement le mot de passe. La connexion au [webmail](https://www.ovh.com/fr/mail/){.external} requiert l'adresse e-mail complète et le mot de passe. Si vous avez oublié le mot de passe de votre adresse e-mail, vous pouvez le modifier directement depuis votre espace client. La procédure de modification est décrite dans ce [guide](https://docs.ovh.com/fr/emails/modifier-mot-de-passe-adresse-email/){.ref}

> [!alert]
>
> La modification du mot de passe d'une adresse e-mail necessite sa mise à jour
> dans votre client de messagerie
> 

### Accès SSH aux fichiers de votre hébergement

Se connecter en SSH ( **S** ecure  **S** hell) nécessite de posséder une offre mutualisé  **PRO**  ou supérieure. La connexion se fait avec les mêmes identifiants et mot de passe que pour la connexion FTP.

Pour avoir une offre permettant l'accès via SSH, dirigez vous vers [nos offres](https://www.ovh.com/fr/hebergement-web){.external}

### Interface administrateur des modules en 1 clic

Lors de l'installation d'un module en un clic, vous personnalisez vous même le mot de passe administrateur. Celui-ci ne sera pas transmis par e-mail. Si vous oubliez le mot de passe, vous pouvez le régénérer depuis la page de connexion à votre module. Un lien est présent en cas de mot de passe oublié.

Un exemple pour le module WordPress :

![hosting](images/2851.png){.thumbnail}

Si le module a été installé depuis le nouvel espace client, il est aussi possible de modifier le mot de passe depuis celui-ci.

Une fois connecté à votre espace client, il faut sélectionner l'hébergement concerné dans la section Hébergement.

![hosting](images/2855.png){.thumbnail}

Vous devez ensuite sélectionner la section Modules en 1 clic puis cliquer sur la roue crantée de droite et Modifier le mot de passe

![hosting](images/2854.png){.thumbnail}

## Aller plus loin <a name="aller-plus-loin"></a>

[Sécuriser son compte OVHcloud avec la double authentification](https://docs.ovh.com/fr/customer/securiser-son-compte-avec-une-2FA/)

Pour des prestations spécialisées (référencement, développement, etc), contactez les [partenaires OVHcloud](https://partner.ovhcloud.com/fr/).

Si vous souhaitez bénéficier d'une assistance à l'usage et à la configuration de vos solutions OVHcloud, nous vous invitons à consulter nos différentes [offres de support](https://www.ovhcloud.com/fr/support-levels/).

Échangez avec notre communauté d'utilisateurs sur <https://community.ovh.com/>.

