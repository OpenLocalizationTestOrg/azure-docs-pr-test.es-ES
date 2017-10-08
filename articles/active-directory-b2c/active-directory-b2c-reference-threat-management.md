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
# <a name="azure-active-directory-b2c-threat-management"></a>Azure Active Directory B2C: administración de amenazas

La administración de amenazas incluye la planeación de la protección frente a ataques contra el sistema y las redes. Ataques por denegación de servicio podrían hacer que los recursos toointended disponible a los usuarios. Contraseña ataques responsable toounauthorized acceso tooresources. Azure Active Directory B2C (Azure AD B2C) tiene características integradas que le pueden ayudar a proteger los datos frente a estas amenazas de varias maneras.

## <a name="denial-of-service-attacks"></a>Ataques por denegación de servicio

B2C de Azure AD usa técnicas de mitigación y detección como cookies SYN y tooprotect de límites de velocidad y la conexión subyacente recursos frente a ataques por denegación de servicio.

## <a name="password-attacks"></a>Ataques a contraseñas

Azure AD B2C también dispone de técnicas de mitigación para los ataques a contraseñas. La mitigación incluye ataques a contraseñas por fuerza bruta y ataques de diccionario. Las contraseñas establecidas por los usuarios son necesario toobe bastante compleja. Mediante el uso de diversas señales, Azure AD B2C analiza integridad Hola de solicitudes. Se ha diseñado B2C de Azure AD toointelligently diferenciar el usuario de los hackers y botnets. B2C de Azure AD proporciona una estrategia sofisticadas toolock cuentas en función de las contraseñas de hello especificadas, en la probabilidad de Hola de un ataque.

Para obtener más información, visite hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).
