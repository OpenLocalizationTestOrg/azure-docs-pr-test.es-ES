---
title: "Azure AD Connect: instancias de servicio de sincronización | Microsoft Docs"
description: "Esta página documenta las consideraciones especiales para instancias de Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e8321c3d16253226a5931cacbce6fa5d50b697bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="6bf71-103">Azure AD Connect: consideraciones especiales para instancias</span><span class="sxs-lookup"><span data-stu-id="6bf71-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="6bf71-104">Azure AD Connect se utiliza habitualmente con la instancia mundial de Azure AD y Office 365.</span><span class="sxs-lookup"><span data-stu-id="6bf71-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="6bf71-105">Pero también hay otras instancias y estas tienen requisitos diferentes para las direcciones URL y otras consideraciones especiales.</span><span class="sxs-lookup"><span data-stu-id="6bf71-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="6bf71-106">Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="6bf71-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="6bf71-107">[Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) es una nube soberana operada por un administrador de datos alemán.</span><span class="sxs-lookup"><span data-stu-id="6bf71-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="6bf71-108">Direcciones URL para abrir en el servidor proxy</span><span class="sxs-lookup"><span data-stu-id="6bf71-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="6bf71-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="6bf71-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="6bf71-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="6bf71-110">\*.windows.net</span></span> |
| <span data-ttu-id="6bf71-111">+Listas de revocación de certificados</span><span class="sxs-lookup"><span data-stu-id="6bf71-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="6bf71-112">Al iniciar sesión en el inquilino de Azure AD tiene que usar una cuenta en el dominio onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="6bf71-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="6bf71-113">Características que actualmente no están presentes en Microsoft Cloud Germany:</span><span class="sxs-lookup"><span data-stu-id="6bf71-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="6bf71-114">**Azure AD Connect Health** no está disponible.</span><span class="sxs-lookup"><span data-stu-id="6bf71-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="6bf71-115">Las **actualizaciones automáticas** no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="6bf71-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="6bf71-116">La **escritura diferida de contraseñas** está disponible en versión preliminar con Azure AD Connect versión 1.1.570.0 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="6bf71-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="6bf71-117">Otros servicios de Azure AD Premium no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="6bf71-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="6bf71-118">Microsoft Azure Government Cloud</span><span class="sxs-lookup"><span data-stu-id="6bf71-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="6bf71-119">[Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/) es una nube para el gobierno de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="6bf71-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="6bf71-120">Esta nube ha sido compatible con versiones anteriores de DirSync.</span><span class="sxs-lookup"><span data-stu-id="6bf71-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="6bf71-121">A partir de la compilación 1.1.180 de Azure AD Connect la próxima generación de la nube es compatible.</span><span class="sxs-lookup"><span data-stu-id="6bf71-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="6bf71-122">Esta generación utiliza solo puntos de conexión basados en EE. UU. y tiene una lista de direcciones URL diferentes para abrir en el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="6bf71-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="6bf71-123">Direcciones URL para abrir en el servidor proxy</span><span class="sxs-lookup"><span data-stu-id="6bf71-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="6bf71-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6bf71-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="6bf71-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="6bf71-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="6bf71-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6bf71-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="6bf71-127">+Listas de revocación de certificados</span><span class="sxs-lookup"><span data-stu-id="6bf71-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="6bf71-128">Azure AD Connect no puede detectar automáticamente que el inquilino de Azure AD se encuentra en la nube de administración pública.</span><span class="sxs-lookup"><span data-stu-id="6bf71-128">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="6bf71-129">En su lugar, tiene realizar las siguientes acciones al instalar Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6bf71-129">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="6bf71-130">Inicie la instalación de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6bf71-130">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="6bf71-131">Cuando vea la primera página en donde se supone que tiene que aceptar el CLUF, no continúe y deje que el Asistente para instalación se continúe ejecutando.</span><span class="sxs-lookup"><span data-stu-id="6bf71-131">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="6bf71-132">Inicie regedit y cambie la clave del registro `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` al valor `2`.</span><span class="sxs-lookup"><span data-stu-id="6bf71-132">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="6bf71-133">Vuelva al Asistente para instalación de Azure AD Connect, acepte el CLUF y continúe.</span><span class="sxs-lookup"><span data-stu-id="6bf71-133">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="6bf71-134">Durante la instalación, asegúrese de usar la ruta de acceso de instalación de **configuración personalizada** (y no la instalación rápida).</span><span class="sxs-lookup"><span data-stu-id="6bf71-134">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="6bf71-135">Luego continúe la instalación normalmente.</span><span class="sxs-lookup"><span data-stu-id="6bf71-135">Then continue the installation as usual.</span></span>

<span data-ttu-id="6bf71-136">Características que actualmente no están presentes en Microsoft Azure Government Cloud:</span><span class="sxs-lookup"><span data-stu-id="6bf71-136">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="6bf71-137">**Azure AD Connect Health** no está disponible.</span><span class="sxs-lookup"><span data-stu-id="6bf71-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="6bf71-138">Las **actualizaciones automáticas** no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="6bf71-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="6bf71-139">La **escritura diferida de contraseñas** está disponible en versión preliminar con Azure AD Connect versión 1.1.570.0 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="6bf71-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="6bf71-140">Otros servicios de Azure AD Premium no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="6bf71-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bf71-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6bf71-141">Next steps</span></span>
<span data-ttu-id="6bf71-142">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="6bf71-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
