---
title: "aplicación de la Galería de tooan aprovisionado Azure AD que se aaaNo a los usuarios | Documentos de Microsoft"
description: "Cómo tootroubleshoot los problemas comunes que se enfrentan cuando no haya usuarios que aparecen en un Azure AD que ha configurado para el aprovisionamiento de usuarios con Azure AD de aplicación de la Galería"
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
ms.date: 05/04/2017
ms.author: asteen
ms.openlocfilehash: 4d9693a202ed657e1de5571b50e5d499bef1bb3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="no-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Ningún usuario se está aprovisionados tooan Azure AD Galería aplicación

El aprovisionamiento automático de una vez se ha configurado para una aplicación (incluida la comprobación de que las credenciales de aplicación Hola proporcionan tooAzure AD tooconnect toohello aplicación son válidos). Entonces los usuarios o grupos son aprovisionados toohello aplicación y viene determinado por hello siguientes cosas:

-   Que los usuarios y grupos que hayan sido **asignado** toohello aplicación. Para obtener más información sobre la asignación, consulte [asignar una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

-   Si no **asignaciones de atributo** son toosync habilitado y configurado atributos válidos de la aplicación de Azure AD toohello. Para más información sobre las asignaciones de atributos, consulte [Personalización de asignaciones de atributos de aprovisionamiento de usuarios para aplicaciones SaaS en Azure Active Directory de usuarios](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

-   Si hay o no presente un **filtro de ámbito** que filtre usuarios en función de valores de atributo concretos. Para más información sobre los filtros de ámbito, consulte [Aprovisionamiento de aplicaciones basado en atributos con filtros de ámbito](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

Al observar que no se van a aprovisionar usuarios, consulte los registros de auditoría de hello en Azure AD y busque entradas del registro para un usuario específico.

puede tener acceso a Hola aprovisionamiento de los registros de auditoría en el portal de Azure, en Hola Hola **Azure Active Directory &gt; aplicaciones empresariales &gt; \[nombre de la aplicación\] &gt; registros de auditoría**ficha. Hola de filtro inicie sesión en hello **el aprovisionamiento de cuentas** categoría tooonly vea Hola aprovisionamiento eventos para esa aplicación. Puede buscar usuarios en función de Hola "identificador coincidente" que se configuró para ellos en asignaciones de atributos de Hola. Por ejemplo, si configuró Hola "nombre principal de usuario" o "dirección de correo electrónico" como Hola coincidencia de atributo en el lado de hello Azure AD y no se aprovisionamiento de usuarios de hello tiene un valor de "audrey@contoso.com". A continuación, buscar registros de auditoría Hola "audrey@contoso.com" y revise a continuación, las entradas que se devuelve.

Hola aprovisionamiento auditoría registra todas las operaciones realizadas por el servicio de aprovisionamiento de hello, incluidas las consultas de Azure AD para los usuarios asignados que están en el ámbito de aprovisionamiento, consultar la aplicación de destino de hello existencia Hola de esos usuarios, comparar Hola de Hola de registro objetos de usuario entre el sistema de Hola. A continuación, agregar, actualizar o deshabilitar la cuenta de usuario de Hola Hola del sistema de destino en función de comparación de Hola.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Áreas con problemas generales con el aprovisionamiento tooconsider

A continuación se muestra una lista de hello áreas con problemas generales que puede profundizar en si tiene una idea de dónde toostart.

* [Aprovisionamiento del servicio no aparece toostart](#provisioning-service-does-not-appear-to-start)
* [Los registros de auditoría indican que hay usuarios omitidos y no aprovisionados, aunque estén asignados](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Aprovisionamiento del servicio no aparece toostart

Si establece hello **estado de aprovisionamiento** toobe **en** en hello **Azure Active Directory &gt; aplicaciones empresariales &gt; \[nombredelaaplicación\] &gt;Provisioning** sección de hello portal de Azure. Sin embargo no otros detalles de estado se muestran en la página después vuelve a cargar posteriores, es probable que el servicio de Hola está ejecutando, pero no se ha completado una sincronización inicial aún. Comprobar hello **registros de auditoría** se ha descrito anteriormente toodetermine qué servicio de Hola de operaciones está ejecutando y si hay errores.

>[!NOTE]
>Una sincronización inicial puede tardar de horas, tooseveral 20 minutos, según el tamaño de hello del directorio de Azure AD de Hola y número de Hola de usuarios en el ámbito de aprovisionamiento. Después de la sincronización inicial de hello las sincronizaciones posteriores son más rápidas, como Hola aprovisionamiento del servicio almacena marcas de agua que representan el estado de Hola de ambos sistemas después de la sincronización inicial de Hola. Esto mejora el rendimiento de las posteriores.
>
>

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Los registros de auditoría indican que hay usuarios omitidos y no aprovisionados, aunque estén asignados

Cuando un usuario se muestra como "Omitir" en los registros de auditoría de hello, es Hola tooread muy importante que los detalles en razón de Hola de toodetermine del mensaje de registro de hello extendidos. Algunas razones y soluciones habituales son:

-   **Se ha configurado un filtro de ámbito** **que está filtrando usuario Hola según un valor de atributo**. Para más información sobre los filtros de ámbito, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **usuario de Hello es "no eficazmente derecho".** Si ve este mensaje de error específico, es porque no hay un problema con el registro de asignación de usuario de hello almacenada en Azure AD. toofix este problema, cancele la asignación Hola usuario (o grupo) de la aplicación hello y vuelva a asignar. Para más información sobre la asignación, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Un atributo obligatorio falta o no se ha llenado para un usuario.** Una tooconsider importante al configurar el aprovisionamiento puede tooreview y configurar asignaciones de atributos de Hola y flujos de trabajo que definen qué flujo de propiedades de usuario (o grupo) de la aplicación de Azure AD toohello. Esto incluye el establecimiento de Hola "hacer coincidir la propiedad" que ser usado toouniquely identificar y asociar los usuarios/grupos entre sistemas de hello dos. Para más información sobre este importante proceso, consulte [Personalización de asignaciones de atributos de aprovisionamiento de usuarios para aplicaciones SaaS en Azure Active Directory de usuarios](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

  * **Asignaciones de grupos de atributos:** Provisioning de hello detalles de nombre y grupos, en miembros de suma toohello, del grupo si se admite para algunas aplicaciones. Puede habilitar o deshabilitar esta funcionalidad habilitando o deshabilitando hello **asignación** para los objetos de grupo se muestra en hello **Provisioning** ficha. Si está habilitado el aprovisionamiento de grupos, asegúrese de tooreview Hola atributo asignaciones tooensure un campo correspondiente se utiliza para saludo "Id. de búsqueda de coincidencias". Esto puede ser alias de correo electrónico o nombre de presentación de hello), como grupo de Hola y sus miembros no aprovisionar si hello búsqueda de coincidencias de propiedad está vacío o no se llena para un grupo en Azure AD.

## <a name="next-steps"></a>Pasos siguientes
[Azure AD Connect Sync: conocimiento del aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md)

