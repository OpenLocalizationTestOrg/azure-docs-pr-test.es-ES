---
title: "aaaOperations seguridad del conjunto de administración y seguridad de datos de auditoría soluciones | Documentos de Microsoft"
description: "En este documento se explica cómo se administran y protegen los datos en la solución Seguridad y auditoría de Operations Management Suite."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Seguridad de datos de la solución Seguridad y auditoría de Operations Management Suite
los clientes de toohelp evitar, detectar y responder toothreats, [Operations Management Suite (OMS) solución de seguridad y auditoría](operations-management-suite-overview.md) recopila y procesa los datos sobre los recursos, que incluye:

* Registro de eventos de seguridad
* Eventos de Seguimiento de eventos para Windows (ETW)
* Eventos de auditoría de AppLocker
* Registro de Firewall de Windows
* Eventos de Advanced Threat Analytics
* Resultados de evaluación de la línea base
* Resultados de evaluación de antimalware
* Resultados de la evaluación de la actualización o revisión
* Secuencias de Syslogs que se habilitan de manera explícita en el agente de Hola

Hacemos privacidad de hello tooprotect compromisos segura y la seguridad de estos datos. Microsoft adhiere a las directrices de seguridad y cumplimiento de toostrict: desde la codificación toooperating un servicio.
En este artículo se explica cómo se administran y protegen los datos en Seguridad y auditoría de OMS.

## <a name="data-sources"></a>Orígenes de datos
Solución de auditoría y seguridad de OMS analizan los datos de las máquinas virtuales y equipos físicos donde está instalado el agente de OMS Hola. La solución Seguridad y auditoría de OMS puede recopilar información de configuración sobre los eventos de seguridad, como los eventos de Windows, los registros de auditoría, los registros de IIS y los mensajes de syslog. Estos son algunos ejemplos de dichos datos: tipo y versión, procesos en ejecución, nombre de la máquina, direcciones IP, usuario conectado e identificador de inquilino.  

## <a name="data-protection"></a>Protección de datos
**Segregación de datos**: los datos se mantienen separados de forma lógica en cada componente en el servicio de Hola. Todos los datos se etiquetan por organización. Este etiquetado persiste a lo largo del ciclo de vida de datos de Hola y se aplica en cada nivel de servicio de Hola. 

**Acceso a datos**: recomendaciones de seguridad de tooprovide e investigar posibles amenazas de seguridad, personal de Microsoft puede tener acceso a la información recopilada o analizar por servicios. Cumplimos toohello [condiciones de Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) y [declaración de privacidad](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), qué estado que Microsoft usará no los datos del cliente o derivar información de él para publicación o similar con fines comerciales. recomendaciones de seguridad de tooprovide e investigar posibles amenazas de seguridad, personal de Microsoft puede tener acceso a la información recopilada o analizar por servicios. Solo se utilizan los datos del cliente como tooprovide necesaria con Azure de servicios, incluido con fines compatible con el suministro de dichos servicios. Conservar todos los datos propios tooyour de permisos.

**Uso de datos**: Microsoft utiliza patrones e inteligencia sobre amenazas visto entre varios inquilinos tooenhance nuestras capacidades de detección y prevención; lo hacemos según se describe en los compromisos de privacidad de hello nuestro [privacidad Instrucción](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

> [!NOTE]
> Ubicación de los datos se configura a nivel de área de trabajo OMS de hello, durante la creación de área de trabajo de hello, que forma parte Hola inicial OMS seguridad y auditoría del proceso de configuración.
> 
> 

## <a name="see-also"></a>Otras referencias
En este documento, ha aprendido cómo se administran y protegen los datos en OMS. toolearn más información sobre la seguridad de OMS y la solución de auditoría, vea:

* [Información general de Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría](oms-security-responding-alerts.md)
* [Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite](oms-security-monitoring-resources.md)

