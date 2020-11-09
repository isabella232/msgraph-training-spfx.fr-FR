---
ms.openlocfilehash: ca72a0d6047d3cd275d34e2d0b4e3c54dbab5375
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831289"
---
# <a name="how-to-run-the-completed-project"></a>Exécution du projet terminé

## <a name="prerequisites"></a>Conditions préalables

Pour exécuter le projet terminé dans ce dossier, vous avez besoin des éléments suivants :

- [Node.js](https://nodejs.org/en/download/releases/) version 10. x
- [Gulp](https://gulpjs.com/)
- Un compte professionnel ou scolaire Microsoft, avec accès à un compte d’administrateur général au sein de la même organisation. Si vous n’avez pas de compte Microsoft, vous pouvez vous [inscrire au programme pour les développeurs office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement gratuit à Office 365.
- Votre client Microsoft 365 doit être [configuré pour le développement de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), avec un catalogue d’applications et un site de test créés avant de commencer ce didacticiel.

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

    ![Capture d’écran de la page d’accès à l’API du centre d’administration SharePoint](../tutorial/images/api-access.png)

### <a name="test-the-web-part"></a>Tester le composant WebPart

1. Accédez à un site SharePoint où vous souhaitez tester le composant WebPart. Créez une page sur laquelle tester le composant WebPart.

1. Utilisez le sélecteur de composants WebPart pour rechercher le composant WebPart **GraphTutorial** et l’ajouter à la page.

    ![Capture d’écran du composant WebPart GraphTutorial dans le sélecteur de composants WebPart](../tutorial/images/add-web-part.png)
