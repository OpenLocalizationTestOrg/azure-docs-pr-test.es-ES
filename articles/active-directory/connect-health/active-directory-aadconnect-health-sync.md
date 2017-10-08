---
title: "Azure AD Connect Health con sincronización de aaaUsing | Documentos de Microsoft"
description: "Ésta es la página de mantenimiento de Connect de hello Azure AD que veremos cómo sincronizar toomonitor Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Supervisión de Azure AD Connect sync con Azure AD Connect Health
Hola siguiendo documentación es toomonitoring específico de Azure AD Connect (Sync) con Azure AD Connect Health.  Para obtener información sobre la supervisión de AD FS con Azure AD Connect Health, consulte [Uso de Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md). Para obtener información adicional sobre la supervisión de los Servicios de dominio de Active Directory con Azure AD Connect Health, consulte [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md)(Uso de Azure AD Connect Health con AD DS).

![Azure AD Connect Health para sincronización](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Alertas de Azure AD Connect Health para sincronización
Alertas de estado conectarse Hello Azure AD para la sección de sincronización proporciona que Hola lista de alertas activas. Cada alerta incluye información relevante, pasos de resolución así como documentación de toorelated de vínculos. Al seleccionar una alerta activa o resuelto verá una nueva hoja con información adicional, así como los pasos que puede seguir tooresolve Hola alerta y documentación de tooadditional de vínculos. También puede ver datos históricos sobre las alertas que se resolvieron en hello anterior.

Al seleccionar una alerta que le proporcionará información adicional, así como los pasos que puede seguir vínculos y alerta de hello tooresolve tooadditional documentación.

![Error de sincronización de Azure AD Connect](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Evaluación limitada de alertas
Si Azure AD Connect no usa la configuración de forma predeterminada de hello (por ejemplo, si el filtrado de atributos se cambia de configuración personalizada de hello predeterminada configuración tooa), a continuación, agente de hello Azure AD Connect Health no cargará los eventos de error hello tooAzure relacionados Conexión de AD.

Esto limita la evaluación de Hola de alertas por servicio de Hola. ¿Se verá un banner que indica esta condición Hola Portal de Azure en su servicio.

![Azure AD Connect Health para sincronización](./media/active-directory-aadconnect-health-sync/banner.png)

Puede cambiar este haciendo clic en "Configuración" y lo que permite tooupload de agente de Azure AD Connect Health todos los registros de errores.

![Azure AD Connect Health para sincronización](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Recomendación de sincronización
Administradores con frecuencia requiere tooknow sobre Hola tarda toosync cambios tooAzure AD y la cantidad de Hola de efectuar cambios. Esta característica proporciona una manera sencilla de toovisualize esto con hello debajo de gráficos:   

* Latencia de operaciones de sincronización
* Tendencia de cambio de objeto

### <a name="sync-latency"></a>Latencia de sincronización
Esta característica proporciona una tendencia gráfica de latencia de operaciones de sincronización de hello (importación, exportación, etc.) para los conectores.  Esto proporciona una rápida y fácilmente toounderstand no solo Hola latencia de las operaciones (más grandes si tiene un gran conjunto de cambios que se producen), sino también un anomalías de manera toodetect de la latencia de Hola que puede requerir más investigación.

![Latencia de sincronización](./media/active-directory-aadconnect-health-sync/synclatency02.png)

De forma predeterminada, se muestra solo la latencia de Hola de operación de 'Export' hello para el conector de Azure AD de Hola.  toosee más operaciones en el conector de Hola u operaciones de tooview desde otros conectores, haga doble clic en el gráfico de hello, seleccione Editar gráfico o haga clic en el botón de "Editar gráfico de latencia" hello y elija la operación específica de Hola y conectores.

### <a name="sync-object-changes"></a>Cambios en el objeto de sincronización
Esta característica proporciona una tendencia gráfica del número de Hola de cambios que se están evaluando y exportan tooAzure AD.  Hoy en día, toogather tratar esta información desde registros de sincronización de hello es difícil.  gráfico de Hello ofrece, no solo una manera más sencilla de supervisar el número de Hola de cambios que se producen en su entorno, sino también una representación visual de los errores de Hola que se están produciendo.

![Latencia de sincronización](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Informe de errores de sincronización de nivel de objeto (vista previa)
Esta característica proporciona un informe sobre los errores de sincronización que pueden producirse cuando se sincronizan datos de identidad entre Windows Server AD y Azure AD con Azure AD Connect.

* Hola errores registrados por el cliente de sincronización de hello en el informe (Azure AD Connect versión 1.1.281.0 o superior)
* Incluye los errores de Hola que se produjeron en la última operación de sincronización hello en el motor de sincronización de Hola. ("Exportación" en hello conector de Azure AD.)
* Agente de Azure AD Connect Health para la sincronización debe tener conectividad saliente toohello requiere extremos para los datos más recientes de hello informe tooinclude Hola.
* informe de Hello es **actualizada después de cada 30 minutos** utilizando los datos de hello cargada por el agente de Azure AD Connect Health para la sincronización. Proporciona Hola después capacidades clave

  * Categorización de errores
  * Lista de objetos con error por categoría
  * Todos los datos de hello sobre errores de hello en un solo lugar
  * Lado por comparación de objetos con error debido a conflictos de tooa
  * Descargar el informe de errores de Hola como un CVS (próximamente)

### <a name="categorization-of-errors"></a>Categorización de errores
informe de Hello clasifica los errores de sincronización existente Hola Hola siguientes categorías:

| Categoría | Descripción |
| --- | --- |
| Atributo duplicado |Errores que se producen cuando Azure AD Connect intenta crear o actualizar objetos con valores duplicados de uno o más atributos en Azure AD que deben ser únicos en un inquilino como, por ejemplo, proxyAddresses o UserPrincipalName. |
| Error de coincidencia de datos |Error cuando se produce un error en hello soft-match objetos toomatch que dan como resultado errores de sincronización. |
| Error de validación de datos |Errores debidos tooinvalid datos, como los caracteres no admitidos en los atributos críticos como UserPrincipalName, dar formato a los errores que no superan la validación antes de escribirse en Azure AD. |
| Atributo grande |Errores cuando uno o más atributos son más grandes que Hola permiten tamaño, longitud o recuento. |
| Otros |Todos los demás errores que no se ajustan en hello encima de las categorías. A raíz de los comentarios recibidos, esta categoría se dividirá en varias subcategorías. |

![Resumen del informe de errores de sincronización](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Categorías del informe de errores de sincronización](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Lista de objetos con error por categoría
Obtención de detalles de cada categoría proporcionará lista Hola de objetos que tienen error hello en esa categoría.
![Lista de informe de errores de sincronización](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Detalles del error
Después de datos está disponible en hello vista para cada error detallada

* Identificadores de hello *objeto AD* implicados
* Identificadores de hello *objeto de AD de Azure* implicados (como corresponda)
* Descripción del error y cómo toofix
* Artículos relacionados

![Detalles del informe de errores de sincronización](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Descargar el informe de errores de hello como CSV
Seleccionando Hola "Export" botón, puede descargar un archivo CSV con todos los detalles de hello todos los errores de Hola.

## <a name="related-links"></a>Vínculos relacionados
* [Solución de problemas de errores durante la sincronización](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [Resistencia de atributos duplicados](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalación del agente de Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operaciones de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso de Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso de Azure AD Connect Health con AD DS](active-directory-aadconnect-health-adds.md)
* [Preguntas más frecuentes de Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historial de versiones de Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)