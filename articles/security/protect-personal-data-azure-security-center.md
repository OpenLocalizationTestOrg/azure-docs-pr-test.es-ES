---
title: aaaProtect datos personales con el centro de seguridad de Azure | Documentos de Microsoft
description: "protección de datos personales mediante Azure Security Center"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a>Protección de datos personales frente a infracciones de seguridad y ataques: Azure Security Center

Este artículo le ayudará a entender cómo incumple toouse Azure Security Center tooprotect de los datos personal y ataques.

## <a name="scenario"></a>Escenario 

Una empresa cruise grandes, con sede en Estados Unidos, Hola está ampliando sus itinerarios toooffer de operaciones en hello Mediterráneo y Mar Báltico, así como Hola británicas. toohelp en los esfuerzos, ha adquirido varias líneas cruise más pequeñas con sede en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido

la compañía de Hello utiliza los datos corporativos de Microsoft Azure toostore en la nube de Hola. Esto incluye información de identificación personal como nombres, direcciones, números de teléfono e información de la tarjeta de crédito. También incluye información de recursos humanos como:

- Direcciones
- Números de teléfono
- Números de identificación fiscal
- Información médica

línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad. Red de Hola de acceso de los empleados corporativos de oficinas remotas y la Agencia de viajes de la compañía de Hola ubicados en todo Hola a todos tienen acceso a recursos de empresa de toosome.
Datos personales pasan a través de la red de hello entre estas ubicaciones y el centro de datos de Microsoft de Hola.

## <a name="problem-statement"></a>Declaración del problema

empresa Hola está preocupa por la amenaza de Hola de ataques en sus recursos de Azure. Desean tooprevent exposición de las personas toounauthorized de datos personales de los empleados y los clientes. Desea obtener instrucciones sobre la prevención y respuesta o corrección, así como un modo eficaz toomonitor hello en curso la seguridad de sus recursos de nube.
Necesita una línea de defensa sólida contra los atacantes sofisticados y organizados que hay en la actualidad.

## <a name="company-goal"></a>Objetivo de la empresa

Uno de los objetivos de la compañía de hello es privacidad de hello tooensure de los datos personales de los empleados y los clientes mediante la protección contra amenazas. Uno de sus objetivos es toorespond inmediatamente toosigns de infracción toomitigate Hola impacto. Necesita una manera de tooassess Hola estado actual de la seguridad, identificar las configuraciones vulnerables y corregirlas.

## <a name="solutions"></a>Soluciones

Microsoft Azure Security Center (ASC) proporciona una solución integrada de supervisión de la seguridad y administración de directivas. Ofrece las funcionalidades sencillas y eficaces de prevención, detección y respuesta ante amenazas.

### <a name="prevention"></a>Prevención

ASC le ayuda a evitar infracciones habilitando las directivas de seguridad tooset, proporcionan acceso just-in-time e implementar las recomendaciones de seguridad.

Una directiva de seguridad define el conjunto de Hola de controles que se recomienda para los recursos dentro de hello especificado suscripción. Justo a tiempo acceso puede ser usado toolock hacia abajo el tráfico entrante tooyour máquinas virtuales de Azure, lo que reduce la exposición tooattacks. Recomendaciones de seguridad se crean ASC después de analizar el estado de seguridad de Hola de los recursos de Azure.

#### <a name="how-do-i-set-security-policies-in-asc"></a>¿Cómo se pueden establecer directivas de seguridad en ASC?

Puede configurar directivas de seguridad para cada suscripción. toomodify una directiva de seguridad, debe ser propietario o colaborador de esa suscripción. Hola portal de Azure, Hola siguientes:

1. Seleccione **directiva** en el panel de hello ASC.

2. Seleccione la suscripción de hello en el que desea que Directiva de hello tooenable.

3. Elija **directivas de prevención** tooconfigure directivas por suscripción. **Recopilar datos de máquinas virtuales** debe establecerse demasiado**en.**

4. Hola **directivas de prevención** opciones, seleccionadas **en** recomendaciones de seguridad de hello tooenable que son relevantes para la suscripción de Hola.

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

Para obtener más instrucciones y una explicación de cada una de las recomendaciones de la directiva de Hola que se pueden habilitar, consulte [establecer directivas de seguridad de Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).

#### <a name="how-do-i-configure-just-in-time-access-jit"></a>¿Cómo se puede configurar el acceso Just-In-Time (JIT)?

Cuando JIT está habilitada, el centro de seguridad para bloquear el tráfico entrante tooyour máquinas virtuales de Azure mediante la creación de una regla de NSG. Seleccionar puertos hello en hello VM toowhich se bloqueará el tráfico entrante hacia abajo. toouse JIT acceso, Hola siguientes:

1. Seleccione hello **en el icono de acceso VM de tiempo** en la hoja de hello ASC.

2. Seleccione hello **recomendado** ficha.

3. En **máquinas virtuales**, seleccione hello las máquinas virtuales que desea tooenable. Esto coloca una máquina virtual de tooa siguiente marca de verificación. 
4. Seleccione **Habilitar JIT** en VM.
5. Seleccione **Guardar**.

A continuación, puede ver los puertos predeterminados de Hola que ASC recomienda al estar habilitado para JIT. También puede agregar y configurar un puerto nuevo en el que desea tooenable Hola justo a tiempo la solución. Hola **en el acceso en tiempo de máquina virtual** icono Hola centro de seguridad muestra el número de Hola de máquinas virtuales configuradas para el acceso JIT. También muestra hello número de solicitudes de acceso autorizado a realizadas en hello última semana.

![](media/protect-personal-data-azure-security-center/jit-vm.png)

Para obtener instrucciones sobre cómo toodo esto, y ver información adicional sobre sólo en el acceso de tiempo, [administrar el acceso de máquina virtual con justo a tiempo.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

#### <a name="how-do-i-implement-asc-security-recommendations"></a>¿Cómo se pueden implementar recomendaciones de seguridad de ASC?

Cuando el Centro de seguridad identifica vulnerabilidades de seguridad potenciales, crea recomendaciones. recomendaciones de Hello guiarle por proceso de Hola de configuración de controles de Hola que sea necesitado. 
1. Seleccione hello **recomendaciones** icono Panel de hello ASC.

2. Ver recomendaciones de hello, que se muestran en un formato de tabla, donde cada línea representa una recomendación.

3. recomendaciones de toofilter, seleccione **filtro** y seleccionar valores de gravedad y el estado de hello desea toosee.

4. toodismiss una recomendación que no es aplicable, puede haga clic y seleccione **descartar.**

5. Evalúe qué recomendación debería aplicarse primero.

6. Aplicar recomendaciones de hello en orden de prioridad.

Para obtener una lista de posibles recomendaciones y procedimientos paso a paso acerca de cómo tooapply cada uno, vea [administrar las recomendaciones de seguridad en el centro de seguridad de Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)

### <a name="detection-and-response"></a>Detección y respuesta

Detección y respuesta van juntas, como se desee toorespond tan pronto como sea posible después de que se detecta una amenaza.
La detección de amenazas ASC funciona mediante la recopilación automáticamente información de seguridad de los recursos de Azure, red de Hola y soluciones de socios conectados. ASC es capaz de actualizar rápidamente los algoritmos de detección a medida que los atacantes idean nuevos y más sofisticados ataques de seguridad. Para obtener información más detallada sobre cómo funciona la detección de amenazas de ASC, consulte [Funcionalidades de detección de Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a>¿Cómo administrar y responder a alertas de toosecurity?

Se muestra una lista de alertas de seguridad con prioridades en el centro de seguridad junto con hello información que necesita tooquickly investigar el problema de Hola. Centro de seguridad también incluye recomendaciones sobre cómo tooremediate un ataque. toomanage la seguridad de alertas, hacer Hola después de:

1. Seleccione hello **alertas de seguridad** el icono Panel de hello ASC. Aquí verá detalles de cada alerta.

2. alertas de toofilter basadas en fecha, el estado y la gravedad, seleccione **filtro** y, a continuación, seleccione los valores de hello que desee toosee.

3. toorespond tooan alerta, selecciónelo y revise la información de hello, seleccione recurso Hola que fuera atacado.

4. Hola **descripción** campo, podrá ver detalles, incluidas las actualizaciones recomendadas.

![](media/protect-personal-data-azure-security-center/security-alerts.png)

Para obtener más instrucciones sobre las alertas de toosecurity responde, consulte [toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)

Para obtener ayuda en la investigación de alertas de seguridad, empresa Hola puede integrar las alertas ASC con su propia solución SIEM, con [integración de Azure registro](https://aka.ms/AzLog).

#### <a name="how-do-i-manage-security-incidents"></a>¿Cómo se pueden administrar incidentes de seguridad?

En ASC, un incidente de seguridad es la suma de todas las alertas de un recurso que se alinean con patrones de cadenas de eliminación. Un incidente revelará lista Hola de alertas relacionadas, lo que permite tooobtain obtener más información sobre cada repetición. Incidentes aparecen en Hola icono de alertas de seguridad y de hoja.

tooreview y administrar incidentes de seguridad, Hola siguientes:

1. Seleccione hello **alertas de seguridad** icono. Si se detecta un incidente de seguridad, aparecerá en el gráfico de alertas de seguridad de Hola. Tendrá un icono distinto de otras alertas.

2. Seleccione toosee incidentes hello más detalles sobre este incidente de seguridad. Detalles adicionales incluyen su descripción completa, su gravedad, su estado actual, Hola atacada recursos, los pasos de corrección de Hola de incidente de Hola y Hola alertas que se incluyeron en este incidente.

Puede filtrar toosee **incidentes solo**, **alertas solo**, o **ambos**.

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a>¿Cómo obtengo acceso Hola informes de inteligencia de amenazas?

ASC analiza la información frente a amenazas de tooidentify de varios orígenes. los equipos de respuesta a incidentes de tooassist investigación y corregir las amenazas, centro de seguridad incluye un informe de inteligencia de amenazas que contiene información sobre la amenaza de Hola que se detectó.

Security Center tiene tres tipos de informes de amenazas, que pueden variar por ataque.
informes de Hello disponibles son:

- Informe de grupo de actividad: proporciona información detallada sobre los atacantes, sus objetivos y las tácticas que emplean.

- Informe de campaña: se centra en los detalles de campañas de ataque específicas.

- Informe de resumen de amenaza: cubre todos los elementos de informes de dos anteriores Hola.

Este tipo de información es muy útil durante el proceso de respuesta a incidentes de hello, que existe un origen de hello toounderstand de investigación en curso de ataque de hello, Hola motivaciones del atacante, y qué toomitigate toodo este problema en adelante.

1. tooaccess Hola inteligencia sobre amenazas de informes, Hola siguientes:

2. Seleccione hello **alertas de seguridad** icono Panel de hello ASC.

3. Seleccionar alerta de seguridad de hello para el que desea tooobtain obtener más información.

4. Hola **informes** , a continuación, haga clic en informe de inteligencia de amenazas de hello vínculo toohello.

5. Se abrirá el archivo PDF de hello, que puede descargar.

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

Para obtener información adicional acerca de hello informe de inteligencia de amenazas ASC, consulte [informe de inteligencia de amenaza del centro de seguridad de Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

### <a name="assessment"></a>Evaluación

toohelp con pruebas, la evaluación y la evaluación de la postura de seguridad, ASC proporciona para evaluación de vulnerabilidad integrado con Qualys agentes en la nube, como parte de su componente de recomendaciones de la máquina virtual.

Hola Qualys agente informes vulnerabilidad datos toohello Qualys plataforma de administración, que, a continuación, envía una vulnerabilidad y datos de supervisión de estado tooASC de nuevo. Hola tooadd recomendación se muestra una solución de evaluación de vulnerabilidad en hello **recomendaciones** hoja en el panel de hello ASC.

Después de instala la solución de evaluación de vulnerabilidades de hello en destino Hola VM, exámenes de centro de seguridad Hola VM toodetect e identifican las vulnerabilidades de sistema y de aplicación. Detecta problemas se muestran bajo hello **recomendaciones de máquinas virtuales** opción.

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a>¿Cómo se puede implementar una solución de evaluación de vulnerabilidades? 

Si una máquina virtual aún no tiene implementada una solución de evaluación de vulnerabilidades integrada, Security Center recomienda su instalación.

1. En panel ASC hello, en hello **recomendaciones** hoja, seleccione **agregar una solución de evaluación de vulnerabilidad.**

2. Seleccione las máquinas virtuales de Hola donde desea que la solución de evaluación de vulnerabilidades de hello tooinstall.

3. Haga clic en **Instalar en las máquinas virtuales de [número de].**

4. Seleccione una solución de socios de hello Azure Marketplace, o bajo **usar una solución existente,** seleccione **Qualys.**

5. Puede activar la configuración de actualización automática de Hola o desactivar en hello **soluciones de socios** hoja.

Para obtener más instrucciones sobre cómo tooimplement una solución de evaluación de vulnerabilidad, consulte [evaluación de vulnerabilidad en el centro de seguridad de Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)

## <a name="next-steps"></a>Pasos siguientes

- [Guía de inicio rápido de Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [Introducción tooAzure centro de seguridad](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [Integración de las alertas de Azure Security Center con la integración de registro de Azure](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/) (Potenciación de Azure Security Center con la evaluación de vulnerabilidades integrada)
