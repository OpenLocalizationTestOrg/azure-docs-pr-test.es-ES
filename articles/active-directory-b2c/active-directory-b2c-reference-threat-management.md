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
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="b5ed1-103">Azure Active Directory B2C: administración de amenazas</span><span class="sxs-lookup"><span data-stu-id="b5ed1-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="b5ed1-104">La administración de amenazas incluye la planeación de la protección frente a ataques contra el sistema y las redes.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="b5ed1-105">Ataques por denegación de servicio podrían hacer que los recursos toointended disponible a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="b5ed1-106">Contraseña ataques responsable toounauthorized acceso tooresources.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="b5ed1-107">Azure Active Directory B2C (Azure AD B2C) tiene características integradas que le pueden ayudar a proteger los datos frente a estas amenazas de varias maneras.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="b5ed1-108">Ataques por denegación de servicio</span><span class="sxs-lookup"><span data-stu-id="b5ed1-108">Denial-of-service attacks</span></span>

<span data-ttu-id="b5ed1-109">B2C de Azure AD usa técnicas de mitigación y detección como cookies SYN y tooprotect de límites de velocidad y la conexión subyacente recursos frente a ataques por denegación de servicio.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="b5ed1-110">Ataques a contraseñas</span><span class="sxs-lookup"><span data-stu-id="b5ed1-110">Password attacks</span></span>

<span data-ttu-id="b5ed1-111">Azure AD B2C también dispone de técnicas de mitigación para los ataques a contraseñas.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="b5ed1-112">La mitigación incluye ataques a contraseñas por fuerza bruta y ataques de diccionario.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="b5ed1-113">Las contraseñas establecidas por los usuarios son necesario toobe bastante compleja.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="b5ed1-114">Mediante el uso de diversas señales, Azure AD B2C analiza integridad Hola de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="b5ed1-115">Se ha diseñado B2C de Azure AD toointelligently diferenciar el usuario de los hackers y botnets.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="b5ed1-116">B2C de Azure AD proporciona una estrategia sofisticadas toolock cuentas en función de las contraseñas de hello especificadas, en la probabilidad de Hola de un ataque.</span><span class="sxs-lookup"><span data-stu-id="b5ed1-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="b5ed1-117">Para obtener más información, visite hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="b5ed1-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
