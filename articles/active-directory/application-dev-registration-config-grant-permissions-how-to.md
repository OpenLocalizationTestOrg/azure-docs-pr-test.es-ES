---
title: "Concesión de permisos a una aplicación personalizada | Microsoft Docs"
description: "Aprenda a conceder permisos a una aplicación personalizada mediante el portal de Azure AD o un parámetro de dirección URL."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 336b945929f80e1a566f7cf71b40fd799a98c12d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a><span data-ttu-id="fe9e1-103">Concesión de permisos a una aplicación personalizada</span><span class="sxs-lookup"><span data-stu-id="fe9e1-103">How to grant permissions to a custom-developed application</span></span>

<span data-ttu-id="fe9e1-104">Si desea otorgar consentimiento de forma preferente en la aplicación o se produce un error por no otorgar consentimiento a una aplicación, pruebe lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="fe9e1-104">If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.</span></span>

## <a name="how-to-perform-admin-consent-for-your-application"></a><span data-ttu-id="fe9e1-105">Concesión del consentimiento del administrador en la aplicación</span><span class="sxs-lookup"><span data-stu-id="fe9e1-105">How to perform Admin Consent for your application</span></span>

<span data-ttu-id="fe9e1-106">Con este procedimiento, se otorga consentimiento a la aplicación para todos los usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="fe9e1-106">This has the effect of granting consent to the application for all users in your organization.</span></span>

1. <span data-ttu-id="fe9e1-107">Acceda a la hoja **Registros de aplicaciones** como **administrador global** y seleccione la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fe9e1-107">Navigate to the **App Registrations** blade as a **global administrator**, then select the app.</span></span>

2. <span data-ttu-id="fe9e1-108">Seleccione **Permisos necesarios** y, en la parte superior de la hoja, haga clic en el botón **Conceder permisos**.</span><span class="sxs-lookup"><span data-stu-id="fe9e1-108">Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.</span></span>

<span data-ttu-id="fe9e1-109">Si lo desea, también puede generar una solicitud para *login.microsoftonline.com* con sus propias configuraciones de aplicación y anexarla a *&prompt=admin\_consent*.</span><span class="sxs-lookup"><span data-stu-id="fe9e1-109">Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="fe9e1-110">Una vez que la sesión se haya iniciado con las credenciales del administrador, la aplicación tendrá consentimiento para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="fe9e1-110">After signing in with admin credentials, the app has been granted consent for all users.</span></span>

## <a name="how-to-force-user-consent-for-your-application"></a><span data-ttu-id="fe9e1-111">Concesión forzosa del consentimiento del usuario en la aplicación</span><span class="sxs-lookup"><span data-stu-id="fe9e1-111">How to force User Consent for your application</span></span>

* <span data-ttu-id="fe9e1-112">Anexe *&prompt=consent* a las solicitudes de autorización que requieran el consentimiento del usuario final con cada autenticación.</span><span class="sxs-lookup"><span data-stu-id="fe9e1-112">Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe9e1-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe9e1-113">Next steps</span></span>

[<span data-ttu-id="fe9e1-114">Consentimiento e integración de aplicaciones en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe9e1-114">Consent and Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="fe9e1-115">Consentimiento y permisos para las aplicaciones convergentes v2.0 de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe9e1-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="fe9e1-116">Azure AD en StackOverflow</span><span class="sxs-lookup"><span data-stu-id="fe9e1-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
