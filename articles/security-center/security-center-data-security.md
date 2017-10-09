---
title: Seguridad de datos del centro de seguridad de aaaAzure | Documentos de Microsoft
description: "En este documento se explica cómo se administran y protegen los datos en Azure Security Center."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 30f8b11272dc5df6d485608abdaa62ba57e63f23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-data-security"></a>Seguridad de datos de Azure Security Center
los clientes de toohelp evitarán, detectaron y responden toothreats, Azure Security Center recopila y procesa los datos relacionados con la seguridad, incluida la información de configuración, metadatos, registros de eventos, archivos de volcado y mucho más. Microsoft adhiere a las directrices de seguridad y cumplimiento de toostrict: desde la codificación toooperating un servicio.

En este artículo se explica cómo se administran y protegen los datos en Azure Security Center.

>[!NOTE] 
>A partir de los principios de junio de 2017, centro de seguridad usará Hola Microsoft Monitoring Agent toocollect y almacenar datos. Vea [migración de la plataforma de Azure Security Center](security-center-platform-migration.md) toolearn más. información de Hello en este artículo representa la funcionalidad del centro de seguridad después de la transición toohello Microsoft Monitoring Agent.
>


## <a name="data-sources"></a>Orígenes de datos
Centro de seguridad de Azure analiza los datos de hello después de visibilidad de tooprovide orígenes en el estado de seguridad, identificar vulnerabilidades y recomienda las mitigaciones y detectar amenazas activas:

- Los servicios de Azure: Utiliza la información sobre la configuración de hello de servicios de Azure implementados mediante la comunicación con el proveedor de recursos de dicho servicio.
- Tráfico de red: usa metadatos muestreados del tráfico de red de la infraestructura de Microsoft, como el IP o el puerto de origen o destino, el tamaño de paquete y el protocolo de red.
- Soluciones de asociados: usa alertas de seguridad de las soluciones de asociados integradas, como firewalls y soluciones antimalware. 
- Sus máquinas virtuales y servidores: usa la información de configuración y la información sobre eventos de seguridad, como los eventos y registros de auditoría de Windows, registros IIS, mensajes de Syslog y archivos de volcado de memoria de las máquinas virtuales. Además, cuando se crea una alerta, centro de seguridad de Azure puede generar una instantánea de disco de máquina virtual de hello afectado y extraer alerta de máquina artefactos relacionados toohello desde el disco de máquina virtual de hello, como un archivo de registro, para fines de análisis forense.


## <a name="data-protection"></a>Protección de datos
**Segregación de datos**: los datos se mantienen separados de forma lógica en cada componente en el servicio de Hola. Todos los datos se etiquetan por organización. Este etiquetado persiste a lo largo del ciclo de vida de datos de Hola y se aplica en cada nivel de servicio de Hola.

**Acceso a datos**: en orden tooprovide recomendaciones de seguridad e investigar posibles amenazas de seguridad, personal de Microsoft puede tener acceso a la información recopilada o analizar por servicios de Azure, incluidos los archivos de volcado, procesar eventos de creación de máquinas virtuales las instantáneas de disco y artefactos, que pueden incluir involuntariamente los datos del cliente o datos personales de las máquinas virtuales. Cumplimos toohello [declaración de privacidad y condiciones de Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), qué estado que Microsoft usará no los datos del cliente o derivar la información de él para ningún propósito comercial publicitario o similar. Solo se utilizan los datos del cliente como tooprovide necesaria con Azure de servicios, incluido con fines compatible con el suministro de dichos servicios. Conservar todos los derechos tooCustomer datos.

**Uso de datos**: Microsoft utiliza patrones e inteligencia sobre amenazas visto entre varios inquilinos tooenhance nuestras capacidades de detección y prevención; lo hacemos según se describe en los compromisos de privacidad de hello nuestro [privacidad Instrucción](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Ubicación de los datos

**Los espacios de trabajo**: no se especifica un área de trabajo para hello después zonas geográficas:, y los datos recopilados de máquinas virtuales de Azure, incluidos los volcados de memoria y algunos tipos de datos de alertas, se almacenan en hello más próximo al área de trabajo. 

| Geoárea de la máquina virtual                        | Geoárea del área de trabajo |
|-------------------------------|---------------|
| Estados Unidos, Brasil, Canadá | Estados Unidos |
| Europa, Reino Unido        | Europa        |
| Asia Pacífico, Japón, India    | Asia Pacífico  |
| Australia                     | Australia     |

 
Instantáneas de disco de máquina virtual se almacenan en hello misma cuenta de almacenamiento como disco de máquina virtual de Hola.
 
Para máquinas virtuales y servidores que ejecutan en otros entornos, por ejemplo, de forma local, puede especificar el área de trabajo de Hola y la región donde se almacenan los datos recopilados. 

**Almacenamiento de Azure Security Center**: se almacena información sobre las alertas de seguridad, incluidas las alertas de socios comerciales, nivel regional según la ubicación de toohello de hello relacionados con recursos de Azure, mientras que la información sobre el estado de mantenimiento de seguridad y recomendación está centralizada en Estados Unidos de Hola o Europa según la ubicación del toocustomer.
Azure Security Center recopila copias efímeras de los archivos de volcado de memoria y las analiza para buscar pruebas de intentos de vulnerabilidad y de riesgos ciertos. Centro de seguridad de Azure realiza este análisis dentro de Hola mismo geográfica como área de trabajo de Hola y eliminaciones Hola copias efímeros si se completa el análisis.

Artefactos de la máquina se almacenan de forma centralizada en Hola la misma región como Hola máquina virtual. 


## <a name="managing-data-collection-from-virtual-machines"></a>Administración de recolección de datos de máquinas virtuales

Al habilitar Security Center en Azure, la recopilación de datos se activa para todas las suscripciones de Azure. También puede activar la recopilación de datos de las suscripciones en la sección Directiva de seguridad de Azure Security Center Hola. Cuando se activa la recopilación de datos, centro de seguridad de Azure aprovisiona Hola Microsoft Monitoring Agent en todas las existentes admite máquinas virtuales de Azure y los nuevos que se crean. agente de Microsoft Monitoring Hola busca seguridad diversas configuraciones y eventos relacionados en [seguimiento de eventos para Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) seguimientos (ETW). Además, sistema operativo de hello generará eventos de registro de eventos durante el curso de hello de la ejecución de la máquina de Hola. Estos son algunos ejemplos de dichos datos: tipo y versión del sistema operativo, registros del sistema operativo (registros de eventos de Windows), procesos en ejecución, nombre de la máquina, direcciones IP, usuario conectado e identificador de inquilino. Hola Microsoft Monitoring Agent lee las entradas de registro de eventos y realiza un seguimiento de ETW y los copia tooyour espacios de trabajo para el análisis. Hola Microsoft Monitoring Agent también copia los espacios de trabajo tooyour archivos de volcado de memoria de bloqueo.

Si utilizas libre de centro de seguridad de Azure, también puede deshabilitar la recopilación de datos de máquinas virtuales en hello directiva de seguridad. Recopilación de datos es necesaria para las suscripciones en el nivel estándar Hola. Las instantáneas de disco de máquina virtual y la recolección de artefactos continuará habilitada aunque la recopilación de datos se deshabilite.


## <a name="see-also"></a>Consulte también
En este documento, se ha explicado cómo se administran y protegen los datos en Azure Security Center. toolearn más información acerca del centro de seguridad de Azure, vea:

* [Guía de operaciones de planificación de Azure Security Center e](security-center-planning-and-operations-guide.md) : más información cómo tooplan y entender las consideraciones de diseño de hello tooadopt Azure Security Center.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.
