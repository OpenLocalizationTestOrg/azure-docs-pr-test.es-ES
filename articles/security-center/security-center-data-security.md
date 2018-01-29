---
title: Seguridad de datos de Azure Security Center | Microsoft Docs
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
ms.date: 12/06/2017
ms.author: yurid
ms.openlocfilehash: c41e233e177f540562d80649c7bffc15e208e870
ms.sourcegitcommit: 094061b19b0a707eace42ae47f39d7a666364d58
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="azure-security-center-data-security"></a>Seguridad de datos de Azure Security Center
Para ayudar a los clientes a evitar, detectar y responder a las amenazas, Azure Security Center recopila y procesa datos relacionados con la seguridad, entre los que se incluyen la información de configuración, los metadatos, los registros de eventos y los archivos de volcado de memoria, entre otros. Microsoft se adhiere a instrucciones estrictas de seguridad y cumplimiento de normas, desde la codificación hasta la operación de un servicio.

En este artículo se explica cómo se administran y protegen los datos en Azure Security Center.

## <a name="data-sources"></a>Orígenes de datos
Azure Security Center analiza los datos de los orígenes siguientes para proporcionar visibilidad de su estado de seguridad, identificar vulnerabilidades y recomendar mitigaciones y detectar amenazas activas:

- Servicios de Azure: utiliza la información acerca de la configuración de los servicios de Azure que se hayan implementado mediante la comunicación con el proveedor de recursos de cada uno de dichos servicios.
- Tráfico de red: usa metadatos muestreados del tráfico de red de la infraestructura de Microsoft, como el IP o el puerto de origen o destino, el tamaño de paquete y el protocolo de red.
- Soluciones de asociados: usa alertas de seguridad de las soluciones de asociados integradas, como firewalls y soluciones antimalware. 
- Sus máquinas virtuales y servidores: usa la información de configuración y la información sobre eventos de seguridad, como los eventos y registros de auditoría de Windows, registros IIS, mensajes de Syslog y archivos de volcado de memoria de las máquinas virtuales. Además, cuando se crea una alerta, Azure Security Center puede generar una instantánea del disco de máquina virtual afectado y extraer los artefactos de máquina relacionados con la alerta desde el disco de máquina virtual, como un archivo de registro, para fines de análisis forense.


## <a name="data-protection"></a>Protección de datos
**Segregación de datos**: los datos se mantienen separados de forma lógica en cada componente a lo largo de todo el servicio. Todos los datos se etiquetan por organización. Este etiquetado persiste a lo largo del ciclo de vida de los datos y se aplica en cada nivel del servicio.

**Acceso a datos**: con el fin de proporcionar recomendaciones de seguridad e investigar las posibles amenazas de seguridad, el personal de Microsoft puede tener acceso a la información recopilada o analizada por los servicios de Azure, incluidos archivos de volcado de memoria, eventos de creación de proceso, instantáneas y artefactos de disco de máquina virtual, que de forma involuntaria pueden incluir datos de cliente o datos personales de sus máquinas virtuales. Cumplimos la [Declaración de privacidad y los Términos de Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), en donde se estipula que Microsoft no utilizará los datos de los clientes ni información derivada de ellos con fines comerciales, publicitarios o similares. Solo usamos los datos del cliente necesarios para proporcionar los servicios de Azure. El usuario conserva todos los derechos sobre los datos del cliente.

**Uso de datos**: Microsoft utiliza los patrones y la información sobre amenazas vistos en varios inquilinos para mejorar las funcionalidades de detección y prevención; esto se realiza según lo dispuesto en los compromisos de privacidad que se describen en nuestra [declaración de privacidad](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Ubicación de los datos

**Sus áreas de trabajo**: se especifica una área de trabajo para las siguientes geoáreas y datos recopilados de sus máquinas virtuales de Azure, como los volcados de datos y algunos tipos de datos de alerta, que se guardan en el área de trabajo más próxima. 

| Geoárea de la máquina virtual                        | Geoárea del área de trabajo |
|-------------------------------|---------------|
| Estados Unidos, Brasil, Canadá | Estados Unidos |
| Europa, Reino Unido        | Europa        |
| Asia Pacífico, Japón, India    | Asia Pacífico  |
| Australia                     | Australia     |

 
Las instantáneas del disco de máquina virtual se almacenan en la misma cuenta de almacenamiento que el disco de máquina virtual.
 
Para máquinas virtuales y servidores que se ejecutan en otros entornos, por ejemplo, de forma local, puede especificar el área de trabajo y la región donde almacenar los datos recopilados. 

**Azure Storage Security Center**: la información acerca de las alertas de seguridad, incluidas las alertas de los asociados, se almacena a nivel regional según la ubicación del recurso de Azure, mientras que la información sobre el estado de mantenimiento de seguridad y la recomendación se almacenan centralmente, ya sea en Estados Unidos o en Europa, en función de la ubicación del cliente.
Azure Security Center recopila copias efímeras de los archivos de volcado de memoria y las analiza para buscar pruebas de intentos de vulnerabilidad y de riesgos ciertos. Azure Security Center realiza este análisis en la misma geoárea en la que se encuentra el área de trabajo y elimina las copias efímeras una vez que el análisis se completa.

Los artefactos de la máquina se almacenan de forma centralizada en la misma región que la máquina virtual. 


## <a name="managing-data-collection-from-virtual-machines"></a>Administración de recolección de datos de máquinas virtuales

Al habilitar Security Center en Azure, la recopilación de datos se activa para todas las suscripciones de Azure. También se puede activar la recopilación de datos para las suscripciones en la sección "Directivas de seguridad" de Azure Security Center. Cuando se activa la recopilación de datos, Azure Security Center aprovisiona el Microsoft Monitoring Agent en todas las máquinas virtuales de Azure compatibles existentes y en las que se crean. Microsoft Monitoring Agent busca diversos eventos y configuraciones relacionados con la seguridad y los envía a [Seguimiento de eventos para Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW). Además, el sistema operativo generará eventos del registro de eventos mientras la máquina se ejecute. Estos son algunos ejemplos de dichos datos: tipo y versión del sistema operativo, registros del sistema operativo (registros de eventos de Windows), procesos en ejecución, nombre de la máquina, direcciones IP, usuario conectado e identificador de inquilino. Microsoft Monitoring Agent lee las entradas de los registros de eventos y los seguimientos de ETW y los copia en las áreas de trabajo para el análisis. Microsoft Monitoring Agent también copia los archivos de volcado de memoria en las áreas de trabajo y habilita los eventos de creación de procesos y la auditoría de línea de comandos.

Si utiliza Azure Security Center gratis, también puede deshabilitar la recopilación de datos de las máquinas virtuales en las directivas de seguridad. La recopilación de datos es necesaria para las suscripciones del nivel estándar. Las instantáneas de disco de máquina virtual y la recolección de artefactos continuará habilitada aunque la recopilación de datos se deshabilite.

## <a name="data-consumption"></a>Consumo de datos

Los clientes pueden utilizar Security Center en relación con datos de secuencias de datos diferentes, tal y como se muestra a continuación:

* **Actividad de Azure**: todas las alertas de seguridad, solicitudes aprobadas [Just-In-Time](https://docs.microsoft.com/azure/security-center/security-center-just-in-time) de Security Center y todas las alertas generadas por [controles de aplicaciones adaptables](https://docs.microsoft.com/azure/security-center/security-center-adaptive-application).
* **Log Analytics**: todas las alertas de seguridad.


> [!NOTE]
> Las recomendaciones de seguridad pueden utilizarse también a través de la API de REST. Lea [Security Resource Provider REST API Reference](https://msdn.microsoft.com/library/mt704034(Azure.100).aspx) (Referencia de la API de REST del proveedor de recursos de seguridad) para más información. 

## <a name="see-also"></a>Otras referencias
En este documento, se ha explicado cómo se administran y protegen los datos en Azure Security Center. Para más información sobre Azure Security Center, consulte:

* [Guía de planeamiento y operaciones de Azure Security Center](security-center-planning-and-operations-guide.md) : aprenda a planear y conozca las consideraciones de diseño necesarias para usar Azure Security Center.
* [Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md) : obtenga información sobre cómo supervisar el estado de los recursos de Azure.
* [Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md) : obtenga información sobre cómo administrar y responder a alertas de seguridad.
* [Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md) : aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.
* [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) : encuentre las preguntas más frecuentes sobre el uso del servicio.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.
