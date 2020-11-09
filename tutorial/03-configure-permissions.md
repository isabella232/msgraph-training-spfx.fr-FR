---
ms.openlocfilehash: 19bd57df9f349d67e9f10e7dd70f02231950b010
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823369"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="31097-101">SharePoint Framework élimine la nécessité d’enregistrer une application dans Azure AD pour obtenir des jetons d’accès pour accéder à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="31097-101">The SharePoint Framework eliminates the need to register an application in Azure AD for getting access tokens to access Microsoft Graph.</span></span> <span data-ttu-id="31097-102">Elle gère l’authentification de l’utilisateur qui est connecté à SharePoint, ce qui permet à votre composant WebPart d’obtenir des jetons utilisateur.</span><span class="sxs-lookup"><span data-stu-id="31097-102">It handles the authentication for the user that is logged into SharePoint, allowing your web part to get user tokens.</span></span> <span data-ttu-id="31097-103">Votre composant WebPart doit indiquer les [étendues d’autorisation de graphique](https://docs.microsoft.com/graph/permissions-reference) dont il a besoin, et un administrateur client peut approuver ces autorisations lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="31097-103">Your web part needs to indicate which [Graph permission scopes](https://docs.microsoft.com/graph/permissions-reference) it requires, and a tenant admin can approve those permissions during installation.</span></span>

## <a name="configure-permissions"></a><span data-ttu-id="31097-104">Configurer des autorisations</span><span class="sxs-lookup"><span data-stu-id="31097-104">Configure permissions</span></span>

1. <span data-ttu-id="31097-105">Open **. dossier/config/package-solution.js**.</span><span class="sxs-lookup"><span data-stu-id="31097-105">Open **./config/package-solution.json**.</span></span>

1. <span data-ttu-id="31097-106">Ajoutez le code suivant à la `solution` propriété.</span><span class="sxs-lookup"><span data-stu-id="31097-106">Add the following code to the `solution` property.</span></span>

    ```json
    "webApiPermissionRequests": [
      {
        "resource": "Microsoft Graph",
        "scope": "Calendars.ReadWrite"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "User.ReadBasic.All"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "Contacts.Read"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "People.Read"
      }
    ]
    ```

<span data-ttu-id="31097-107">L' `Calendars.ReadWrite` autorisation permet à votre composant WebPart d’extraire le calendrier de l’utilisateur et d’ajouter des événements à l’aide de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="31097-107">The `Calendars.ReadWrite` permission allows your web part to retrieve the user's calendar and add events using Microsoft Graph.</span></span> <span data-ttu-id="31097-108">Les autres autorisations sont utilisées par les composants de la boîte à outils Microsoft Graph pour afficher des informations sur les participants aux événements et les organisateurs.</span><span class="sxs-lookup"><span data-stu-id="31097-108">The other permissions are used by components in the Microsoft Graph Toolkit to render information about event attendees and organizers.</span></span>

## <a name="optional-test-token-acquisition"></a><span data-ttu-id="31097-109">Facultatif : test d’acquisition de jeton</span><span class="sxs-lookup"><span data-stu-id="31097-109">Optional: Test token acquisition</span></span>

> [!NOTE]
> <span data-ttu-id="31097-110">Le reste des étapes de cette page sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="31097-110">The rest of the steps on this page are optional.</span></span> <span data-ttu-id="31097-111">Si vous préférez utiliser le codage Microsoft Graph immédiatement, vous pouvez passer à [un affichage Calendrier](/graph/tutorials/spfx?tutorial-step=3).</span><span class="sxs-lookup"><span data-stu-id="31097-111">If you'd prefer to get to the Microsoft Graph coding right away, you can proceed to [Get a calendar view](/graph/tutorials/spfx?tutorial-step=3).</span></span>

<span data-ttu-id="31097-112">Nous allons ajouter du code temporaire au composant WebPart pour tester l’acquisition de jetons.</span><span class="sxs-lookup"><span data-stu-id="31097-112">Let's add some temporary code to the web part to test token acquisition.</span></span>

1. <span data-ttu-id="31097-113">Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.TS** et ajoutez l' `import` instruction suivante en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="31097-113">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import { AadTokenProvider } from '@microsoft/sp-http';
    ```

1. <span data-ttu-id="31097-114">Remplacez la fonction `render` existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="31097-114">Replace the existing `render` function with the following.</span></span>

    ```typescript
    public render(): void {
    this.context.aadTokenProviderFactory
      .getTokenProvider()
      .then((provider: AadTokenProvider)=> {
      provider
        .getToken('https://graph.microsoft.com')
        .then((token: string) => {
          this.domElement.innerHTML = `
          <div class="${ styles.graphTutorial }">
            <div class="${ styles.container }">
              <div class="${ styles.row }">
                <div class="${ styles.column }">
                  <span class="${ styles.title }">Welcome to SharePoint!</span>
                  <p><code style="word-break: break-all;">${ token }</code></p>
                </div>
              </div>
            </div>
          </div>`;
        });
      });
    }
    ```

### <a name="deploy-the-web-part"></a><span data-ttu-id="31097-115">Déployer le composant WebPart</span><span class="sxs-lookup"><span data-stu-id="31097-115">Deploy the web part</span></span>

1. <span data-ttu-id="31097-116">Exécutez les deux commandes suivantes dans votre interface CLI pour créer et créer un package de votre composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="31097-116">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="31097-117">Ouvrez votre navigateur et accédez au catalogue d’applications SharePoint de votre client.</span><span class="sxs-lookup"><span data-stu-id="31097-117">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="31097-118">Sélectionnez l’élément de menu **apps pour SharePoint** dans la partie gauche.</span><span class="sxs-lookup"><span data-stu-id="31097-118">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="31097-119">Téléchargez le fichier **./SharePoint/solution/Graph-Tutorial.sppkg** .</span><span class="sxs-lookup"><span data-stu-id="31097-119">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="31097-120">Dans l’invite **do do Trust...** , confirmez que l’invite affiche la liste des 4 autorisations Microsoft Graph que vous avez définies dans le fichier **package-solution.js** .</span><span class="sxs-lookup"><span data-stu-id="31097-120">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="31097-121">Sélectionnez **mettre cette solution à disposition de tous les sites de l’organisation** , puis sélectionnez **déployer**.</span><span class="sxs-lookup"><span data-stu-id="31097-121">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="31097-122">Accédez au [Centre d’administration SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) à l’aide d’un administrateur client.</span><span class="sxs-lookup"><span data-stu-id="31097-122">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

1. <span data-ttu-id="31097-123">Dans le menu de gauche, sélectionnez **avancé** , puis **accès à l’API**.</span><span class="sxs-lookup"><span data-stu-id="31097-123">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

1. <span data-ttu-id="31097-124">Sélectionnez chacune des demandes en attente dans le package **Graph-Tutorial-Client-Side-solution** , puis choisissez **approuver**.</span><span class="sxs-lookup"><span data-stu-id="31097-124">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

    ![Capture d’écran de la page d’accès à l’API du centre d’administration SharePoint](images/api-access.png)

### <a name="test-the-web-part"></a><span data-ttu-id="31097-126">Tester le composant WebPart</span><span class="sxs-lookup"><span data-stu-id="31097-126">Test the web part</span></span>

1. <span data-ttu-id="31097-127">Accédez à un site SharePoint où vous souhaitez tester le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="31097-127">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="31097-128">Créez une page sur laquelle tester le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="31097-128">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="31097-129">Utilisez le sélecteur de composants WebPart pour rechercher le composant WebPart **GraphTutorial** et l’ajouter à la page.</span><span class="sxs-lookup"><span data-stu-id="31097-129">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Capture d’écran du composant WebPart GraphTutorial dans le sélecteur de composants WebPart](images/add-web-part.png)

1. <span data-ttu-id="31097-131">Le jeton d’accès s’imprime sous l' **écran d’accueil de SharePoint !**</span><span class="sxs-lookup"><span data-stu-id="31097-131">The access token is printed below the **Welcome to SharePoint!**</span></span> <span data-ttu-id="31097-132">message dans le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="31097-132">message in the web part.</span></span> <span data-ttu-id="31097-133">Vous pouvez copier ce jeton et l’analyser à [https://jwt.ms/](https://jwt.ms/) l’adresse pour vérifier qu’il contient les étendues d’autorisation requises par le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="31097-133">You can copy this token and parse it at [https://jwt.ms/](https://jwt.ms/) to confirm that it contains the permission scopes required by the web part.</span></span>

    ![Capture d’écran du composant WebPart affichant un jeton d’accès](images/access-token.png)
