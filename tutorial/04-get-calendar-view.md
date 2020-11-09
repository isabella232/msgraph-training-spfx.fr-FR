---
ms.openlocfilehash: c239c1ea6daae99cc5a65b7b95508ccb2a1bf014
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823357"
---
<!-- markdownlint-disable MD002 MD041 -->

SharePoint Framework fournit le [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) pour effectuer des appels à Microsoft Graph. Cette classe inclut dans la [bibliothèque cliente JavaScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript)une pré-authentification avec l’utilisateur actuellement connecté.

Étant donné qu’il enveloppe la bibliothèque JavaScript existante, son utilisation est identique et elle est entièrement compatible avec les définitions de l’autotest de Microsoft Graph.

## <a name="get-the-users-calendar"></a>Obtenir le calendrier de l’utilisateur

1. Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.TS** et ajoutez les `import` instructions suivantes en haut du fichier.

    ```typescript
    import { MSGraphClient } from '@microsoft/sp-http';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import { startOfWeek, endOfWeek, setDay, set } from 'date-fns';
    ```

1. Ajoutez la fonction suivante à la classe **GraphTutorialWebPart** pour afficher une erreur.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderGraphErrorSnippet":::

1. Ajoutez la fonction suivante pour imprimer les événements dans le calendrier de l’utilisateur.

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

1. Remplacez la fonction `render` existante par ce qui suit.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderSnippet":::

    Notez ce que fait ce code.

    - Elle utilise `this.context.msGraphClientFactory.getClient` pour obtenir un objet **MSGraphClient** authentifié.
    - Il appelle le `/me/calendarView` point de terminaison, en définissant les paramètres de la `startDateTime` requête et le `endDateTime` début et la fin de la semaine en cours.
    - Il utilise `select` pour limiter les champs qui sont renvoyés, en ne demandant que les champs utilisés par l’application.
    - Il utilise `orderby` pour trier les événements en fonction de leur heure de début.
    - Il utilise `top` pour limiter les résultats à 25 événements.

## <a name="deploy-the-web-part"></a>Déployer le composant WebPart

1. Exécutez les deux commandes suivantes dans votre interface CLI pour créer et créer un package de votre composant WebPart.

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. Ouvrez votre navigateur et accédez au catalogue d’applications SharePoint de votre client. Sélectionnez l’élément de menu **apps pour SharePoint** dans la partie gauche.

1. Téléchargez le fichier **./SharePoint/solution/Graph-Tutorial.sppkg** .

1. Dans l’invite **do do Trust...** , confirmez que l’invite affiche la liste des 4 autorisations Microsoft Graph que vous avez définies dans le fichier **package-solution.js** . Sélectionnez **mettre cette solution à disposition de tous les sites de l’organisation** , puis sélectionnez **déployer**.

1. Si vous n’avez pas encore approuvé les autorisations de graphique pour votre composant WebPart, faites-le maintenant.

    1. Accédez au [Centre d’administration SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) à l’aide d’un administrateur client.

    1. Dans le menu de gauche, sélectionnez **avancé** , puis **accès à l’API**.

    1. Sélectionnez chacune des demandes en attente dans le package **Graph-Tutorial-Client-Side-solution** , puis choisissez **approuver**.

        ![Capture d’écran de la page d’accès à l’API du centre d’administration SharePoint](images/api-access.png)

## <a name="test-the-web-part"></a>Tester le composant WebPart

1. Accédez à un site SharePoint où vous souhaitez tester le composant WebPart. Créez une page sur laquelle tester le composant WebPart.

1. Utilisez le sélecteur de composants WebPart pour rechercher le composant WebPart **GraphTutorial** et l’ajouter à la page.

    ![Capture d’écran du composant WebPart GraphTutorial dans le sélecteur de composants WebPart](images/add-web-part.png)

1. Une liste d’événements pour la semaine en cours est imprimée dans le composant WebPart.

    ![Capture d’écran du composant WebPart affichant une liste d’événements](images/calendar-list.png)
