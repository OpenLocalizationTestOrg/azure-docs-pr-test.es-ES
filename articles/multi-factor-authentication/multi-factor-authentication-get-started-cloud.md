---
title: "Introducción a Azure MFA en la nube | Microsoft Docs"
description: "En esta página de Microsoft Azure Multi-Factor Authentication se describe cómo empezar a trabajar con Azure MFA en la nube."
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
ms.openlocfilehash: 19f3228b874fc4e37bf83388dae4341428226482
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-the-cloud"></a><span data-ttu-id="7d879-103">Introducción a Azure Multi-Factor Authentication en la nube</span><span class="sxs-lookup"><span data-stu-id="7d879-103">Getting started with Azure Multi-Factor Authentication in the cloud</span></span>
<span data-ttu-id="7d879-104">En este artículo aprenderá a usar Azure Multi-Factor Authentication en la nube.</span><span class="sxs-lookup"><span data-stu-id="7d879-104">This article walks through how to get started using Azure Multi-Factor Authentication in the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="7d879-105">La siguiente documentación proporciona información sobre cómo habilitar usuarios mediante el **Portal de Azure clásico**.</span><span class="sxs-lookup"><span data-stu-id="7d879-105">The following documentation provides information on how to enable users using the **Azure Classic Portal**.</span></span> <span data-ttu-id="7d879-106">Si busca información sobre cómo configurar Azure Multi-Factor Authentication para usuarios de Office 365, consulte [Configurar la autenticación multifactor para usuarios de Office 365](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="7d879-106">If you are looking for information on how to set up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![MFA en la nube](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="7d879-108">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="7d879-108">Prerequisite</span></span>
<span data-ttu-id="7d879-109">[Registrarse para obtener una suscripción a Azure](https://azure.microsoft.com/pricing/free-trial/) : si todavía no dispone de una suscripción de Azure, es necesario que se registre para obtener una.</span><span class="sxs-lookup"><span data-stu-id="7d879-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need to sign-up for one.</span></span> <span data-ttu-id="7d879-110">Si simplemente está comenzando a utilizar Azure MFA, puede usar una suscripción de prueba.</span><span class="sxs-lookup"><span data-stu-id="7d879-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="7d879-111">Habilitación de Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="7d879-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="7d879-112">Siempre y cuando los usuarios tengan licencias que incluyen Azure Multi-Factor Authentication, no hay nada que se pueda hacer para activar Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="7d879-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="7d879-113">Puede iniciar la solicitud de la verificación en dos pasos en cada usuario individual.</span><span class="sxs-lookup"><span data-stu-id="7d879-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="7d879-114">Las licencias que habilitan Azure MFA son:</span><span class="sxs-lookup"><span data-stu-id="7d879-114">The licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="7d879-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="7d879-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="7d879-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="7d879-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="7d879-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="7d879-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="7d879-118">Si no dispone una de estas tres licencias o no tiene suficientes licencias para cubrir a todos los usuarios, es correcto también.</span><span class="sxs-lookup"><span data-stu-id="7d879-118">If you don't have one of these three licenses, or you don't have enough licenses to cover all of your users, that's ok too.</span></span> <span data-ttu-id="7d879-119">Solo tiene que realizar un paso adicional y [crear un proveedor de Muti-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md) en el directorio.</span><span class="sxs-lookup"><span data-stu-id="7d879-119">You just have to do an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="7d879-120">Activación de la verificación en dos pasos para los usuarios</span><span class="sxs-lookup"><span data-stu-id="7d879-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="7d879-121">Utilice uno de los procedimientos enumerados en el artículo sobre la [exigencia de verificación en dos pasos para un usuario o un grupo](multi-factor-authentication-get-started-user-states.md) para empezar a usar Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="7d879-121">Use one of the procedures listed in [How to require two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) to start using Azure MFA.</span></span> <span data-ttu-id="7d879-122">Puede elegir exigir la verificación en dos pasos para todos los inicios de sesión o crear directivas de acceso condicional para exigir la verificación en dos pasos únicamente cuando usted lo necesite.</span><span class="sxs-lookup"><span data-stu-id="7d879-122">You can choose to enforce two-step verification for all sign-ins, or you can create conditional access policies to require two-step verification only when it matters to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d879-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7d879-123">Next Steps</span></span>
<span data-ttu-id="7d879-124">Ahora que ha configurado Azure Multi-Factor Authentication en la nube, puede configurar la implementación.</span><span class="sxs-lookup"><span data-stu-id="7d879-124">Now that you have set up Azure Multi-Factor Authentication in the cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="7d879-125">Consulte [Configuración de Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) para conocer más detalles.</span><span class="sxs-lookup"><span data-stu-id="7d879-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

