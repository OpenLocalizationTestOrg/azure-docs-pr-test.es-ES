---
title: aaaAzure AD Connect en Microsoft Cloud Alemania
description: "Azure AD Connect integrará sus directorios locales con Azure Active Directory. Esto le permite tooprovide una identidad común para las aplicaciones de Office 365, Azure y SaaS integrada con Azure AD."
keywords: "Introducción tooAzure AD Connect, información general de Azure AD Connect, ¿qué es Azure AD Connect, instalar active directory, Alemania, bosque negro"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="d4a5b-105">Azure AD Connect en Microsoft Cloud Germany- Versión preliminar pública</span><span class="sxs-lookup"><span data-stu-id="d4a5b-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="d4a5b-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="d4a5b-106">Introduction</span></span>
<span data-ttu-id="d4a5b-107">Azure AD Connect proporciona sincronización entre instancias de Active Directory y Azure Active Directory locales.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="d4a5b-108">Actualmente, muchos de los escenarios de hello en [Alemania Microsoft Cloud](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) debe realizarla de operador de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="d4a5b-109">Al usar Microsoft Cloud Alemania, debe tener en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="d4a5b-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="d4a5b-110">Hola que direcciones URL siguientes deben estar abiertas en un servidor proxy para sincronización toooccur correctamente:</span><span class="sxs-lookup"><span data-stu-id="d4a5b-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="d4a5b-111">*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="d4a5b-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="d4a5b-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="d4a5b-112">*.windows.net</span></span>
  * * <span data-ttu-id="d4a5b-113">Listas de revocación de certificados</span><span class="sxs-lookup"><span data-stu-id="d4a5b-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="d4a5b-114">Al iniciar sesión en el directorio de Azure AD tooyour, debe usar una cuenta de dominio de onmicrosoft.de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="d4a5b-115">Hola siguientes características no está disponible:</span><span class="sxs-lookup"><span data-stu-id="d4a5b-115">hello following features are not available:</span></span>
  * <span data-ttu-id="d4a5b-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="d4a5b-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="d4a5b-117">Actualizaciones automáticas</span><span class="sxs-lookup"><span data-stu-id="d4a5b-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="d4a5b-118">Descargar</span><span class="sxs-lookup"><span data-stu-id="d4a5b-118">Download</span></span>
<span data-ttu-id="d4a5b-119">Puede descargar Azure AD Connect de hoja de Azure AD Connect hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="d4a5b-120">Siga las instrucciones de Hola por debajo de la hoja de toolocate hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="d4a5b-121">Hola hoja de Connect de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4a5b-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="d4a5b-122">Una vez que haya iniciado sesión toohello portal de Azure, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="d4a5b-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="d4a5b-123">Vaya tooBrowse</span><span class="sxs-lookup"><span data-stu-id="d4a5b-123">Go tooBrowse</span></span>
2. <span data-ttu-id="d4a5b-124">Seleccione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="d4a5b-125">Después, seleccione Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="d4a5b-126">Debería ver Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4a5b-126">You should see hello following:</span></span>

![Hoja Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="d4a5b-128">Hello tabla siguiente describen características de Hola se muestra en la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="d4a5b-129">Título</span><span class="sxs-lookup"><span data-stu-id="d4a5b-129">Title</span></span> | <span data-ttu-id="d4a5b-130">Description</span><span class="sxs-lookup"><span data-stu-id="d4a5b-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4a5b-131">ESTADO DE SINCRONIZACIÓN</span><span class="sxs-lookup"><span data-stu-id="d4a5b-131">SYNC STATUS</span></span> |<span data-ttu-id="d4a5b-132">Le permite saber si la sincronización está habilitada o no.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="d4a5b-133">ÚLTIMA SINCRONIZACIÓN</span><span class="sxs-lookup"><span data-stu-id="d4a5b-133">LAST SYNC</span></span> |<span data-ttu-id="d4a5b-134">Hola última vez una sincronización correcta completada.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="d4a5b-135">DOMINIOS FEDERADOS</span><span class="sxs-lookup"><span data-stu-id="d4a5b-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="d4a5b-136">Muestra el número de Hola de dominios federados configurado actualmente.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="d4a5b-137">Instalación</span><span class="sxs-lookup"><span data-stu-id="d4a5b-137">Installation</span></span>
<span data-ttu-id="d4a5b-138">tooinstall Azure AD Connect, puede usar la documentación de hello [aquí](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="d4a5b-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="d4a5b-139">Características avanzadas e información adicional</span><span class="sxs-lookup"><span data-stu-id="d4a5b-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="d4a5b-140">Para obtener información adicional e instrucciones sobre la configuración personalizada o configuraciones avanzadas, empiece con la [integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d4a5b-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="d4a5b-141">Esta página proporciona información y vínculos tooadditional instrucciones.</span><span class="sxs-lookup"><span data-stu-id="d4a5b-141">This page provides information and links tooadditional guidance.</span></span>

