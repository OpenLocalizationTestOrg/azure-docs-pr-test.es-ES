---
title: "aaaGet inició Azure MFA en la nube de hello | Documentos de Microsoft"
description: "Se trata de una página de autenticación multifactor de Azure de Microsoft de Hola que describe cómo se inicia tooget con Azure MFA en la nube de Hola."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="cc284-103">Introducción a la autenticación multifactor Azure en la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="cc284-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="cc284-104">Este artículo le guía a través de cómo tooget a usar la autenticación multifactor Azure en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc284-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="cc284-105">Hello siguiente documentación proporciona información acerca de cómo los usuarios de tooenable mediante Hola **Portal clásico de Azure**.</span><span class="sxs-lookup"><span data-stu-id="cc284-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="cc284-106">Si desea obtener información acerca de cómo tooset la autenticación multifactor de Azure para los usuarios de Office 365, vea [configurar la autenticación multifactor para Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="cc284-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![MFA en hello en la nube](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="cc284-108">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="cc284-108">Prerequisite</span></span>
<span data-ttu-id="cc284-109">[Registrarse para obtener una suscripción de Azure](https://azure.microsoft.com/pricing/free-trial/) -si ya no dispone de una suscripción de Azure, necesita toosign telefónico para uno.</span><span class="sxs-lookup"><span data-stu-id="cc284-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="cc284-110">Si simplemente está comenzando a utilizar Azure MFA, puede usar una suscripción de prueba.</span><span class="sxs-lookup"><span data-stu-id="cc284-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="cc284-111">Habilitación de Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="cc284-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="cc284-112">Siempre y cuando los usuarios tienen licencias que incluyen la autenticación multifactor de Azure, no hay nada que necesite toodo tooturn en Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="cc284-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="cc284-113">Puede iniciar la solicitud de la verificación en dos pasos en cada usuario individual.</span><span class="sxs-lookup"><span data-stu-id="cc284-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="cc284-114">licencias de Hola que habilitarla de Azure son:</span><span class="sxs-lookup"><span data-stu-id="cc284-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="cc284-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="cc284-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="cc284-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="cc284-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="cc284-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="cc284-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="cc284-118">Si no dispone de uno de estos tres licencias o no tiene suficientes licencias toocover todos los usuarios, que Aceptar demasiado.</span><span class="sxs-lookup"><span data-stu-id="cc284-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="cc284-119">Sólo tiene toodo un paso adicional y [crear un proveedor de autenticación multifactor](multi-factor-authentication-get-started-auth-provider.md) en el directorio.</span><span class="sxs-lookup"><span data-stu-id="cc284-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="cc284-120">Activación de la verificación en dos pasos para los usuarios</span><span class="sxs-lookup"><span data-stu-id="cc284-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="cc284-121">Utilice uno de los procedimientos de hello enumerados en [cómo verificacion de toorequire para un usuario o grupo](multi-factor-authentication-get-started-user-states.md) toostart uso de MFA de Azure.</span><span class="sxs-lookup"><span data-stu-id="cc284-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="cc284-122">Puede elegir verificacion de tooenforce para todos los inicios de sesión o puede crear verificacion de toorequire de directivas de acceso condicional cuando es importante tooyou.</span><span class="sxs-lookup"><span data-stu-id="cc284-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc284-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc284-123">Next Steps</span></span>
<span data-ttu-id="cc284-124">Ahora que ha configurado la autenticación multifactor de Azure en la nube de hello, puede configurar y configurar la implementación.</span><span class="sxs-lookup"><span data-stu-id="cc284-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="cc284-125">Consulte [Configuración de Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) para conocer más detalles.</span><span class="sxs-lookup"><span data-stu-id="cc284-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

