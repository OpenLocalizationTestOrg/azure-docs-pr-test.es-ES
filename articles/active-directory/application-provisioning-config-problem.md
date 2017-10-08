---
title: "aaaProblem configuración de aplicación de la Galería de Azure AD tooan de aprovisionamiento de usuarios | Documentos de Microsoft"
description: "¿Cómo tootroubleshoot los problemas comunes que se enfrentan al configurar la aplicación de tooan ya aparece en la Galería de aplicaciones de Azure AD Hola de aprovisionamiento de usuarios"
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
ms.openlocfilehash: 19b12be019b05faecef74c6f92a9de03b52a5ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-user-provisioning-tooan-azure-ad-gallery-application"></a>Problema con la configuración de la aplicación de la Galería de Azure AD tooan de aprovisionamiento de usuarios

Configuración de [aprovisionamiento automático de usuarios](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning) para una aplicación (si se admite), requiere que las instrucciones concretas sea tooprepare seguido de aplicación de hello para el aprovisionamiento automático. A continuación, puede usar Hola tooconfigure portal Azure Hola aprovisionar la aplicación de servicio toosynchronize usuario cuentas toohello.

Siempre debe empezar por buscar el programa de instalación Hola tutorial toosetting específico de aprovisionamiento para la aplicación. A continuación, siga los pasos tooconfigure ambos aplicación hello y Azure AD toocreate Hola conexión aprovisionamiento. Encontrará una lista de tutoriales de aplicación en [lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

## <a name="how-toosee-if-provisioning-is-working"></a>Cómo funciona toosee si se está preparando 

Una vez configurado el servicio de hello, se pueden dibujar mayoría visiones operación Hola del servicio de hello en dos lugares:

-   **Registros de auditoría** : hello aprovisionamiento realizan todas las operaciones de Hola Hola aprovisionamiento del servicio de registro de registros de auditoría, incluidas las consultas de Azure AD para asignan los usuarios que pertenecen al ámbito de aprovisionamiento. Aplicación de destino de hello existencia Hola de esos usuarios, comparar objetos de usuario de hello entre sistema Hola de consulta. A continuación, agregar, actualizar o deshabilitar la cuenta de usuario de Hola Hola del sistema de destino en función de comparación de Hola. puede tener acceso a Hola aprovisionamiento de los registros de auditoría en el portal de Azure, en Hola Hola **Azure Active Directory &gt; aplicaciones empresariales &gt; \[nombre de la aplicación\] &gt; registros de auditoría**ficha. Hola de filtro inicie sesión en hello **el aprovisionamiento de cuentas** categoría tooonly vea Hola aprovisionamiento eventos para esa aplicación.

-   **Aprovisionamiento de estado:** un resumen de aprovisionamiento de la última Hola de ejecución de una aplicación determinada puede verse en hello **Azure Active Directory &gt; aplicaciones empresariales &gt; \[nombre de la aplicación\] &gt; Aprovisionamiento** sección final Hola de pantalla de bienvenida en la configuración de servicio de Hola. Esta sección resume cuántos usuarios (o grupos) se está sincronizando actualmente entre Hola dos sistemas, y si hay errores. Detalles del error esté en los registros de auditoría de Hola. Tenga en cuenta que Hola estado de aprovisionamiento no se rellena hasta que se ha completado una sincronización inicial completa entre Azure AD y aplicación hello.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Áreas con problemas generales con el aprovisionamiento tooconsider

A continuación se muestra una lista de hello áreas con problemas generales que puede profundizar en si tiene una idea de dónde toostart.

* [Aprovisionamiento del servicio no aparece toostart](#provisioning-service-does-not-appear-to-start)
* [No se puede guardar la configuración debido a credenciales tooapp no funciona](#can’t-save-configuration-due-to-app-credentials-not-working)
* [Los registros de auditoría indican que hay usuarios "omitidos" y no aprovisionados, aunque estén asignados](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Aprovisionamiento del servicio no aparece toostart

Si establece hello **estado de aprovisionamiento** toobe **en** en hello **Azure Active Directory &gt; aplicaciones empresariales &gt; \[nombredelaaplicación\] &gt;Provisioning** sección de hello portal de Azure. No obstante, no se muestran más detalles de estado en esa página tras recargas posteriores. Es probable que el servicio de hello está ejecutando pero no se ha completado una sincronización inicial aún. Comprobar hello **registros de auditoría** se ha descrito anteriormente toodetermine qué servicio de Hola de operaciones está ejecutando y si hay errores.

>[!NOTE]
>Una sincronización inicial puede tardar de horas, tooseveral 20 minutos, según el tamaño de hello del directorio de Azure AD de Hola y número de Hola de usuarios en el ámbito de aprovisionamiento. Las sincronizaciones posteriores después de la sincronización inicial de hello ser más rápidas, como las marcas de agua que representan el estado de Hola de ambos sistemas después de la sincronización inicial hello, mejorar el rendimiento de las sincronizaciones posteriores de almacenes de hello aprovisionamiento del servicio.
>
>

## <a name="cant-save-configuration-due-tooapp-credentials-not-working"></a>No se puede guardar la configuración debido a credenciales tooapp no funciona

En orden para aprovisionamiento toowork, Azure AD necesita unas credenciales válidas que le permiten administración de usuarios tooconnect tooa API proporcionada por esa aplicación. Si estas credenciales no funcionan o no sabe wat son, revise tutorial Hola para configurar esta aplicación, que se ha descrito anteriormente.

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Los registros de auditoría indican que hay usuarios omitidos y no aprovisionados, aunque estén asignados

Cuando un usuario se muestra como "Omitir" en los registros de auditoría de hello, es Hola tooread muy importante que los detalles en razón de Hola de toodetermine del mensaje de registro de hello extendidos. Algunas razones y soluciones habituales son:

-   **Se ha configurado un filtro de ámbito** **que está filtrando usuario Hola según un valor de atributo**. Para más información sobre los filtros de ámbito, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **usuario de Hello es "no eficazmente derecho".** Si ve este mensaje de error específico, es porque no hay un problema con el registro de asignación de usuario de hello almacenada en Azure AD. toofix este problema, cancele la asignación Hola usuario (o grupo) de la aplicación hello y vuelva a asignar. Para más información sobre la asignación, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Un atributo obligatorio falta o no se ha llenado para un usuario.** Una tooconsider importante al configurar el aprovisionamiento puede tooreview y configurar asignaciones de atributos de Hola y flujos de trabajo que definen qué flujo de propiedades de usuario (o grupo) de la aplicación de Azure AD toohello. Esto incluye el establecimiento de Hola "hacer coincidir la propiedad" que ser usado toouniquely identificar y asociar los usuarios/grupos entre sistemas de hello dos. Para más información sobre este importante proceso, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings>.

   * **Asignaciones de grupos de atributos:** Provisioning de hello detalles de nombre y grupos, en miembros de suma toohello, del grupo si se admite para algunas aplicaciones. Puede habilitar o deshabilitar esta funcionalidad habilitando o deshabilitando hello **asignación** para los objetos de grupo se muestra en hello **Provisioning** ficha. Si está habilitado el aprovisionamiento de grupos, asegúrese de tooreview Hola atributo asignaciones tooensure un campo correspondiente se utiliza para saludo "Id. de búsqueda de coincidencias". Esto puede ser alias de correo electrónico o nombre de presentación de hello), como grupo de Hola y sus miembros no aprovisionar si hello búsqueda de coincidencias de propiedad está vacío o no se llena para un grupo en Azure AD.

#<a name="next-steps"></a>Pasos siguientes
[Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones con Azure Active Directory](active-directory-saas-app-provisioning.md)
