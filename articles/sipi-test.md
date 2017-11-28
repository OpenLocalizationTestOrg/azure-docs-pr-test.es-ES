---
title: Archivo de prueba de Sipi | Documentos de Microsoft
description: Archivo de prueba para comprobar las dependencias de ReadyForTest
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="d3663-103">Archivo de prueba de Sipi</span><span class="sxs-lookup"><span data-stu-id="d3663-103">Sipi test file</span></span>

<span data-ttu-id="d3663-104">Este inicio rápido le ayuda a registrar una aplicación en un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="d3663-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="d3663-105">Cuando haya terminado, la aplicación se habrá registrado para su uso en el inquilino de Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="d3663-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3663-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d3663-106">Prerequisites</span></span>

<span data-ttu-id="d3663-107">Para crear una aplicación que acepte registros e inicios de sesión de consumidores, primero deberá registrarla en un inquilino de Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d3663-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="d3663-108">Para obtener su propio inquilino, siga los pasos descritos en [Creación de un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d3663-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="d3663-109">Las aplicaciones creadas en la hoja de Azure AD B2C de Azure Portal se deben administrar desde la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="d3663-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="d3663-110">Si edita las aplicaciones B2C mediante PowerShell u otro portal, dejan de ser compatibles y no funcionan con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d3663-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="d3663-111">Consulte los detalles en la sección [Aplicaciones con errores](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="d3663-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="d3663-112">Ir a la configuración de B2C</span><span class="sxs-lookup"><span data-stu-id="d3663-112">Navigate to B2C settings</span></span>

<span data-ttu-id="d3663-113">Inicie sesión en [Azure Portal](https://portal.azure.com/) como administrador global del inquilino B2C.</span><span class="sxs-lookup"><span data-stu-id="d3663-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="d3663-114">Elija los pasos siguientes en función del tipo de aplicación que vaya a registrar:</span><span class="sxs-lookup"><span data-stu-id="d3663-114">Choose next steps based on the application type you are registering:</span></span>
