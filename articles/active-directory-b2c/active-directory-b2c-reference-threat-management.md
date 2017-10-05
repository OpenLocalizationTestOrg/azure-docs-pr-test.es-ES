---
title: "Azure Active Directory B2C: administración de amenazas | Microsoft Docs"
description: "Obtenga información sobre las técnicas de detección y mitigación de los ataques por denegación de servicio y los ataques a contraseñas en Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="0f381-103">Azure Active Directory B2C: administración de amenazas</span><span class="sxs-lookup"><span data-stu-id="0f381-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="0f381-104">La administración de amenazas incluye la planeación de la protección frente a ataques contra el sistema y las redes.</span><span class="sxs-lookup"><span data-stu-id="0f381-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="0f381-105">Los ataques por denegación de servicio pueden hacer que los recursos no estén disponibles para los usuarios previstos.</span><span class="sxs-lookup"><span data-stu-id="0f381-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="0f381-106">Los ataques a contraseñas pueden dar lugar a un acceso no autorizado a los recursos.</span><span class="sxs-lookup"><span data-stu-id="0f381-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="0f381-107">Azure Active Directory B2C (Azure AD B2C) tiene características integradas que le pueden ayudar a proteger los datos frente a estas amenazas de varias maneras.</span><span class="sxs-lookup"><span data-stu-id="0f381-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="0f381-108">Ataques por denegación de servicio</span><span class="sxs-lookup"><span data-stu-id="0f381-108">Denial-of-service attacks</span></span>

<span data-ttu-id="0f381-109">Azure AD B2C usa técnicas de detección y mitigación, como las cookies SYN y los límites de velocidad y conexión, para proteger los recursos subyacentes frente a los ataques por denegación de servicio.</span><span class="sxs-lookup"><span data-stu-id="0f381-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="0f381-110">Ataques a contraseñas</span><span class="sxs-lookup"><span data-stu-id="0f381-110">Password attacks</span></span>

<span data-ttu-id="0f381-111">Azure AD B2C también dispone de técnicas de mitigación para los ataques a contraseñas.</span><span class="sxs-lookup"><span data-stu-id="0f381-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="0f381-112">La mitigación incluye ataques a contraseñas por fuerza bruta y ataques de diccionario.</span><span class="sxs-lookup"><span data-stu-id="0f381-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="0f381-113">Las contraseñas establecidas por los usuarios deben tener una complejidad razonable.</span><span class="sxs-lookup"><span data-stu-id="0f381-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="0f381-114">Mediante el uso de diversas señales, Azure AD B2C analiza la integridad de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="0f381-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="0f381-115">Azure AD B2C está diseñado para diferenciar de forma inteligente los usuarios previstos frente a los hackers y las redes de robots (botnets).</span><span class="sxs-lookup"><span data-stu-id="0f381-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="0f381-116">Azure AD B2C proporciona una estrategia sofisticada para bloquear cuentas en función de las contraseñas usadas ante la posibilidad de un ataque.</span><span class="sxs-lookup"><span data-stu-id="0f381-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="0f381-117">Para obtener más información, visite el [Centro de confianza de Microsoft](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="0f381-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
