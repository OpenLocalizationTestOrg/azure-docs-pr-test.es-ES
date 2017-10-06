---
title: "aaaUser aprovisionar la aplicación de la Galería de Azure AD tooan es tomar horas o más | Documentos de Microsoft"
description: "Cómo toofind out ¿por qué aprovisionar la aplicación de tooyour puede esté tardando más de lo esperado"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a>Aplicación de la Galería de Azure AD tooan de aprovisionamiento de usuarios es tomar horas o más

Cuando habilita por primera vez el aprovisionamiento automático de una aplicación, la sincronización inicial Hola puede tardar de horas, tooseveral 20 minutos, según el tamaño de hello del directorio de Azure AD de Hola y número de Hola de usuarios en el ámbito de aprovisionamiento. 

Las sincronizaciones posteriores después de la sincronización inicial de hello ser más rápidas, como las marcas de agua que representan el estado de Hola de ambos sistemas después de la sincronización inicial hello, mejorar el rendimiento de las sincronizaciones posteriores de almacenes de hello aprovisionamiento del servicio.

## <a name="how-tooimprove-provisioning-performance"></a>¿Cómo tooimprove aprovisionamiento de rendimiento

Si la sincronización inicial Hola está tardando más de unas pocas horas, es único lo que puede hacer tooimprove rendimiento:

-   **Filtros de ámbito del usuario.** Filtros de ámbito permiten toofine ajustar datos de Hola Hola aprovisionamiento extrae de servicio de Azure AD mediante el filtrado de usuarios basados en valores de atributo determinados. Para más información sobre los filtros de ámbito, consulte [Aprovisionamiento de aplicaciones basado en atributos con filtros de ámbito](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

## <a name="next-steps"></a>Pasos siguientes
[Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones con Azure Active Directory](active-directory-saas-app-provisioning.md)

