---
title: "aaaWeb valoración para Operations Management Suite seguridad y auditoría solución previsto | Documentos de Microsoft"
description: "Este documento explica cómo toouse web valoración para auditoría y seguridad de OMS solución tooperform una evaluación de la línea de base de todos los servidores web supervisados para el propósito de seguridad y cumplimiento."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Evaluación de línea de base web en la solución Security and Audit de Operations Management Suite
Este documento le permitirá usar OMS seguridad y auditoría web previsto evaluación capacidades tooaccess Hola estado seguro de los recursos supervisados.

## <a name="what-is-web-baseline-assessment"></a>¿Qué es la evaluación de base de referencia web?
Actualmente, Seguridad de OMS proporciona una evaluación de línea de base de seguridad para sistemas operativos. Analiza configuraciones del sistema operativo Hola de los servidores de cada 24 horas y proporciona una vista a la configuración de potencialmente vulnerable. Consulte [Evaluación de línea base en la solución Security and Audit de Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline) para más información sobre esto.

objetivo de Hola de hello evaluación de la línea de base de Web es la configuración del servidor de web potencialmente vulnerable toofind. Hola tres fuentes principales para las configuraciones de línea de base de hello web: configuración. NET, ASP.NET e IIS.  Simplemente como hello evaluación de línea de base del sistema operativo, seguridad de OMS se va tooscan sus servidores web cada 24 horas y proporcionan una vista de estado de seguridad de ellos.  En los servicios de Internet Information Server (IIS), las configuraciones son personalizables, que permite varias toobe de niveles de sitio y la aplicación se reemplaza. Analizador de Hello comprueba la configuración de hello en cada nivel de aplicación o el sitio de nivel de raíz de suma toohello predeterminado. Esto ayuda a configuración potencialmente vulnerable tooidentify y corregir rápidamente, junto con nuestras recomendaciones para dicha configuración.

>[!NOTE] 
>Puede descargar los identificadores de configuración comunes de Hola y reglas de línea de base utilizadas por la seguridad de OMS en este [página](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).


## <a name="web-security-baseline-assessment"></a>Evaluación de base de referencia de seguridad web

De esta versión preliminar característica Hola son accesibles a través de hello opción de búsqueda de OMS y Hola seguridad de OMS y panel de auditoría. Siga los pasos de hello debajo de consulta de hello apropian tooperform:

1. Hola **Microsoft Operations Management Suite** panel principal, haga clic en **seguridad y auditoría** icono.
2. Hola **seguridad y auditoría** panel, puede ver la perspectiva de línea de base de hello Web previsto perspectiva siguiente toohello sistema operativo.
   
    ![Evaluación de base de referencia de seguridad web de Security and Audit de OMS](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. panel izquierdo de Hello muestra hello de línea de base de toohello en comparación con los servidores Web, porcentaje medio de Hola de reglas que se pasan en todos los servidores de hello evalúa y lista de Hola de servidores que se evalúa.
4. Hola derecho Hola único panel muestran las reglas que generó un error *gravedad*, y *RuleType*. Al hacer clic en cualquiera de las reglas del panel derecho de Hola se mostrarán los detalles de Hola de esa regla. Se muestra un ejemplo de Hola por debajo de la imagen. regla de Hola que se evalúa aparece en *configuración de la regla*. Hola *AzId* campo que es un identificador único para cada regla usada por Microsoft para el seguimiento de las reglas de línea de base de Hola. Además los usuarios de toothat pueden ver hello *resultado esperado* (valor recomendado de Microsoft), y otros detalles relacionados con los riesgos de seguridad de Hola de regla de Hola.
    
    ![Consultar](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. Puede crear sus propias consultas resultados de hello tooreview. 

Hola primera consulta, que puede utilizar es hello **Web Resumen de la evaluación de línea de base**. Hola **empieza la búsqueda aquí** , escriba esta consulta: *tipo = SecurityBaselineSummary BaselineType = Web*. Hola te mostramos un ejemplo de salida:

![Resultado de la consulta](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
>En esta consulta, cada registro indica el resumen de evaluación para un solo servidor.

Una vez que esté en hello **Log Search**, puede escribir consultas diferentes tooobtain obtener más información acerca de la evaluación de línea de base de hello web. Además toohello consulta anterior, se puede usar Hola los en esta vista previa siguiendo:

**Web Baseline Rule Assessment** (Evaluación de regla de la línea de base web): cada registro representa una sola evaluación de regla de la línea de base web en un único servidor. Incluye todos los datos de una regla con errores, hello *SitePath* en qué Hola regla se evaluó, hello *resultado esperado*, hello y *resultado real*.

Consulta: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*

![Resultado de la consulta 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

**Mostrar todos los resultados de un servidor específico**: esta consulta muestra cómo toosee da como resultado de un servidor específico: consulta: *tipo = SecurityBaseline BaselineType = equipo Web = BaselineTestVM1*

![Resultado de la consulta 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Puede usar estos registros y consultas toocreate sus propios paneles, informes o alertas. Este es un control de interfaz de usuario de ejemplo que se puede agregar panel tooyour. Puede obtener información sobre cómo toovisualize los datos mediante el Diseñador de vistas de OMS [aquí](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). pantalla de bienvenida siguiente es un ejemplo de cómo icono Hola será similar a una vez realizada esta personalización.

![dashboard](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a>Otras referencias
En este documento, ha aprendido acerca de la evaluación de base de referencia web de Security and Audit de OMS. toolearn más información acerca de la seguridad de OMS, consulte Hola siguientes artículos:

* [Información general de Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría](oms-security-responding-alerts.md)
* [Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite](oms-security-monitoring-resources.md)

