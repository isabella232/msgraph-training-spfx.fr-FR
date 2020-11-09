---
ms.openlocfilehash: 19bd57df9f349d67e9f10e7dd70f02231950b010
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823369"
---
<!-- markdownlint-disable MD002 MD041 -->

SharePoint Framework élimine la nécessité d’enregistrer une application dans Azure AD pour obtenir des jetons d’accès pour accéder à Microsoft Graph. Elle gère l’authentification de l’utilisateur qui est connecté à SharePoint, ce qui permet à votre composant WebPart d’obtenir des jetons utilisateur. Votre composant WebPart doit indiquer les [étendues d’autorisation de graphique](https://docs.microsoft.com/graph/permissions-reference) dont il a besoin, et un administrateur client peut approuver ces autorisations lors de l’installation.

## <a name="configure-permissions"></a>Configurer des autorisations

1. Open **. dossier/config/package-solution.js**.

1. Ajoutez le code suivant à la `solution` propriété.

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

L' `Calendars.ReadWrite` autorisation permet à votre composant WebPart d’extraire le calendrier de l’utilisateur et d’ajouter des événements à l’aide de Microsoft Graph. Les autres autorisations sont utilisées par les composants de la boîte à outils Microsoft Graph pour afficher des informations sur les participants aux événements et les organisateurs.

## <a name="optional-test-token-acquisition"></a>Facultatif : test d’acquisition de jeton

> [!NOTE]
> Le reste des étapes de cette page sont facultatifs. Si vous préférez utiliser le codage Microsoft Graph immédiatement, vous pouvez passer à [un affichage Calendrier](/graph/tutorials/spfx?tutorial-step=3).

Nous allons ajouter du code temporaire au composant WebPart pour tester l’acquisition de jetons.

1. Ouvrez **./SRC/WebParts/graphTutorial/GraphTutorialWebPart.TS** et ajoutez l' `import` instruction suivante en haut du fichier.

    ```typescript
    import { AadTokenProvider } from '@microsoft/sp-http';
    ```

1. Remplacez la fonction `render` existante par ce qui suit.

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

### <a name="deploy-the-web-part"></a>Déployer le composant WebPart

1. Exécutez les deux commandes suivantes dans votre interface CLI pour créer et créer un package de votre composant WebPart.

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. Ouvrez votre navigateur et accédez au catalogue d’applications SharePoint de votre client. Sélectionnez l’élément de menu **apps pour SharePoint** dans la partie gauche.

1. Téléchargez le fichier **./SharePoint/solution/Graph-Tutorial.sppkg** .

1. Dans l’invite **do do Trust...** , confirmez que l’invite affiche la liste des 4 autorisations Microsoft Graph que vous avez définies dans le fichier **package-solution.js** . Sélectionnez **mettre cette solution à disposition de tous les sites de l’organisation** , puis sélectionnez **déployer**.

1. Accédez au [Centre d’administration SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) à l’aide d’un administrateur client.

1. Dans le menu de gauche, sélectionnez **avancé** , puis **accès à l’API**.

1. Sélectionnez chacune des demandes en attente dans le package **Graph-Tutorial-Client-Side-solution** , puis choisissez **approuver**.

    ![Capture d’écran de la page d’accès à l’API du centre d’administration SharePoint](images/api-access.png)

### <a name="test-the-web-part"></a>Tester le composant WebPart

1. Accédez à un site SharePoint où vous souhaitez tester le composant WebPart. Créez une page sur laquelle tester le composant WebPart.

1. Utilisez le sélecteur de composants WebPart pour rechercher le composant WebPart **GraphTutorial** et l’ajouter à la page.

    ![Capture d’écran du composant WebPart GraphTutorial dans le sélecteur de composants WebPart](images/add-web-part.png)

1. Le jeton d’accès s’imprime sous l' **écran d’accueil de SharePoint !** message dans le composant WebPart. Vous pouvez copier ce jeton et l’analyser à [https://jwt.ms/](https://jwt.ms/) l’adresse pour vérifier qu’il contient les étendues d’autorisation requises par le composant WebPart.

    ![Capture d’écran du composant WebPart affichant un jeton d’accès](images/access-token.png)
