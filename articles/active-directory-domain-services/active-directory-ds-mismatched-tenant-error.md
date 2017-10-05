---
title: Resolver errores de directorios que no coinciden en dominios administrados existentes de Azure AD Domain Services | Microsoft Docs
description: Entender y resolver errores de directorios que no coinciden en dominios administrados existentes de Azure AD Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 40eb75b7-827e-4d30-af6c-ca3c2af915c7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: 
ms.date: 07/06/2017
ms.author: maheshu
ms.openlocfilehash: ca9ff29f5f91b8d796a29706ab49a82e417d1ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="resolve-mismatched-directory-errors-for-existing-azure-ad-domain-services-managed-domains"></a>Resolver errores de directorios que no coinciden en dominios administrados existentes de Azure AD Domain Services
Tiene un dominio administrado que se ha habilitado mediante el Portal de Azure clásico. Cuando navega al nuevo Azure Portal y ve el dominio administrado, aparece el siguiente mensaje de error:

![Error de directorio que no coincide](.\media\getting-started\mismatched-tenant-error.png)

Este dominio administrado no se puede administrar mientras no se resuelva el error.


## <a name="whats-causing-this-error"></a>¿Qué es lo que causa este error?
Este error se produce cuando el dominio administrado y la red virtual en la que está habilitado pertenecen a dos inquilinos de Azure AD diferentes. Por ejemplo, tiene un dominio administrado denominado "contoso.com" que se ha habilitado para el inquilino de Azure AD de Contoso, pero la red virtual de Azure en la que se ha habilitado el dominio administrado pertenece a Fabrikam, un inquilino de Azure AD diferente.

El nuevo Azure Portal (y, en concreto, la extensión de Azure AD Domain Services) se basa en Azure Resource Manager. En el entorno moderno de Azure Resource Manager, se aplican ciertas restricciones para proporcionar mayor seguridad y un control de acceso basado en rol (RBAC) a los recursos. La operación de habilitar Azure AD Domain Services para un inquilino de Azure AD es delicada, ya que hace que los valores hash de credenciales se sincronicen con el dominio administrado. Para realizar esta operación, debe ser un administrador de inquilinos del directorio. Además, debe tener privilegios administrativos en la red virtual en la que se habilita el dominio administrado. Para que las comprobaciones de RBAC funcionen de forma coherente, el dominio administrado y la red virtual deben pertenecer al mismo inquilino de Azure AD.

En resumen, no puede habilitar un dominio administrado para un inquilino de Azure AD de "contoso.com" en una red virtual que pertenezca a una suscripción de Azure propiedad de otro inquilino de Azure AD de "fabrikam.com". El Portal de Azure clásico no se basa en la plataforma de Resource Manager y no aplica estas restricciones.

**Configuración válida**: en este escenario de implementación, el dominio administrado de Contoso está habilitado para el inquilino de Azure AD de Contoso. El dominio administrado se expone en una red virtual que pertenece a una suscripción de Azure propiedad del inquilino de Azure AD de Contoso. Por lo tanto, tanto el dominio administrado como la red virtual pertenecen al mismo inquilino de Azure AD. Esta configuración es válida y totalmente compatible.

![Configuración de inquilino válida](./media/getting-started/valid-tenant-config.png)

**Configuración de inquilino que no coincide**: en este escenario de implementación, el dominio administrado de Contoso está habilitado para el inquilino de Azure AD de Contoso, pero el dominio administrado se expone en una red virtual que pertenece a una suscripción de Azure propiedad del inquilino de Azure AD de Fabrikam. Por lo tanto, el dominio administrado y la red virtual pertenecen a dos inquilinos de Azure AD diferentes. Esta configuración es una configuración de inquilino que no coincide y no se admite. La red virtual debe moverse al mismo inquilino de Azure AD (es decir, Contoso) que el dominio administrado. Vea la sección [Resolución](#resolution) para obtener más información.

![Configuración de inquilino que no coincide](./media/getting-started/mismatched-tenant-config.png)

Por lo tanto, verá este error en los escenarios en los que el dominio administrado y la red virtual en la que está habilitado pertenecen a dos inquilinos de Azure AD diferentes.

Las reglas siguientes se aplican al entorno de Resource Manager:
- Un directorio de Azure AD puede tener varias suscripciones de Azure.
- Una suscripción de Azure puede tener varios recursos, como redes virtuales.
- Solo hay un dominio administrado de Azure AD Domain Services habilitado para un directorio de Azure AD.
- Un dominio administrado de Azure AD Domain Services puede habilitarse en una red virtual que pertenezca a cualquiera de las suscripciones de Azure incluidas dentro del mismo inquilino de Azure AD.


## <a name="resolution"></a>Resolución
Tiene dos opciones para resolver el error de directorio que no coincide. Puede hacer lo siguiente:

- Haga clic en el botón **Eliminar** para eliminar el dominio administrado existente. Vuelva a crearlo en [Azure Portal](https://portal.azure.com), de modo que el dominio administrado y la red virtual en la que está disponible pertenezcan al directorio de Azure AD. Debe unir de nuevo al dominio administrado recién creado todas las máquinas que antes estaban unidas al dominio eliminado.

- Póngase en contacto con el soporte técnico de Azure para mover la suscripción de Azure que contiene la red virtual al directorio de Azure AD al que pertenece el dominio administrado. Haga clic en **Nueva solicitud de soporte técnico** y especifique **directorio que no coincide** en la sección **Detalles** de la solicitud de soporte técnico. Incluya la información proporcionada en el mensaje de error como parte de la solicitud de soporte técnico.


## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Guía de solución de problemas de Azure AD Domain Services](active-directory-ds-troubleshooting.md)
