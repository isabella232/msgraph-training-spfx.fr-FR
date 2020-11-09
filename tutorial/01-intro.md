---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823345"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="10a81-101">Ce didacticiel vous apprend à créer un [composant WebPart côté client SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) qui utilise l’API Microsoft Graph pour récupérer des informations de calendrier pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="10a81-101">This tutorial teaches you how to build a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="10a81-102">Si vous préférez télécharger simplement le didacticiel terminé, vous pouvez télécharger ou cloner le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).</span><span class="sxs-lookup"><span data-stu-id="10a81-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10a81-103">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="10a81-103">Prerequisites</span></span>

<span data-ttu-id="10a81-104">Avant de commencer ce didacticiel, les outils suivants doivent être installés sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="10a81-104">Before you start this tutorial, you should have the following tools installed on your development machine.</span></span>

- [<span data-ttu-id="10a81-105">Node.js</span><span class="sxs-lookup"><span data-stu-id="10a81-105">Node.js</span></span>](https://nodejs.org/en/download/releases/)
- [<span data-ttu-id="10a81-106">Yeoman</span><span class="sxs-lookup"><span data-stu-id="10a81-106">Yeoman</span></span>](https://yeoman.io/)
- [<span data-ttu-id="10a81-107">Gulp</span><span class="sxs-lookup"><span data-stu-id="10a81-107">Gulp</span></span>](https://gulpjs.com/)
- [<span data-ttu-id="10a81-108">Générateur SharePoint Yeoman</span><span class="sxs-lookup"><span data-stu-id="10a81-108">Yeoman SharePoint generator</span></span>](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

<span data-ttu-id="10a81-109">Vous trouverez plus de détails sur la configuration requise pour le développement de SharePoint Framework dans [la rubrique Configuration de votre environnement de développement SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).</span><span class="sxs-lookup"><span data-stu-id="10a81-109">You can find more details about requirements for SharePoint Framework development at [Set up your SharePoint Framework development environment](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10a81-110">SharePoint Framework requiert Node.js version 10. x.</span><span class="sxs-lookup"><span data-stu-id="10a81-110">SharePoint Framework requires Node.js version 10.x.</span></span> <span data-ttu-id="10a81-111">Veillez à installer la version appropriée.</span><span class="sxs-lookup"><span data-stu-id="10a81-111">Be sure to install the correct version.</span></span>

<span data-ttu-id="10a81-112">Vous devez également disposer d’un compte professionnel ou scolaire Microsoft, avec accès à un compte d’administrateur général au sein de la même organisation.</span><span class="sxs-lookup"><span data-stu-id="10a81-112">You should also have a Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="10a81-113">Si vous n’avez pas de compte Microsoft, vous pouvez vous [inscrire au programme pour les développeurs office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement gratuit à Office 365.</span><span class="sxs-lookup"><span data-stu-id="10a81-113">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

<span data-ttu-id="10a81-114">Votre client Microsoft 365 doit être [configuré pour le développement de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), avec un catalogue d’applications et un site de test créés avant de commencer ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="10a81-114">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="10a81-115">Ce didacticiel a été écrit avec les versions suivantes des outils ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="10a81-115">This tutorial was written with the following versions of the above tools.</span></span> <span data-ttu-id="10a81-116">Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais cela n’a pas été testé.</span><span class="sxs-lookup"><span data-stu-id="10a81-116">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="10a81-117">Node.js 10.22.0</span><span class="sxs-lookup"><span data-stu-id="10a81-117">Node.js 10.22.0</span></span>
> - <span data-ttu-id="10a81-118">Yeoman 3.1.1</span><span class="sxs-lookup"><span data-stu-id="10a81-118">Yeoman 3.1.1</span></span>
> - <span data-ttu-id="10a81-119">Gulp 4.0.2</span><span class="sxs-lookup"><span data-stu-id="10a81-119">Gulp 4.0.2</span></span>
> - <span data-ttu-id="10a81-120">Yeoman du générateur SharePoint 1.11.0</span><span class="sxs-lookup"><span data-stu-id="10a81-120">Yeoman SharePoint generator 1.11.0</span></span>

## <a name="feedback"></a><span data-ttu-id="10a81-121">Commentaires</span><span class="sxs-lookup"><span data-stu-id="10a81-121">Feedback</span></span>

<span data-ttu-id="10a81-122">Veuillez fournir des commentaires sur ce didacticiel dans le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).</span><span class="sxs-lookup"><span data-stu-id="10a81-122">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>
