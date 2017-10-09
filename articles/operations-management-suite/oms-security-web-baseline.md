---
title: "aaaOperations Management Suite seguridad y auditoría solución Web previsto | Documentos de Microsoft"
description: "Este documento se explica cómo toouse OMS seguridad y auditoría solución tooperform una evaluación de la línea de base de web de todos los servidores web supervisados para el propósito de seguridad y cumplimiento."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Evaluación de línea de base web en la solución Security and Audit de Operations Management Suite
Este documento le ayuda a toouse [Operations Management Suite (OMS) solución de seguridad y auditoría](operations-management-suite-overview.md) web capacidades tooaccess Hola estado seguro de los recursos supervisados de evaluación de línea de base.

## <a name="what-is-web-baseline-assessment"></a>¿Qué es la evaluación de línea de base web?
Actualmente, Seguridad de OMS proporciona una evaluación de línea de base de seguridad para sistemas operativos. Analiza la configuración del sistema operativo Hola de los servidores de cada 24 horas y proporciona una vista a la configuración de potencialmente vulnerable. Consulte [Evaluación de línea base en la solución Security and Audit de Operations Management Suite](oms-security-baseline.md) para más información sobre esto.

objetivo de Hola de evaluación de línea de base de hello web es la configuración del servidor de web potencialmente vulnerable toofind. Hola tres fuentes principales para las configuraciones de línea de base de hello web: configuración. NET, ASP.NET e IIS.  Simplemente como hello evaluación de línea de base del sistema operativo, seguridad de OMS se va tooscan sus servidores web cada 24 horas y proporcionan una vista de estado de seguridad de ellos.  En los servicios de Internet Information Server (IIS), las configuraciones son personalizables, que permite varias toobe de niveles de sitio y la aplicación se reemplaza. Analizador de Hello comprueba la configuración de hello en cada nivel de aplicación o el sitio de nivel de raíz de suma toohello predeterminado. Esto ayuda a ubicaciones de configuración de una vulnerabilidad potencial tooidentify y corregir rápidamente.


## <a name="web-security-baseline-assessment"></a>Evaluación de línea de base de seguridad web
De esta versión preliminar esta característica va toobe acceso mediante la opción de búsqueda de OMS Hola. Siga los pasos de hello debajo de consulta de hello apropian tooperform:

1. Hola **Microsoft Operations Management Suite** panel principal haga clic en **seguridad y auditoría** icono.
2. Hola **seguridad y auditoría** panel, haga clic en **Log Search** botón.
3. Hola primera consulta, que puede utilizar es hello **Web Resumen de la evaluación de línea de base**. Hola **empieza la búsqueda aquí** , escriba esta consulta: tipo*= SecurityBaselineSummary BaselineType = web*. Hola después de la pantalla tiene un ejemplo de salida:

![Resumen de evaluación de línea de base web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> En esta consulta, cada registro indica el resumen de evaluación para un solo servidor.

Una vez que esté en hello **Log Search**, puede escribir consultas diferentes tooobtain obtener más información acerca de la evaluación de línea de base de hello web. Además toohello consulta anterior, también sirve Hola los en esta versión preliminar siguiendo.

**Web Baseline Rule Assessment** (Evaluación de regla de la línea de base web): cada registro representa una sola evaluación de regla de la línea de base web en un único servidor. Incluye todos los datos de la regla de hello, ubicación, resultado de hello esperada y resultado real de Hola.

**Consulta**: Type*=SecurityBaseline BaselineType=web*

![Evaluación de regla de la línea de base web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**Mostrar todos los resultados de un servidor específico**: esta consulta muestra cómo toosee da como resultado de un servidor específico.

**Consulta**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*

![Todos los resultados](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

También puede utilizar estos registros y consultas toocreate sus propios paneles, informes o alertas. pantalla de bienvenida a continuación tiene un control de interfaz de usuario de ejemplo que se puede agregar panel tooyour. Puede obtener información sobre cómo toovisualize los datos mediante el Diseñador de vistas de OMS [aquí](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). pantalla de bienvenida siguiente es un ejemplo de cómo icono Hola será similar a una vez realizada esta personalización.

![Ejemplo de interfaz de usuario](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> Si desea que los valores de hello tooknow que se comprueban para la evaluación de la línea de base de hello, puede descargar [esta hoja de cálculo de Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) que contenga esta configuración.

## <a name="see-also"></a>Otras referencias
En este documento, ha aprendido acerca de la evaluación de línea de base web de Seguridad y auditoría de OMS. toolearn más información acerca de la seguridad de OMS, consulte Hola siguientes artículos:

* [Información general de Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría](oms-security-responding-alerts.md)
* [Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite](oms-security-monitoring-resources.md)

