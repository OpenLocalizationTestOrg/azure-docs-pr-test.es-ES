---
title: "aaaFind espera cuando un usuario específico será capaz de tooaccess una aplicación | Documentos de Microsoft"
description: "Cómo toofind cuando un usuario sumamente importante ser capaz de tooaccess una aplicación se haya configurado para el aprovisionamiento de usuarios con Azure AD"
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a>Determinar cuándo un usuario específico será capaz de tooaccess una aplicación
Cuando se utiliza el aprovisionamiento automático de usuarios con una aplicación, Azure AD aprovisiona y actualiza automáticamente las cuentas de usuario en una aplicación en función de aspectos tales como la [asignación de usuario y grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) con un intervalo programado periódicamente, normalmente cada 10 minutos.

## <a name="how-long-does-it-take"></a>¿Cuánto tiempo tarda?

Hola que tarda un toobe determinado usuario aprovisionado depende principalmente de si ya se ha producido una sincronización inicial "completa".

Hola primera sincronización entre Azure AD y una aplicación puede tardar en cualquier parte de horas de tooseveral de 20 minutos, según el tamaño de hello del directorio de hello Azure AD y número de Hola de usuarios en el ámbito de aprovisionamiento. 

Las sincronizaciones posteriores después de la sincronización inicial de hello ser más rápidas (por ejemplo, dentro de 10 minutos), como almacenes de aprovisionamiento del servicio de hello las marcas de agua que representan el estado de Hola de ambos sistemas después de la sincronización inicial hello, mejorar el rendimiento de las sincronizaciones posteriores.

## <a name="how-toocheck-hello-status-of-a-user"></a>¿Cómo toocheck Hola estado de un usuario

estado de aprovisionamiento de hello toosee para un usuario seleccionado, consulte los registros de auditoría de Azure AD de Hola.

puede tener acceso a Hola aprovisionamiento de los registros de auditoría en el portal de Azure, en Hola Hola **Azure Active Directory &gt; aplicaciones empresariales &gt; \[nombre de la aplicación\] &gt; registros de auditoría**ficha. Hola de filtro inicie sesión en hello **el aprovisionamiento de cuentas** categoría tooonly vea Hola aprovisionamiento eventos para esa aplicación. Puede buscar usuarios en función de Hola "identificador coincidente" que se configuró para ellos en asignaciones de atributos de Hola. 

Por ejemplo, si configuró Hola "nombre principal de usuario" o "dirección de correo electrónico" como Hola coincidencia de atributo en el lado de hello Azure AD y no se aprovisionamiento de usuarios de hello tiene un valor de "audrey@contoso.com", a continuación, los registros de auditoría de Hola de búsqueda para"audrey@contoso.com" y, a continuación, revisar se devuelven las entradas.

Hola aprovisionamiento auditoría registra registro todos hello las operaciones realizadas por hello aprovisionamiento del servicio, incluyendo:

* Consultar en Azure AD los usuarios asignados que están en el ámbito de aprovisionamiento
* Consultar la aplicación de destino de hello existencia Hola de esos usuarios
* Comparar objetos de usuario de hello entre sistema Hola
* Agregar, actualizar o deshabilitar la cuenta de usuario de Hola Hola del sistema de destino en función de comparación de Hola

## <a name="next-steps"></a>Pasos siguientes
[Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''.
