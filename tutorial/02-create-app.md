---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823301"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="1c865-101">Dans ce didacticiel, vous allez créer un [composant WebPart côté client SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) qui utilisera Microsoft Graph pour obtenir le calendrier de l’utilisateur pour la semaine en cours et permettre à l’utilisateur d’ajouter un événement à son calendrier.</span><span class="sxs-lookup"><span data-stu-id="1c865-101">In this tutorial, you'll create a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that will use Microsoft Graph to get the user's calendar for the current week and allow the user to add an event to their calendar.</span></span>

## <a name="create-a-web-part-project"></a><span data-ttu-id="1c865-102">Créer un projet de composant WebPart</span><span class="sxs-lookup"><span data-stu-id="1c865-102">Create a web part project</span></span>

1. <span data-ttu-id="1c865-103">Ouvrez votre interface de ligne de commande (CLI) dans un répertoire vide où vous souhaitez créer le projet.</span><span class="sxs-lookup"><span data-stu-id="1c865-103">Open your command-line interface (CLI) in an empty directory where you want to create the project.</span></span> <span data-ttu-id="1c865-104">Exécutez la commande suivante pour démarrer le générateur Yeoman SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1c865-104">Run the following command to start the Yeoman SharePoint generator.</span></span>

    ```Shell
    yo @microsoft/sharepoint
    ```

1. <span data-ttu-id="1c865-105">Répondez aux invites comme suit.</span><span class="sxs-lookup"><span data-stu-id="1c865-105">Respond to the prompts as follows.</span></span>

    - <span data-ttu-id="1c865-106">**Quel est le nom de votre solution ?**</span><span class="sxs-lookup"><span data-stu-id="1c865-106">**What is your solution name?**</span></span> `graph-tutorial`
    - <span data-ttu-id="1c865-107">**Quels packages de base voulez-vous cibler pour vos composants ?**</span><span class="sxs-lookup"><span data-stu-id="1c865-107">**Which baseline packages do you want to target for your component(s)?**</span></span> `SharePoint Online only (latest)`
    - <span data-ttu-id="1c865-108">**Où souhaitez-vous placer les fichiers ?**</span><span class="sxs-lookup"><span data-stu-id="1c865-108">**Where do you want to place the files?**</span></span> `Use the current folder`
    - <span data-ttu-id="1c865-109">**Voulez-vous autoriser l’administrateur client à choisir de pouvoir déployer la solution sur tous les sites immédiatement sans exécuter de déploiement de fonctionnalité ni ajouter d’applications sur les sites.**</span><span class="sxs-lookup"><span data-stu-id="1c865-109">**Do you want to allow the tenant admin the choice of being able to deploy the solution to all sites immediately without running any feature deployment or adding apps in sites?**</span></span> `Yes`
    - <span data-ttu-id="1c865-110">**Les composants de la solution nécessitent-ils des autorisations pour accéder aux API Web qui sont uniques et qui ne sont pas partagées avec d’autres composants dans les dix ant ?**</span><span class="sxs-lookup"><span data-stu-id="1c865-110">**Will the components in the solution require permissions to access web APIs that are unique and not shared with other components in the ten ant?**</span></span> `No`
    - <span data-ttu-id="1c865-111">**Quel type de composant côté client créer ?**</span><span class="sxs-lookup"><span data-stu-id="1c865-111">**Which type of client-side component to create?**</span></span> `WebPart`
    - <span data-ttu-id="1c865-112">**Quel est le nom de votre composant WebPart ?**</span><span class="sxs-lookup"><span data-stu-id="1c865-112">**What is your Web part name?**</span></span> `GraphTutorial`
    - <span data-ttu-id="1c865-113">**Quelle est la description de votre composant WebPart ?**</span><span class="sxs-lookup"><span data-stu-id="1c865-113">**What is your Web part description?**</span></span> `GraphTutorial description`
    - <span data-ttu-id="1c865-114">**Quelle infrastructure voulez-vous utiliser ?**</span><span class="sxs-lookup"><span data-stu-id="1c865-114">**Which framework would you like to use?**</span></span> `No JavaScript framework`

1. <span data-ttu-id="1c865-115">Exécutez la commande suivante pour mettre à jour la version de la machine à écrire dans le projet sur 3,7.</span><span class="sxs-lookup"><span data-stu-id="1c865-115">Run the following command to update the TypeScript version in the project to 3.7.</span></span>

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. <span data-ttu-id="1c865-116">Open **./tsconfig.js** et remplacez `rush-stack-compiler-3.3` par `rush-stack-compiler-3.7` .</span><span class="sxs-lookup"><span data-stu-id="1c865-116">Open **./tsconfig.json** and replace `rush-stack-compiler-3.3` with `rush-stack-compiler-3.7`.</span></span>

1. <span data-ttu-id="1c865-117">Ouvrez **./tslint.jssur** et supprimez la `"no-use-before-declare": true,` ligne.</span><span class="sxs-lookup"><span data-stu-id="1c865-117">Open **./tslint.json** and remove the `"no-use-before-declare": true,` line.</span></span> <span data-ttu-id="1c865-118">La `no-use-before-declare` règle est déconseillée et génère une erreur lors du processus de génération.</span><span class="sxs-lookup"><span data-stu-id="1c865-118">The `no-use-before-declare` rule is deprecated and will cause an error during the build process.</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="1c865-119">Installer les dépendances</span><span class="sxs-lookup"><span data-stu-id="1c865-119">Install dependencies</span></span>

<span data-ttu-id="1c865-120">Avant de poursuivre, installez des packages NPM supplémentaires que vous utiliserez plus tard.</span><span class="sxs-lookup"><span data-stu-id="1c865-120">Before moving on, install some additional NPM packages that you will use later.</span></span>

- <span data-ttu-id="1c865-121">[Définitions de l’Autodactylographié Microsoft Graph](https://github.com/microsoftgraph/msgraph-typescript-typings) pour fournir des objets IntelliSense pour Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1c865-121">[Microsoft Graph TypeScript definitions](https://github.com/microsoftgraph/msgraph-typescript-typings) to provide Intellisense for Microsoft Graph objects.</span></span>
- <span data-ttu-id="1c865-122">[Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) pour fournir des composants d’interface utilisateur pour le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="1c865-122">[Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to provide UI components for the web part.</span></span>
- <span data-ttu-id="1c865-123">[Date-FNS](https://date-fns.org/) pour des fonctions utiles pour l’utilisation de dates.</span><span class="sxs-lookup"><span data-stu-id="1c865-123">[date-fns](https://date-fns.org/) for helpful functions for working with dates.</span></span>

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
