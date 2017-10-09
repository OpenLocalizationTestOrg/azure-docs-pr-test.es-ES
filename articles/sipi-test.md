---
title: Archivo de prueba de Sipi | Documentos de Microsoft
description: Probar las dependencias de archivo toocheck ReadyForTest
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="daff4-103">Archivo de prueba de Sipi</span><span class="sxs-lookup"><span data-stu-id="daff4-103">Sipi test file</span></span>

<span data-ttu-id="daff4-104">Este inicio rápido le ayuda a registrar una aplicación en un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="daff4-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="daff4-105">Cuando haya terminado, la aplicación se registra para su uso en el inquilino de hello Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="daff4-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daff4-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="daff4-106">Prerequisites</span></span>

<span data-ttu-id="daff4-107">toobuild una aplicación que acepta consumidor registrarse e iniciar sesión, necesita primero la aplicación de hello tooregister con un inquilino de Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="daff4-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="daff4-108">Obtener su propio inquilino mediante el uso de pasos de hello descritos en [crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="daff4-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="daff4-109">Aplicaciones creadas a partir de la hoja de Azure AD B2C Hola Hola portal de Azure deben administrarse desde Hola misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="daff4-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="daff4-110">Si edita las aplicaciones de B2C Hola con PowerShell u otro portal, que se convierten en no compatibles y no funcionan con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="daff4-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="daff4-111">Ver detalles de hello [errores en aplicaciones](#faulted-apps) sección.</span><span class="sxs-lookup"><span data-stu-id="daff4-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="daff4-112">Desplácese tooB2C configuración</span><span class="sxs-lookup"><span data-stu-id="daff4-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="daff4-113">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) como Hola administrador Global del inquilino de hello B2C.</span><span class="sxs-lookup"><span data-stu-id="daff4-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="daff4-114">Elija los pasos siguientes en función de tipo de aplicación Hola que va a registrar:</span><span class="sxs-lookup"><span data-stu-id="daff4-114">Choose next steps based on hello application type you are registering:</span></span>
