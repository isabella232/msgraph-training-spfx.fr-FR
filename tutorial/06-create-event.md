---
ms.openlocfilehash: 0d7c9cc909e2f848cc9760d5862bb1863501f02b
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823288"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans cette section, vous allez mettre à jour le composant WebPart pour permettre à l’utilisateur d’ajouter un événement à son calendrier pour l’heure sociale hebdomadaire de l’équipe. Dans ce scénario, l’équipe a une heure sociale hebdomadaire à 4 h le vendredi.

1. Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.TS** et remplacez la `addSocialToCalendar()` méthode existante par ce qui suit.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="addSocialToCalendarSnippet":::

    Examinez ce que fait ce code.

    - Il détermine le prochain vendredi prochain et crée une **Date** pour 4 heures ce jour.
    - Il construit un nouvel objet **MicrosoftGraph. Event** , en définissant le paramètre start sur la valeur de la **Date** , et la fin pour une heure plus tard.
    - Il utilise le **MSGraphClient** pour publier le nouvel événement sur le `/me/events` point de terminaison.
    - Il restitue de nouveau le composant WebPart afin que l’affichage soit mis à jour avec le nouvel événement.

1. Créez, empaquetez et téléchargez de nouveau le composant WebPart, puis actualisez la page dans laquelle vous le testez.

1. Cliquez sur le bouton **Ajouter une équipe sociale** . Une fois que la page est actualisée, faites défiler jusqu’à vendredi et recherchez le nouvel événement.

    ![Capture d’écran du nouvel événement créé dans le composant WebPart](images/new-event.png)
