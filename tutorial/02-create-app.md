---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823301"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans ce didacticiel, vous allez créer un [composant WebPart côté client SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) qui utilisera Microsoft Graph pour obtenir le calendrier de l’utilisateur pour la semaine en cours et permettre à l’utilisateur d’ajouter un événement à son calendrier.

## <a name="create-a-web-part-project"></a>Créer un projet de composant WebPart

1. Ouvrez votre interface de ligne de commande (CLI) dans un répertoire vide où vous souhaitez créer le projet. Exécutez la commande suivante pour démarrer le générateur Yeoman SharePoint.

    ```Shell
    yo @microsoft/sharepoint
    ```

1. Répondez aux invites comme suit.

    - **Quel est le nom de votre solution ?** `graph-tutorial`
    - **Quels packages de base voulez-vous cibler pour vos composants ?** `SharePoint Online only (latest)`
    - **Où souhaitez-vous placer les fichiers ?** `Use the current folder`
    - **Voulez-vous autoriser l’administrateur client à choisir de pouvoir déployer la solution sur tous les sites immédiatement sans exécuter de déploiement de fonctionnalité ni ajouter d’applications sur les sites.** `Yes`
    - **Les composants de la solution nécessitent-ils des autorisations pour accéder aux API Web qui sont uniques et qui ne sont pas partagées avec d’autres composants dans les dix ant ?** `No`
    - **Quel type de composant côté client créer ?** `WebPart`
    - **Quel est le nom de votre composant WebPart ?** `GraphTutorial`
    - **Quelle est la description de votre composant WebPart ?** `GraphTutorial description`
    - **Quelle infrastructure voulez-vous utiliser ?** `No JavaScript framework`

1. Exécutez la commande suivante pour mettre à jour la version de la machine à écrire dans le projet sur 3,7.

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. Open **./tsconfig.js** et remplacez `rush-stack-compiler-3.3` par `rush-stack-compiler-3.7` .

1. Ouvrez **./tslint.jssur** et supprimez la `"no-use-before-declare": true,` ligne. La `no-use-before-declare` règle est déconseillée et génère une erreur lors du processus de génération.

## <a name="install-dependencies"></a>Installer les dépendances

Avant de poursuivre, installez des packages NPM supplémentaires que vous utiliserez plus tard.

- [Définitions de l’Autodactylographié Microsoft Graph](https://github.com/microsoftgraph/msgraph-typescript-typings) pour fournir des objets IntelliSense pour Microsoft Graph.
- [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) pour fournir des composants d’interface utilisateur pour le composant WebPart.
- [Date-FNS](https://date-fns.org/) pour des fonctions utiles pour l’utilisation de dates.

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
