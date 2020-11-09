---
ms.openlocfilehash: ee9addcbcf58fa971b3e67fb3d84cfb36bf275dd
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823375"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans cette section, vous allez utiliser [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) pour remplacer la liste simple d’événements par une interface utilisateur enrichie.

Le kit de outils fournit un [composant d’Agenda](https://docs.microsoft.com/graph/toolkit/components/agenda), qui est bien adapté pour afficher notre liste d’événements.

## <a name="update-the-web-part"></a>Mettre à jour le composant WebPart

1. Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.module.SCSS**. Remplacez la valeur de l' `background-color` attribut de l' `.row` entrée par `$ms-color-white` .

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="rowScssSnippet" highlight="4":::

1. Ajoutez l’entrée suivante dans l' `.graphTutorial` entrée.

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="addSocialBtnSnippet":::

1. Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.TS** et ajoutez l' `import` instruction suivante en haut du fichier.

    ```typescript
    import { Providers, SharePointProvider, MgtAgenda } from '@microsoft/mgt';
    ```

1. Ajoutez la fonction suivante à la classe **GraphTutorialWebPart** pour initialiser la boîte à outils.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="onInitSnippet":::

1. Remplacez la fonction `renderCalendarView` existante par ce qui suit.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderCalendarViewSnippet":::

    Cette action remplace la liste de base par le composant **Agenda** de la boîte à outils.

1. Créez, empaquetez et téléchargez de nouveau le composant WebPart, puis actualisez la page dans laquelle vous le testez.

    ![Capture d’écran du composant WebPart avec le composant Agenda](images/mgt-agenda.png)

## <a name="an-alternate-approach"></a>Une approche alternative

À ce stade, vous avez du code qui :

- Utilise le **MSGraphClient** pour obtenir l’affichage Calendrier de l’utilisateur pour la semaine en cours à partir de Microsoft Graph.
- Ajoutez ces événements au composant **Agenda** à partir de la boîte à outils Microsoft Graph.

Avec cette approche, vous disposez d’un contrôle total sur l’appel de l’API Graph et vous pouvez effectuer le traitement des événements avant le rendu souhaité. Toutefois, si cela n’est pas obligatoire, vous pouvez simplifier en laissant le composant **Agenda** effectuer le travail pour vous.

Tous les composants de la boîte à outils Microsoft Graph sont capables d’effectuer tous les appels d’API pertinents à Microsoft Graph. Par exemple, en ajoutant simplement le composant **Agenda** au composant WebPart, et en ne définissant aucune propriété, le composant WebPart utilise ses paramètres par défaut pour obtenir des événements pour la journée en cours. Examinons comment obtenir les mêmes résultats que nous avons actuellement (événements pour la semaine en cours).

1. Remplacez la `render` méthode existante par ce qui suit.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="alternateRenderSnippet":::

    À présent, au lieu d’appeler une API dans `render` , il vous suffit d’ajouter un `mgt-agenda` élément directement dans le code html. En définissant `date` sur le début de la semaine et `days` sur 7, le composant fera le même appel d’API que la version précédente de `render` was.

1. Ajoutez la fonction vide suivante à la classe **GraphTutorialWebPart** .

    ```typescript
    private async addSocialToCalendar() {}
    ```

    > [!NOTE]
    > Nous avons également ajouté un bouton **Ajouter une équipe social** au composant WebPart et ajouté la `addSocialToCalendar` méthode en tant qu’écouteur d’événements.  Vous allez implémenter le code sous-jacent dans la section suivante. Pour le moment, nous souhaitons juste que le code soit compilé.

1. Créez, empaquetez et téléchargez de nouveau le composant WebPart, puis actualisez la page dans laquelle vous le testez. L’affichage doit être identique à celui de votre test précédent.

### <a name="using-the-toolkit-vs-making-api-calls"></a>Utilisation de la boîte à outils vs des appels d’API

À ce stade, vous vous demandez peut-être pourquoi vous avez rencontré les problèmes liés à l’utilisation de l' **MSGraphClient** , lorsque le kit d’outils procède à votre travail. Le kit de outils est conçu pour afficher les résultats que vous interrogez à partir de Microsoft Graph, comme une liste d’événements. Toutefois, il existe des scénarios dans lesquels vous devez faire des appels d’API.

- Les appels d’API qui ne sont pas une `GET` demande. Par exemple, la création d’un événement dans le calendrier ou la mise à jour du numéro de téléphone d’un utilisateur.
- Appels d’API permettant d’obtenir des données destinées à être utilisées « en arrière-plan » et non affichées directement.
