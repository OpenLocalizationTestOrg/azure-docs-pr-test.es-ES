---
title: Azure AD Connect en Microsoft Cloud Germany
description: "Azure AD Connect integrará sus directorios locales con Azure Active Directory. Esto le permite proporcionar una identidad común para las aplicaciones de Office 365, Azure y SaaS integradas con Azure AD."
keywords: "introducción a Azure AD Connect, información general de Azure AD Connect, qué es Azure AD Connect, instalación de active directory, Alemania, Selva Negra"
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
ms.openlocfilehash: 4c55b116c0dc080ae316caca873a7b693caa793b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="8dc06-105">Azure AD Connect en Microsoft Cloud Germany- Versión preliminar pública</span><span class="sxs-lookup"><span data-stu-id="8dc06-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="8dc06-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="8dc06-106">Introduction</span></span>
<span data-ttu-id="8dc06-107">Azure AD Connect proporciona sincronización entre instancias de Active Directory y Azure Active Directory locales.</span><span class="sxs-lookup"><span data-stu-id="8dc06-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="8dc06-108">Actualmente, muchos de los escenarios en [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) debe realizarlos el operador.</span><span class="sxs-lookup"><span data-stu-id="8dc06-108">Currently, many of the scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by the operator.</span></span> <span data-ttu-id="8dc06-109">Al usar Microsoft Cloud Germany, debe tener en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8dc06-109">When using Microsoft Cloud Germany, you must be aware of the following:</span></span>

* <span data-ttu-id="8dc06-110">Las direcciones URL siguientes deben estar abiertas en un servidor proxy para que tenga lugar correctamente la sincronización:</span><span class="sxs-lookup"><span data-stu-id="8dc06-110">The following URLs must be opened on a proxy server for synchronization to occur successfully:</span></span>
  
  * <span data-ttu-id="8dc06-111">*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="8dc06-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="8dc06-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="8dc06-112">*.windows.net</span></span>
  * * <span data-ttu-id="8dc06-113">Listas de revocación de certificados</span><span class="sxs-lookup"><span data-stu-id="8dc06-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="8dc06-114">Al iniciar sesión en el directorio de Azure AD tiene que usar una cuenta en el dominio onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="8dc06-114">When you sign in to your Azure AD directory, you must use an account in the onmicrosoft.de domain.</span></span>
* <span data-ttu-id="8dc06-115">No están disponibles las características siguientes:</span><span class="sxs-lookup"><span data-stu-id="8dc06-115">The following features are not available:</span></span>
  * <span data-ttu-id="8dc06-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="8dc06-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="8dc06-117">Actualizaciones automáticas</span><span class="sxs-lookup"><span data-stu-id="8dc06-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="8dc06-118">Descargar</span><span class="sxs-lookup"><span data-stu-id="8dc06-118">Download</span></span>
<span data-ttu-id="8dc06-119">Puede descargar Azure AD Connect en la hoja Azure AD Connect en el portal.</span><span class="sxs-lookup"><span data-stu-id="8dc06-119">You can download Azure AD Connect from the Azure AD Connect blade within the portal.</span></span>  <span data-ttu-id="8dc06-120">Utilice las instrucciones siguientes para localizar la hoja Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8dc06-120">Use the instructions below to locate the Azure AD Connect blade.</span></span>

### <a name="the-azure-ad-connect-blade"></a><span data-ttu-id="8dc06-121">Hoja Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="8dc06-121">The Azure AD Connect Blade</span></span>
<span data-ttu-id="8dc06-122">Cuando haya iniciado sesión en Azure Portal, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="8dc06-122">Once you have signed in to the Azure portal, do the following:</span></span>

1. <span data-ttu-id="8dc06-123">Vaya a Examinar.</span><span class="sxs-lookup"><span data-stu-id="8dc06-123">Go to Browse</span></span>
2. <span data-ttu-id="8dc06-124">Seleccione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8dc06-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="8dc06-125">Después, seleccione Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8dc06-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="8dc06-126">Verá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8dc06-126">You should see the following:</span></span>

![Hoja Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="8dc06-128">En la tabla siguiente se describen las características mostradas en la hoja.</span><span class="sxs-lookup"><span data-stu-id="8dc06-128">The following table describes the features shown in the blade.</span></span>

| <span data-ttu-id="8dc06-129">Título</span><span class="sxs-lookup"><span data-stu-id="8dc06-129">Title</span></span> | <span data-ttu-id="8dc06-130">Description</span><span class="sxs-lookup"><span data-stu-id="8dc06-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8dc06-131">ESTADO DE SINCRONIZACIÓN</span><span class="sxs-lookup"><span data-stu-id="8dc06-131">SYNC STATUS</span></span> |<span data-ttu-id="8dc06-132">Le permite saber si la sincronización está habilitada o no.</span><span class="sxs-lookup"><span data-stu-id="8dc06-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="8dc06-133">ÚLTIMA SINCRONIZACIÓN</span><span class="sxs-lookup"><span data-stu-id="8dc06-133">LAST SYNC</span></span> |<span data-ttu-id="8dc06-134">La última vez que se realizó correctamente una sincronización.</span><span class="sxs-lookup"><span data-stu-id="8dc06-134">The last time a successful sync completed.</span></span> |
| <span data-ttu-id="8dc06-135">DOMINIOS FEDERADOS</span><span class="sxs-lookup"><span data-stu-id="8dc06-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="8dc06-136">Muestra el número de dominios federados configurados.</span><span class="sxs-lookup"><span data-stu-id="8dc06-136">Shows the number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="8dc06-137">Instalación</span><span class="sxs-lookup"><span data-stu-id="8dc06-137">Installation</span></span>
<span data-ttu-id="8dc06-138">Para instalar Azure AD Connect, puede utilizar [esta](active-directory-aadconnect.md#install-azure-ad-connect)documentación.</span><span class="sxs-lookup"><span data-stu-id="8dc06-138">To install Azure AD Connect, you can use the documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="8dc06-139">Características avanzadas e información adicional</span><span class="sxs-lookup"><span data-stu-id="8dc06-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="8dc06-140">Para obtener información adicional e instrucciones sobre la configuración personalizada o configuraciones avanzadas, empiece con la [integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="8dc06-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="8dc06-141">Esta página proporciona información y vínculos a información adicional.</span><span class="sxs-lookup"><span data-stu-id="8dc06-141">This page provides information and links to additional guidance.</span></span>

