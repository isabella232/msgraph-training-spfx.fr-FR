---
ms.openlocfilehash: ca72a0d6047d3cd275d34e2d0b4e3c54dbab5375
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831289"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="e4f4c-101">Exécution du projet terminé</span><span class="sxs-lookup"><span data-stu-id="e4f4c-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4f4c-102">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e4f4c-102">Prerequisites</span></span>

<span data-ttu-id="e4f4c-103">Pour exécuter le projet terminé dans ce dossier, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e4f4c-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="e4f4c-104">[Node.js](https://nodejs.org/en/download/releases/) version 10. x</span><span class="sxs-lookup"><span data-stu-id="e4f4c-104">[Node.js](https://nodejs.org/en/download/releases/) version 10.x</span></span>
- [<span data-ttu-id="e4f4c-105">Gulp</span><span class="sxs-lookup"><span data-stu-id="e4f4c-105">Gulp</span></span>](https://gulpjs.com/)
- <span data-ttu-id="e4f4c-106">Un compte professionnel ou scolaire Microsoft, avec accès à un compte d’administrateur général au sein de la même organisation.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-106">A Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="e4f4c-107">Si vous n’avez pas de compte Microsoft, vous pouvez vous [inscrire au programme pour les développeurs office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement gratuit à Office 365.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-107">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>
- <span data-ttu-id="e4f4c-108">Votre client Microsoft 365 doit être [configuré pour le développement de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), avec un catalogue d’applications et un site de test créés avant de commencer ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-108">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

### <a name="deploy-the-web-part"></a><span data-ttu-id="e4f4c-109">Déployer le composant WebPart</span><span class="sxs-lookup"><span data-stu-id="e4f4c-109">Deploy the web part</span></span>

1. <span data-ttu-id="e4f4c-110">Exécutez les deux commandes suivantes dans votre interface CLI pour créer et créer un package de votre composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-110">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="e4f4c-111">Ouvrez votre navigateur et accédez au catalogue d’applications SharePoint de votre client.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-111">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="e4f4c-112">Sélectionnez l’élément de menu **apps pour SharePoint** dans la partie gauche.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-112">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="e4f4c-113">Téléchargez le fichier **./SharePoint/solution/Graph-Tutorial.sppkg** .</span><span class="sxs-lookup"><span data-stu-id="e4f4c-113">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="e4f4c-114">Dans l’invite **do do Trust...** , confirmez que l’invite affiche la liste des 4 autorisations Microsoft Graph que vous avez définies dans le fichier **package-solution.js** .</span><span class="sxs-lookup"><span data-stu-id="e4f4c-114">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="e4f4c-115">Sélectionnez **mettre cette solution à disposition de tous les sites de l’organisation** , puis sélectionnez **déployer**.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-115">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="e4f4c-116">Accédez au [Centre d’administration SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) à l’aide d’un administrateur client.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-116">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

1. <span data-ttu-id="e4f4c-117">Dans le menu de gauche, sélectionnez **avancé** , puis **accès à l’API**.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-117">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

1. <span data-ttu-id="e4f4c-118">Sélectionnez chacune des demandes en attente dans le package **Graph-Tutorial-Client-Side-solution** , puis choisissez **approuver**.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-118">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

    ![Capture d’écran de la page d’accès à l’API du centre d’administration SharePoint](../tutorial/images/api-access.png)

### <a name="test-the-web-part"></a><span data-ttu-id="e4f4c-120">Tester le composant WebPart</span><span class="sxs-lookup"><span data-stu-id="e4f4c-120">Test the web part</span></span>

1. <span data-ttu-id="e4f4c-121">Accédez à un site SharePoint où vous souhaitez tester le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-121">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="e4f4c-122">Créez une page sur laquelle tester le composant WebPart.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-122">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="e4f4c-123">Utilisez le sélecteur de composants WebPart pour rechercher le composant WebPart **GraphTutorial** et l’ajouter à la page.</span><span class="sxs-lookup"><span data-stu-id="e4f4c-123">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Capture d’écran du composant WebPart GraphTutorial dans le sélecteur de composants WebPart](../tutorial/images/add-web-part.png)
