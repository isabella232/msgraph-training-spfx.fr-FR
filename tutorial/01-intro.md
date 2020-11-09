---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823345"
---
<!-- markdownlint-disable MD002 MD041 -->

Ce didacticiel vous apprend à créer un [composant WebPart côté client SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) qui utilise l’API Microsoft Graph pour récupérer des informations de calendrier pour un utilisateur.

> [!TIP]
> Si vous préférez télécharger simplement le didacticiel terminé, vous pouvez télécharger ou cloner le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).

## <a name="prerequisites"></a>Conditions préalables

Avant de commencer ce didacticiel, les outils suivants doivent être installés sur votre ordinateur de développement.

- [Node.js](https://nodejs.org/en/download/releases/)
- [Yeoman](https://yeoman.io/)
- [Gulp](https://gulpjs.com/)
- [Générateur SharePoint Yeoman](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

Vous trouverez plus de détails sur la configuration requise pour le développement de SharePoint Framework dans [la rubrique Configuration de votre environnement de développement SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).

> [!IMPORTANT]
> SharePoint Framework requiert Node.js version 10. x. Veillez à installer la version appropriée.

Vous devez également disposer d’un compte professionnel ou scolaire Microsoft, avec accès à un compte d’administrateur général au sein de la même organisation. Si vous n’avez pas de compte Microsoft, vous pouvez vous [inscrire au programme pour les développeurs office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement gratuit à Office 365.

Votre client Microsoft 365 doit être [configuré pour le développement de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), avec un catalogue d’applications et un site de test créés avant de commencer ce didacticiel.

> [!NOTE]
> Ce didacticiel a été écrit avec les versions suivantes des outils ci-dessus. Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais cela n’a pas été testé.
>
> - Node.js 10.22.0
> - Yeoman 3.1.1
> - Gulp 4.0.2
> - Yeoman du générateur SharePoint 1.11.0

## <a name="feedback"></a>Commentaires

Veuillez fournir des commentaires sur ce didacticiel dans le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).
