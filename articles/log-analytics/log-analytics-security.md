---
title: "seguridad de datos de análisis de aaaLog | Documentos de Microsoft"
description: "Obtenga información sobre cómo Log Analytics protege su privacidad y sus datos."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Seguridad de datos de Log Analytics
Microsoft está comprometido tooprotecting su privacidad y los datos, al tiempo que ofrece software y los servicios que le ayuden a administrar Hola infraestructura de TI de su organización. Reconocemos que cuando confía sus datos tooothers, esa confianza requiere una seguridad rigurosa. Microsoft adhiere a las directrices de seguridad y cumplimiento de toostrict: desde la codificación toooperating un servicio.

 La seguridad y la protección de los datos son prioritarias en Microsoft. Póngase en contacto con nosotros tiene preguntas, sugerencias o problemas acerca de hello después de obtener información, incluidas nuestras directivas de seguridad en [opciones de soporte técnico de Azure](http://azure.microsoft.com/support/options/).

Este artículo explica cómo se recopilan, procesan y protegido por el análisis de registro de hello Operations Management Suite (OMS). Puede usar el servicio web de agentes tooconnect toohello, utilizar datos operativos de System Center Operations Manager toocollect o recuperar datos de diagnóstico de Azure para su uso por el análisis de registro. los datos recopilados Hola se envían a través de hello Internet mediante la autenticación basada en certificado de & SSL 3 toohello servicio de análisis de registros, que se hospeda en Microsoft Azure. Agente de hello comprimir datos antes de enviarlo.

Hola servicio de análisis de registros administra los datos en la nube segura mediante el uso de hello siguientes métodos:

* Segregación de datos
* Retención de datos
* Seguridad física
* Administración de incidentes
* Cumplimiento normativo
* Certificaciones de estándares de seguridad

## <a name="data-segregation"></a>Segregación de datos
Los datos del cliente se mantienen separados de forma lógica en cada componente en hello servicio OMS. Todos los datos se etiquetan por organización. Este etiquetado persiste a lo largo del ciclo de vida de datos de Hola y se aplica en cada nivel de servicio de Hola. Cada cliente tiene un blob de Azure dedicado que aloja los datos a largo plazo de Hola

## <a name="data-retention"></a>Retención de datos
Los datos indizados de búsqueda de registro se almacenan y mantienen tooyour correspondiente plan de precios. Para obtener más información, consulte [Precios de Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).

Microsoft elimina los datos del cliente 30 días después de cerrar el área de trabajo OMS Hola. Microsoft también elimina la cuenta de almacenamiento de Azure donde residen los datos de Hola Hola. Cuando se eliminan los datos de cliente, no se destruyen unidades físicas.

Hello en la tabla siguiente enumera algunas de las soluciones disponibles de hello en OMS y ejemplos Hola tipos de datos que recopilan.

| **Solución** | **Tipos de datos** |
| --- | --- |
| Evaluación de la configuración |Datos de configuración, metadatos y datos de estado |
| Planificación de capacidad |Datos de rendimiento y metadatos |
| Antimalware |Datos de configuración y metadatos |
| Evaluación de la actualización del sistema |Metadatos y datos de estado |
| Administración de registros |Registros IIS, de eventos de Windows o de eventos definidos por el usuario |
| Seguimiento de cambios |Inventario de software y metadatos de servicio de Windows |
| Evaluación de SQL y Active Directory |Datos de WMI, datos de registro, datos de rendimiento y resultados de la vista de administración dinámica de SQL Server |

Hello en la tabla siguiente muestra ejemplos de tipos de datos:

| **Tipo de datos** | **Fields** |
| --- | --- |
| Alerta |Alert Name, Alert Description, BaseManagedEntityId, Problem ID, IsMonitorAlert, RuleId, ResolutionState, Priority, Severity, Category, Owner, ResolvedBy, TimeRaised, TimeAdded, LastModified, LastModifiedBy, LastModifiedExceptRepeatCount, TimeResolved, TimeResolutionStateLastModified, TimeResolutionStateLastModifiedInDB, RepeatCount |
| Configuración |CustomerID, AgentID, EntityID, ManagedTypeID, ManagedTypePropertyID, CurrentValue, ChangeDate |
| Evento |EventId, EventOriginalID, BaseManagedEntityInternalId, RuleId, PublisherId, PublisherName, FullNumber, Number, Category, ChannelLevel, LoggingComputer, EventData, EventParameters, TimeGenerated, TimeAdded <br>**Nota:** al escribir eventos con campos personalizados en el registro de eventos de Windows toohello, OMS los recopila. |
| Metadatos |BaseManagedEntityId, ObjectStatus, OrganizationalUnit, ActiveDirectoryObjectSid, PhysicalProcessors, NetworkName, IPAddress, ForestDNSName, NetbiosComputerName, VirtualMachineName, LastInventoryDate, HostServerNameIsVirtualMachine, IP Address, NetbiosDomainName, LogicalProcessors, DNSName, DisplayName, DomainDnsName, ActiveDirectorySite, PrincipalName, OffsetInMinuteFromGreenwichTime |
| Rendimiento |ObjectName, CounterName, PerfmonInstanceName, PerformanceDataId, PerformanceSourceInternalID, SampleValue, TimeSampled, TimeAdded |
| Estado |StateChangeEventId, StateId, NewHealthState, OldHealthState, Context, TimeGenerated, TimeAdded, StateId2, BaseManagedEntityId, MonitorId, HealthState, LastModified, LastGreenAlertGenerated, DatabaseTimeModified |

## <a name="physical-security"></a>Seguridad física
Hola análisis de registros en el servicio OMS es atendido por personal de Microsoft y todas las actividades se registran y se pueden auditar. servicio de Hola se ejecuta completamente en Azure y cumple Hola criterios de ingeniería comunes de Azure. Puede ver detalles acerca de la seguridad física de Hola de activos de Azure en la página 18 de hello [información general de seguridad de Microsoft Azure](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf). Áreas de toosecure de derechos de acceso físico se cambian dentro de un día para cualquier persona que ya no tiene la responsabilidad de servicio de OMS hello, incluida la transferencia y la terminación. Puede leer acerca de la infraestructura física global Hola usamos en [Microsoft Datacenters](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx).

## <a name="incident-management"></a>Administración de incidentes
OMS incluye un proceso de administración de incidentes que cumplen todos los servicios de Microsoft. toosummarize,:

* Usar un modelo de responsabilidad compartida donde una parte de la responsabilidad de seguridad pertenece tooMicrosoft y una parte pertenece toohello cliente
* Administramos los incidentes de seguridad de Azure.
  * Iniciamos una investigación tras la detección de un incidente.
  * Evaluar el impacto de Hola y la gravedad de un incidente por un miembro del equipo en la llamada de respuesta a incidentes. Se basa en la evidencia, evaluación de hello puede o no puede dar lugar a más consultas toohello seguridad del equipo de respuesta.
  * Diagnosticar un incidente por seguridad respuesta expertos tooconduct Hola técnica o forense investigación, identifique las estrategias de contención, la mitigación y la solución. Si el equipo de seguridad de hello considera que los datos del cliente pueden haber vuelto expuesto tooan ilegal o no autorizado ejecución individual en paralelo de hello proceso de notificación de incidentes de cliente comienza en paralelo.  
  * Estabilice y se recupera del incidente de Hola. equipo de respuesta a incidentes de Hello crea un problema de Hola de toomitigate de plan de recuperación. Pueden llevarse a cabo procesos de gestión de crisis, como poner en cuarentena sistemas afectados, de inmediato y en paralelo al diagnóstico. Pueden planificarse más mitigaciones término que se producen después de que transcurra el riesgo inmediato de Hola.  
  * Cerrar el incidente de Hola y llevar a cabo un análisis detallado. equipo de respuesta a incidentes de Hello crea un análisis detallado que se describan los detalles de Hola de hello incidente, con directivas de toorevise de intención de hello, procedimientos y procesos tooprevent una periodicidad de evento Hola.
* Notificamos a los clientes de los incidentes de seguridad.
  * Determinar el ámbito de Hola de clientes afectados y tooprovide todo el personal que se ve afectado como detallada un aviso como sea posible
  * Crear un tooprovide de aviso de clientes con información lo suficientemente detallada para que puedan realizar una investigación en su extremo y cumplir los compromisos que han realizado los usuarios finales de tootheir mientras no innecesariamente retrasando el proceso de notificación de Hola.
  * Confirme y declarar incidente hello, según sea necesario.
  * Envíe a los clientes una notificación de incidentes puntual y de acuerdo con cualquier compromiso contractual o jurídico. Las notificaciones de incidentes de seguridad se entregan tooone o varios de los administradores de un cliente de alguna forma de instrucciones SELECT de Microsoft, incluido el correo electrónico.
* Formamos y preparamos al equipo.
  * Personal de Microsoft es toocomplete requiere seguridad y concienciación, lo que les ayuda a tooidentify y sospecha que hay problemas de seguridad de informes.  
  * Operadores que trabajan en hello servicio de Microsoft Azure tienen las obligaciones de entrenamiento de adición que rodea a sus sistemas de toosensitive de acceso que hospeda los datos del cliente.
  * El personal de respuesta de seguridad de Microsoft recibe cursos especializados para los roles que desempeñan.

En caso de pérdida de datos de cualquier cliente, se notificará a cada cliente en el plazo de un día. Sin embargo, con OMS nunca se han perdido datos de cliente. Además, mantenemos copias de los datos que creamos y los distribuimos geográficamente.

Para obtener más información acerca de cómo Microsoft responde toosecurity incidentes, consulte [respuestas de seguridad de Microsoft Azure en hello en la nube](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf).

## <a name="compliance"></a>Cumplimiento normativo
Hola de seguridad de la información de OMS software desarrollo y el servicio del equipo y el programa de gobernanza es compatible con sus requisitos empresariales y cumple las normativas y toolaws tal y como se describe en [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) y [Cumplimiento del centro de confianza de Microsoft](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx). En estas páginas también se describe cómo OMS establece los requisitos de seguridad identifica los controles de seguridad, y administra y supervisa los riesgos. Cada año, revisamos las directivas, los estándares, los procedimientos y las instrucciones.

Cada miembro del equipo de desarrollo de OMS recibe cursos formales sobre seguridad de aplicaciones. Internamente, utilizamos un sistema de control de versiones para el desarrollo de software. Cada proyecto de software está protegido por el sistema de control de versiones de Hola.

Microsoft cuenta con un equipo de seguridad y cumplimiento normativo que supervisa y evalúa todos los servicios de Microsoft. Los responsables de seguridad de información constituyen equipo hello y no están asociados con hello ingeniería departamentos que desarrollar OMS. los responsables de seguridad Hola tienen su propia cadena de administración y realizar evaluaciones independientes de productos y la seguridad de tooensure de servicios y la conformidad.

Al comité de dirección de Microsoft se le notifica mediante informes anuales sobre todos los programas de información de seguridad de Microsoft.

Hola equipo software de OMS servicio y desarrollo está trabajando activamente con los equipos de cumplimiento y Legal de Microsoft de Hola y otro tooacquire de socios del sector certificaciones distintos.

## <a name="certifications-and-attestations"></a>Certificaciones y atestaciones
OMS Log Analytics cumple Hola según los requisitos:

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [Tarjeta Industry (PCI compatible) datos estándar de seguridad pago (PCI DSS)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI) por hello PCI Security Standards Council.
* [Conformidad con Service Organization Control (SOC) 1, tipo 1 y SOC 2, tipo 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2)
* [HIPAA y HITECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) para aquellas empresas que posean un contrato de asociación comercial según las normas HIPAA.
* Criterios de ingeniería comunes de Windows
* Microsoft Trustworthy Computing
* Como un servicio de Azure, componentes de Hola que OMS usa cumplen requisitos de cumplimiento de tooAzure. Puede obtener más información en el artículo [Microsoft Trust Center Compliance](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx) (Cumplimiento normativo del Centro de confianza de Microsoft Azure).

> [!NOTE]
> En algunas certificaciones o atestaciones, Log Analytics aparece con su nombre anterior, *Operational Insights*.
>
>


## <a name="cloud-computing-security-data-flow"></a>Flujo de datos de seguridad de informática en la nube
Hello siguiente diagrama muestra una arquitectura de seguridad en la nube como flujo de Hola de información de su empresa y cómo se protege tal cual mueve toohello servicio de análisis de registros, que vio por parte del usuario en el portal de OMS Hola. Para obtener más información acerca de cada paso sigue diagrama Hola.

![Imagen de recopilación de datos de OMS y seguridad](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1. Suscripción a Log Analytics y recopilación de datos
Para su tooLog de datos de toosend de organización análisis, configurar a agentes de Windows, los agentes se ejecutan en máquinas virtuales de Azure o agentes de OMS para Linux. Si se utilizan agentes de Operations Manager, a continuación, usar un asistente de configuración en tooconfigure de consola de operaciones de hello ellos. Los usuarios (que podrían ser usted, otros usuarios individuales o un grupo de personas) crear una o varias cuentas OMS (áreas de trabajo OMS) y registrar a agentes mediante uno de hello siguientes cuentas:

* [Id. de organización](../active-directory/sign-up-organization.md)
* [Cuenta de Microsoft: Outlook, Office Live, MSN](http://www.microsoft.com/account/default.aspx)

Un espacio de trabajo de OMS es donde se recopilan, agregan, analizan y presentan los datos. Un área de trabajo se utiliza principalmente como medio toopartition datos, y cada área de trabajo es único. Por ejemplo, conviene toohave administran sus datos de producción con una área de trabajo OMS y los datos de prueba se administran con otra área de trabajo. Áreas de trabajo también ayudan a un datos de toohello de acceso del usuario de control de administrador. Cada espacio de trabajo puede tener, a su vez, varias cuentas de usuario asociada; y viceversa: cada cuenta de usuario puede tener varios espacios de OMS. Las áreas de trabajo se crean en función de la región del centro de datos. Cada área de trabajo está replicada tooother centros de datos en la región de hello, principalmente para la disponibilidad del servicio de OMS.

Operations Manager, cuando se complete el Asistente de configuración de hello, cada grupo de administración de Operations Manager establece una conexión con hello servicio de análisis de registros. A continuación, usar Hola Asistente para agregar equipos toochoose qué equipos de grupo de administración de hello pueden servicio toohello de toosend datos. Para otros tipos de agentes, cada uno conecta con seguridad toohello servicio OMS.

Se cifran todas las comunicaciones entre sistemas conectados y Hola servicio de análisis de registros.  Hello TLS protocolo (HTTPS) se utiliza para el cifrado.  se sigue el proceso SDL Microsoft Hello tooensure análisis de registros está actualizado con los avances más recientes de hello en los protocolos criptográficos.

Cada tipo de agente recopila datos para Log Analytics. Hola el tipo de datos que se recopilan es depende de los tipos de Hola de soluciones usadas. Puede ver un resumen de recolección de datos en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md). Además, hay información más detallada disponible sobre este tema para la mayoría de las soluciones. Una solución es una agrupación de vistas predefinidas, consultas de búsqueda de registros, reglas de recopilación de datos y lógica de procesamiento. Solo los administradores pueden usar tooimport una solución de análisis de registros. Después de importa la solución de hello, resulta servidores de administración de Operations Manager ha movido toohello (si se usa) y, a continuación, los agentes de tooany que ha elegido. Posteriormente, los agentes de hello recopilan datos de Hola.

## <a name="2-send-data-from-agents"></a>2. Envío de datos desde agentes
Registrar todos los tipos de agente con una clave de registro y se establece una conexión segura entre el agente de Hola y el servicio de análisis de registros de hello mediante la autenticación basada en certificados y SSL con el puerto 443. OMS usa un toogenerate almacén secreto y mantener las claves. Las claves privadas se giran cada 90 días y se almacenan en Azure y se administran mediante hello Azure operaciones que siguen procedimientos legales y cumplimiento estrictos.

Con Operations Manager, registra un área de trabajo con el servicio de análisis de registros de Hola y se establece una conexión HTTPS segura entre el servidor de administración de Operations Manager Hola.

Agentes de Windows que se ejecutan en máquinas virtuales de Azure, almacenamiento de solo lectura es ninguna clave para eventos de diagnóstico de tooread usado en las tablas de Azure.

Si cualquier agente no se puede toocommunicate toohello servicio por algún motivo, hello datos recopilados se almacenan localmente en una caché temporal y servidor de administración de hello intenta datos de hello tooresend cada ocho minutos durante dos horas. datos almacenados en caché del agente de Hello está protegidos por el almacén de credenciales del sistema operativo Hola. Si el servicio de hello no se puede procesar datos Hola después de dos horas, agentes de hello pondrá en cola datos Hola. Si se llena la cola de hello, OMS inicia quitar tipos de datos, a partir de los datos de rendimiento. límite de la cola de Hello agente es una clave del registro para que pueda modificar, si es necesario. Los datos recopilados se comprimen y envían servicio toohello, omitiendo las bases de datos local, por lo que no se agrega cualquier toothem de carga. Después de recopila Hola se envían datos, se quita de la memoria caché de Hola.

Tal y como se describió anteriormente, los datos de los agentes se envían a través de SSL tooMicrosoft centros de datos de Azure. Si lo desea, puede usar ExpressRoute tooprovide mayor seguridad para los datos de Hola. ExpressRoute es una manera toodirectly conectarse tooAzure desde la red WAN existente, como un protocolo múltiple etiquetar conmutación VPN (MPLS), proporcionado por un proveedor de servicios de red. Para obtener más información, consulte el artículo sobre [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3. Hola servicio de análisis de registros recibe y procesa los datos
Hola servicio de análisis de registros asegura que los datos entrantes provienen de un origen de confianza mediante la validación de certificados y la integridad de los datos Hola con autenticación de Azure. Hello datos sin procesar se almacenan entonces como un blob en [almacenamiento de Microsoft Azure](../storage/common/storage-introduction.md) y no está cifrada. Sin embargo, cada blob de almacenamiento de Azure tiene un conjunto de conjunto único de claves, que es accesible toothat solo usuario. tipo de Hola de datos que se almacenarán depende de tipos de Hola de soluciones que se han importado y usan toocollect datos. A continuación, Hola servicio de análisis de registros procesa datos sin procesar de hello para el blob de almacenamiento de Azure de Hola.

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4. Usar datos de análisis de registros tooaccess Hola
Puede iniciar sesión tooLog análisis en el portal de OMS hello mediante cuenta profesional de Hola o cuenta de Microsoft que configuró anteriormente. Todo el tráfico entre el portal de OMS de Hola y análisis de registros de OMS se envía por un canal HTTPS seguro. Al usar el portal de OMS hello, se genera un identificador de sesión en el cliente de usuario de hello (explorador web) y datos se almacenan en una caché local hasta que finaliza la sesión de Hola. Cuando termina, se elimina la caché de Hola. Las cookies del cliente, que no contienen información de identificación personal, no se quitan automáticamente. Las de sesión se marcan con HTTPOnly y se protegen. Tras un período de inactividad predeterminado, se termina la sesión del portal OMS Hola.

Mediante el portal OMS de hello, puede exportar el archivo CSV de datos tooa y puede tener acceso a datos mediante las API de búsqueda. Exportar a CSV es too50 limitado, 000 filas por exportación y datos de API es too5 restringido, 000 filas por la búsqueda.

## <a name="next-steps"></a>Pasos siguientes
* [Empezar a trabajar con análisis de registros](log-analytics-get-started.md) toolearn más información sobre análisis de registros y póngase en marcha en minutos.
