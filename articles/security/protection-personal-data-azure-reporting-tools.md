---
title: "aaaDocument protección de datos personales con herramientas de informes de Azure | Documentos de Microsoft"
description: "Cómo toouse Azure toohelp informes de servicios y tecnologías de proteger la privacidad de los datos personales."
services: security
documentationcenter: na
author: barclayn
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
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>Documentación de protección de datos personales con herramientas de informes de Azure

Este artículo describe cómo toouse Azure reporting services y tecnologías toohelp proteger la privacidad de los datos personales.

## <a name="scenario"></a>Escenario

Una empresa cruise grandes, con sede en Estados Unidos de hello, está ampliando sus itinerarios toooffer de operaciones en Hola Mediterráneo, Adriático y Mar Báltico, así como Hola británicas. toohelp estos esfuerzos, ha adquirido varias líneas cruise más pequeñas que encuentre en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido

la compañía de Hello utiliza Microsoft Azure para su procesamiento y almacenamiento de los datos corporativos. Esto incluye información de identificación personal como nombres, direcciones, números de teléfono e información de la tarjeta de crédito de su clientela global. También incluye información de recursos humanos tradicionales como direcciones, números de teléfono, los números de identificación fiscal y médica información acerca de los empleados de la compañía en todas las ubicaciones. línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad que incluye información personal tootrack relaciones con los clientes actuales y pasados.

Red de Hola de acceso de los empleados corporativos de oficinas remotas y la Agencia de viajes de la compañía de Hola ubicados en todo Hola a todos tienen acceso a recursos de empresa de toosome.

## <a name="problem-statement"></a>Declaración del problema

empresa Hola debe proteger la privacidad de Hola de datos personales de los empleados y los clientes a través de una estrategia de seguridad de varias capas que usa características de seguridad de los controles de tooimpose estricta del procesamiento de tooand de acceso de datos personales y de administración de Azure y debe ser toodemonstrate capaz de medidas de su protección toointernal y auditores externos.

## <a name="company-goal"></a>Objetivo de la empresa

Como parte de su estrategia de seguridad de defensa en profundidad, es un tootrack de objetivo de la empresa en todos los procesos de tooand de acceso de datos personales y asegúrese de que la documentación de protección de privacidad adecuado para los datos personales activa y en funcionamiento.

## <a name="solutions"></a>Soluciones

Microsoft Azure proporciona el registro de supervisión, completa y toohelp de herramientas de diagnóstico realizar un seguimiento y registrar las actividades y eventos asociados a obtener acceso y procesar datos personales, geográfica flujo de datos y los datos de toopersonal de acceso de otros fabricantes. Dado que la seguridad de los datos personales en la nube de hello constituye una responsabilidad compartida, Microsoft también proporciona a los clientes:

- Información detallada sobre su propio procesamiento de datos de los clientes

- Medidas de seguridad administradas por Microsoft

- Dónde y cómo envía datos de los clientes

- Detalles del proceso de revisiones de privacidad de Microsoft

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) es el directorio multiinquilino basado en la nube y el servicio de administración de identidades de Microsoft. Hola en el inicio de sesión del servicio y proporcionarán funciones de informes de auditoría con el inicio de sesión detallada y toohelp de información de actividad de aplicación uso para supervisar y asegurar datos personales toocustomers' el acceso adecuado y los empleados.

Hay dos tipos de informes de actividad:

- Hola [actividad informes y registros de auditoría](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) proporcionan un registro detallado de las actividades y tareas del sistema

- Hola [registro/informe de actividad de inicios de sesión](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) muestra quién ha realizado cada actividad enumerada en el informe de auditoría de Hola

Con hello dos juntos, puede seguir el historial de cada tarea lleva a cabo Hola y saber quién realizó cada uno. Ambos tipos de informes son personalizables y se pueden filtrar.

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>¿Cómo obtengo acceso Hola auditoría y seguridad registros?

Hello registros de auditoría y seguridad son accesibles desde el portal de Active Directory de Hola de tres maneras diferentes: a través de hello **actividad** sección (seleccione **registros de auditoría** o **deiniciosdesesión**), o desde **usuarios y grupos** o **aplicaciones empresariales** en **administrar** en Active Directory. Los informes también pueden obtenerse a través de hello Azure Active Directory API de informes. 

1. Hola portal de Azure, seleccione **Azure Active Directory.**

2. Hola **actividad** sección, seleccione **registros de auditoría.**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. Personalizar la vista de lista de hello haciendo clic en **columnas** en la barra de herramientas de Hola.

4.  Seleccione un elemento en toosee de vista de lista de hello todos los detalles disponibles sobre él.

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

Los informes de Azure Active Directory también incluyen dos tipos de informes de seguridad, **usuarios marcados en riesgo** e **inicios de sesión no seguros**, que pueden ayudarle a supervisar posibles riesgos en su entorno de Azure.

Para obtener más información acerca de hello servicio de informes, consulte [reporting de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

Visite [informes de actividad de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) para obtener más detalles acerca de los informes de hello disponibles en Azure Active Directory. Este sitio incluye más detalles acerca de cómo tooaccess y usar [informes de actividad de registros de auditoría](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) y [informes de actividad de inicio de sesión](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) en el portal de Hola. También incluye información sobre los informes de seguridad [usuarios marcados en riesgo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) e [inicio de sesión no seguro](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins).

Visite hello [auditoría referencia de la API de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) sitio para obtener más información acerca de cómo tooconnect tooAzure Directory reporting mediante programación.

### <a name="log-analytics"></a>Log Analytics

[Análisis de registros](https://azure.microsoft.com/services/log-analytics/) puede [recopilar datos de Azure Monitor](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate con otros datos y proporcionar análisis adicionales. Azure Monitor recopila y analiza datos de supervisión para su entorno de Azure. 

Las herramientas de análisis de Log Analytics, como búsquedas de registros, vistas y soluciones funcionan con todos los datos recopilados, que proceden del análisis centralizado de todo el entorno. Análisis de registros pueden agregar y analizar los registros de eventos de Windows, registros de IIS y Syslogs, que puede ayudar a detectar posibles infracciones de datos personales que pudieron exponer a los usuarios de los datos personales toounauthorized.

#### <a name="how-do-i-use-log-analytics"></a>¿Cómo se puede usar Log Analytics?

Análisis de registros puede tener acceso a través del portal de OMS de Hola o hello portal de Azure, desde cualquier explorador web. Análisis de registros incluyen una recuperación de tooquickly de lenguaje de consulta y consolidan los datos en el repositorio de Hola. Puede crear y guardar búsquedas de registros toodirectly analizar los datos en el portal de Hola.

toocreate un área de trabajo de análisis de registros en el portal de Azure, Hola Hola siguientes:

1. Seleccione **análisis de registros** de lista de hello de servicios en hello Marketplace.

2. Seleccione **crear,** , a continuación, especificar nombre de Hola de su área de trabajo OMS, seleccione su suscripción, el grupo de recursos, la ubicación y nivel de precios.

3. Haga clic en **Aceptar** toodisplay una lista de las áreas de trabajo.

4. Seleccione un área de trabajo toosee sus detalles.

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

Visite hello [documentación de análisis de registros](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn más información acerca del servicio de Hola.

Visite hello [empezar a trabajar con un área de trabajo de análisis de registros](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) tutorial toocreate un área de trabajo de evaluación y obtenga información acerca de conceptos básicos de Hola de cómo toouse Hola servicio.

Visite Hola siguiente páginas web para obtener información más detallada de cómo se registra tooconnect toouse análisis de registros con hello descritos anteriormente:

[Orígenes de datos de registros de eventos de Windows en Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[Registros de IIS en Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[Orígenes de datos de Syslog en Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Azure Monitor o registro de actividad de Azure 

[Azure Monitor](https://azure.microsoft.com/services/monitor/) ofrece registros y métricas de infraestructuras a nivel básico para la mayoría de los servicios de Microsoft Azure.
Supervisión puede ayudar toogain información detallada acerca de las aplicaciones de Azure. Monitor de Azure se basa en la extensión de diagnósticos de Azure hello (Windows o Linux) para recopilar la mayoría de los registros y las métricas de nivel de aplicación. [Hello Azure Activity Log](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) es uno de los recursos de hello puede ver con el Monitor de Azure. Realiza un seguimiento de todas las llamadas API y proporciona abundante información sobre las actividades que se producen en [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).
Puede buscar hello (anteriormente denominados operativa o los registros de auditoría) de registro de actividad para obtener información sobre el recurso tal como lo ve Hola infraestructura de Azure. 

Aunque gran parte de información de hello registra Hola actividad registro pertenece tooperformance y servicio de mantenimiento, también hay información tooprotection relacionado de datos. Gracias a Hola registro de actividad, puede determinar Hola "qué, quién y cuándo" para las operaciones (PUT, POST, DELETE) realizadas en los recursos de hello en su suscripción de Azure de escritura.

Por ejemplo, proporciona un registro cuando un administrador elimina un grupo de seguridad de red, lo que puede afectar Hola protección de datos personales. Las entradas de registros de actividad se almacenan en Azure Monitor durante 90 días.

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>¿Cómo se puede usar datos de hello recopilados por el Monitor de Azure?

Hay un número de datos de formas toouse hello en el registro de actividad de Hola y otros recursos de Monitor de Azure.

- Puede transmitir tooother ubicaciones de datos de hello en línea real.

- Puede almacenar datos de Hola durante periodos más largos de tiempo que los valores predeterminados de hello, con un [cuenta de almacenamiento de Azure](https://docs.microsoft.com/azure/storage/common/storage-introduction) y establecer una directiva de retención.

- Puede datos Hola visual en gráficos y gráficos, mediante hello [portal de Azure](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), o herramientas de visualización de otro fabricante.

- Puede consultar datos de hello mediante la API de REST de Monitor de Azure, comandos de CLI, hello [PowerShell](https://docs.microsoft.com/powershell/) cmdlets, u Hola .NET SDK.

tooget trabajar con el Monitor de Azure, seleccione **más servicios** Hola portal de Azure.

1. Desplácese hacia abajo demasiado**Monitor** en hello **supervisar y administrar** sección.

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  Abre el monitor en hello **registro de actividad** vista.

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

Puede crear y guardar consultas para filtros comunes y, a continuación, pin hello más importantes consultas tooa panel del portal, por lo que siempre sabrá si se han producido eventos que cumplen los criterios.

1. Puede filtrar la vista Hola por grupo de recursos, el intervalo de tiempo y la categoría de eventos.

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. A continuación, puede anclar panel del portal tooa consultas haciendo clic en hello **Pin** botón. Esto ayuda a crear un único origen de información de datos operativos de los servicios. nombre de la consulta de Hola y el número de resultados se mostrará en el panel de Hola.

También puede usar las métricas de hello Monitor tooview para todos los recursos de Azure, configurar alertas y la configuración de diagnóstico y buscar en el registro de hello. Para obtener más información sobre cómo toouse Hola Monitor de Azure y registro de actividad, vea [empezar a trabajar con el Monitor de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).

### <a name="azure-diagnostics"></a>Diagnóstico de Azure 

capacidad de diagnóstico de Hello en Azure habilita la recopilación de datos de varios orígenes. registros de eventos de Windows Hello, que incluyen el registro de seguridad de hello, pueden ser especialmente útiles en el seguimiento y documentar la protección de datos personales. registro de seguridad de Hello realiza un seguimiento de eventos correctos y erróneos de inicio de sesión, así como los cambios de permisos, la detección de patrones que indica a ciertos tipos de ataques, cambios en las directivas relacionadas con la seguridad, los cambios de pertenencia de grupo de seguridad y mucho más.

Por ejemplo, 4695 de Id. de evento de alerta unprotection del toohello intentada también de los datos protegidos auditables. Esto refiere toohello API de protección de datos (DPAPI), lo que ayuda a tooprotect datos, como las claves privadas y las credenciales almacenadas, cualquier otra información confidencial.

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>¿Cómo se habilita la extensión de diagnósticos de Hola para máquinas virtuales de Windows?

Puede usar extensión de diagnósticos de PowerShell tooenable Hola para una máquina virtual de Windows, así como los datos de registro toocollect. pasos de Hola para hacerlo dependen en qué modelo de implementación que utilice (Administrador de recursos o estándar). extensión de diagnósticos de hello tooenable en una máquina virtual existente creada mediante el modelo de implementación del Administrador de recursos de hello, puede usar hello [cmdlet de PowerShell Set-AzureRMVMDiagnosticsExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* es Hola ruta de acceso toohello archivo que contiene la configuración de diagnóstico de hello en XML. Para obtener más instrucciones sobre cómo habilitar diagnósticos de Azure en una máquina virtual, consulte [usar PowerShell tooenable diagnósticos de Azure en una máquina virtual con Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

Hola extensión de diagnósticos de Azure puede transferir la cuenta de almacenamiento de Azure de hello recopilan datos tooan o enviarlo tooservices como Application Insights. A continuación, puede usar datos de hello para la auditoría.

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>¿Cómo se pueden almacenar y ver los datos de diagnóstico?

Es importante tooremember que datos de diagnóstico no se almacenan permanentemente a menos que transfiera toohello Microsoft almacenamiento emulador o tooAzure el almacenamiento de Azure. toostore y ver datos de diagnóstico en almacenamiento de Azure, siga estos pasos:

1. Especifique una cuenta de almacenamiento en archivo ServiceConfiguration.cscfg de Hola. Servicio de Blob de Hola o servicio de tabla de hello, según tipo hello de datos, pueden usar diagnósticos de Azure. Los registros de eventos de Windows se almacenan con formato de tabla.

2. Transferencia de datos de Hola. Puede solicitar datos de diagnóstico de hello tootransfer a través del archivo de configuración de Hola. Para SDK 2.4 y anteriores, también puede realizar solicitud de hello mediante programación.

3. Ver datos de hello, con [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [Explorador de servidores](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) en Visual Studio, o [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) en Azure Management Studio.

Para obtener más información acerca de cómo tooperform de estos pasos, consulte [almacenar y ver datos de diagnóstico en almacenamiento de Azure.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Azure Storage Analytics 

Análisis de almacenamiento registra información detallada acerca del servicio de almacenamiento de tooa de solicitudes correctas e incorrectas. Esta información puede ser toomonitor usa las solicitudes individuales, que pueden ayudar a documentar toopersonal acceder a los datos almacenados en el servicio de Hola. Sin embargo, el registro de Storage Analytics no se habilita de forma predeterminada para su cuenta de almacenamiento. Puede habilitarlo en hello portal de Azure.

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>¿Cómo se puede configurar la supervisión para una cuenta de almacenamiento?

tooconfigure supervisión para una cuenta de almacenamiento, Hola siguientes:

1. Seleccione **cuentas de almacenamiento** Hola portal de Azure, seleccione Hola nombre de cuenta de hello que desea toomonitor.

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. Hola **supervisión** sección, seleccione **diagnósticos.**

3.  Seleccione hello **tipo** de datos de métricas que necesite toomonitor para cada servicio (archivo de Blob, tabla). registros de diagnósticos toosave tooinstruct de almacenamiento de Azure para lectura, escritura y eliminación de las solicitudes para hello, tabla, servicios blob y cola, seleccionan **Blob registros, registros de la tabla** y **registros de la cola.**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. Con el control deslizante de hello en parte inferior de hello, establecer hello **retención** directiva en días (valor de 1 – 365). Siete días es predeterminado de Hola.

5. Seleccione **guardar** valores de configuración de tooapply Hola.

Las entradas del registro de almacenamiento contienen Hola después de obtener información acerca de las solicitudes individuales:

- Información de tiempos como hora de inicio, latencia de un extremo a otro y latencia del servidor.

- Detalles de operación de almacenamiento de hello como tipo de operación de hello, clave de Hola de cliente de Hola de objeto de almacenamiento de hello es tener acceso, correcto o error y código de estado HTTP de hello devuelve a toohello cliente.

- Detalles de autenticación como tipo de saludo de cliente de Hola de autenticación utilizado.

- Información de simultaneidad como valor de ETag de Hola y última marca de tiempo modificada.

- tamaños de Hola de mensajes de solicitud y respuesta de saludo.

Para obtener más instrucciones sobre cómo tooenable análisis de almacenamiento de registro, consulte [supervisar una cuenta de almacenamiento en hello portal de Azure.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Azure Security Center 

[Centro de seguridad de Azure](https://azure.microsoft.com/services/security-center/) monitores Hola estado de seguridad de los recursos de Azure en orden tooprevent y detectar amenazas y se proporcionan recomendaciones para responder. Proporciona varios documentos de toohelp maneras sus medidas de seguridad que protegen Hola privacidad de los datos personales.

La supervisión del estado de seguridad le ayuda a garantizar el cumplimiento de sus directivas de seguridad. Supervisión de la seguridad es una estrategia proactiva que audita los sistemas de tooidentify de recursos que no cumplen los estándares de la organización o los procedimientos recomendados. Puede supervisar el estado de seguridad de Hola de hello recursos siguientes:

- Compute (máquinas virtuales y servicios en la nube)

- Redes (redes virtuales)

- Almacenamiento y datos (detección de amenazas y auditoría de la base de datos y el servidor, TDE y cifrado de almacenamiento)

- Aplicaciones (posibles problemas de seguridad)

Problemas de seguridad en cualquiera de estas categorías podrían plantear privacidad toohello amenaza de datos personales.

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>¿Cómo se puede ver el estado de seguridad de Hola de los recursos de Azure?

Centro de seguridad periódicamente analiza el estado de seguridad de Hola de los recursos de Azure. Puede ver las vulnerabilidades de seguridad que se identifica en hello **prevención** sección del panel de Hola.

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. Hola **prevención** sección, seleccione hello **proceso** icono. Verás un **información general,** junto con hello **máquinas virtuales** listado de todas las máquinas virtuales y sus Estados de seguridad y Hola **servicios en la nube** lista de roles web y de trabajo supervisa el centro de seguridad.

2. En hello **Introducción** ficha, la segunda una recomendación tooview obtener más información.

3. En hello **máquinas virtuales** ficha, seleccione una máquina virtual tooview obtener más detalles.

Cuando se habilita la recopilación de datos en el centro de seguridad de Azure, Hola Microsoft Monitoring Agent se aprovisiona automáticamente en todas las existentes y cualquier admitido nuevas máquinas virtuales que se implementan. Los datos que recopila este agente se almacenan en un área de trabajo de [Log Analytics](https://azure.microsoft.com/services/log-analytics/) asociada con la suscripción o en una nueva área de trabajo.

Security Center proporciona [informes de inteligencia de amenazas](https://docs.microsoft.com/azure/security-center/security-center-threat-report). Estos proporcionan información útil toohelp discernir del atacante Hola identidad, objetivos, los ataques actuales e históricos campañas y tácticas, las herramientas y procedimientos que se utilizan. También se incluye información de corrección y mitigación.

Hola principal propósito de estos informes de amenaza es toohelp se toorespond eficazmente toohello inmediata de amenazas y ayuda las medidas posteriormente problema de hello toomitigate. información de Hello en los informes de hello también puede ser útil al documentar su respuesta a incidentes para los informes y con fines de auditoría.

Informes de inteligencia sobre amenazas de Hola se presentan en. Formato PDF, tiene acceso a través de un vínculo de hello **informes** campo de hello **sospechosa proceso ejecutado** hoja para cada alerta de seguridad en el centro de seguridad de Azure.

Para obtener más información sobre cómo tooview y uso Hola informes de inteligencia de amenazas, consulte [informe de inteligencia de amenaza del centro de seguridad de Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>Pasos siguientes:

[Introducción a hello Azure Active Directory API de informes](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[¿Qué es Log Analytics?](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Información general sobre la supervisión en Microsoft Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[Introducción toohello registro de actividad de Azure (vídeo)](https://azure.microsoft.com/resources/videos/intro-activity-log/)
