---
ms.openlocfilehash: 0d7c9cc909e2f848cc9760d5862bb1863501f02b
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823288"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="a085f-101">Dans cette section, vous allez mettre à jour le composant WebPart pour permettre à l’utilisateur d’ajouter un événement à son calendrier pour l’heure sociale hebdomadaire de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="a085f-101">In this section you'll update the web part to allow the user to add an event to their calendar for the team's weekly social hour.</span></span> <span data-ttu-id="a085f-102">Dans ce scénario, l’équipe a une heure sociale hebdomadaire à 4 h le vendredi.</span><span class="sxs-lookup"><span data-stu-id="a085f-102">In this scenario, the team has a weekly social hour at 4 PM on Friday.</span></span>

1. <span data-ttu-id="a085f-103">Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.TS** et remplacez la `addSocialToCalendar()` méthode existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="a085f-103">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and replace the existing `addSocialToCalendar()` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="addSocialToCalendarSnippet":::

    <span data-ttu-id="a085f-104">Examinez ce que fait ce code.</span><span class="sxs-lookup"><span data-stu-id="a085f-104">Consider what this code does.</span></span>

    - <span data-ttu-id="a085f-105">Il détermine le prochain vendredi prochain et crée une **Date** pour 4 heures ce jour.</span><span class="sxs-lookup"><span data-stu-id="a085f-105">It determines the next upcoming Friday and constructs a **Date** for 4 PM on that day.</span></span>
    - <span data-ttu-id="a085f-106">Il construit un nouvel objet **MicrosoftGraph. Event** , en définissant le paramètre start sur la valeur de la **Date** , et la fin pour une heure plus tard.</span><span class="sxs-lookup"><span data-stu-id="a085f-106">It constructs a new **MicrosoftGraph.Event** object, setting the start to the value of the **Date** , and the end for one hour later.</span></span>
    - <span data-ttu-id="a085f-107">Il utilise le **MSGraphClient** pour publier le nouvel événement sur le `/me/events` point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="a085f-107">It uses the **MSGraphClient** to POST the new event to the `/me/events` endpoint.</span></span>
    - <span data-ttu-id="a085f-108">Il restitue de nouveau le composant WebPart afin que l’affichage soit mis à jour avec le nouvel événement.</span><span class="sxs-lookup"><span data-stu-id="a085f-108">It re-renders the web part so the view is updated with the new event.</span></span>

1. <span data-ttu-id="a085f-109">Créez, empaquetez et téléchargez de nouveau le composant WebPart, puis actualisez la page dans laquelle vous le testez.</span><span class="sxs-lookup"><span data-stu-id="a085f-109">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

1. <span data-ttu-id="a085f-110">Cliquez sur le bouton **Ajouter une équipe sociale** .</span><span class="sxs-lookup"><span data-stu-id="a085f-110">Click the **Add team social** button.</span></span> <span data-ttu-id="a085f-111">Une fois que la page est actualisée, faites défiler jusqu’à vendredi et recherchez le nouvel événement.</span><span class="sxs-lookup"><span data-stu-id="a085f-111">Once the page refreshes, scroll down to Friday and find the new event.</span></span>

    ![Capture d’écran du nouvel événement créé dans le composant WebPart](images/new-event.png)
