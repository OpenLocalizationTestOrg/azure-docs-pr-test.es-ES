---
title: "aaaGet inició guía para desarrolladores de Azure | Documentos de Microsoft"
description: "En este tema se proporciona información esencial para los desarrolladores tooget iniciada con la plataforma de Microsoft Azure Hola para sus necesidades de desarrollo."
services: 
cloud: 
documentationcenter: 
author: ggailey777
manager: erikre
ms.assetid: 
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: glenga
ms.openlocfilehash: 72dc2678db7738923d4bc7783e297fea6fcded83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-guide-for-azure-developers"></a>Guía de introducción para desarrolladores de Azure

## <a name="what-is-azure"></a>¿Qué es Azure?

Azure es una plataforma de nube completa que puede hospedar las aplicaciones existentes, simplificar el desarrollo de Hola de nuevas aplicaciones y mejorar incluso aplicaciones locales. Azure integra servicios de nube de Hola que necesita toodevelop, probar, implementar y administrar las aplicaciones, mientras aprovecha las eficiencias de Hola de nube informática.

Con el hospedaje de las aplicaciones en Azure, puede empezar con tamaño pequeño y escalar fácilmente su aplicación a medida que aumente la demanda de los clientes. Azure también ofrece confiabilidad Hola requerido para aplicaciones de alta disponibilidad, incluso como conmutación por error entre diferentes regiones. Hola [portal de Azure](https://portal.azure.com) le permite administrar fácilmente todos los servicios de Azure. También puede administrar los servicios mediante programación, con las API y las plantillas específicas del servicio.

**A quiénes va destinada esta**: esta guía es una plataforma Windows Azure para desarrolladores de aplicaciones de toohello de introducción. Proporciona instrucciones y la dirección que necesita toostart creación de nuevas aplicaciones en Azure o migrar tooAzure de las aplicaciones existentes.

## <a name="where-do-i-start"></a>¿Por dónde empiezo?

Con todos los servicios de Hola que ofrece Azure, puede ser un toofigure tarea desalentadora qué servicios necesita toosupport su arquitectura de la solución. Este Hola de aspectos destacados de la sección Azure los servicios que suelen usar los desarrolladores. Para obtener una lista de todos los servicios de Azure, vea hello [documentación de Azure](../../index.md).

En primer lugar, debe decidir cómo toohost su aplicación en Azure. ¿Necesita toomanage toda la infraestructura como una máquina virtual (VM). ¿Puede usar funciones de administración de plataforma de Hola que proporciona Azure? ¿Tal vez necesite solo una ejecución de código de toohost de framework sin servidor?

Su aplicación necesita almacenamiento en la nube, para lo cual Azure ofrece varias opciones. Puede aprovechar las ventajas de la autenticación empresarial de Azure. También hay herramientas de desarrollo y supervisión basadas en la nube, y la mayoría de servicios de hospedaje ofrece integración con DevOps.

Ahora, echemos un vistazo a algunos de los servicios específicos de Hola que se recomienda investigar para sus aplicaciones.

### <a name="application-hosting"></a>Hospedaje de aplicaciones

Azure proporciona varias toorun de ofertas de proceso basada en la nube a la aplicación para que no tengan tooworry acerca de los detalles de la infraestructura de Hola. Puede escalar fácilmente los recursos vertical u horizontalmente a medida que aumente el uso de la aplicación.

Azure ofrece servicios para sus necesidades de desarrollo y hospedaje de aplicaciones. Azure proporciona la infraestructura como-servicio (IaaS) toogive pleno control sobre el hospedaje de aplicaciones. Las ofertas de plataforma como servicio (PaaS) de Azure proporcionan Hola totalmente administrados servicios necesarios toopower sus aplicaciones. Hay incluso true sin servidor de hospedaje en Azure donde todo lo que necesita toodo es escribir su código.

![Opciones de hospedaje de aplicaciones en Azure](./media/azure-developer-guide/azure-developer-hosting-options.png)


#### <a name="azure-app-service"></a>Servicio de aplicaciones de Azure 

Cuando desee hello toopublish de ruta de acceso más rápida en los proyectos basados en web, considere la posibilidad de servicio de aplicaciones de Azure. Servicio de aplicaciones resulta fácil tooextend su web toosupport de aplicaciones en los clientes móviles y publicar fácil las API de REST. Esta plataforma proporciona autenticación mediante el uso de proveedores de redes sociales, autoescala basada en el tráfico, pruebas en producción e implementaciones de contenedor y continuas.

Cuando se crea una aplicación de servicio de aplicaciones, seleccione uno de los siguientes tipos de hello:

- [Web Apps](../../app-service-web/app-service-web-overview.md):  permite hospedar sitios web y aplicaciones web escritas en .NET, Java, PHP, Node.js y Python.

- [Aplicaciones móviles](../../app-service-mobile/app-service-mobile-value-prop.md): acceso de toosupport extiende las aplicaciones Web desde dispositivos móviles. Habilita la autenticación con proveedores de redes sociales y Azure Active Directory (Azure AD), proporciona almacenamiento back-end y se integra con [Azure Notification Hubs](../../notification-hubs/notification-hubs-push-notification-overview.md) para las notificaciones push.

- [Aplicaciones de API](../../app-service-api/app-service-api-apps-why-best-platform.md): permite más segura exponer las API en la nube de hello con metadatos de Swagger para que los clientes pueden utilizar fácilmente.

Dado que comparten todos los tipos de aplicación de tres Hola en tiempo de ejecución de servicio de aplicaciones, puede hospedar un sitio Web, compatibilidad con clientes móviles y exponer las API en Azure, todo ello desde Hola mismo proyecto o solución. toolearn más información acerca del servicio de aplicaciones, consulte [aplicación de servicio de funcionamiento](../../app-service/app-service-how-works-readme.md).

App Service se ha diseñado teniendo en cuenta DevOps. Admite varias herramientas de publicación e implementaciones de integración continuas, incluidos webhooks de GitHub, Jenkins, Visual Studio Team Services o TeamCity, entre otros.

Puede migrar su tooApp existente de aplicaciones servicio mediante hello [herramienta de migración en línea](https://www.migratetoazure.net/).

>**Cuando toouse**: usar el servicio de aplicación cuando migra tooAzure de las aplicaciones web existentes, y cuando necesite una plataforma de hospedaje completamente administrada para las aplicaciones web. También puede utilizar el servicio de aplicaciones cuando necesite a clientes móviles toosupport o exponer las API de REST con la aplicación.

>**Introducción**: servicio de aplicaciones resulta fácil toocreate e implementar su primer [aplicación web](../../app-service-web/web-sites-dotnet-get-started.md), [aplicación móvil](../../app-service-mobile/app-service-mobile-ios-get-started.md), o [aplicación de API de](../../app-service-api/app-service-api-dotnet-get-started.md).

>**Pruébelo ahora**: servicio de aplicaciones le permite aprovisionar una plataforma de aplicación de corta duración tootry Hola sin necesidad de toosign hacia arriba para una cuenta de Azure. Pruebe la plataforma de Hola y [crear la aplicación de servicio de aplicaciones de Azure](https://tryappservice.azure.com/).

#### <a name="azure-virtual-machines"></a>Máquinas virtuales de Azure

Como proveedor de infraestructura como-servicio (IaaS), Azure le permite implementar tooor migrar su tooeither de aplicación Windows o máquinas virtuales de Linux. Junto con red Virtual de Azure, máquinas virtuales de Azure admite la implementación de Hola de tooAzure Windows o máquinas virtuales de Linux. Con las máquinas virtuales, tiene control total sobre la configuración de Hola de máquina de Hola. Al usar las máquinas virtuales, es responsabilidad suya la instalación, la configuración y el mantenimiento del software del servidor, así como las revisiones del sistema operativo.

Debido a nivel de Hola de control que tiene con máquinas virtuales, puede ejecutar una amplia variedad de cargas de trabajo de servidor en Azure que no se ajustan en un modelo de PaaS. Estas cargas de trabajo incluyen servidores de base de datos, Windows Server Active Directory y Microsoft SharePoint. Para obtener más información, consulte la documentación de máquinas virtuales de Hola para cualquiera [Linux](/azure/virtual-machines/linux/) o [Windows](/azure/virtual-machines/windows/).

>**Cuando toouse**: usan de máquinas virtuales cuando desee full control sobre su aplicación toomigrate o infraestructura locales aplicación las cargas de trabajo tooAzure sin necesidad de cambios de toomake.

>**Introducción**: crear un [VM de Linux](../../virtual-machines/virtual-machines-linux-quick-create-portal.md) o [VM de Windows](../../virtual-machines/virtual-machines-windows-hero-tutorial.md) de hello portal de Azure.

#### <a name="azure-functions-serverless"></a>Azure Functions (sin servidor)

En lugar de preocuparse de crear y administrar un toorun de infraestructura de aplicación o hello todo el código. ¿Qué ocurre si simplemente podría escribir el código y hacer que se ejecute en respuesta tooevents o según una programación?  [Las funciones de Azure](../../azure-functions/functions-overview.md) es un "sin servidor"-estilo de oferta que permite escribir simplemente Hola código que necesita. Con Functions, la ejecución del código se desencadena mediante solicitudes HTTP, webhooks, eventos de servicios en la nube o según una programación. El desarrollo se puede realizar en el lenguaje que se prefiera, como C\#, F\#, Node.js, Python o PHP. Con la facturación basada en el consumo, solo paga por tiempo de presentación que se ejecuta el código y Azure escala según sea necesario.

>**Cuando toouse**: utilizar funciones de Azure cuando tiene código que se desencadena por otros servicios de Azure, por eventos basados en web, o según una programación. También puede utilizar funciones cuando no necesita Hola sobrecarga de un proyecto completo hospedado o que solo desee toopay para tiempo de presentación que se ejecuta el código. más información, consulte toolearn [información general de las funciones de Azure](../../azure-functions/functions-overview.md).

>**Introducción**: siga el tutorial de inicio rápido de las funciones hello demasiado[crear la primera función](../../azure-functions/functions-create-first-azure-function.md) desde el portal de Hola.

>**Pruébelo ahora**: funciones de Azure permite ejecutar el código sin necesidad de toosign hacia arriba para una cuenta de Azure. Pruébelo ahora y [cree su primera función de Azure](https://tryappservice.azure.com/).

#### <a name="azure-service-fabric"></a>Azure Service Fabric

Azure Service Fabric es una plataforma de sistemas distribuidos que resulta fácil toobuild, empaquetar, implementar y administrar microservicios escalables y confiables. También proporciona capacidades de administración de aplicaciones completas para el aprovisionamiento, la implementación, la supervisión, la actualización/aplicación de revisiones y eliminación de aplicaciones implementadas. Las aplicaciones, que se ejecutan en un grupo compartido de máquinas, pueden empezar siendo pequeñas y escalar toohundreds o miles de equipos según sea necesario.

Service Fabric admite WebAPI con Open Web Interface para .NET (OWIN) y ASP.NET Core. Ofrece varios SDK para compilar servicios en Linux tanto en .NET Core como Java. toolearn más información acerca de Service Fabric, vea hello [ruta de acceso de aprendizaje de Service Fabric](https://azure.microsoft.com/documentation/learning-paths/service-fabric/).

>**Cuando toouse:** Service Fabric es una buena elección cuando está creando una aplicación o volver a escribir un toouse existente de la aplicación una arquitectura de microservicio. Usar a Service Fabric si necesita más control sobre o acceso directo a la infraestructura subyacente de Hola.

>**Para empezar:**[cree su primera aplicación de Azure Service Fabric](../../service-fabric/service-fabric-create-your-first-application-in-visual-studio.md).

### <a name="enhance-your-applications-with-azure-services"></a>Mejore sus aplicaciones con los servicios de Azure

Además tooapplication hospedaje, Azure proporciona las ofertas de servicio que pueden mejorar la funcionalidad de hello, el desarrollo y mantenimiento de las aplicaciones, tanto en la nube de Hola y local.

#### <a name="hosted-storage-and-data-access"></a>Acceso de datos y almacenamiento hospedado

Mayoría de las aplicaciones debe almacenar los datos, por lo que independientemente de cómo decidir toohost su aplicación en Azure, considere la posibilidad de uno o varios de hello después de servicios de almacenamiento y los datos.

-   **La base de datos de SQL Azure**: versión basada en Azure Hola Microsoft motor de SQL Server para almacenar datos tabulares relacional en la nube de Hola. SQL Database ofrece un rendimiento predecible, escalabilidad sin tiempo de inactividad, continuidad empresarial y protección de datos.

    >**Cuando toouse**: cuando la aplicación requiera almacenamiento de datos con la integridad referencial, compatibilidad transaccional y soporte técnico para las consultas TSQL.

    >**Introducción**: [crear una base de datos SQL en minutos mediante Hola portal de Azure](../../sql-database/sql-database-get-started.md).

-   **Azure Storage**: ofrece un almacenamiento duradero y de alta disponibilidad para blobs, colas, archivos y otros tipos de datos no relacionales. Almacenamiento de información proporciona la base de almacenamiento de Hola para máquinas virtuales.

    >**Cuando toouse**: cuando la aplicación almacena datos no relacionales, como pares de clave-valor (tablas), los blobs, recursos compartidos de archivos o mensajes de (colas).

    >**Para empezar**: elija uno de estos tipos de almacenamiento: [blobs](../../storage/blobs/storage-dotnet-how-to-use-blobs.md), [tablas](../../cosmos-db/table-storage-how-to-use-dotnet.md), [colas](../../storage/queues/storage-dotnet-how-to-use-queues.md) o [archivos](../../storage/files/storage-dotnet-how-to-use-files.md).

-   **Azure DocumentDB**: un servicio de base de datos NoSQL totalmente administrado y escalable, que incluye consultas SQL a datos de objeto. Para acceder a DocumentDB puede usar los controladores de MongoDB existentes.
    >**Cuando toouse:** cuando la aplicación necesite consultas SQL puede tooexecute toobe en documentos JSON, o si usa MongoDB.

    >**Para empezar**: [cree una aplicación de consola de C# para DocumentDB](../../documentdb/documentdb-get-started.md). Si es un desarrollador de MongoDB, consulte el artículo sobre la [compatibilidad del protocolo DocumentDB para MongoDB](../../documentdb/documentdb-protocol-mongodb.md).

Puede usar [Data Factory de Azure](../../data-factory/data-factory-introduction.md) toomove locales existentes tooAzure de datos. Si no estás listo toomove datos toohello en la nube, [conexiones híbridas](../../biztalk-services/integration-hybrid-connection-overview.md) en servicios de BizTalk le permite conectarse su servicio en la aplicación hospeda recursos tooon local de la aplicación. También puede conectar los servicios de datos y almacenamiento de tooAzure procedentes de aplicaciones local.

#### <a name="docker-support"></a>Compatibilidad con Docker

Los contenedores de Docker, una forma de virtualización del sistema operativo, le permiten implementar aplicaciones de forma más eficaz y predecible. Una aplicación en contenedores funciona en Hola de producción igual manera que en los sistemas de desarrollo y pruebas. Puede administrar los contenedores mediante las herramientas estándar de Docker. Puede utilizar sus conocimientos y herramientas de código abierto populares toodeploy y administrar aplicaciones basadas en el contenedor en Azure.

Azure proporciona varias maneras de contenedores de toouse en sus aplicaciones.

-   **Extensión de máquina virtual Docker Azure**: le permite configurar la máquina virtual con tooact de herramientas de Docker como un host Docker.

    >**Cuando toouse**: si desea que las implementaciones de toogenerate contenedor coherente para las aplicaciones en una máquina virtual, o cuando desee toouse [Docker Compose](https://docs.docker.com/compose/overview/).

    >**Introducción**: [crear un entorno de Docker en Azure con la extensión de máquina virtual Docker hello](../../virtual-machines/virtual-machines-linux-dockerextension.md).

-   **Servicio de contenedor de Azure**: permite crear, configurar y administrar un clúster de máquinas virtuales que están preconfigurados aplicaciones toorun en contenedores. toolearn más información acerca del servicio de contenedor, consulte [introducción de servicio de contenedor de Azure](../../container-service/container-service-intro.md).

    >**Cuando toouse**: si necesita toobuild para entornos de producción entornos escalables que proporcionan herramientas de programación y administración adicionales o si va a implementar un clúster de Docker Swarm.

    >**Para empezar**: [implemente un clúster de Container Service](../../container-service/dcos-swarm/container-service-deployment.md).

-   **Docker Machine**: permite instalar y administrar un motor de Docker en hosts virtuales mediante comandos de docker-machine.

    >**Cuando toouse**: cuando necesite tooquickly prototipo una aplicación mediante la creación de un único host de Docker.

-   **Imagen de Docker personalizada para App Service**: permite usar contenedores de Docker desde un registro de contenedor o un contenedor de cliente al implementar una aplicación web en Linux.

    >**Cuando toouse**: al implementar una aplicación web en la imagen de Docker de tooa de Linux.

    >**Para empezar**: [use una imagen de Docker personalizada para App Service en Linux](../../app-service-web/app-service-linux-using-custom-docker-image.md).

### <a name="authentication"></a>Autenticación

Su toonot fundamental solo saber quién está utilizando sus aplicaciones, pero también tooprevent no autorizado tener acceso a recursos de tooyour. Azure proporciona tooauthenticate de varias maneras de los clientes de la aplicación.

-   **Azure Active Directory (Azure AD)**: Hola para varios inquilinos basada en la nube, identidad y acceso servicio Administración de Microsoft. Puede agregar el inicio de sesión único en aplicaciones de tooyour (SSO) mediante la integración con Azure AD. Puede obtener acceso a propiedades de directorio mediante el uso de hello Azure AD Graph API directamente o hello API Graph de Microsoft. Puede integrar con soporte técnico de Azure AD para el marco de autorización de OAuth2.0 de Hola y conéctese de identificador abierto mediante el uso de puntos de conexión HTTP/REST nativo y Hola bibliotecas de autenticación de Azure AD multiplataforma.

    >**Cuando toouse**: si desea tooprovide una experiencia SSO, trabajar con datos basados en el gráfico o autenticar a los usuarios basados en dominio.

    >**Introducción**: toolearn más información, vea hello [Guía del desarrollador de Azure Active Directory](../../active-directory/active-directory-developers-guide.md).

-   **Autenticación del servicio de aplicación**: Si elige toohost de servicio de aplicaciones de la aplicación, también obtendrá compatibilidad con la autenticación integrada para Azure AD, junto con proveedores de identidades sociales, como Facebook, Google, Microsoft y Twitter.

    >**Cuando toouse**: si desea tooenable la autenticación en una aplicación de servicio de aplicaciones con Azure AD, proveedores de identidades sociales, o ambos.

    >**Introducción**: toolearn más información acerca de la autenticación en el servicio de aplicaciones, consulte [autenticación y autorización en el servicio de aplicación de Azure](../../app-service/app-service-authentication-overview.md).

toolearn más información acerca de prácticas recomendadas de seguridad en Azure, consulte [patrones y prácticas recomendadas de seguridad de Azure](../../security/security-best-practices-and-patterns.md).

### <a name="monitoring"></a>Supervisión

Con la aplicación funcionando en Azure, debe toobe toomonitor capaz de rendimiento, controlar problemas y ver cómo los clientes usan la aplicación. Azure ofrece varias opciones de supervisión.

-   **Visual Studio Application Insights**: servicio de análisis extensible hospedados en Azure que se integra con Visual Studio toomonitor sus aplicaciones web en vivo. Proporciona datos de Hola que necesita toocontinuously mejoran el rendimiento de Hola y facilidad de uso de las aplicaciones, si está hospedados en Azure o no.

    >**Introducción**: Hola de seguimiento [tutorial de Application Insights](../../application-insights/app-insights-overview.md).

-   **Monitor de Azure**: un servicio que le ayuda a toovisualize, consulta, route, archivar y actúan en los registros generados por la infraestructura de Azure y los recursos y las métricas de Hola. El Monitor proporciona vistas de datos de Hola que se produzcan en hello portal de Azure y es un único origen para la supervisión de recursos de Azure.
 
    >**Para empezar**: [introducción a Azure Monitor](../../monitoring-and-diagnostics/monitoring-get-started.md).

### <a name="devops-integration"></a>Integración con DevOps

El aprovisionamiento de máquinas virtuales o publicar sus aplicaciones web con la integración continua, Azure se integra con la mayoría de las herramientas de DevOps populares Hola. Con compatibilidad con herramientas como Jenkins, GitHub, Puppet, Chef, TeamCity, Ansible, VSTS y otras personas, puede trabajar con las herramientas de Hola que ya tiene y maximizar su experiencia existente.

>**Pruébelo ahora:** [probar varias integraciones de DevOps de hello](https://azure.microsoft.com/try/devops/).

>**Introducción**: toosee DevOps opciones para una aplicación de servicio de aplicaciones, consulte [tooAzure servicio de aplicaciones de la implementación continua](../../app-service-web/app-service-continuous-deployment.md).


## <a name="azure-regions"></a>Regiones de Azure

Azure es una plataforma de nube global que está disponible con carácter general en muchas regiones alrededor de Hola a todos. Al aprovisionar un servicio, una aplicación o una máquina virtual de Azure, son más frecuentes tooselect una región, que representa un centro de datos específico que se ejecuta la aplicación o donde se almacenan los datos. Estas regiones corresponden toospecific ubicaciones, que se publican en hello [regiones de Azure](https://azure.microsoft.com/regions/) página.

### <a name="choose-hello-best-region-for-your-application-and-data"></a>Elija Hola región recomendado para la aplicación y los datos

Una de las ventajas de Hola de uso de Azure es que puede implementar sus centros de datos de aplicaciones toovarious mundo Hola. región de Hola que elija puede afectar al rendimiento de saludo de la aplicación. Por ejemplo, es mejor toochoose una región que sea toomost más cerca de la latencia de tooreduce de clientes en las solicitudes de red. Puede que le interese tooselect los requisitos legales de región toomeet Hola para distribuir la aplicación en determinados países. Siempre es una mejor práctica toostore aplicación de datos en el mismo centro de datos de Hola o en un centro de datos lo más cerca posible toohello centro de datos que hospeda la aplicación.

### <a name="multi-region-apps"></a>Aplicaciones para varias regiones

Aunque es improbable, no es imposible que un toogo todo centro de datos sin conexión debido a un evento como un error de Internet o un desastre natural. Es una mejor práctica toohost vitales para el negocio las aplicaciones en más de un centro de datos de disponibilidad máxima tooprovide. El uso de varias regiones también reduce la latencia para los usuarios globales y ofrece más flexibilidad a la hora de actualizar las aplicaciones.

Algunos servicios, como máquinas virtuales y servicios de aplicaciones, usan [Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md) compatibilidad con varias regiones de tooenable con conmutación por error entre las aplicaciones empresariales de alta disponibilidad de las regiones toosupport. Para ver un ejemplo, consulte [Arquitectura de referencia de Azure: aplicación web con alta disponibilidad](../../guidance/guidance-web-apps-multi-region.md).

>**Cuando toouse**: si tiene aplicaciones de enterprise y alta disponibilidad que se benefician de conmutación por error y la replicación.

## <a name="how-do-i-manage-my-applications-and-projects"></a>¿Cómo administro mis aplicaciones y proyectos?

Azure proporciona un amplio conjunto de experiencias de toocreate y administrar recursos de Azure, las aplicaciones y los proyectos tanto mediante programación en hello [portal de Azure](https://portal.azure.com/).

### <a name="command-line-interfaces-and-powershell"></a>Interfaces de línea de comandos y PowerShell

Azure proporciona toomanage de dos maneras las aplicaciones y servicios desde la línea de comandos de hello mediante intensiva de errores, Terminal, símbolo de Hola o la herramienta de línea de comandos de elección. Por lo general, puede realizar Hola mismo tareas desde línea de comandos de hello en hello portal de Azure, como la creación y configuración de máquinas virtuales, redes virtuales, las aplicaciones web y otros servicios.

-   [Interfaz de línea de comandos (CLI de Azure)](../../xplat-cli-install.md): le permite conectarse tooan suscripción de Azure y programar varias tareas con recursos de Azure desde la línea de comandos de Hola.

-   [Azure PowerShell](../../powershell-install-configure.md): proporciona un conjunto de módulos con los cmdlets que permiten toomanage Azure recursos mediante Windows PowerShell.

### <a name="azure-portal"></a>Azure Portal

Hola portal de Azure es una aplicación basada en web que puede usar toocreate, administrar y quite los servicios y recursos de Azure. Hello portal de Azure se encuentra en <https://portal.azure.com>. Incluye un panel personalizable, herramientas para administrar recursos de Azure y la configuración de toosubscription de acceso y la información de facturación. Para obtener más información, vea hello [información general del portal Azure](../../azure-portal-overview.md).

### <a name="rest-apis"></a>API de REST

Azure se basa en un conjunto de API de REST que admiten Hola UI del portal de Azure. La mayoría de estas API de REST es también compatible toolet aprovisionar y administrar sus recursos de Azure y aplicaciones desde cualquier dispositivo acceso a Internet mediante programación. Para el conjunto completo de Hola de documentación de la API de REST, vea hello [referencia de SDK de REST de Azure](https://docs.microsoft.com/rest/api/).

### <a name="apis"></a>API existentes

Además tooREST API, muchos servicios de Azure también le permiten administrar mediante programación los recursos de las aplicaciones con específica de la plataforma Azure SDK, incluido el SDK para hello después de plataformas de desarrollo:

-   [.NET](https://go.microsoft.com/fwlink/?linkid=834925)
-   [Node.js](http://azure.github.io/azure-sdk-for-node/)
-   [Java](https://docs.microsoft.com/java/api/)
-   [PHP](https://github.com/Azure/azure-sdk-for-php/blob/master/README.md)
-   [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/)
-   [Ruby](https://github.com/Azure/azure-sdk-for-ruby/blob/master/README.md)

Servicios como [aplicaciones móviles](../../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md) y [servicios multimedia de Azure](../../media-services/media-services-dotnet-how-to-use.md) proporcionar toolet del SDK de cliente tener acceso a los servicios de aplicaciones de cliente móviles y web.

### <a name="azure-resource-manager"></a>Administrador de recursos de Azure 
    
Ejecuta la aplicación en Azure es probable que implica trabajar con varios servicios de Azure, todos de que siguen a Hola vida mismo ciclo y puede considerarse como una unidad lógica. Por ejemplo, una aplicación web podría usar los servicios Web Apps, SQL Database, Storage, Azure Redis Cache y Azure Content Delivery Network. [El Administrador de recursos Azure](../../azure-resource-manager/resource-group-overview.md) permite trabajar con recursos de hello en la aplicación como un grupo. Puede implementar, actualizar o eliminar todos los recursos de hello en una única operación coordinada.

Además en que toologically agrupar y administrar los recursos relacionados, Azure Resource Manager incluye capacidades de implementación que le permiten personalizar la implementación de Hola y la configuración de recursos relacionados. Por ejemplo, con Resource Manager puede implementar y configurar una aplicación que consta de varias máquinas virtuales, un equilibrador de carga y una instancia de Azure SQL Database como una sola unidad.

Estas implementaciones se desarrollan usando una plantilla de Azure Resource Manager, que es un documento con formato JSON. Las plantillas permiten definir una implementación y administrar las aplicaciones mediante plantillas declarativas en lugar de scripts. Las plantillas pueden funcionar en diferentes entornos, como pruebas, almacenamiento provisional y producción. Por ejemplo, mediante el uso de plantillas, puede agregar un repositorio de GitHub de tooa de botón que se puede implementar código de hello en hello repositorio tooa formado por los servicios de Azure con un solo clic.

>**Cuando toouse**: Use el Administrador de recursos plantillas cuando desee que una implementación basada en la plantilla de la aplicación que se puede administrar mediante programación con las API de REST, Hola CLI de Azure y Azure PowerShell.

>**Introducción**: tooget iniciado mediante plantillas, consulte [plantillas del Administrador de recursos de Azure de creación](../../resource-group-authoring-templates.md).

## <a name="understanding-accounts-subscriptions-and-billing"></a>Descripción de las cuentas, suscripciones y facturación

Como los desarrolladores, nos gustan toodive directamente en código de hello y se pruebe tooget iniciado tan rápido como sea posible con la realización de nuestras aplicaciones ejecutar. Por supuesto, queremos tooencourage toostart trabajando en Azure tan fácilmente como sea posible. toohelp que sea fácil, Azure ofrece un [evaluación gratuita](https://azure.microsoft.com/free/). Algunos servicios incluso tienen una funcionalidad "Pruébelo gratis", como [servicio de aplicaciones de Azure](https://tryappservice.azure.com/), que no requiere demasiado incluso crear una cuenta. Como diversión sea toodive en codificar e implementar su tooAzure de la aplicación, también es importante tootake algunos toounderstand tiempo funcionamiento de Azure desde la perspectiva de las cuentas de usuario, las suscripciones y facturación.

### <a name="what-is-an-azure-account"></a>¿Qué es una cuenta de Azure?

toobe puede toocreate o trabajar con una suscripción de Azure, debe tener una cuenta de Azure. Una cuenta de Azure es simplemente una identidad en Azure AD o en un directorio, por ejemplo, una organización profesional o académica, que sea de confianza para Azure AD. Si no pertenece toosuch una organización, siempre puede crear una suscripción mediante su Account Microsoft, que es de confianza para Azure AD. toolearn más información acerca de la integración local de Windows Server Active Directory con Azure AD, consulte [integrar las identidades locales con Azure Active Directory](../../active-directory/active-directory-aadconnect.md).

Cada suscripción de Azure tiene una relación de confianza con una instancia de Azure AD. Esto significa que confía en ese directorio tooauthenticate usuarios, servicios y dispositivos. Varias suscripciones pueden confiar Hola mismo directorio, pero una suscripción confía en un único directorio. más información, consulte toolearn [suscripciones de Azure están asociadas con Azure Active Directory](../../active-directory/active-directory-how-subscriptions-associated-directory.md).

Además toodefining identidades de cuenta de Azure individuales, también denominada *usuarios*, también puede definir *grupos* en Azure AD. Crear grupos de usuarios es un tooresources de acceso de toomanage buena forma de una suscripción mediante el uso de control de acceso basado en roles (RBAC). toolearn toocreate grupos, vea [crear un grupo en la vista previa de Azure Active Directory](../../active-directory/active-directory-groups-create-azure-portal.md). También puede crear y administrar grupos [con PowerShell](../../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

### <a name="manage-your-subscriptions"></a>Administración de suscripciones

Una suscripción es una unidad lógica de servicios de Azure que está vinculado tooan cuenta de Azure. Cada cuenta asociada tiene un rol en una suscripción. La facturación de los servicios de Azure se realiza por suscripción. Para obtener una lista de ofertas de suscripción disponibles Hola por tipo, consulte [Microsoft Azure ofrecen detalles](https://azure.microsoft.com/support/legal/offer-details/).

#### <a name="administrator-roles"></a>Roles de administrador

Una suscripción de Azure tiene varios roles de administrador de cuenta, que puede asignar en cualquier momento.

-   **Administrador de la cuenta**: este rol tiene control total sobre la suscripción de Hola y es cuenta Hola que se encarga de facturación.

-   **Administrador de servicios**: este rol tiene control sobre todos los servicios de hello en la suscripción de Hola. De forma predeterminada, esto es hello misma cuenta como Hola Administrador de la cuenta.

-   **Coadministrador**: este rol tiene Hola mismo acceso como Hola Administrador de servicios, excepto en que no se puede cambiar la asociación de Hola de hello suscripción tooan directorio de Azure.

toolearn más información acerca de los roles de administrador, consulte [cómo tooadd o cambiar roles de administrador de Azure](../../billing/billing-add-change-azure-subscription-administrator.md#add-an-admin-for-a-subscription).

#### <a name="resource-groups"></a>Grupos de recursos

Al aprovisionar nuevos servicios de Azure, puede hacerlo en una suscripción determinada. Servicios individuales de Azure, que también se llaman a los recursos, se crean en el contexto de Hola de un grupo de recursos. Grupos de recursos que sea más fácil toodeploy y administración recursos de la aplicación. Un grupo de recursos debe contener todos los recursos de hello para la aplicación que desee toowork con como una unidad. Puede mover recursos entre grupos de recursos e incluso toodifferent suscripciones. toolearn acerca de cómo mover recursos, vea [Mover grupo de recursos de toonew de recursos o suscripción](../../resource-group-move-resources.md).

Hola Explorador de recursos de Azure es una herramienta excelente para visualizar los recursos de Hola que ya ha creado en su suscripción. más información, consulte toolearn [tooview utilice el Explorador de recursos de Azure y modificar recursos](../../resource-manager-resource-explorer.md).

#### <a name="grant-access-tooresources"></a>Conceder acceso tooresources

Al permitir el acceso a recursos tooAzure, siempre es una práctica recomendada para proporcionar a los usuarios con hello privilegios tooperform requiere que una tarea determinada.

-   **Control de acceso basado en roles (RBAC)**: en Azure, puede conceder acceso a las cuentas de toouser (entidades) en un ámbito especificado: suscripción, grupo de recursos o los recursos individuales. RBAC le permite implementar un conjunto de recursos en un grupo de recursos y conceder permisos tooa usuario o grupo específico. También le permiten limitar el acceso a los recursos de Hola de tooonly que pertenecen el grupo de recursos de destino de toohello. También puede conceder acceso tooa único recurso, por ejemplo, una máquina virtual o una red virtual. acceso de toogrant, asignar un usuario de toohello de rol, grupo o entidad de servicio. Hay muchos roles predefinidos y puede definir también sus propios roles personalizados.

    >**Cuando toouse**: cuando se necesitan la administración de acceso específico para usuarios y grupos.

    >**Introducción**: más información, consulte toolearn [comenzar con la administración de acceso de hello portal de Azure](../../active-directory/role-based-access-control-what-is.md).

-   **Objetos de entidad de seguridad de servicio**: además tooproviding tener acceso a las entidades de seguridad toouser y grupos, puede conceder Hola misma entidad de servicio de acceso tooa.

    > **Cuando toouse**: cuando es la administración de recursos de Azure o conceder acceso a las aplicaciones mediante programación. Para más información, consulte [Uso del portal para crear una aplicación de Azure Active Directory y una entidad de servicio con acceso a los recursos](../../resource-group-create-service-principal-portal.md).

#### <a name="tags"></a>Etiquetas

Administrador de recursos de Azure le permite asignar etiquetas personalizadas tooindividual recursos. Etiquetas, que son pares de clave y valor, pueden resultar útiles cuando se necesitan recursos tooorganize de supervisión o de facturación. Las etiquetas proporcionan un tootrack los recursos de manera a través de varios grupos de recursos. Puede asignar las etiquetas en el portal de hello, en la plantilla de Azure Resource Manager Hola o mediante programación, mediante el uso de API de REST de hello, hello Azure CLI o PowerShell. Puede asignar varias etiquetas tooeach recursos. más información, consulte toolearn [mediante etiquetas tooorganize los recursos de Azure](../../resource-group-using-tags.md).

### <a name="billing"></a>Facturación

En movimiento Hola desde servicios hospedados en toocloud informáticos en local, seguimiento y calcular el uso del servicio y los costos relacionados son problemas importantes. Es importante toobe puede tooestimate qué nuevos recursos costos toorun mensualmente. También debe toobe tooproject capaz de aspecto de facturación de Hola durante un mes determinado en función de gasto actual de Hola.

#### <a name="get-resource-usage-data"></a>Obtención de datos de uso de recursos

Azure proporciona un conjunto de API de REST de facturación que proporcione acceso tooresource consumo y la información de metadatos para las suscripciones de Azure. Estos ofrecen las API de facturación Hola capacidad toobetter predecir y administrar los costos de Azure. Puede realizar un seguimiento y analizar el gasto en incrementos de una hora, crear alertas de gastos y predecir la facturación futura en función de las tendencias de uso actuales.

>**Introducción**: toolearn más sobre el uso de hello las API de facturación, consulte [información general sobre el uso de facturación de Azure y RateCard APIs](../../billing-usage-rate-card-overview.md).

#### <a name="predict-future-costs"></a>Predicción de los costos futuros

Aunque resulta difícil tooestimate costos antelación, Azure tiene un [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/) que puede utilizar cuando se calculan el costo de Hola de implementa recursos. También puede usar la hoja de facturación de hello en el portal de Hola y Hola las API de REST de facturación tooestimate costos futuros, en función del consumo actual.

>**Introducción**: consulte [introducción a las API de Billing Usage y RateCard de Azure](../../billing-usage-rate-card-overview.md).

#### <a name="set-up-billing-alerts"></a>Configurar alertas de facturación para las suscripciones de Microsoft Azure

Después de implementar su aplicación o solución en Azure, puede crear alertas que le envíen que correos electrónicos al enfoque Hola los límites que se definen en la alerta de Hola de gastos.

>**Introducción**: más información, consulte toolearn [configurar alertas para las suscripciones de Microsoft Azure de facturación](../../billing-set-up-alerts.md).
