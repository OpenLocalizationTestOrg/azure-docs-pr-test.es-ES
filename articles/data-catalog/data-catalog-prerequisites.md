---
title: "requisitos previos del catálogo de datos de aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre los requisitos previos de hello que necesita tooget iniciado con el catálogo de datos de Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="b528c-103">Requisitos previos de Catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="b528c-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="b528c-104">Debe tootake cuidado algunas cosas para poder configurar el catálogo de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b528c-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="b528c-105">No se preocupe, este proceso lleva poco tiempo.</span><span class="sxs-lookup"><span data-stu-id="b528c-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="b528c-106">Suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="b528c-106">Azure subscription</span></span>
<span data-ttu-id="b528c-107">tooset el catálogo de datos, debe ser propietario de Hola o copropietario de una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b528c-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="b528c-108">Suscripciones de Azure le ayudarán a organizar los recursos de toocloud-servicio de acceso como el catálogo de datos.</span><span class="sxs-lookup"><span data-stu-id="b528c-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="b528c-109">También le ayudan a controlar cómo se informa, factura y paga el uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="b528c-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="b528c-110">Cada suscripción puede tener una configuración de facturación y pago independiente, por lo que puede tener suscripciones y planes que varían según el departamento, proyecto, oficina regional, etc.</span><span class="sxs-lookup"><span data-stu-id="b528c-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="b528c-111">Cada servicio en la nube pertenece tooa suscripción, y deberá toohave una suscripción antes de configurar el catálogo de datos.</span><span class="sxs-lookup"><span data-stu-id="b528c-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="b528c-112">más información, consulte toolearn [administrar cuentas, suscripciones y roles administrativos](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b528c-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="b528c-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b528c-113">Azure Active Directory</span></span>
<span data-ttu-id="b528c-114">tooset el catálogo de datos, debe haber iniciado sesión con una cuenta de usuario de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b528c-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="b528c-115">Azure AD proporciona una manera sencilla para la identidad de negocio toomanage y acceso, tanto en la nube de Hola y local.</span><span class="sxs-lookup"><span data-stu-id="b528c-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="b528c-116">Los usuarios pueden utilizar una sola cuenta profesional o educativa para tooany de inicio de sesión único en la nube y local de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b528c-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="b528c-117">El catálogo de datos usa inicio de sesión en Azure AD tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="b528c-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="b528c-118">más información, consulte toolearn [¿qué es Azure Active Directory?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b528c-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b528c-119">Mediante el uso de hello [portal de Azure](http://portal.azure.com/), puede iniciar sesión cuenta con una cuenta Microsoft personal o Azure Active Directory profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="b528c-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="b528c-120">tooset el catálogo de datos mediante el uso de Hola o portal de Azure o hello [portal del catálogo de datos](http://www.azuredatacatalog.com), debe iniciar sesión con una cuenta de Azure Active Directory, no una cuenta personal.</span><span class="sxs-lookup"><span data-stu-id="b528c-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="b528c-121">Configuración de directivas de Active Directory</span><span class="sxs-lookup"><span data-stu-id="b528c-121">Active Directory policy configuration</span></span>
<span data-ttu-id="b528c-122">Puede darse el caso donde puede iniciar sesión en el portal del catálogo de datos de toohello, pero al intentar toosign en la herramienta de registro de origen de datos de toohello, recibirá un mensaje de error que le impide el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b528c-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="b528c-123">Podría producirse un comportamiento de este problema solo cuando se encuentra en la red de empresa de Hola o puede ocurrir sólo cuando se conecta desde la red de empresa de hello fuera.</span><span class="sxs-lookup"><span data-stu-id="b528c-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="b528c-124">herramienta de registro de origen de datos de Hello utiliza autenticación mediante formularios toovalidate sus credenciales de usuario en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b528c-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="b528c-125">toohelp que iniciar sesión correctamente, un administrador de Active Directory debe habilitar la autenticación de formularios de hello directiva de autenticación Global.</span><span class="sxs-lookup"><span data-stu-id="b528c-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="b528c-126">En la directiva de autenticación Global de hello, métodos de autenticación pueden ser conexiones habilitadas por separado para la intranet y extranet, tal y como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b528c-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="b528c-127">Errores de inicio de sesión pueden ocurrir si la autenticación de formularios no está habilitada para red de Hola desde el que se está conectando.</span><span class="sxs-lookup"><span data-stu-id="b528c-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Directiva de autenticación global de Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="b528c-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b528c-129">Next steps</span></span>
<span data-ttu-id="b528c-130">Para obtener más información, vea [Configuración de directivas de autenticación](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="b528c-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
