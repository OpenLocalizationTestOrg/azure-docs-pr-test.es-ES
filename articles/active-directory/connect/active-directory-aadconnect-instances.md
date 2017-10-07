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
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="0fb54-103">Azure AD Connect: consideraciones especiales para instancias</span><span class="sxs-lookup"><span data-stu-id="0fb54-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="0fb54-104">Azure AD Connect se utiliza normalmente con la instancia de todo el mundo Hola de Azure AD y Office 365.</span><span class="sxs-lookup"><span data-stu-id="0fb54-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="0fb54-105">Pero también hay otras instancias y estas tienen requisitos diferentes para las direcciones URL y otras consideraciones especiales.</span><span class="sxs-lookup"><span data-stu-id="0fb54-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="0fb54-106">Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="0fb54-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="0fb54-107">Hola [Alemania Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) es una nube soberano operada por un usuario de confianza de alemán de datos.</span><span class="sxs-lookup"><span data-stu-id="0fb54-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="0fb54-108">Tooopen de direcciones URL en el servidor proxy</span><span class="sxs-lookup"><span data-stu-id="0fb54-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="0fb54-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="0fb54-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="0fb54-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="0fb54-110">\*.windows.net</span></span> |
| <span data-ttu-id="0fb54-111">+Listas de revocación de certificados</span><span class="sxs-lookup"><span data-stu-id="0fb54-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="0fb54-112">Al iniciar sesión en el inquilino de Azure AD tooyour, debe usar una cuenta de dominio de onmicrosoft.de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fb54-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="0fb54-113">Características actualmente no está presentes en hello Microsoft Cloud Alemania:</span><span class="sxs-lookup"><span data-stu-id="0fb54-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="0fb54-114">**Azure AD Connect Health** no está disponible.</span><span class="sxs-lookup"><span data-stu-id="0fb54-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="0fb54-115">Las **actualizaciones automáticas** no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="0fb54-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="0fb54-116">La **escritura diferida de contraseñas** está disponible en versión preliminar con Azure AD Connect versión 1.1.570.0 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="0fb54-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="0fb54-117">Otros servicios de Azure AD Premium no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="0fb54-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="0fb54-118">Microsoft Azure Government Cloud</span><span class="sxs-lookup"><span data-stu-id="0fb54-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="0fb54-119">Hola [nube de Microsoft Azure Government](https://azure.microsoft.com/features/gov/) es una nube de gobierno de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="0fb54-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="0fb54-120">Esta nube ha sido compatible con versiones anteriores de DirSync.</span><span class="sxs-lookup"><span data-stu-id="0fb54-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="0fb54-121">De compilación 1.1.180 de Azure AD Connect, Hola siguiente generación de nube de hello es compatible.</span><span class="sxs-lookup"><span data-stu-id="0fb54-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="0fb54-122">Esta generación utiliza los puntos de conexión según solo Estados Unidos y tiene una lista de direcciones URL tooopen diferentes en el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="0fb54-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="0fb54-123">Tooopen de direcciones URL en el servidor proxy</span><span class="sxs-lookup"><span data-stu-id="0fb54-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="0fb54-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="0fb54-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="0fb54-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="0fb54-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="0fb54-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="0fb54-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="0fb54-127">+Listas de revocación de certificados</span><span class="sxs-lookup"><span data-stu-id="0fb54-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="0fb54-128">Azure AD Connect no es capaz de tooautomatically detectar que el inquilino de Azure AD se encuentra en la nube de gobierno Hola.</span><span class="sxs-lookup"><span data-stu-id="0fb54-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="0fb54-129">En su lugar debe hello tootake las siguientes acciones cuando instalar Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0fb54-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="0fb54-130">Iniciar instalación de Azure AD Connect Hola.</span><span class="sxs-lookup"><span data-stu-id="0fb54-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="0fb54-131">Cuando vea la primera página de Hola se supone que tooaccept Hola términos de licencia, no continúe pero dejar el Asistente para la instalación Hola ejecutar.</span><span class="sxs-lookup"><span data-stu-id="0fb54-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="0fb54-132">Inicie regedit y cambie la clave del registro de hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valor `2`.</span><span class="sxs-lookup"><span data-stu-id="0fb54-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="0fb54-133">Volver al Asistente para la instalación de toohello AD Azure Connect, acepte Hola términos de licencia y continuar.</span><span class="sxs-lookup"><span data-stu-id="0fb54-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="0fb54-134">Durante la instalación, asegúrese de que hello toouse **configuración personalizada** instalación ruta de acceso (y no Express).</span><span class="sxs-lookup"><span data-stu-id="0fb54-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="0fb54-135">A continuación, continuar instalación hello como de costumbre.</span><span class="sxs-lookup"><span data-stu-id="0fb54-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="0fb54-136">Características actualmente no está presentes en la nube de Microsoft Azure Government hello:</span><span class="sxs-lookup"><span data-stu-id="0fb54-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="0fb54-137">**Azure AD Connect Health** no está disponible.</span><span class="sxs-lookup"><span data-stu-id="0fb54-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="0fb54-138">Las **actualizaciones automáticas** no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="0fb54-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="0fb54-139">La **escritura diferida de contraseñas** está disponible en versión preliminar con Azure AD Connect versión 1.1.570.0 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="0fb54-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="0fb54-140">Otros servicios de Azure AD Premium no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="0fb54-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fb54-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0fb54-141">Next steps</span></span>
<span data-ttu-id="0fb54-142">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="0fb54-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
