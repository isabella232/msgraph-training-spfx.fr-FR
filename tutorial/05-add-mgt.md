---
ms.openlocfilehash: ee9addcbcf58fa971b3e67fb3d84cfb36bf275dd
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823375"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="333a7-101">Dans cette section, vous allez utiliser [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) pour remplacer la liste simple d’événements par une interface utilisateur enrichie.</span><span class="sxs-lookup"><span data-stu-id="333a7-101">In this section, you'll use the [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to replace the simple list of events with rich UI.</span></span>

<span data-ttu-id="333a7-102">Le kit de outils fournit un [composant d’Agenda](https://docs.microsoft.com/graph/toolkit/components/agenda), qui est bien adapté pour afficher notre liste d’événements.</span><span class="sxs-lookup"><span data-stu-id="333a7-102">The toolkit provides an [Agenda component](https://docs.microsoft.com/graph/toolkit/components/agenda), which is well-suited to render our list of events.</span></span>

## <a name="update-the-web-part"></a><span data-ttu-id="333a7-103">Mettre à jour le composant WebPart</span><span class="sxs-lookup"><span data-stu-id="333a7-103">Update the web part</span></span>

1. <span data-ttu-id="333a7-104">Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.module.SCSS**.</span><span class="sxs-lookup"><span data-stu-id="333a7-104">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.module.scss**.</span></span> <span data-ttu-id="333a7-105">Remplacez la valeur de l' `background-color` attribut de l' `.row` entrée par `$ms-color-white` .</span><span class="sxs-lookup"><span data-stu-id="333a7-105">Change the value of the `background-color` attribute in the `.row` entry to `$ms-color-white`.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="rowScssSnippet" highlight="4":::

1. <span data-ttu-id="333a7-106">Ajoutez l’entrée suivante dans l' `.graphTutorial` entrée.</span><span class="sxs-lookup"><span data-stu-id="333a7-106">Add the following entry inside the `.graphTutorial` entry.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="addSocialBtnSnippet":::

1. <span data-ttu-id="333a7-107">Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.TS** et ajoutez l' `import` instruction suivante en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="333a7-107">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import { Providers, SharePointProvider, MgtAgenda } from '@microsoft/mgt';
    ```

1. <span data-ttu-id="333a7-108">Ajoutez la fonction suivante à la classe **GraphTutorialWebPart** pour initialiser la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="333a7-108">Add the following function to the **GraphTutorialWebPart** class to initialize the toolkit.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="onInitSnippet":::

1. <span data-ttu-id="333a7-109">Remplacez la fonction `renderCalendarView` existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="333a7-109">Replace the existing `renderCalendarView` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderCalendarViewSnippet":::

    <span data-ttu-id="333a7-110">Cette action remplace la liste de base par le composant **Agenda** de la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="333a7-110">This replaces the basic list with the **Agenda** component from the toolkit.</span></span>

1. <span data-ttu-id="333a7-111">Créez, empaquetez et téléchargez de nouveau le composant WebPart, puis actualisez la page dans laquelle vous le testez.</span><span class="sxs-lookup"><span data-stu-id="333a7-111">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

    ![Capture d’écran du composant WebPart avec le composant Agenda](images/mgt-agenda.png)

## <a name="an-alternate-approach"></a><span data-ttu-id="333a7-113">Une approche alternative</span><span class="sxs-lookup"><span data-stu-id="333a7-113">An alternate approach</span></span>

<span data-ttu-id="333a7-114">À ce stade, vous avez du code qui :</span><span class="sxs-lookup"><span data-stu-id="333a7-114">At this point, you have code that:</span></span>

- <span data-ttu-id="333a7-115">Utilise le **MSGraphClient** pour obtenir l’affichage Calendrier de l’utilisateur pour la semaine en cours à partir de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="333a7-115">Uses the **MSGraphClient** to get the user's calendar view for the current week from Microsoft Graph.</span></span>
- <span data-ttu-id="333a7-116">Ajoutez ces événements au composant **Agenda** à partir de la boîte à outils Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="333a7-116">Add those events to the **Agenda** component from the Microsoft Graph Toolkit.</span></span>

<span data-ttu-id="333a7-117">Avec cette approche, vous disposez d’un contrôle total sur l’appel de l’API Graph et vous pouvez effectuer le traitement des événements avant le rendu souhaité.</span><span class="sxs-lookup"><span data-stu-id="333a7-117">With this approach, you have full control over the Graph API call and can do any processing of the events prior to rendering that you want.</span></span> <span data-ttu-id="333a7-118">Toutefois, si cela n’est pas obligatoire, vous pouvez simplifier en laissant le composant **Agenda** effectuer le travail pour vous.</span><span class="sxs-lookup"><span data-stu-id="333a7-118">However, if that isn't required, you can simplify by letting the **Agenda** component do the work for you.</span></span>

<span data-ttu-id="333a7-119">Tous les composants de la boîte à outils Microsoft Graph sont capables d’effectuer tous les appels d’API pertinents à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="333a7-119">All Microsoft Graph Toolkit components are capable of making all of the relevant API calls to the Microsoft Graph.</span></span> <span data-ttu-id="333a7-120">Par exemple, en ajoutant simplement le composant **Agenda** au composant WebPart, et en ne définissant aucune propriété, le composant WebPart utilise ses paramètres par défaut pour obtenir des événements pour la journée en cours.</span><span class="sxs-lookup"><span data-stu-id="333a7-120">For example, by just adding the **Agenda** component to the web part, and not setting any properties, the web part would use its default settings to get events for the current day.</span></span> <span data-ttu-id="333a7-121">Examinons comment obtenir les mêmes résultats que nous avons actuellement (événements pour la semaine en cours).</span><span class="sxs-lookup"><span data-stu-id="333a7-121">Let's look at how we can achieve the same results we currently have (events for the current week).</span></span>

1. <span data-ttu-id="333a7-122">Remplacez la `render` méthode existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="333a7-122">Replace the existing `render` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="alternateRenderSnippet":::

    <span data-ttu-id="333a7-123">À présent, au lieu d’appeler une API dans `render` , il vous suffit d’ajouter un `mgt-agenda` élément directement dans le code html.</span><span class="sxs-lookup"><span data-stu-id="333a7-123">Now, instead of making an API call in `render`, you simply add an `mgt-agenda` element directly into the HTML.</span></span> <span data-ttu-id="333a7-124">En définissant `date` sur le début de la semaine et `days` sur 7, le composant fera le même appel d’API que la version précédente de `render` was.</span><span class="sxs-lookup"><span data-stu-id="333a7-124">By setting `date` to the start of the week, and `days` to 7, the component will make the same API call the previous version of `render` was making.</span></span>

1. <span data-ttu-id="333a7-125">Ajoutez la fonction vide suivante à la classe **GraphTutorialWebPart** .</span><span class="sxs-lookup"><span data-stu-id="333a7-125">Add the following empty function to the **GraphTutorialWebPart** class.</span></span>

    ```typescript
    private async addSocialToCalendar() {}
    ```

    > [!NOTE]
    > <span data-ttu-id="333a7-126">Nous avons également ajouté un bouton **Ajouter une équipe social** au composant WebPart et ajouté la `addSocialToCalendar` méthode en tant qu’écouteur d’événements.</span><span class="sxs-lookup"><span data-stu-id="333a7-126">We also added an **Add team social** button to the web part, and added the `addSocialToCalendar` method as an event listener.</span></span>  <span data-ttu-id="333a7-127">Vous allez implémenter le code sous-jacent dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="333a7-127">You'll implement the code behind that in the next section.</span></span> <span data-ttu-id="333a7-128">Pour le moment, nous souhaitons juste que le code soit compilé.</span><span class="sxs-lookup"><span data-stu-id="333a7-128">For now, we just want the code to compile.</span></span>

1. <span data-ttu-id="333a7-129">Créez, empaquetez et téléchargez de nouveau le composant WebPart, puis actualisez la page dans laquelle vous le testez.</span><span class="sxs-lookup"><span data-stu-id="333a7-129">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span> <span data-ttu-id="333a7-130">L’affichage doit être identique à celui de votre test précédent.</span><span class="sxs-lookup"><span data-stu-id="333a7-130">The view should be the same as your previous test.</span></span>

### <a name="using-the-toolkit-vs-making-api-calls"></a><span data-ttu-id="333a7-131">Utilisation de la boîte à outils vs des appels d’API</span><span class="sxs-lookup"><span data-stu-id="333a7-131">Using the toolkit vs making API calls</span></span>

<span data-ttu-id="333a7-132">À ce stade, vous vous demandez peut-être pourquoi vous avez rencontré les problèmes liés à l’utilisation de l' **MSGraphClient** , lorsque le kit d’outils procède à votre travail.</span><span class="sxs-lookup"><span data-stu-id="333a7-132">At this point you may be wondering why you went through the trouble of using the **MSGraphClient** at all, when the toolkit does the work for you.</span></span> <span data-ttu-id="333a7-133">Le kit de outils est conçu pour afficher les résultats que vous interrogez à partir de Microsoft Graph, comme une liste d’événements.</span><span class="sxs-lookup"><span data-stu-id="333a7-133">The toolkit is designed for rendering results that you query from Microsoft Graph, such as a list of events.</span></span> <span data-ttu-id="333a7-134">Toutefois, il existe des scénarios dans lesquels vous devez faire des appels d’API.</span><span class="sxs-lookup"><span data-stu-id="333a7-134">However, there are scenarios where making API calls yourself is necessary.</span></span>

- <span data-ttu-id="333a7-135">Les appels d’API qui ne sont pas une `GET` demande.</span><span class="sxs-lookup"><span data-stu-id="333a7-135">Any API calls that are not a `GET` request.</span></span> <span data-ttu-id="333a7-136">Par exemple, la création d’un événement dans le calendrier ou la mise à jour du numéro de téléphone d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="333a7-136">For example, creating a new event on the calendar, or updating a user's phone number.</span></span>
- <span data-ttu-id="333a7-137">Appels d’API permettant d’obtenir des données destinées à être utilisées « en arrière-plan » et non affichées directement.</span><span class="sxs-lookup"><span data-stu-id="333a7-137">API calls to get data that's intended to be used "behind the scenes" and not rendered directly.</span></span>
