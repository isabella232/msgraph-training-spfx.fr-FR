---
ms.openlocfilehash: c239c1ea6daae99cc5a65b7b95508ccb2a1bf014
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823357"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="a3d1e-101">SharePoint Framework fournit le [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) pour effectuer des appels à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-101">The SharePoint Framework provides the [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) for making calls to Microsoft Graph.</span></span> <span data-ttu-id="a3d1e-102">Cette classe inclut dans la [bibliothèque cliente JavaScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript)une pré-authentification avec l’utilisateur actuellement connecté.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-102">This class wraps the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript), pre-authenticating it with the current logged on user.</span></span>

<span data-ttu-id="a3d1e-103">Étant donné qu’il enveloppe la bibliothèque JavaScript existante, son utilisation est identique et elle est entièrement compatible avec les définitions de l’autotest de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-103">Because it wraps the existing JavaScript library, its usage is the same, and it's fully compatible with the Microsoft Graph TypeScript definitions.</span></span>

## <a name="get-the-users-calendar"></a><span data-ttu-id="a3d1e-104">Obtenir le calendrier de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a3d1e-104">Get the user's calendar</span></span>

1. <span data-ttu-id="a3d1e-105">Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.TS** et ajoutez les `import` instructions suivantes en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-105">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statements at the top of the file.</span></span>

    ```typescript
    import { MSGraphClient } from '@microsoft/sp-http';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import { startOfWeek, endOfWeek, setDay, set } from 'date-fns';
    ```

1. <span data-ttu-id="a3d1e-106">Ajoutez la fonction suivante à la classe **GraphTutorialWebPart** pour afficher une erreur.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-106">Add the following function to the **GraphTutorialWebPart** class to render an error.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderGraphErrorSnippet":::

1. <span data-ttu-id="a3d1e-107">Ajoutez la fonction suivante pour imprimer les événements dans le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-107">Add the following function to print out the events in the user's calendar.</span></span>

    ```typescript
    private renderCalendarView(events: MicrosoftGraph.Event[]) : void {
      const viewContainer = this.domElement.querySelector('#calendarView');
      let html = '';

      // Temporary: print events as a list
      for(const event of events) {
        html += `
          <p class="${ styles.description }">Subject: ${event.subject}</p>
          <p class="${ styles.description }">Organizer: ${event.organizer.emailAddress.name}</p>
          <p class="${ styles.description }">Start: ${event.start.dateTime}</p>
          <p class="${ styles.description }">End: ${event.end.dateTime}</p>
          `;
      }

      viewContainer.innerHTML = html;
    }
    ```

1. <span data-ttu-id="a3d1e-108">Remplacez la fonction `render` existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-108">Replace the existing `render` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderSnippet":::

    <span data-ttu-id="a3d1e-109">Notez ce que fait ce code.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-109">Notice what this code does.</span></span>

    - <span data-ttu-id="a3d1e-110">Elle utilise `this.context.msGraphClientFactory.getClient` pour obtenir un objet **MSGraphClient** authentifié.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-110">It uses `this.context.msGraphClientFactory.getClient` to get an authenticated **MSGraphClient** object.</span></span>
    - <span data-ttu-id="a3d1e-111">Il appelle le `/me/calendarView` point de terminaison, en définissant les paramètres de la `startDateTime` requête et le `endDateTime` début et la fin de la semaine en cours.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-111">It calls the `/me/calendarView` endpoint, setting the `startDateTime` and `endDateTime` query parameters to the start and end of the current week.</span></span>
    - <span data-ttu-id="a3d1e-112">Il utilise `select` pour limiter les champs qui sont renvoyés, en ne demandant que les champs utilisés par l’application.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-112">It uses `select` to limit which fields are returned, requesting only the fields the app uses.</span></span>
    - <span data-ttu-id="a3d1e-113">Il utilise `orderby` pour trier les événements en fonction de leur heure de début.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-113">It uses `orderby` to sort the events by their start time.</span></span>
    - <span data-ttu-id="a3d1e-114">Il utilise `top` pour limiter les résultats à 25 événements.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-114">It uses `top` to limit the results to 25 events.</span></span>

## <a name="deploy-the-web-part"></a><span data-ttu-id="a3d1e-115">Déployer le composant WebPart</span><span class="sxs-lookup"><span data-stu-id="a3d1e-115">Deploy the web part</span></span>

1. <span data-ttu-id="a3d1e-116">Exécutez les deux commandes suivantes dans votre interface CLI pour créer et créer un package de votre composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-116">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="a3d1e-117">Ouvrez votre navigateur et accédez au catalogue d’applications SharePoint de votre client.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-117">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="a3d1e-118">Sélectionnez l’élément de menu **apps pour SharePoint** dans la partie gauche.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-118">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="a3d1e-119">Téléchargez le fichier **./SharePoint/solution/Graph-Tutorial.sppkg** .</span><span class="sxs-lookup"><span data-stu-id="a3d1e-119">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="a3d1e-120">Dans l’invite **do do Trust...** , confirmez que l’invite affiche la liste des 4 autorisations Microsoft Graph que vous avez définies dans le fichier **package-solution.js** .</span><span class="sxs-lookup"><span data-stu-id="a3d1e-120">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="a3d1e-121">Sélectionnez **mettre cette solution à disposition de tous les sites de l’organisation** , puis sélectionnez **déployer**.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-121">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="a3d1e-122">Si vous n’avez pas encore approuvé les autorisations de graphique pour votre composant WebPart, faites-le maintenant.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-122">If you have not already approved the Graph permissions for your web part, do that now.</span></span>

    1. <span data-ttu-id="a3d1e-123">Accédez au [Centre d’administration SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) à l’aide d’un administrateur client.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-123">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

    1. <span data-ttu-id="a3d1e-124">Dans le menu de gauche, sélectionnez **avancé** , puis **accès à l’API**.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-124">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

    1. <span data-ttu-id="a3d1e-125">Sélectionnez chacune des demandes en attente dans le package **Graph-Tutorial-Client-Side-solution** , puis choisissez **approuver**.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-125">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

        ![Capture d’écran de la page d’accès à l’API du centre d’administration SharePoint](images/api-access.png)

## <a name="test-the-web-part"></a><span data-ttu-id="a3d1e-127">Tester le composant WebPart</span><span class="sxs-lookup"><span data-stu-id="a3d1e-127">Test the web part</span></span>

1. <span data-ttu-id="a3d1e-128">Accédez à un site SharePoint où vous souhaitez tester le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-128">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="a3d1e-129">Créez une page sur laquelle tester le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-129">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="a3d1e-130">Utilisez le sélecteur de composants WebPart pour rechercher le composant WebPart **GraphTutorial** et l’ajouter à la page.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-130">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Capture d’écran du composant WebPart GraphTutorial dans le sélecteur de composants WebPart](images/add-web-part.png)

1. <span data-ttu-id="a3d1e-132">Une liste d’événements pour la semaine en cours est imprimée dans le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="a3d1e-132">A list of events for the current week are printed in the web part.</span></span>

    ![Capture d’écran du composant WebPart affichant une liste d’événements](images/calendar-list.png)
