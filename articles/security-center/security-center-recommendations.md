---
title: recomendaciones de seguridad de aaaManaging en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento explica cómo las recomendaciones del Centro de seguridad de Azure ayudan a proteger los recursos de Azure y a cumplir con las directivas de seguridad."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>Administración de recomendaciones de seguridad en el Centro de seguridad de Azure
Este documento le guía a través de cómo toouse recomendaciones en Azure Security Center toohelp proteger los recursos de Azure.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  Este documento no es una guía paso a paso.
>
>

## <a name="what-are-security-recommendations"></a>¿Cuáles son las recomendaciones de seguridad?
Centro de seguridad periódicamente analiza el estado de seguridad de Hola de los recursos de Azure. Cuando el Centro de seguridad identifica vulnerabilidades de seguridad potenciales, crea recomendaciones. recomendaciones de Hello guiarle por proceso de Hola de configuración de controles de Hola que sea necesitado.

## <a name="implementing-security-recommendations"></a>Implementación de recomendaciones de seguridad
### <a name="set-recommendations"></a>Obtención de recomendaciones
En [Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md), aprenderá lo siguiente:

* Configurar directivas de seguridad.
* Activar la recopilación de datos.
* Elija qué toosee recomendaciones como parte de la directiva de seguridad.

Las recomendaciones de directiva actuales se centran en las actualizaciones del sistema, las reglas de línea de base, los programas antimalware, los [grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md) en subredes y las interfaces de red, la auditoría de bases de datos SQL, el cifrado de datos transparente de bases de datos SQL y los firewalls de aplicaciones web.  [Establecimiento de directivas de seguridad](security-center-policies.md) proporciona una descripción de cada opción de recomendación.

### <a name="monitor-recommendations"></a>Supervisión de recomendaciones
Después de establecer una directiva de seguridad, el centro de seguridad analiza el estado de seguridad de Hola de sus tooidentify posibles vulnerabilidades de recursos. Hola **recomendaciones** icono hello **centro de seguridad** hoja le permite saber el número total de Hola de recomendaciones que se identifica mediante el centro de seguridad.

![Icono Recomendaciones][1]

detalles de hello toosee de cada recomendación:

Seleccione hello **recomendaciones icono** en hello **centro de seguridad** hoja. Hola **recomendaciones** abre la hoja.

recomendaciones de Hola se muestran en un formato de tabla, donde cada línea representa una recomendación concreta. Hola columnas de esta tabla son:

* **DESCRIPCIÓN**: recomendación de Hola y establecer qué debe toobe realiza tooaddress se explica lo.
* **RECURSOS**: enumera Hola recursos toowhich esta recomendación se aplica.
* **ESTADO**: describe Hola el estado actual de la recomendación de hello:
  * **Abra**: recomendación de hello todavía no se han abordado todavía.
  * **En curso**: recomendación de saludo se está aplicada toohello recursos y no se requiere ninguna acción por parte del usuario.
  * **Resolver**: ya se ha completado la recomendación de hello (en este caso, línea hello está atenuado).
* **GRAVEDAD**: describe la gravedad de Hola de esa recomendación determinada:
  * **Alta**: existe una vulnerabilidad en un recurso importante (como una aplicación, una máquina virtual o un grupo de seguridad de red) y requiere atención.
  * **Medio**: existe una vulnerabilidad y pasos adicionales o no críticos tooeliminate requiere que este archivo o toocomplete un proceso.
  * **Baja**: existe una vulnerabilidad que se debe abordar, pero no requiere una atención inmediata. (De forma predeterminada, no se presentan recomendaciones bajas, pero puede filtrar según las recomendaciones bajas si desea que toosee les.)

Uso de tabla de Hola a continuación como un toohelp de referencia comprende recomendaciones disponibles hello y lo que hace cada uno de ellos si se aplica.

> [!NOTE]
> Le interesará hello toounderstand [clásico y modelos de implementación del Administrador de recursos](../azure-classic-rm.md) para recursos de Azure.
>
>

| Recomendación | Description |
| --- | --- |
| [Habilitar la colección de datos de las suscripciones](security-center-enable-data-collection.md) |Se recomienda activar la recopilación de datos en la directiva de seguridad de Hola para cada una de las suscripciones y todas las máquinas virtuales (VM) en el nodo suscripciones. |
| [Corrección de vulnerabilidades del SO](security-center-remediate-os-vulnerabilities.md) |Se recomienda que las configuraciones de sistema operativo se alinean con hello recomienda reglas de configuración, por ejemplo, no permiten toobe contraseñas guardado. |
| [Aplicar actualizaciones del sistema](security-center-apply-system-updates.md) |Se recomienda que implemente tooVMs actualizaciones críticas y seguridad del sistema que faltan. |
| [Aplicación del control de acceso a redes Just-In-Time](security-center-just-in-time.md) | Se recomienda que aplique acceso a la máquina virtual Just-In-Time. Hola justo a la característica de tiempo está en la vista previa y disponible en hello nivel estándar del centro de seguridad. Vea [precios](security-center-pricing.md) toolearn más información acerca del centro de seguridad de los niveles de precios. |
| [Reiniciar tras actualizar el sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Recomienda que reinicie un proceso de máquina virtual toocomplete Hola de aplicar las actualizaciones del sistema. |
| [Add a web application firewall](security-center-add-web-application-firewall.md) |Recomienda implementar un Firewall de aplicaciones web (WAF) para los puntos de conexión web. Se muestra una recomendación WAFS para cualquier IP pública (dirección IP de nivel de instancia o con equilibrio de carga) que tiene un grupo de seguridad de red asociado con puertos abiertos web entrantes (80 y 443). </br>Centro de seguridad, se recomienda que aprovisionar un toohelp WAFS defenderse contra los ataques que se dirige a las aplicaciones web en máquinas virtuales y en el entorno del servicio de aplicaciones. Un entorno de App Service es una opción de plan de servicio [Premium](https://azure.microsoft.com/pricing/details/app-service/) de Azure App Service que proporciona un entorno plenamente aislado y dedicado para ejecutar de forma segura las aplicaciones de Azure App Service. toolearn más información acerca de ASE, vea hello [documentación del entorno de servicio de aplicación](../app-service/app-service-app-service-environments-readme.md).</br>Puede proteger varias aplicaciones web en el centro de seguridad mediante la adición de estas implementaciones de WAFS aplicaciones tooyour existentes. |
| [Finalización de la protección de la aplicación](security-center-add-web-application-firewall.md#finalize-application-protection) |configuración de hello toocomplete de un WAFS, tráfico debe ser redirigidos toohello WAFS dispositivo. Seguir esta recomendación completa cambios de instalación necesarios de Hola. |
| [Agregar un firewall de próxima generación](security-center-add-next-generation-firewall.md) |Recomienda agregar un servidor de seguridad de próxima generación (NGFW) desde un tooincrease de partner de Microsoft la protección de la seguridad. |
| [Enrutar el tráfico solo a través de NGFW](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Se recomienda que configure reglas de grupo (NSG) de seguridad de red que fuerce el tráfico entrante tooyour máquina virtual a través de su NGFW. |
| [Instalación de Endpoint Protection](security-center-install-endpoint-protection.md) |Recomienda que aprovisione tooVMs de programas antimalware (sólo VM de Windows). |
| [Resolver alertas de estado de Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recomienda resolver los errores de Endpoint Protection. |
| [Habilitar grupos de seguridad de red en subredes o máquinas virtuales](security-center-enable-network-security-groups.md) |Recomienda habilitar NSG en subredes o máquinas virtuales. |
| [Restringir el acceso a través de puntos de conexión accesibles desde Internet](security-center-restrict-access-through-internet-facing-endpoints.md) |Recomienda configurar reglas de tráfico de entrada para los NSG. |
| [Habilitar la auditoría y la detección de amenazas en los servidores SQL Server](security-center-enable-auditing-on-sql-servers.md) |Recomienda activar la detección de amenazas y la auditoría para los servidores de Azure SQL. (solo el servicio SQL de Azure. No incluye los servidores SQL que se ejecutan en las máquinas virtuales). |
| [Habilitación de la auditoría y la detección de amenazas en bases de datos SQL](security-center-enable-auditing-on-sql-databases.md) |Recomienda activar la detección de amenazas y la auditoría en las bases de datos de Azure SQL. (solo el servicio SQL de Azure. No incluye los servidores SQL que se ejecutan en las máquinas virtuales). |
| [Habilitar Cifrado de datos transparente en bases de datos SQL](security-center-enable-transparent-data-encryption.md) |Recomienda habilitar el cifrado en las bases de datos SQL (Solo el servicio SQL de Azure). |
| [Habilitar el Agente de máquina virtual](security-center-enable-vm-agent.md) |Permite toosee que las máquinas virtuales requieren Hola a agente de máquina virtual. Hola agente de máquina virtual debe estar instalado en las máquinas virtuales tooprovision revisión de análisis, análisis de la línea de base y los programas antimalware. Hola agente de máquina virtual está instalado de forma predeterminada para las máquinas virtuales que se implementan desde hello Azure Marketplace. artículo de Hello [agente de máquina virtual y extensiones: parte 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) proporciona información acerca de cómo tooinstall Hola agente de máquina virtual. |
| [Aplicar cifrado de discos](security-center-apply-disk-encryption.md) |Se recomienda cifrar los discos de la máquina virtual mediante Cifrado de discos de Azure (máquinas virtuales Linux y Windows). El cifrado se recomienda para hello SO y volúmenes de datos en la máquina virtual. |
| [Proporcionar datos de los contactos de seguridad](security-center-provide-security-contact-details.md) |Recomienda que proporcione información de los contactos de seguridad para cada una de sus suscripciones. La información de los contactos es una dirección de correo electrónico y un número de teléfono. Hola información es toocontact usado si busca de nuestro equipo de seguridad que se ponga en peligro sus recursos. |
| [Actualizar versión del sistema operativo](security-center-update-os-version.md) |Se recomienda actualizar la versión de sistema operativo (SO) de Hola para su servicio en la nube toohello versión más reciente disponible para la familia del SO.  toolearn más información acerca de los servicios en la nube, vea hello [Introducción a los servicios de nube](../cloud-services/cloud-services-choose-me.md). |
| [Evaluación de vulnerabilidades no instalada](security-center-vulnerability-assessment-recommendations.md) |Se recomienda instalar una solución de evaluación de vulnerabilidades en la máquina virtual. |
| [Corrección de vulnerabilidades](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Le permite toosee vulnerabilidades de sistema y las aplicaciones detectadas por la solución de evaluación de vulnerabilidades de hello instalado en la máquina virtual. |
| [Habilitar el cifrado para la cuenta de Azure Storage](security-center-enable-encryption-for-storage-account.md) | Es recomendable que habilite el cifrado del servicio de Azure Storage para datos en reposo. Cifrado de servicio de almacenamiento (SSE) funciona mediante el cifrado de datos de hello cuando se escribe tooAzure almacenamiento y descifra antes de la recuperación. SSE actualmente solo está disponible para hello servicio Blob de Azure y puede usarse para blobs en bloques, blobs de página y blobs en anexos. más información, consulte toolearn [cifrado del servicio de almacenamiento de datos en reposo](../storage/common/storage-service-encryption.md).</br>SSE solo es compatible con las cuentas de almacenamiento de Resource Manager. |

Puede filtrar y descartar las recomendaciones.

1. Seleccione **filtro** en hello **recomendaciones** hoja. Hola **filtro** hoja se abre y seleccionar valores de gravedad y el estado de hello, que se va toosee.

    ![Filtrar recomendaciones][2]
2. Si determina que una recomendación no es aplicable, puede descartar la recomendación de hello y, a continuación, filtrarlos fuera de la vista. Hay dos toodismiss formas una recomendación. Una manera es tooright haga clic en un elemento y, a continuación, seleccione **descartar**. Hola otro es toohover sobre un elemento, haga clic en hello tres puntos que aparecen toohello derecha y, a continuación, seleccionan **descartar**. Para ver las recomendaciones descartadas, haga clic en **Filtro** y seleccione **Descartadas**.

    ![Descartar recomendación][3]

### <a name="apply-recommendations"></a>Aplicación de recomendaciones
Después de revisar todas las recomendaciones, decida cuáles son las primeras que debe aplicar. Se recomienda utilizar la clasificación de gravedad hello como Hola tooevaluate parámetro principal primero se deben aplicar las recomendaciones.

En la tabla Hola de recomendaciones anteriores, seleccione una recomendación y guiará a través de él como un ejemplo de cómo tooapply una recomendación.

## <a name="next-steps"></a>Pasos siguientes
En este documento, eran recomendaciones toosecurity se ha introducido en el centro de seguridad. toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : más información cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
