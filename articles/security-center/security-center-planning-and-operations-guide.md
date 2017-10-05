---
title: "Guía de planeamiento y operaciones de Security Center | Microsoft Docs"
description: Este documento lo ayuda a planear antes de adoptar Azure Security Center y proporciona consideraciones sobre las operaciones diarias.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: c502e4363dbaa37455d1aad90d1e9fa855fd09b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Guía de planeamiento y operaciones de Azure Security Center
Esta guía está destinada a profesionales de tecnologías de la información (TI), arquitectos de TI, analistas de seguridad de la información y administradores de la nube cuyas organizaciones estén planeando utilizar Azure Security Center.

>[!NOTE] 
>Desde primeros de junio de 2017, Security Center usará Microsoft Monitoring Agent para recopilar y almacenar datos. Consulte [Migración de la plataforma de Azure Security Center](security-center-platform-migration.md) para más información. La información de este artículo representa la funcionalidad de Security Center después de la transición a Microsoft Monitoring Agent.
>

## <a name="planning-guide"></a>Guía de planeamiento
Esta guía abarca un conjunto de pasos y tareas que se pueden seguir para optimizar el uso de Security Center en función de los requisitos de seguridad y el modelo de administración de nube de su organización. Para poder beneficiarse plenamente de Security Center, es importante comprender cómo distintas personas o equipos de su organización usarán el servicio para satisfacer las necesidades relativas al desarrollo y las operaciones seguros, la supervisión, el gobierno y la respuesta a incidentes. Las áreas clave que se deben tener en cuenta al planear el uso de Security Center son:

* Roles de seguridad y controles de acceso
* Directivas de seguridad y recomendaciones
* Recopilación de datos y almacenamiento
* Supervisión continuada de la seguridad
* Respuesta a los incidentes

En la siguiente sección obtendrá información sobre cómo planear cada una de esas áreas y aplicar las recomendaciones según sus requisitos.

> [!NOTE]
> Lea en [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) una lista de preguntas habituales que también pueden ser útiles durante la fase de diseño y planeamiento.
> 

## <a name="security-roles-and-access-controls"></a>Roles de seguridad y controles de acceso
Según el tamaño y la estructura de su organización, puede que varias personas y equipos usen Security Center para llevar a cabo diferentes tareas relacionadas con la seguridad. En el siguiente diagrama se ofrece un ejemplo de personas ficticias y sus respectivos roles y responsabilidades en cuanto a la seguridad:

![Roles](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

Security Center hace posible que estos usuarios cumplan estas diversas responsabilidades. Por ejemplo:

**Jeff (Propietario de la carga de trabajo de la nube)**

* Administración de una carga de trabajo de nube y sus recursos relacionados
* Responsable de la implementación y el mantenimiento de las protecciones de acuerdo con la directiva de seguridad de la empresa

**Ellen (CISO/CIO)**

* Responsable de todos los aspectos de seguridad de la empresa
* Desea comprender la postura de la empresa en materia de seguridad con respecto a las cargas de trabajo de nube
* Se le debe informar de los riesgos y ataques principales

**David (Seguridad de TI)**

* Define directivas de seguridad de la empresa para garantizar que existen las protecciones adecuadas
* Supervisa el cumplimiento con directivas
* Genera informes para la dirección ejecutiva o los auditores

**Judy (Operaciones de seguridad)**

* Supervisa y responde a alertas de seguridad las 24 horas, los 7 días de la semana
* Transfiere el problema al propietario de la carga de trabajo de nube o al analista de seguridad de TI

**Sam (Analista de seguridad)**

* Investigación de los ataques
* Trabajar con el propietario de la carga de trabajo de nube para aplicar correcciones 

Security Center usa el [control de acceso basado en rol (RBAC)](../active-directory/role-based-access-control-configure.md), que proporciona [roles integrados](../active-directory/role-based-access-built-in-roles.md) que se pueden asignar a usuarios, grupos y servicios en Azure. Cuando un usuario abre Security Center, solo ve la información relacionada con los recursos a los que tienen acceso. Esto significa que al usuario se le asigna el rol de Propietario, Colaborador o Lector para la suscripción o el grupo de recursos a los que pertenece un recurso. Además de estos roles, hay dos roles específicos de Security Center:

- **Lector de seguridad**: el usuario que pertenece a este rol puede ver los derechos para Security Center, lo que incluye recomendaciones, alertas, directivas y estados, pero no puede realizar cambios.
- **Administrador de seguridad**: igual que el lector de seguridad pero también puede actualizar la directiva de seguridad o descartar recomendaciones y alertas.

Los roles de Security Center descritos anteriormente no tienen acceso a otras áreas de servicio de Azure, como Storage, Web y móvil o Internet de las cosas.  

> [!NOTE]
> El usuario debe ser al menos propietario de una suscripción o de un grupo de recursos, o ser colaborador de estos, para poder ver Security Center en Azure. 
> 
> 

Con las personas que se explican en este diagrama, sería necesario el siguiente control de acceso basado en rol (RBAC):

**Jeff (Propietario de la carga de trabajo de la nube)**

* Propietario o colaborador del grupo de recursos

**David (Seguridad de TI)**

* Propietario o colaborador de la suscripción o administrador de seguridad

**Judy (Operaciones de seguridad)**

* Lector de suscripción o lector de seguridad para ver alertas
* Debe ser propietario o colaborador de la suscripción o administrador de seguridad para descartar alertas

**Sam (Analista de seguridad)**

* Lector de la suscripción para ver las alertas
* Debe ser propietario o colaborador de la suscripción para descartar las alertas
* Puede requerir acceso al área de trabajo

Otra información importante que se debe tener en cuenta:

* Solo los propietarios o colaboradores de la suscripción y los administradores de seguridad pueden editar una directiva de seguridad
* Los únicos que pueden aplicar recomendaciones de seguridad para un recurso son los propietarios y los colaboradores de la suscripción y del grupo de recursos.

Cuando planee el control de acceso mediante RBAC para Security Center, asegúrese de comprender quiénes en su organización van a usar Security Center. También, los tipos de tareas que realizarán, y luego configure RBAC en consecuencia.

> [!NOTE]
> Es recomendable que asigne el rol de menos permisos que los usuarios necesiten para realizar sus tareas. Por ejemplo, a los usuarios que solo necesiten ver información sobre el estado de seguridad de los recursos, pero no llevar a cabo acciones como aplicar recomendaciones o editar directivas, se les debe asignar el rol Lector.
> 
> 

## <a name="security-policies-and-recommendations"></a>Directivas de seguridad y recomendaciones
Una directiva de seguridad define el conjunto de controles recomendados para los recursos en la suscripción específica. En Security Center, se definen directivas de acuerdo con los requisitos de seguridad de la compañía y el tipo de aplicaciones o la confidencialidad de los datos.

Las directivas que están habilitadas en el nivel de suscripción se propagarán automáticamente a todos los grupos de recursos de la suscripción, como se muestra en el diagrama siguiente:

![Directivas de seguridad](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> Si necesita revisar qué directivas se han cambiado, puede usar los [registros de auditoría de Azure](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/). Los cambios en directivas se reflejan siempre en los registros de auditoría de Azure.
> 
> 

### <a name="security-recommendations"></a>Recomendaciones de seguridad
Antes de configurar las directivas de seguridad, revise cada una de las [recomendaciones de seguridad](security-center-recommendations.md)y determine si son adecuadas para los diversos grupos de recursos y suscripciones. También es importante entender qué acción debe realizarse para abordar las [recomendaciones de seguridad](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) y qué persona de su organización será responsable de supervisar las nuevas recomendaciones y llevar a cabo los pasos necesarios.

Security Center recomendará que proporcione los detalles de contacto de seguridad para su suscripción de Azure. Esta información la utilizará Microsoft para ponerse en contacto con usted si Microsoft Security Response Center (MSRC) detecta que un tercero no autorizado o ilegal ha accedido a los datos de clientes. Consulte [Proporcionar detalles de contacto de seguridad en Azure Security Center](security-center-provide-security-contact-details.md) para más información sobre cómo habilitar esta recomendación.

## <a name="data-collection-and-storage"></a>Recopilación de datos y almacenamiento
Azure Security Center usa Microsoft Monitoring Agent, que es el mismo agente que usan la solución Operations Management Suite y el servicio Log Analytics, para recopilar datos de seguridad de las máquinas virtuales. Los datos recopilados por este agente se almacenan en las áreas de trabajo de Log Analytics.

### <a name="agent"></a>Agente

Una vez que la recopilación de datos está habilitada en la directiva de seguridad, Microsoft Monitoring Agent (para [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) o [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) se instala en todas las máquinas virtuales de Azure admitidas y en las nuevas que se hayan creado.  Si la máquina virtual ya tiene instalado Microsoft Monitoring Agent, Azure Security Center aprovechará al agente instalado actual. El proceso del agente está diseñado para que no sea invasivo y tenga un impacto mínimo sobre el rendimiento de la máquina virtual.

Microsoft Monitoring Agent para Windows requiere el uso del puerto TCP 443. Para más información, consulte el [artículo de solución de problemas](security-center-troubleshooting-guide.md).

Si en algún momento desea deshabilitar la recopilación de datos, puede desactivarla en la directiva de seguridad. Sin embargo, como Microsoft Monitoring Agent se puede usar en otros servicios de administración y supervisión de Azure, el agente no se desinstalará automáticamente cuando desactive la recopilación de datos en  Security Center. En caso necesario, puede desinstalar el agente manualmente.

> [!NOTE]
> Para encontrar una lista de máquinas virtuales admitidas, lea las [preguntas frecuentes sobre Azure Security Center](security-center-faq.md).
> 

### <a name="workspace"></a>Área de trabajo

Los datos recopilados por Microsoft Monitoring Agent (en nombre de Azure Security Center) se almacenarán en las áreas de trabajo existentes de Log Analytics asociadas con la suscripción de Azure o en unas nuevas áreas de trabajo, según la región geográfica de la máquina virtual. 

En el portal de Azure, puede realizar una exploración para ver una lista de las áreas de trabajo de Log Analytics, incluidas las creadas por Azure Security Center. Se creará un grupo de recursos relacionado para las nuevas áreas de trabajo. Ambas siguen esta convención de nomenclatura: 

* Área de trabajo: *DefaultWorkspace-[subscription-ID]-[geo]*
* Grupo de recursos: *DefaultResouceGroup-[geo]*

En el caso de las áreas de trabajo creadas por Azure Security Center, los datos se conservan durante 30 días. En las áreas de trabajo existentes, la retención se basa en el plan de tarifa del área de trabajo.

> [!NOTE]
> Microsoft está totalmente comprometido a proteger la privacidad y la seguridad de estos datos. Microsoft se adhiere a instrucciones estrictas de seguridad y cumplimiento de normas, desde la codificación hasta la operación de un servicio. Para más información sobre el control de datos y la privacidad, lea [Seguridad de datos de Azure Security Center](security-center-data-security.md).
> 

## <a name="ongoing-security-monitoring"></a>Supervisión continuada de la seguridad
Después de la configuración inicial y la aplicación de las recomendaciones de Security Center, el siguiente paso consiste en considerar los procesos operativos de Security Center.

Para acceder a Security Center desde Azure Portal, haga clic en **Examinar** y escriba **Security Center** en el campo **Filtro**. Las vistas que el usuario obtiene dependen de la aplicación de estos filtros. En el ejemplo siguiente se muestra un entorno con muchos problemas que es necesario solucionar:

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Security Center no interferirá en los procedimientos operativos normales, sino que supervisará de forma pasiva las implementaciones y proporcionará recomendaciones basadas en las directivas de seguridad que se hayan habilitado.

Cuando elige por primera vez usar Security Center para su entorno actual de Azure, debe asegurarse de revisar todas las recomendaciones. Puede hacerlo en el icono **Recomendaciones** o por recurso (**Compute**, **Redes**, **Almacenamiento y datos** y **Aplicación**).

Después de que procese todas las recomendaciones, la sección **Prevención** debería aparecer en verde para los recursos correspondientes. A partir de este momento, la supervisión continua resulta más sencilla, ya que solo tomará medidas en respuesta a los cambios en los iconos de recomendaciones y estado de seguridad.

La sección **Detección** es más reactiva, ya que se trata de alertas sobre los problemas que están ocurriendo en ese momento o que ocurrieron en el pasado y se detectaron en los controles de Security Center y sistemas de terceros. El icono Alertas de seguridad mostrará gráficos de barras que representan el número de alertas de detección de amenazas encontradas cada día y su distribución entre las diversas categorías de gravedad (baja, media, alta). Para más información sobre Alertas de seguridad, lea [Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> También puede aprovechar Microsoft Power BI para visualizar los datos de Security Center. Consulte [Obtención de información mediante los datos de Azure Security Center con Power BI](security-center-powerbi.md).
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>Supervisión de recursos nuevos o modificados
La mayor parte de los entornos de Azure son dinámicos, con incorporaciones o retiradas periódicas de recursos, configuraciones o cambios, etc. Security Center ayuda a garantizar la visibilidad del estado de seguridad de estos nuevos recursos.

Cuando agregue nuevos recursos (máquinas virtuales, bases de datos SQL) a su entorno de Azure, Security Center los detectará automáticamente y empezará a supervisar su seguridad. Esto también incluye los roles web de PaaS y los roles de trabajo. Si la recopilación de datos está habilitada en la [directiva de seguridad](security-center-policies.md), se habilitarán automáticamente funcionalidades de supervisión adicionales para las máquinas virtuales.

![Áreas clave](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. En máquinas virtuales, haga clic en **Compute**, en la sección **Prevención**. Cualquier problema con la habilitación de los datos o recomendaciones relacionadas aparecerán en la pestaña **Información general** y la sección **Monitoring Recommendations** (Recomendaciones de supervisión).
2. Vea las **recomendaciones** para comprobar si se identificó algún riesgo de seguridad para el nuevo recurso.
3. Es muy habitual que cuando se agregan nuevas máquinas virtuales a su entorno, al principio solo esté instalado el sistema operativo. Es posible que el propietario del recurso tarde un tiempo en implementar otras aplicaciones que se usarán en estas máquinas virtuales.  Idealmente, debe conocer el objetivo final de esta carga de trabajo. ¿Va a ser un servidor de aplicaciones? En función de lo que vaya a ser esta nueva carga de trabajo, puede habilitar la **directiva de seguridad**correspondiente, lo cual es el tercer paso de este flujo de trabajo.
4. A medida que se agreguen nuevos recursos a su entorno de Azure, es posible que aparezcan nuevas alertas en el icono **Alertas de seguridad** . Compruebe siempre si hay nuevas alertas en este icono y actúe según las recomendaciones de Security Center.

También debería supervisar periódicamente el estado de los recursos existentes para identificar los cambios de configuración que hayan creado riesgos de seguridad, la separación respecto a las líneas base recomendadas y las alertas de seguridad. Comience en el panel de Security Center. Desde allí deberá revisar tres áreas principales de forma periódica.

![Operaciones](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. En el panel de la sección **Prevención** se proporciona acceso rápido a los recursos principales. Use esta opción para supervisar los recursos Compute, Redes, Almacenamiento y datos y Aplicación.
2. El panel **Recomendaciones** permite revisar las recomendaciones de Security Center. Durante la supervisión continuada, es posible que no vea recomendaciones todos los días, lo cual es normal ya que procesó todas las recomendaciones durante la configuración inicial de Security Center. Por este motivo, es posible que no aparezca en esta sección información nueva todos los días y solo tenga que acceder a ella cuando sea necesario.
3. La sección **Detección** podría cambiar con mucha frecuencia o con muy poca. Revise siempre las alertas de seguridad y tome medidas basadas en las recomendaciones de Security Center.

## <a name="incident-response"></a>Respuesta a los incidentes
Security Center detecta amenazas y alerta sobre ellas a medida que se producen. Las organizaciones deben estar al tanto de las nuevas alertas de seguridad y tomar medidas según sea necesario para investigarlas o solucionar el ataque. Para más información sobre cómo funciona la detección de amenazas de Security Center, consulte [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md).

Aunque el objetivo de este artículo no es ayudarle a crear su propio plan de respuesta a incidentes, vamos a usar las respuestas de seguridad de Microsoft Azure en el ciclo de vida de la nube como base para las fases de la respuesta a incidentes. Estas fases se muestran en el diagrama siguiente:

![Actividad sospechosa](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> Puede usar la guía [Computer Security Incident Handling Guide](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) sobre el tratamiento de los incidentes de seguridad informática del National Institute of Standards and Technology (NIST) de EE. UU. como ayuda para crear el suyo propio.
> 

Puede utilizar alertas de Security Center durante las fases siguientes:

* **Detectar**: identifique una actividad sospechosa en uno o varios recursos. 
* **Evaluar**: realice la evaluación inicial para más información acerca de la actividad sospechosa.
* **Diagnosticar**: siga los pasos de corrección para llevar a cabo el procedimiento técnico para solucionar el problema.

Cada alerta de seguridad proporciona información que sirve para comprender la naturaleza del ataque y sugerir posibles mitigaciones. Algunas alertas también proporcionan vínculos a más datos o a otras fuentes de información dentro de Azure. Puede usar la información proporcionada para proseguir la investigación y para iniciar la mitigación, y también puede buscar datos relacionados con la seguridad que se almacenan en el área de trabajo.

En el ejemplo siguiente se muestra una actividad sospechosa de RDP:

![Actividad sospechosa](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

Como ve, esta hoja muestra detalles relacionados con la hora en que ocurrió el ataque, el nombre del host de origen, la máquina virtual de destino y también pasos recomendados. En algunas circunstancias, la información de origen del ataque puede estar vacía. Consulte [Missing Source Information in Azure Security Center Alerts](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) (Falta de información de origen en las alertas de Azure Security Center) para más información acerca de este tipo de comportamiento.

En el vídeo [How to Leverage the Azure Security Center & Microsoft Operations Management Suite for an Incident Response](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) (Uso de Azure Security Center y Microsoft Operations Management Suite para dar respuesta a incidentes), puede ver algunas demostraciones que le ayuden a entender cómo se puede usar Security Center en cada una de estas fases.

> [!NOTE]
> Para más información acerca de cómo usar las funcionalidades de Security Center durante el proceso de respuesta ante incidentes, consulte [Uso de Azure Security Center para responder a incidentes](security-center-incident-response.md) . 
> 
> 

## <a name="see-also"></a>Consulte también
En este documento, ha aprendido a planear la adopción de Security Center. Para más información sobre el Centro de seguridad, consulte los siguientes recursos:

* [Administración y respuesta a las alertas de seguridad en el Centro de seguridad de Azure](security-center-managing-and-responding-alerts.md)
* [Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md) : obtenga información sobre cómo supervisar el estado de los recursos de Azure.
* [Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md) : aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.
* [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) : encuentre las preguntas más frecuentes sobre el uso del servicio.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.

