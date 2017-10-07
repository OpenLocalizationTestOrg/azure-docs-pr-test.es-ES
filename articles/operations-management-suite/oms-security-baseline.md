---
title: "aaaOperations Management Suite seguridad y auditoría solución previsto | Documentos de Microsoft"
description: "Este documento se explica cómo toouse OMS seguridad y auditoría solución tooperform una evaluación de la línea de base de todos los equipos supervisados a fin de cumplimiento y seguridad."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Evaluación de línea base en la solución Seguridad y auditoría de Operations Management Suite
Este documento le ayuda a toouse [Operations Management Suite (OMS) solución de seguridad y auditoría](operations-management-suite-overview.md) capacidades tooaccess Hola estado seguro de los recursos supervisados de evaluación de línea de base.

## <a name="what-is-baseline-assessment"></a>¿Qué es la evaluación de línea base?
Microsoft, junto con organizaciones gubernamentales y del sector de todo el mundo, define una configuración de Windows que representa implementaciones de servidor muy seguras. Esta configuración es un conjunto de claves del Registro, la configuración de la directiva de auditoría y la configuración de la directiva de seguridad, junto con los valores recomendados de Microsoft para esta configuración. Este conjunto de reglas se conoce como línea base de seguridad. La funcionalidad de evaluación de línea base de Seguridad y auditoría de OMS puede examinar sin problemas todos los equipos para ver el cumplimiento. 

Existen tres tipos de reglas:

* **Reglas del Registro**: comprueba que las claves del Registro están establecidas correctamente.
* **Reglas de directiva de auditoría**: reglas relativas a la directiva de auditoría.
* **Las reglas de directiva de seguridad**: permisos de usuario de sobre hello en máquina Hola de reglas.

> [!NOTE]
> Lectura [tooassess usar OMS seguridad Hola línea base de configuración de seguridad](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) para obtener una descripción breve de esta característica.
> 
> 

## <a name="security-baseline-assessment"></a>Evaluación de línea base de seguridad
Puede revisar la evaluación de línea de base de seguridad actual para todos los equipos que se supervisan mediante seguridad de OMS y auditoría mediante el panel de Hola.  Ejecute hello siguiente panel de evaluación de la línea de base de seguridad de pasos tooaccess hello:

1. Hola **Microsoft Operations Management Suite** panel principal, haga clic en **seguridad y auditoría** icono.
2. Hola **seguridad y auditoría** panel, haga clic en **valoración** en **dominios de seguridad**. Hola **evaluación de la línea de base de seguridad** como se muestra en hello después de la imagen se muestra el panel:
   
    ![Evaluación de línea base de Seguridad y auditoría de OMS](./media/oms-security-baseline/oms-security-baseline-fig1.png)

Este panel se divide en tres áreas principales:

* **Equipos en comparación con toobaseline**: esta sección ofrece un resumen del número de Hola de equipos que antes de que se accedía y Hola porcentaje de equipos que superaron la evaluación de Hola. También ofrece top 10 equipos contenidos Hola y el resultado de porcentaje de hello para la evaluación de Hola.
* **Requiere el estado de las reglas**: esta sección tiene conocimiento de la intención toobring Hola de reglas de hello no se pudo por gravedad y reglas por tipo con errores. Son críticas, buscando toohello primer gráfico que puede identificar rápidamente si Hola mayoría reglas con errores o no. También ofrece una lista de hello top 10 las reglas con errores y su gravedad. gráfico de segundo de Hello muestra tipo hello de regla de error durante la evaluación de Hola. 
* **Falta la evaluación de la línea de base de equipos**: en esta sección una lista de equipos de Hola que no se tiene acceso debido a incompatibilidades de sistema de toooperating o errores. 

### <a name="accessing-computers-compared-toobaseline"></a>Acceso a equipos en comparación con toobaseline
Lo ideal es que todos los equipos están sea compatible con la evaluación de línea de base de seguridad de Hola. Sin embargo, se espera que en algunas circunstancias esto no suceda. Como parte del proceso de administración de seguridad de hello, es importante tooinclude Revisar equipos Hola que no se pudo toopass todas las pruebas de evaluación de seguridad. Un toovisualize de forma rápida que está seleccionando la opción de hello **tiene acceso a los equipos** ubicado en hello **equipos comparan toobaseline** sección. Debería ver Hola registro búsqueda resultados con hello una lista de equipos como se muestra en hello después de pantalla:

![Resultados del equipo al que se ha accedido](./media/oms-security-baseline/oms-security-baseline-fig2.png)

resultado de la búsqueda de Hola se muestra en un formato de tabla, donde hello primera columna tiene el nombre del equipo de Hola y segundo color de hello tiene número de Hola de reglas que no se pudo. información de hello tooretrieve con respecto al tipo de Hola de regla de error, haga clic en número de Hola de las reglas con errores además de nombre de equipo de Hola. Debería ver un toohello similar de resultados mostrado en hello después de imagen:

![Detalles de los resultados del equipo al que se ha accedido](./media/oms-security-baseline/oms-security-baseline-fig3.png)

En este resultado de búsqueda, se tienen Hola total de reglas de acceso, Hola número de reglas críticas que no se pudo, Hola reglas de advertencia y Hola reglas de error en la información.

### <a name="accessing-required-rules-status"></a>Acceso al estado de las reglas necesarias
Después de obtener información de hello sobre Hola de número de porcentaje de equipos que superaron la evaluación de hello, puede que desee tooobtain obtener más información acerca de las reglas que se producen errores en la importancia crítica toohello correspondiente. Esto ayuda a de visualización tooprioritize qué equipos deben ser dirigido tooensure primera estarán cumplen los requisitos de evaluación de hello siguiente. Mantenga el mouse sobre parte fundamental de Hola de gráfico de hello ubicado en hello **reglas con errores por gravedad** aparezca como mosaico en **requiere el estado de las reglas** y haga clic en él. Debería ver un toohello similar resultado después de pantalla:

![Reglas con errores por detalles de gravedad](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

En este resultado de registro Consulte tipo hello de regla de línea de base que no se pudo, descripción de Hola de esta regla y el identificador de hello Common Configuration Enumeration (CCE) de esta regla de seguridad. Estos atributos debe ser suficiente tooperform una acción correctora toofix este problema en el equipo de destino de Hola.

> [!NOTE]
> Para obtener más información acerca de CCE, tener acceso a hello [National Vulnerability Database](https://nvd.nist.gov/cce/index.cfm).
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a>Acceso a equipos sin evaluación de línea base
OMS admite miembro del dominio hello y perfil de línea de base de controlador de dominio en Windows Server 2008 R2 hasta tooWindows Server 2012 R2. La línea base de Windows Server 2016 todavía no está finalizada y se agregará en cuanto se publique. Todos los demás sistemas operativos analizados a través de evaluación de línea de base de seguridad de OMS y auditoría aparece debajo de hello **equipos falta la evaluación de la línea de base** sección.

## <a name="see-also"></a>Otras referencias
En este documento, ha aprendido acerca de la evaluación de línea base de Seguridad y auditoría de OMS. toolearn más información acerca de la seguridad de OMS, consulte Hola siguientes artículos:

* [Información general de Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría](oms-security-responding-alerts.md)
* [Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite](oms-security-monitoring-resources.md)

