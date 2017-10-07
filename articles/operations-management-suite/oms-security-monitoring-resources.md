---
title: "Recursos de Operations Management Suite solución de seguridad y auditoría aaaMonitoring | Documentos de Microsoft"
description: "Este documento ayuda a toouse OMS seguridad y auditoría capacidades toomonitor los recursos e identificar problemas de seguridad."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite
Este documento le ayuda a usar OMS seguridad y auditoría capacidades toomonitor los recursos e identificar problemas de seguridad.

## <a name="what-is-oms"></a>¿Qué es OMS?
Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura en la nube y local. Para obtener más información acerca de OMS, lea el artículo de hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="monitoring-resources"></a>Supervisión de recursos
Siempre que sea posible, le interesará tooprevent de incidentes de seguridad de elementos no utilizados en primer lugar en Hola. Sin embargo, resulta imposible tooprevent todos los incidentes de seguridad. Cuando se produce un incidente de seguridad, deberá tooensure que se minimiza su impacto.  Hay tres recomendaciones importantes que pueden ser utilizado toominimize Hola número y Hola impacto de los incidentes de seguridad:

* Evaluar de forma regular las vulnerabilidades del entorno.
* Comprobar con regularidad todos los sistemas informáticos y tooensure de dispositivos de red que tienen todas las revisiones más recientes de hello instalado.
* Comprobar con regularidad todos los registros y mecanismos de registro, incluidos los registros de eventos del sistema operativo, los registros específicos de la aplicación y los registros del sistema de detección de intrusiones.

Seguridad de OMS y auditoría permite solución tooactively de TI supervisar todos los recursos, que pueden ayudar a minimiza el impacto de Hola de incidentes de seguridad. Auditoría y seguridad de OMS tiene dominios de seguridad que pueden utilizarse para la supervisión de recursos. dominios de seguridad de Hello proporciona acceso rápido tooa opciones, para hello de supervisión de seguridad siguientes dominios se tratarán con más detalle:

* Evaluación de malware
* Evaluación de la actualización
* Identidad y acceso

> [!NOTE]
> Para obtener una descripción general de todas estas opciones, lea [Introducción a la solución Seguridad y auditoría de Operations Management Suite](oms-security-getting-started.md).
> 
> 

### <a name="monitoring-system-protection"></a>Supervisión de la protección del sistema
En una defensa en el enfoque de profundidad, es importante para hello cada capa de protección de estado general de seguridad del recurso. Equipos con detectan amenazas y los equipos con protección insuficiente se muestran en hello icono de evaluación de Malware en dominios de seguridad. Con información de hello en hello evaluación de Malware, puede identificar un plan tooapply protección toohello los servidores que lo necesitan. tooaccess que este Hola de seguimiento de la opción de los pasos a continuación:

1. Hola **Microsoft Operations Management Suite** panel principal haga clic en **seguridad y auditoría** icono.
   
    ![Seguridad y auditoría](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Hola **seguridad y auditoría** panel, haga clic en **evaluación Antimalware** en **dominios de seguridad**. Hola **evaluación Antimalware** tal y como se muestra a continuación se muestra el panel:

![Evaluación de malware](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

Puede usar hello **evaluación de Malware** Hola de panel tooidentify problemas de seguridad siguientes:

* **Amenazas activas**: equipos que se pusieron en peligro y amenazas activas en el sistema de Hola.
* **Corregido amenazas**: se corrigieron los equipos que se pusieron en peligro pero amenazas Hola.
* **Firma sin actualizar**: los equipos que tienen protección contra malware habilitada pero firma hello no está actualizada.
* **Sin protección en tiempo real**: equipos que no tienen instalado el antimalware.

### <a name="monitoring-updates"></a>Supervisión de actualizaciones
Aplicar actualizaciones de seguridad más reciente de hello es una práctica recomendada de seguridad y debe incorporarse en su estrategia de administración de actualizaciones. Servicio del agente de supervisión de Microsoft (HealthService.exe) lee información de actualización de los equipos supervisados y, a continuación, envía este servicio OMS toohello información actualizada en la nube de Hola para su procesamiento. Hola servicio del agente de supervisión de Microsoft está configurado como un servicio automático y se debería estar ejecutando siempre en el equipo de destino de Hola.

![Supervisión de actualizaciones](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

Lógica es toohello aplicado actualizar datos y servicio de nube de hello registra datos de Hola. Si se encuentran las actualizaciones que faltan, se muestran en hello **actualizaciones** panel. Puede usar hello **actualizaciones** toowork de panel que le faltan actualizaciones y desarrollar un plan tooapply ellos toohello servidores que lo requieran. Siga estos pasos Hola Hola tooaccess **actualizaciones** panel:

1. Hola **Microsoft Operations Management Suite** panel principal haga clic en **seguridad y auditoría** icono.
2. Hola **seguridad y auditoría** panel, haga clic en **evaluación de actualizaciones** en **dominios de seguridad**. Aparecerá el panel de actualización de Hello tal y como se muestra a continuación:

![Evaluación de la actualización](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

En este panel puede realizar un evaluación toounderstand Hola actual estado de actualización de los equipos y resolver las amenazas más importantes de Hola. Mediante el uso de hello **actualizaciones de seguridad o crítico** icono, los administradores de TI será tooaccess capaz de obtener información detallada sobre las actualizaciones de Hola que faltan tal y como se muestra a continuación:

![resultado de la búsqueda](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

Este informe incluye información crítica que se puede usar tooidentify Hola tipo de amenaza de este sistema sea vulnerable a, que incluye artículos de Microsoft KB Hola asociados con la actualización de seguridad de Hola y Hola Bulletin MS que tiene más detalles acerca de Hola vulnerabilidad.

### <a name="monitoring-identity-and-access"></a>Supervisión de la identidad y el acceso
Puesto que los usuarios trabajan desde cualquier lugar, usan diferentes dispositivos y obtienen acceso a una gran cantidad de aplicaciones locales y en la nube, es fundamental que se protejan sus credenciales. Los ataques de robo de credenciales son aquellos en los que un atacante inicialmente obtiene tooaccess de credenciales de usuario normales de acceso tooa un sistema dentro de la red de Hola. En muchas ocasiones, este tipo de ataque inicial es solo una red de toohello del acceso de manera tooget, objetivo definitivo de hello es toodiscover cuentas con privilegios. 

Los atacantes permanecerá en red de hello, usar gratuitamente herramientas tooextract credenciales desde las sesiones de Hola de otras cuentas de inicio de sesión. Dependiendo de la configuración del sistema hello, estas credenciales se pueden extraer con formato de Hola de hash, vales o contraseñas de texto simple incluso.  

> [!NOTE]
> equipos que están directamente exponen toohello que Internet verá muchas error intenta ese toologin try con todos los tipos de nombres de usuario conocida (por ejemplo, administrador). En la mayoría de los casos es apropiado si no se utilizan nombres de usuario conocida de Hola y Hola contraseña es suficientemente eficaz.
> 
> 

Es posible tooidentify estos intrusos antes de poner en peligro una cuenta con privilegios. Puede aprovechar **OMS solución de seguridad y auditoría** toomonitor identidad y acceso. Siga estos pasos Hola Hola tooaccess **Identity and Access** panel:

1. Hola **Microsoft Operations Management Suite** panel principal, haga clic en seguridad y auditoría en mosaico.
2. Hola **seguridad y auditoría** panel, haga clic en **Identity and Access** en **dominios de seguridad**. Hola **Identity and Access** tal y como se muestra a continuación se muestra el panel:

![identidad y acceso](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

Debe incluir la supervisión de la identidad como parte de su estrategia de supervisión regular. El administrador de TI debe comprobar si hay un nombre de usuario válido específico con el que se hayan realizado muchos intentos. Esto podría indicar que cualquier atacante que adquirió el nombre de usuario real de Hola e intente forzar toobrute o una herramienta automática que usa contraseña codificados de forma rígida que ha caducado.

Este habilitar panel tooquickly de TI identificar recursos del posibles amenazas relacionadas tooidentity y acceso toocompany. Está determinado tooalso identificar posibles tendencias importantes, por ejemplo en mosaico de los inicios de sesión de un período de hello, puede ver durante el período de tiempo cuántas veces se realizó un intento de inicio de sesión erróneos. En este caso Hola equipo **FileServer** recibido 35 intentos de inicio de sesión. Puede obtener más información sobre este equipo haciendo clic en él. 

![más detalles](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

informe de Hello generado para este equipo aporta valiosos detalles sobre este patrón. Observado que hello **cuenta** Hola proporciona columna Hola cuenta de usuario que se usa tootry tooaccess system, hello **TIMEGENERATED** proporciona columna Hola en qué Hola intento se realizó el intervalo de tiempo y Hola **LOGONTYPENAME** proporciona columna Hola ubicación donde realizó este intento. Si estos intentos realizados localmente en el sistema de Hola por un programa, Hola **proceso** columna, Mostrar nombre del proceso de Hola. En escenarios donde procede el intento de inicio de sesión de Hola desde un programa, ya tiene el nombre de proceso de hello está disponible y ahora puede realizar más investigación en el sistema de destino de Hola.

## <a name="see-also"></a>Otras referencias
En este documento, se habrá aprendido cómo toomonitor de solución de auditoría y seguridad de OMS toouse sus recursos. toolearn más información acerca de la seguridad de OMS, consulte Hola siguientes artículos:

* [Información general de Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Introducción a la solución Seguridad y auditoría de Operations Management Suite](oms-security-getting-started.md)
* [Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría](oms-security-responding-alerts.md)

