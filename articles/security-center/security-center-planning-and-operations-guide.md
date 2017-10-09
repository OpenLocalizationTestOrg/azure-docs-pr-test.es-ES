---
title: "Guía de operaciones de planificación de aaaSecurity Center e | Documentos de Microsoft"
description: "Este documento le ayuda a tooplan antes de la adopción de centro de seguridad de Azure y consideraciones relativas a las operaciones diarias."
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
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Guía de planeamiento y operaciones de Azure Security Center
Esta guía es para profesionales de informática (TI), arquitectos de TI, los analistas de seguridad de información y los administradores de la nube cuyas organizaciones va toouse Azure Security Center.

>[!NOTE] 
>A partir de los principios de junio de 2017, centro de seguridad usará Hola Microsoft Monitoring Agent toocollect y almacenar datos. Vea [migración de la plataforma de Azure Security Center](security-center-platform-migration.md) toolearn más. información de Hello en este artículo representa la funcionalidad del centro de seguridad después de la transición toohello Microsoft Monitoring Agent.
>

## <a name="planning-guide"></a>Guía de planeamiento
Esta guía incluye un conjunto de pasos y tareas que puede seguir toooptimize que el uso del centro de seguridad según los requisitos de seguridad de su organización y el modelo de administración en la nube. provecho de tootake del centro de seguridad, es importante toounderstand cómo distintas personas o equipos en su organización utilizar desarrollo seguro de hello servicio toomeet y supervisión de operaciones, gobierno, y necesita respuesta a incidentes. Hola áreas clave tooconsider al planear el centro de seguridad de toouse son:

* Roles de seguridad y controles de acceso
* Directivas de seguridad y recomendaciones
* Recopilación de datos y almacenamiento
* Supervisión continuada de la seguridad
* Respuesta a los incidentes

En la siguiente sección hello, aprenderá cómo tooplan para cada una de esas áreas y aplicar las recomendaciones según sus requisitos.

> [!NOTE]
> Lectura [preguntas más frecuentes (P+F) de Azure Security Center](security-center-faq.md) para obtener una lista de preguntas comunes que también pueden ser útiles durante Hola diseño y la fase de planeamiento.
> 

## <a name="security-roles-and-access-controls"></a>Roles de seguridad y controles de acceso
Según el tamaño de Hola y la estructura de su organización, varios usuarios y equipos pueden utilizar tareas relacionadas con la seguridad del centro de seguridad tooperform diferentes. Hola después diagrama tiene un ejemplo de roles ficticios y sus respectivos roles y responsabilidades de seguridad:

![Roles](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

Centro de seguridad permite a estas personas toomeet estas diversas responsabilidades. Por ejemplo:

**Jeff (Propietario de la carga de trabajo de la nube)**

* Administración de una carga de trabajo de nube y sus recursos relacionados
* Responsable de la implementación y el mantenimiento de las protecciones de acuerdo con la directiva de seguridad de la empresa

**Ellen (CISO/CIO)**

* Responsable de todos los aspectos de seguridad para la empresa de Hola
* Desea postura de seguridad de la compañía de toounderstand hello en cargas de trabajo en la nube
* Necesita toobe informa de los riesgos y ataques principales

**David (Seguridad de TI)**

* Existen tooensure Hola adecuado protecciones de directivas de seguridad de la compañía de conjuntos
* Supervisa el cumplimiento con directivas
* Genera informes para la dirección ejecutiva o los auditores

**Judy (Operaciones de seguridad)**

* Supervisa y responde toosecurity alertas 24/7
* Eleva tooCloud propietario de la carga de trabajo o el analista de seguridad de TI

**Sam (Analista de seguridad)**

* Investigación de los ataques
* Trabajar con la corrección de tooapply de propietario de la carga de trabajo en la nube 

Centro de seguridad usa [Control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md), lo que proporciona [roles integrados](../active-directory/role-based-access-built-in-roles.md) que se puede asignar toousers, grupos y servicios de Azure. Cuando un usuario abre el centro de seguridad, solo ven información relacionada con tooresources tienen acceso. Lo que significa que usuario Hola se asigna el rol de Hola de propietario, Colaborador o lector toohello suscripción o grupo de recursos que pertenece el recurso. En los roles de toothese adición, hay dos funciones específicas de centro de seguridad:

- **Lector de seguridad**: usuario que pertenece el rol de toothis es ser capaz de tooview derechos tooSecurity Center, que incluye recomendaciones, alertas, directivas y mantenimiento, pero no será capaz de toomake cambios.
- **Administrador de seguridad**: mismo descartar como lector de seguridad pero también puede actualizar directiva de seguridad de hello, recomendaciones y alertas.

Hola roles de centro de seguridad que se ha descrito anteriormente no tienen acceso a las áreas de servicio de tooother de Azure como almacenamiento, Web y móviles o Internet de las cosas.  

> [!NOTE]
> Un usuario necesita toobe al menos una suscripción, el propietario del grupo de recursos o colaborador toobe pueda toosee centro de seguridad de Azure. 
> 
> 

Con los roles de Hola se han explicado en el diagrama anterior hello, Hola se necesitaría RBAC siguiente:

**Jeff (Propietario de la carga de trabajo de la nube)**

* Propietario o colaborador del grupo de recursos

**David (Seguridad de TI)**

* Propietario o colaborador de la suscripción o administrador de seguridad

**Judy (Operaciones de seguridad)**

* Lector de suscripción o los avisos de tooview de gráficos de seguridad
* Suscripción propietario o colaborador o administrador de seguridad necesario toodismiss alertas

**Sam (Analista de seguridad)**

* Avisos de tooview de gráficos de suscripción
* Propietario o colaborador de suscripción necesario toodismiss alertas
* El área de trabajo de Access toohello pueden requerir

Otro tooconsider de información importante:

* Solo los propietarios o colaboradores de la suscripción y los administradores de seguridad pueden editar una directiva de seguridad
* Los únicos que pueden aplicar recomendaciones de seguridad para un recurso son los propietarios y los colaboradores de la suscripción y del grupo de recursos.

Al planificar el control de acceso mediante RBAC de centro de seguridad, ser toounderstand seguro de que en su organización va a utilizar el centro de seguridad. También, los tipos de tareas que realizarán, y luego configure RBAC en consecuencia.

> [!NOTE]
> Se recomienda que se definan Hola rol menos permisivo necesarios para los usuarios toocomplete sus tareas. Por ejemplo, los usuarios que solo necesitan tooview información sobre el estado de seguridad de Hola de recursos pero no realizar acciones como aplicar recomendaciones o editar directivas, deben asignarse rol de lector de Hola.
> 
> 

## <a name="security-policies-and-recommendations"></a>Directivas de seguridad y recomendaciones
Una directiva de seguridad define el conjunto de Hola de controles, que se recomiendan para los recursos dentro de hello especificado suscripción. En el centro de seguridad, define directivas según tooyour requisitos de seguridad y empresa tipo hello de aplicaciones o importancia de los datos de Hola.

Las directivas que se habilitarán automáticamente en el nivel de suscripción de hello propagan tooall los grupos de recursos dentro de la suscripción de hello como se muestra en hello siguiente diagrama:

![Directivas de seguridad](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> Si necesita tooreview qué directivas se han cambiado, puede usar [los registros de auditoría de Azure](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/). Los cambios en directivas se reflejan siempre en los registros de auditoría de Azure.
> 
> 

### <a name="security-recommendations"></a>Recomendaciones de seguridad
Antes de configurar las directivas de seguridad, revise cada uno de hello [recomendaciones de seguridad](security-center-recommendations.md)y determinar si estas directivas son apropiadas para sus diversos grupos de recursos y suscripciones. También es importante toounderstand qué acción debe realizarse tooaddress [recomendaciones de seguridad](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) y usuarios de la organización será responsable de la supervisión de las nuevas recomendaciones y tomar Hola necesarios pasos.

Security Center recomendará que proporcione los detalles de contacto de seguridad para su suscripción de Azure. Toocontact Microsoft usará esta información si Hola Microsoft Security Response Center (MSRC) detecta que una entidad ilegal o no autorizada ha obtenido acceso a los datos de clientes. Lectura [proporcionar detalles de contacto de seguridad en Azure Security Center](security-center-provide-security-contact-details.md) para obtener más información acerca de cómo tooenable esta recomendación.

## <a name="data-collection-and-storage"></a>Recopilación de datos y almacenamiento
Centro de seguridad de Azure usa Hola Microsoft Monitoring Agent: se trata de hello usa el mismo agente por hello Operations Management Suite y el servicio de análisis de registros: toocollect datos de seguridad de las máquinas virtuales. Los datos recopilados por este agente se almacenan en las áreas de trabajo de Log Analytics.

### <a name="agent"></a>Agente

Después de habilita la recopilación de datos en la directiva de seguridad de hello, Hola Microsoft Monitoring Agent (para [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) o [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) está instalado en todas las máquinas virtuales de Azure y los nuevos que se crean.  Si Hola que Hola el agente de supervisión de Microsoft instalado, la máquina virtual ya tiene Azure Security Center aprovecharán Hola actual había instalado el agente. proceso del agente de Hello está diseñada toobe no invasiva y tener un impacto muy mínimo en el rendimiento de la máquina virtual.

Hola supervisión Microsoft agente para Windows requiere que utilizan el puerto TCP 443. Vea hello [artículo de solución de problemas](security-center-troubleshooting-guide.md) para obtener más detalles.

Si en algún momento desea toodisable la recopilación de datos, puede desactivarlo en directiva de seguridad de Hola. Sin embargo, dado Hola Microsoft Monitoring Agent puede utilizarse por otra administración de Azure y supervisar los servicios, Hola agente no se desinstalará automáticamente cuando para desactivar la recopilación de datos en el centro de seguridad. Puede desinstalar manualmente el agente de hello si es necesario.

> [!NOTE]
> una lista de las máquinas virtuales compatibles, leer hello toofind [preguntas más frecuentes (P+F) de Azure Security Center](security-center-faq.md).
> 

### <a name="workspace"></a>Área de trabajo

Datos recopilados de hello que Microsoft Monitoring Agent (en nombre del centro de seguridad de Azure) se almacenará en cualquier un existente espacios de trabajo de análisis de registros asociados con su suscripción de Azure o áreas de trabajo nuevo, teniendo en hello cuenta geográfica del programa Hola a máquina virtual. 

Hola portal de Azure, puede examinar toosee una lista de las áreas de trabajo de análisis de registros, las que se crearon por el centro de seguridad de Azure incluidas. Se creará un grupo de recursos relacionado para las nuevas áreas de trabajo. Ambas siguen esta convención de nomenclatura: 

* Área de trabajo: *DefaultWorkspace-[subscription-ID]-[geo]*
* Grupo de recursos: *DefaultResouceGroup-[geo]*

En el caso de las áreas de trabajo creadas por Azure Security Center, los datos se conservan durante 30 días. Para salir de áreas de trabajo, retención se basa en el área de trabajo de hello tarifa.

> [!NOTE]
> Asegúrese de Microsoft privacidad de hello tooprotect compromisos segura y la seguridad de estos datos. Microsoft adhiere a las directrices de seguridad y cumplimiento de toostrict: desde la codificación toooperating un servicio. Para más información sobre el control de datos y la privacidad, lea [Seguridad de datos de Azure Security Center](security-center-data-security.md).
> 

## <a name="ongoing-security-monitoring"></a>Supervisión continuada de la seguridad
Después de la configuración inicial y la aplicación de recomendaciones de centro de seguridad, paso siguiente Hola está considerando procesos operativos del centro de seguridad.

tooaccess centro de seguridad de hello portal de Azure puede hacer clic en **examinar** y tipo **centro de seguridad** en hello **filtro** campo. vistas de Hola que Hola usuario obtiene según los filtros toothese aplicar, en Hola de ejemplo siguiente se muestra un entorno con muchos de los problemas toobe dirigido:

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Centro de seguridad no interfiera con los procedimientos operativos normales, que pasivamente supervisar las implementaciones y proporcionará recomendaciones basadas en las directivas de seguridad de hello que ha habilitado.

Cuando primero participar en toouse centro de seguridad para el actual entorno de Azure, asegúrese de revisar todas las recomendaciones, que se pueden efectuar en hello **recomendaciones** icono o por recurso (**proceso** **Red**, **almacenamiento & datos**, **aplicación**).

Una vez que resolver todas las recomendaciones, Hola **prevención** sección debe ser verde para todos los recursos que se han trabajado. La supervisión continua en este momento se vuelve más fácil porque solo tardará acciones según los cambios en hello seguridad de estado y recomendaciones de iconos del recurso.

Hola **detección** sección es más reactiva, se trata de alertas sobre los problemas que son ambos se está produciendo ahora, o se produjo en hello anterior y detectados por los controles del centro de seguridad y sistemas de terceros 3rd. icono de alertas de seguridad de Hello mostrará gráficos de barras que representan el número de Hola de las alertas de detección de amenazas encontradas en cada día y su distribución entre las categorías de gravedad diferente de hello (bajo, medio, alto). Para obtener más información acerca de las alertas de seguridad, lea [toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> También puede aprovechar Microsoft Power BI toovisualize los datos del centro de seguridad. Consulte [Obtención de información mediante los datos de Azure Security Center con Power BI](security-center-powerbi.md).
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>Supervisión de recursos nuevos o modificados
La mayor parte de los entornos de Azure son dinámicos, con incorporaciones o retiradas periódicas de recursos, configuraciones o cambios, etc. Centro de seguridad le ayuda a asegurarse de que tienen visibilidad sobre el estado de seguridad de Hola de estos recursos nuevo.

Al agregar nuevos recursos (máquinas virtuales, bases de datos de SQL) tooyour entorno de Azure, centro de seguridad automáticamente detectar estos recursos y comenzar toomonitor su seguridad. Esto también incluye los roles web de PaaS y los roles de trabajo. Si está habilitada la recopilación de datos en hello [directiva de seguridad](security-center-policies.md), más las capacidades de supervisión se habilitará automáticamente para las máquinas virtuales.

![Áreas clave](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. En máquinas virtuales, haga clic en **Compute**, en la sección **Prevención**. Los problemas con la habilitación de datos o recomendaciones relacionadas se producirá en hello **Introducción** ficha, y **supervisión recomendaciones** sección.
2. Hola de vista **recomendaciones** toosee lo que, si los hay, se identificaron los riesgos de seguridad para el nuevo recurso de Hola.
3. Es muy común que cuando nuevas máquinas virtuales se agregan tooyour entorno, sistema operativo solo de hello inicialmente está instalado. propietario del recurso de Hola que tenga algún tiempo toodeploy otras aplicaciones que se va a utilizar estas máquinas virtuales.  Idealmente, debe saber la intención final de Hola de esta carga de trabajo. ¿Que va toobe un servidor de aplicaciones? En función de qué esta nueva carga de trabajo es toobe continuo, puede habilitar Hola adecuado **directiva de seguridad**, que es el tercer paso de hello en este flujo de trabajo.
4. Al agregar nuevos recursos tooyour entorno de Azure, es posible que aparezcan nuevas alertas de hello **alertas de seguridad** icono. Siempre compruebe si hay nuevas alertas en este icono y actuar según las recomendaciones de tooSecurity Center.

También deberá tooregularly Hola estado del monitor de cambios de configuración de tooidentify de recursos existente que ha creado los riesgos de seguridad, una desviación de líneas de base recomendadas y las alertas de seguridad. Empieza en el panel del centro de seguridad de Hola. Desde allí tendrá tres tooreview áreas principales de forma coherente.

![Operaciones](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. Hola **prevención** panel sección proporciona recursos clave de acceso rápido tooyour. Utilice este proceso, redes, almacenamiento y datos y aplicaciones de opción toomonitor.
2. Hola **recomendaciones** panel le permite tooreview recomendaciones de centro de seguridad. Durante la supervisión continua es posible que no tiene las recomendaciones a diario, que es normal, ya que dirigirse todas las recomendaciones sobre la instalación de centro de seguridad inicial de Hola. Por esta razón, que no tenga ninguna nueva información de esta sección todos los días y solo necesitarán tooaccess, según sea necesario.
3. Hola **detección** sección podría cambiar de forma muy frecuente o muy poco frecuente. Revise siempre las alertas de seguridad y tome medidas basadas en las recomendaciones de Security Center.

## <a name="incident-response"></a>Respuesta a los incidentes
Centro de seguridad detecta y le avisa toothreats cuando se producen. Las organizaciones deben supervisar para nuevas alertas de seguridad y actuar como sea necesario tooinvestigate aún más o corregir ataque Hola. Para más información sobre cómo funciona la detección de amenazas de Security Center, consulte [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md).

Aunque este artículo no es requisito Hola intención tooassist crear su propio plan de respuesta a incidentes, vamos toouse respuestas de seguridad de Microsoft Azure en el ciclo de vida de hello en la nube como base de hello en tres fases de la respuesta a incidentes. fases de Hola se muestran en hello siguiente diagrama:

![Actividad sospechosa](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> Puede usar Hola National Institute of Standards and Technology (NIST) [Guía de control de incidentes de seguridad de equipo](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) como una referencia tooassist ayudará a generar sus propios.
> 

Puede utilizar alertas del centro de seguridad durante Hola siguientes fases:

* **Detectar**: identifique una actividad sospechosa en uno o varios recursos. 
* **Evaluar**: realizar Hola evaluación inicial tooobtain obtener más información sobre la actividad sospechosa Hola.
* **Diagnosticar**: usar Hola corrección pasos tooconduct Hola procedimiento técnica tooaddress Hola problema.

Cada alerta de seguridad se proporciona información que se puede usar toobetter comprender la naturaleza Hola de ataque de Hola y sugerir posibles mitigaciones. Algunas alertas también proporcionan vínculos tooeither más información o tooother orígenes de información dentro de Azure. Puede usar información de hello proporcionada para una investigación adicional y mitigación de toobegin y también puede buscar datos relacionados con la seguridad que se almacenan en el área de trabajo.

Hello en el ejemplo siguiente se muestra una actividad sospechosa de RDP tienen lugar:

![Actividad sospechosa](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

Como puede ver, esta hoja muestra detalles relacionados con el tiempo de presentación que ataque Hola llevó a cabo, Hola nombre de host de origen, Hola VM de destino y también proporciona pasos de recomendación. En algunos Hola circunstancias información de origen del ataque Hola puede estar vacío. Consulte [Missing Source Information in Azure Security Center Alerts](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) (Falta de información de origen en las alertas de Azure Security Center) para más información acerca de este tipo de comportamiento.

Hola [cómo tooLeverage hello Azure Security Center & Microsoft Operations Management Suite para una respuesta a incidentes](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) vídeo puede ver algunas demostraciones que pueden ayudar a toounderstand cómo pueden usarse centro de seguridad en cada uno una de estas fases.

> [!NOTE]
> Lectura [al aprovechar Azure Security Center para la respuesta a incidentes](security-center-incident-response.md) para obtener más información sobre la forma tooassist de capacidades de centro de seguridad de toouse durante la respuesta a incidentes de procesar. 
> 
> 

## <a name="see-also"></a>Otras referencias
En este documento, se habrá aprendido cómo tooplan para la adopción de centro de seguridad. toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Administrar y responder a alertas de toosecurity en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md)
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.

