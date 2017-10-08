---
title: "aaaAzure comparación de servicio de aplicaciones, máquinas virtuales, Service Fabric y servicios en la nube | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toochoose entre el servicio de aplicaciones de Azure, máquinas virtuales, Service Fabric y servicios en la nube para hospedar aplicaciones de web."
services: app-service\web, virtual-machines, cloud-services
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 7d346a23-532a-42a9-98a8-23b7286d32a8
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 07/07/2016
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7577332ed049df66178c7b2cd5c440a7f93a7865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-virtual-machines-service-fabric-and-cloud-services-comparison"></a>Comparación de Servicio de aplicaciones de Azure, Máquinas virtuales, Service Fabric y Servicios en la nube
## <a name="overview"></a>Información general
Azure ofrece varias maneras de sitios web de toohost: [servicio de aplicaciones de Azure][Azure App Service], [máquinas virtuales][Virtual Machines], [Service Fabric ] [ Service Fabric], y [servicios en la nube][Cloud Services]. En este artículo le ayuda a entender las opciones de Hola y tomar Hola la decisión correcta para la aplicación web.

Servicio de aplicaciones de Azure es Hola mejor opción para la mayoría de las aplicaciones web. Implementación y administración se integran en la plataforma de hello, sitios pueden escalar rápidamente toohandle grandes cargas de tráfico y Administrador de tráfico y equilibrio de carga integrados Hola proporcionar una alta disponibilidad. Puede mover existente sitios tooAzure servicio de aplicaciones fácilmente con un [herramienta de migración en línea](https://www.migratetoazure.net/), usar una aplicación de código abierto de hello Web Application Gallery o crear un sitio nuevo con el framework de Hola y herramientas de generación de su elección. Hola [WebJobs] [ WebJobs] característica hace fácil tooadd fondo trabajo procesamiento tooyour aplicación de servicio de aplicaciones web.

Service Fabric es una buena opción si va a crear una nueva aplicación o volver a escribir una aplicación existente toouse una arquitectura de microservicio. Las aplicaciones, que se ejecutan en un grupo compartido de máquinas, pueden empezar siendo pequeñas y crecer toomassive escala con cientos o miles de equipos según sea necesario. Servicios con estado hace más fácil tooconsistently y almacenan el estado de aplicación de forma confiable y Service Fabric administra automáticamente la partición de servicio, la escala y la disponibilidad en su nombre.  Service Fabric también admite WebAPI con Open Web Interface para .NET (OWIN) y ASP.NET Core.  TooApp comparado servicio, Service Fabric también proporciona más control sobre o acceso directo a la infraestructura subyacente de Hola. Puede acceder de forma remota a los servidores o configurar las tareas de inicio de los servidores. Servicios en la nube es tooService similar tejido en el grado de control y facilidad de uso, pero ahora es un servicio heredado y Service Fabric se recomienda para nuevo desarrollo.

Si tiene una aplicación existente que requeriría toorun modificaciones sustanciales en el servicio de aplicaciones o del tejido de servicio, puede elegir las máquinas virtuales en toosimplify orden migrar toohello en la nube. Sin embargo, configurar correctamente, proteger y mantener las máquinas virtuales requieren mucho más tiempo y experiencia en TI compara tooAzure servicio de aplicaciones y el tejido de servicio. Si está pensando en máquinas virtuales de Azure, asegúrese de tener en cuenta Hola mantenimiento continuado esfuerzo requerido toopatch, actualizar y administrar su entorno de máquinas virtuales. Máquinas virtuales de Azure es una infraestructura como servicio (IaaS), mientras que Servicio de aplicaciones y Service Fabric son plataformas como servicio (Paas). 

## <a name="features"></a>Comparación de características
Hello en la tabla siguiente compara las capacidades de Hola de servicio de aplicaciones, servicios en la nube, máquinas virtuales y Service Fabric toohelp hacer mejor opción de Hola. Para obtener información actual sobre hello SLA para cada opción, consulte [contratos de nivel de servicio de Azure](https://azure.microsoft.com/support/legal/sla/).

| Característica | Servicio de aplicaciones (aplicaciones web) | Servicios en la nube (roles web) | Máquinas virtuales | Service Fabric | Notas |
| --- | --- | --- | --- | --- | --- |
| Implementación casi instantánea |X | | |X |Implementar una aplicación o un tooa de actualización de la aplicación servicio de nube o la creación de una máquina virtual, puede tardar varios minutos como mínimo; implementar una aplicación web de tooa de aplicación tarda a unos segundos. |
| Escalar verticalmente máquinas toolarger sin volver a implementar |X | | |X | |
| Instancias de servidor Web comparten contenido y configuración, lo que significa que no tengan tooredeploy o volver a configurar cuando se escala. |X | | |X | |
| Varios entornos de implementación (producción y ensayo) |X |X | |X |Service Fabric permite toohave varios entornos para sus aplicaciones o toodeploy distintas versiones de la aplicación en paralelo. |
| Administración de actualización automática del SO |X |X | | |Las actualizaciones automáticas del SO están previstas para las próximas versiones de Service Fabric. |
| Intercambio fluido entre plataformas (mover fácilmente entre 32 bits y 64 bits) |X |X | | | |
| Código de implementación con GIT, FTP |X | |X | | |
| Código de implementación con Web Deploy |X | |X | |Servicios en la nube es compatible con uso de hello Web Deploy toodeploy actualizaciones tooindividual de instancias de rol. Sin embargo, no puede usar para la implementación inicial de un rol, y si utilizar Web Deploy para realizar una actualización por separado tiene toodeploy tooeach instancia de un rol. Son necesarias varias instancias en tooqualify de orden para hello SLA de servicio de nube para entornos de producción. |
| Soporte para WebMatrix |X | |X | | |
| Tooservices de acceso como el Bus de servicio, almacenamiento, base de datos SQL |X |X |X |X | |
| Web de host o nivel de servicios web de una arquitectura multinivel |X |X |X |X | |
| Nivel medio del host de una arquitectura multinivel |X |X |X |X |Aplicaciones de servicio de aplicaciones web pueden hospedar un nivel intermedio de la API de REST y fácilmente Hola [WebJobs](http://go.microsoft.com/fwlink/?linkid=390226) característica puede hospedar el procesamiento de trabajos en segundo plano. Puede ejecutar trabajos Web en una sitio Web dedicado tooachieve independiente una escalabilidad de nivel de Hola. vista previa de Hello [aplicaciones de API](../app-service-api/app-service-api-apps-why-best-platform.md) característica proporciona incluso más características para hospedar servicios REST. |
| Soporte integrado de MySQL como servicio |X |X |X | |Servicios en la nube pueden integrar MySQL como servicio a través de ofertas de ClearDB, pero no como parte del flujo de trabajo de hello Portal de Azure. |
| Soporte para ASP.NET, ASP clásico, Node.js, PHP, Python |X |X |X |X |Tejido de servicio admite la creación de hello de un front-end de web con [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md) o puede implementar cualquier tipo de aplicación (Node.js, Java, etcetera) como un [ejecutable invitado](../service-fabric/service-fabric-deploy-existing-app.md). |
| Escalar horizontalmente toomultiple instancias sin volver a implementar |X |X |X |X |Máquinas virtuales puede escalar horizontalmente toomultiple instancias, pero se deben escribir servicios de Hola que se ejecutan en ellos toohandle este escalado horizontal. Tooconfigure un solicita tooroute de equilibrador de carga en los equipos de hello y cree un grupo de afinidad tooprevent simultáneas reinicios de todas las instancias debido a errores de hardware o toomaintenance. |
| Soporte para SSL |X |X |X |X |En el caso de las aplicaciones web del Servicio de aplicaciones, solo se admite SSL para nombres de dominio personalizados para el modo Básico y Estándar. Para más información sobre el uso de SSL con aplicaciones web, consulte [Configuración de un certificado SSL para un sitio web Azure](app-service-web-tutorial-custom-ssl.md). |
| Integración de Visual Studio |X |X |X |X | |
| Depuración remota |X |X |X | | |
| Código de implementación con TFS |X |X |X |X | |
| Aislamiento de red con [Red virtual de Azure](/azure/virtual-network/) |X |X |X |X |Consulte también [Integración de redes virtuales de Sitios web Azure](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) |
| Soporte técnico para el [Administrador de tráfico de Azure](/azure/traffic-manager/) |X |X |X |X | |
| Supervisión de extremo integrado |X |X |X | | |
| Tooservers de acceso al escritorio remoto | |X |X |X | |
| Instalación de cualquier MSI personalizado | |X |X |X |Service Fabric permite toohost archivo de cualquier archivo ejecutable como una [ejecutable invitado](../service-fabric/service-fabric-deploy-existing-app.md) o puede instalar cualquier aplicación en hello las máquinas virtuales. |
| Tareas de inicio/ejecutar toodefine de capacidad | |X |X |X | |
| Puede escuchar eventos de tooETW | |X |X |X | |

## <a name="scenarios"></a>Escenarios y recomendaciones
Estos son algunos escenarios comunes de aplicación con recomendaciones como opción de hospedaje web de Azure toowhich podría ser más adecuado para cada uno.

* [Se necesita un front-end web con procesamiento en segundo plano y aplicaciones de negocio de base de datos back-end toorun integradas con recursos locales.](#onprem)
* [Se necesita un toohost de manera confiable llegar Mi sitio Web corporativo que se escala bien y ofertas globales.](#corp)
* [Tengo una aplicación IIS6 ejecutándose en Windows Server 2003.](#iis6)
* [Soy propietario de una pequeña empresa, y se necesita una manera económica toohost Mi sitio pero con el crecimiento futuro en mente.](#smallbusiness)
* [Soy un diseñador gráfico o web, y desee toodesign y crear sitios web para mis clientes.](#designer)
* [Estoy migrando mi aplicación de varios nivel con una toohello de front-end web en la nube.](#multitier)
* [Mi aplicación depende de Windows muy personalizados o entornos de Linux y se desea toomove toohello en la nube.](#custom)
* [Mi sitio utiliza software de código abierto y deseo toohost en Azure.](#oss)
* [Tengo una aplicación de línea de negocio que necesita la red corporativa de tooconnect toohello.](#lob)
* [Desea toohost un servicio web o API de REST para clientes móviles.](#mobile)

### <a id="onprem"></a>Se necesita un front-end web con procesamiento en segundo plano y aplicaciones de negocio de base de datos back-end toorun integradas con recursos locales.
El Servicio de aplicaciones de Azure es una solución excelente para aplicaciones empresariales complejas. Le permite desarrollar aplicaciones que se adaptan automáticamente en una plataforma con equilibrio de carga, se protegen con Active Directory y conectan a recursos locales de tooyour. Simplifica la administración de esas aplicaciones fáciles a través de una API y portal de talla mundial y permite una visión general toogain cómo los clientes que los utilice con herramientas de una visión general de aplicaciones. Hola [Webjobs] [ Webjobs] característica le permite ejecutar procesos en segundo plano y hacerla recursos de back-tooon local tooconnect fácil tareas como parte de la capa web, mientras la conectividad híbrida y características de red virtual. El Servicio de aplicaciones de Azure proporciona SLA con un tiempo activo garantizado del 99,9% para las aplicaciones web y le permite:

* Ejecutar sus aplicaciones de manera confiable en una plataforma en la nube que se mantiene por sí misma y aplica revisiones automáticamente.
* Escalar automáticamente entre una red global de centros de datos.
* Realizar copias de seguridad y restaurar para la recuperación ante desastres.
* Cumplir con ISO, SOC2 y PCI.
* Integrarse con Active Directory

### <a id="corp"></a>Se necesita un toohost de manera confiable llegar Mi sitio Web corporativo que se escala bien y ofertas globales.
El Servicio de aplicaciones de Azure es una excelente solución para hospedar sitios web corporativos. Permite tooscale de aplicaciones web rápida y fácilmente toomeet exigir a través de una red mundial de centros de datos. Ofrece alcance local, tolerancia a errores y administración del tráfico inteligente. Todo en una plataforma que proporciona herramientas de administración de nivel internacional, permitiéndole toogain una visión general de estado de sitio y tráfico de los sitios forma rápida y sencilla. El Servicio de aplicaciones de Azure proporciona SLA con un tiempo activo garantizado del 99,9% para las aplicaciones web y le permite:

* Ejecutar sus sitios web de manera confiable en una plataforma en la nube que se mantiene por sí misma y aplica revisiones automáticamente.
* Escalar automáticamente entre una red global de centros de datos.
* Realizar copias de seguridad y restaurar para la recuperación ante desastres.
* Administrar registros y tráfico con herramientas integradas.
* Cumplir con ISO, SOC2 y PCI.
* Integrarse con Active Directory

### <a id="iis6"></a> Tengo una aplicación IIS6 ejecutándose en Windows Server 2003.
Servicio de aplicaciones de Azure hace fácil tooavoid Hola los costos de infraestructura asociados con la migración de aplicaciones de IIS 6 anterior. Microsoft ha creado [herramientas de migración de toouse fácil e instrucciones de migración detallado](https://www.movemetowebsites.net/) que habilitar compatibilidad de toocheck e identificar los cambios que necesitan toobe realizado. Integración con Visual Studio, TFS y herramientas comunes de CMS hace fácil toodeploy IIS6 aplicaciones directamente en la nube toohello. Una vez implementado, Hola Portal de Azure proporciona herramientas de administración sólida que le permiten tooscale hacia abajo toomanage costos y la demanda de toomeet según sea necesario. Herramienta de migración de Hola de hacer lo siguiente:

* Rápida y fácilmente migrar su toohello nube heredada de Windows Server 2003 web application.
* Participación tooleave su toocreate de local de base de datos SQL adjunta una aplicación híbrida.
* Mover automáticamente su base de datos SQL junto con la aplicación heredada.

### <a id="smallbusiness"></a>Soy propietario de una pequeña empresa, y se necesita una manera económica toohost Mi sitio pero con el crecimiento futuro en mente.
El Servicio de aplicaciones de Azure es una solución excelente para este escenario, porque puede empezar a usarlo gratis y luego agregar más capacidades cuando las necesite. Cada aplicación web gratuita incluye un dominio proporcionado por Azure (*su_compañía*. azurewebsites.net), y plataforma de hello incluye herramientas integradas de implementación y administración, así como una galería de aplicaciones que hacen que sea fácil tooget iniciado. Hay muchos otros servicios y opciones de escalado que permiten hello tooevolve de sitio con la demanda de los usuarios mayor. Con el Servicio de aplicaciones de Azure, puede:

* Comenzar con el nivel gratuito de Hola y, a continuación, escalar según sea necesario.
* Utilice Hola Galería de aplicaciones tooquickly configurar aplicaciones web populares, como por ejemplo WordPress.
* Agregar Azure servicios y características tooyour aplicación adicional según sea necesario.
* Proteger su aplicación web con HTTPS.

### <a id="designer"></a>Soy un diseñador gráfico o web, y desee toodesign y crear sitios Web para mis clientes
Para diseñadores y desarrolladores web, el Servicio de aplicaciones de Azure se integra fácilmente con diversos marcos y herramientas, admite la implementación de Git y FTP y ofrece una integración estrecha con herramientas y servicios como Visual Studio y Base de datos SQL. Con el Servicio de aplicaciones, puede:

* Usar herramientas de línea de comandos para [tareas automatizadas][scripting].
* Trabajar con lenguajes populares como [.Net][dotnet], [PHP][PHP], [Node.js][nodejs] y [Python][Python].
* Seleccione los tres niveles diferentes de escala para escalar toovery altas capacidades.
* Integrar con otros servicios de Azure, como [base de datos SQL][sqldatabase], [Service Bus] [ servicebus] y [almacenamiento] [ Storage], o asociados ofertas de hello [tienda de Azure][azurestore], como MySQL y MongoDB.
* Integrarse con herramientas como Visual Studio, Git, WebMatrix, WebDeploy, TFS y FTP.

### <a id="multitier"></a>Estoy migrando mi aplicación de varios nivel con una toohello de front-end web en la nube
Si ejecuta una aplicación de varios niveles, por ejemplo, un servidor web que se conecta la base de datos de tooa, servicio de aplicaciones de Azure es una buena opción que ofrece una estrecha integración con la base de datos de SQL Azure. Y puede usar características de hello trabajos Web para ejecutar procesos de back-end.

Elija a Service Fabric para uno o varios de los niveles si necesita más controlan sobre el entorno del servidor hello, como tooremote de capacidad de hello en el servidor o configurar las tareas de inicio del servidor.

Elija máquinas virtuales para uno o varios de los niveles si desea que toouse su propia imagen de máquina o ejecute software de servidor o servicios que no se puede configurar en el tejido de servicio.

### <a id="custom"></a>Mi aplicación depende de Windows muy personalizados o entornos de Linux y se desea toomove toohello en la nube.
Si la aplicación requiere la instalación compleja o configuración del sistema operativo de hello y software, las máquinas virtuales es probablemente la mejor solución de Hola. Con Máquinas virtuales, puede hacer lo siguiente:

* Utilice toostart de galería de máquina Virtual de hello con un sistema operativo, como Windows o Linux y, a continuación, personalizarla en función de sus requisitos de aplicación.
* Crear y cargar una imagen personalizada de una toorun de servidor local existente en una máquina virtual en Azure.

### <a id="oss"></a>Mi sitio utiliza software de código abierto y deseo toohost en Azure
Si el marco de código abierto es compatible con el servicio de aplicaciones, idiomas de Hola y marcos de trabajo necesarios para la aplicación se configuran automáticamente para usted. El Servicio de aplicaciones le permite:

* Usar muchos lenguajes de código abierto populares, como [.NET][dotnet], [PHP][PHP], [Node.js][nodejs] y [Python][Python].
* Configurar WordPress, Drupal, Umbraco, DNN y muchas otras aplicaciones web de terceros.
* Migrar una aplicación existente o crear uno nuevo de hello Galería de aplicaciones.

Si no se admite el marco de código abierto en el servicio de aplicaciones, puede ejecutarlo en uno de hello otra opciones de hospedaje de web de Azure. Con máquinas virtuales, instalar y configurar el software de hello en la imagen de la máquina de hello, que puede ser Windows o Linux.

### <a id="lob"></a>Tengo una aplicación de línea de negocio que necesita la red corporativa de tooconnect toohello
Si desea toocreate una aplicación de línea de negocio, el sitio Web podría requerir tooservices acceso directo o datos en la red corporativa de Hola. Esto es posible en el servicio de aplicaciones, Service Fabric y máquinas virtuales con hello [servicio de red Virtual de Azure](/azure/virtual-network/). En el servicio de aplicaciones puede usar hello [característica de integración de red virtual](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/), lo que permite su toorun de las aplicaciones de Azure como si estuvieran en la red corporativa.

### <a id="mobile"></a>Desea toohost un servicio web o API de REST para clientes móviles
Servicios web basados en HTTP permiten toosupport una amplia variedad de clientes, incluidos a los clientes móviles. Marcos de trabajo como ASP.NET Web API integran con Visual Studio toomake toocreate más fácil y consumen servicios REST.  Estos servicios se exponen desde un punto de conexión de web, por lo que es posible toouse cualquiera web hospedaje técnica en Azure toosupport este escenario. Sin embargo, el Servicio de aplicaciones es una elección excelente para hospedar las API de REST. Con el Servicio de aplicaciones, puede:

* Cree rápidamente un [aplicación móvil](../app-service-mobile/app-service-mobile-value-prop.md) o [aplicación de API](../app-service-api/app-service-api-apps-why-best-platform.md) toohost servicio de web HTTP de hello en uno de los centros de datos distribuidos globalmente de Azure.
* Migrar los servicios existentes o crear otros nuevos.
* Lograr el SLA de disponibilidad con una sola instancia o escalar horizontalmente máquinas toomultiple dedicado.
* Hola use publica sitio tooprovide las API de REST tooany clientes HTTP, incluidos los clientes móviles.

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta, vaya demasiado<a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>, donde puede inmediatamente crear una aplicación de inicio de corta duración en el servicio de aplicación de Azure de forma gratuita. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a id="nextsteps"></a> Pasos siguientes
Para obtener más información acerca de web Hola tres opciones de hospedaje, vea [Introducción a Azure](../fundamentals-introduction-to-azure.md).

tooget a trabajar con opciones de hello elegido para la aplicación, vea Hola recursos siguientes:

* [Azure App Service](/azure/app-service/)
* [Servicios en la nube de Azure](/azure/cloud-services/)
* [Máquinas virtuales de Azure](/azure/virtual-machines/)
* [Service Fabric](/azure/service-fabric/)

<!-- URL List -->

[Azure App Service]: /azure/app-service/
[Cloud Services]: /azure/cloud-services/
[Virtual Machines]: /azure/virtual-machines/
[Service Fabric]: /azure/service-fabric/
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: app-service-web-tutorial-custom-ssl.md
[azurestore]: https://azuremarketplace.microsoft.com/en-us/marketplace/apps
[scripting]: https://azure.microsoft.com/documentation/scripts/?services=web-sites
[dotnet]: https://azure.microsoft.com/develop/net/
[nodejs]: https://azure.microsoft.com/develop/nodejs/
[PHP]: https://azure.microsoft.com/develop/php/
[Python]: https://azure.microsoft.com/develop/python/
[servicebus]: /azure/service-bus/
[sqldatabase]: /azure/sql-database/
[Storage]: /azure/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png
