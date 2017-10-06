---
title: aaaIntro tooMicrosoft Azure | Documentos de Microsoft
description: "¿TooMicrosoft nuevo Azure? Obtener una visión general básica de hello servicios que ofrece ejemplos de cómo le servirán de ayuda."
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 6791506abe813e19ca7b04d78d35cb46352a9028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-microsoft-azure"></a>Introducción a Microsoft Azure
Microsoft Azure es la plataforma de aplicaciones de Microsoft para la nube pública de Hola.  objetivo de Hola de este artículo es toogive que una base para entender los conceptos básicos de Hola de Azure, incluso si no sabe nada acerca de la informática en nube.

**¿Cómo tooread este artículo**

Azure está aumentando el tiempo total de Hola por lo que resulta fácil tooget sobrecargado.  Comience con los servicios básicos de hello, que se enumeran en primer lugar en este artículo y, haga clic en servicios de tooadditional. Eso no significa que no se puede usar simplemente servicios adicionales de Hola por sí mismos, pero servicios básicos de hello constituyen el núcleo de Hola de una aplicación que se ejecuta en Azure.

**Envíenos sus comentarios**

Sus comentarios son importantes. Este artículo debería proporcionarle una eficaz visión global de Azure. Si no es así, proporcione información en la sección de comentarios de Hola final Hola de página de Hola. Ofrecen algunos detalles acerca de lo que esperaba toosee y cómo tooimprove Hola artículo.  

## <a name="hello-components-of-azure"></a>Hola componentes de Azure
Azure agrupa servicios por categorías en el Portal de administración de Hola y en diversas ayudas visuales que como hello [¿qué es Azure Infografía](https://azure.microsoft.com/documentation/infographics/azure/) . Hola Portal de administración es lo que usa toomanage más (pero no todos) de servicios de Azure.

Este artículo se utiliza un **otra organización** tootalk acerca de los servicios basados en función similar y toocall los servicios de subcarpetas importantes que forman parte de los más grandes.  

![Componentes de Azure](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 *Ilustración: Azure proporciona servicios de aplicaciones accesibles desde Internet que se ejecutan en centros de datos de Azure.*

## <a name="management-portal"></a>Portal de administración
Azure tiene una interfaz web llamada hello [Portal de administración](http://manage.windowsazure.com) que permite a los administradores tooaccess y administrar la mayoría, pero Azure no todas las características.  Normalmente, Microsoft publica portal de interfaz de usuario más reciente de hello en la versión beta antes de retirarlo uno anterior. Hello otra más reciente se denomina hello ["Portal de vista previa de Azure"](https://portal.azure.com/).

Normalmente hay un largo periodo de solapamiento en el que los dos portales están activos. Aunque los servicios fundamentales aparecerán en los dos portales, es posible que no toda la funcionalidad esté disponible en ambos. Nuevos servicios pueden aparecer en hello más recientes primeros y anteriores servicios del portal y funcionalidad solo puede existir en hello uno anterior.  mensaje de Hola aquí es que comprueben si no encuentra algo en el portal anterior de hello, hello otra más reciente y viceversa.

## <a name="compute"></a>Proceso
Uno de los aspectos más básicas de hello que una plataforma de nube es ejecutar las aplicaciones. Cada uno de los modelos de proceso de Azure de hello tiene su propio tooplay de rol.

Puede usar estas tecnologías por separado o combinarlos según sea necesario toocreate Hola derecho foundation para la aplicación. enfoque de Hola que elija dependerá de los problemas que está tratando de toosolve.

### <a name="azure-virtual-machines"></a>Máquinas virtuales de Azure
![Azure Virtual Machines ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*Figura: Máquinas virtuales de Azure ofrece un control total sobre instancias de máquina virtual en la nube de Hola.*

Hola capacidad toocreate una máquina virtual a petición, si se proporciona de una imagen estándar o de uno, puede ser muy útil. Este enfoque, conocido comúnmente como Infraestructura como servicio (IaaS), es lo que proporciona Máquinas virtuales de Azure. La figura 2 muestra una combinación de cómo se ejecuta una máquina Virtual (VM) y cómo toocreate desde un disco duro virtual.  

toocreate una máquina virtual, especifique qué VHD hello y toouse del tamaño de máquina virtual.  A continuación, paga por tiempo Hola ese Hola que VM se esté ejecutando. Se paga por minuto de Hola y solo mientras se está ejecutando, aunque hay una carga mínima en almacenamiento para mantener Hola VHD disponible. Azure ofrece una galería de VHD (denominados "imágenes") que contienen un toostart de sistema operativo de arranque de existencias. Entre ellos se incluyen opciones de Microsoft y sus asociados, como Windows Server y Linux, SQL Server, Oracle y muchos más. Está libre toocreate discos duros virtuales e imágenes y, a continuación, cargarlos usted mismo. Puede incluso cargar VHD que contengan únicamente datos y luego obtener acceso a ellos desde sus máquinas virtuales en ejecución.

Siempre que sea Hola VHD procede de, puede almacenar de forma continua los cambios realizados mientras se ejecuta una máquina virtual. Hello próxima vez que cree una máquina virtual desde ese archivo VHD, lo recoja donde lo dejó. Hola discos duros virtuales que Hola volver a máquinas virtuales se almacenan en blobs de almacenamiento de Azure, que se van a describir más adelante.  Que significa que las máquinas virtuales no desaparecen debido a errores de disco y toohardware de tooensure de redundancia. Es también posible toocopy Hola cambiado VHD fuera de Azure, a continuación, ejecuta de forma local.

La aplicación ahora ejecuta dentro de una o más máquinas virtuales, dependiendo de cómo se creó con anterioridad o decidir toocreate, desde el principio.

Este toocloud enfoque bastante general puede ser usado tooaddress distintos problemas en muchos de informática.

**Escenarios de máquina virtual**

1. **Desarrollo/pruebas** -pueda utilizarlos toocreate una plataforma de desarrollo y pruebas económica que puede cerrar cuando haya terminado de usarlo. O también, podría crear y ejecutar aplicaciones que utilicen los lenguajes y las bibliotecas que prefiera. Esas aplicaciones pueden utilizar cualquiera de las opciones de administración de datos de Hola que proporciona Azure, y también puede elegir toouse SQL Server u otro DBMS que se ejecuta en una o más máquinas virtuales.
2. **Mover aplicaciones tooAzure (elevación y MAYÚS)** -"Elevación y Mayús" hace referencia toomoving la aplicación mucho igual que haría un toomove carga un objeto grande.  Se "elevación" Hola VHD del centro de datos local y "cambiar" se tooAzure y ejecutarlo en él.  Normalmente habrá toodo algunas dependencias de tooremove de trabajo en otros sistemas. Si hay muchas, quizá le convenga más utilizar la tercera opción.  
3. **Ampliar el centro de datos** : use máquinas virtuales de Azure como extensión de su centro de datos local, ejecutando SharePoint u otras aplicaciones. toosupport esto, es posible toocreate dominios de Windows en la nube de hello mediante la ejecución de Active Directory en máquinas virtuales de Azure. Puede utilizar tootie de red Virtual de Azure (que se mencionará más adelante) la red local y la red en Azure juntos.

### <a name="web-apps"></a>Web Apps
![Web Apps de Azure ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *Figura: Aplicaciones Web de Azure se ejecuta una aplicación de sitio Web en hello nube sin necesidad de servidor de web toomanage Hola subyacente.*

Uno de hello tareas más comunes que los usuarios realizan en la nube de Hola se ejecuta aplicaciones web y sitios Web. Máquinas virtuales de Azure permite esto, pero todavía se deja con la responsabilidad de Hola de administrar una o varias máquinas virtuales y Hola subyacente sistemas operativos. Los roles web de servicios en la nube pueden hacerlo, pero su implementación y mantenimiento conlleva también trabajo administrativo.  ¿Qué ocurre si su intención es un sitio Web que alguien se encarga de trabajo administrativo de Hola para usted?

Esto es exactamente lo que proporciona Aplicaciones web. Este modelo de proceso ofrece un entorno web administrado mediante el portal de administración de Azure de hello, así como las API. Puede mover una aplicación de sitio Web existente en las aplicaciones Web sin cambios, o puede crear una nueva directamente en la nube de Hola. Una vez que se ejecuta un sitio Web, puede agregar o quitar instancias dinámicamente, confiando en aplicaciones Web de Azure tooload equilibrar las solicitudes entre ellos. Las aplicaciones de Azure ofrece una opción compartida, donde el sitio Web se ejecuta en una máquina virtual con otros sitios, y una opción estándar que permite un toorun de sitio en su propia máquina virtual. opción estándar de Hello también le permite aumentar tamaño de hello (eficacia informática) de las instancias si es necesario.

Para el desarrollo, Aplicaciones web es compatible con .NET, PHP, Node.js, Java y Python, junto con Base de datos SQL y MySQL (de ClearDB, un socio de Microsoft) para el almacenamiento relacional. También ofrece compatibilidad integrada con varias aplicaciones conocidas, como WordPress, Joomla y Drupal. objetivo de Hello es tooprovide un bajo costo, escalable y una amplia utilidad plataforma para crear aplicaciones web y sitios Web en la nube pública de Hola.

**Escenarios de Aplicaciones web**

Aplicaciones Web está previsto toobe útiles para las organizaciones, los desarrolladores y agencias de diseño web. En el caso de las corporaciones, constituye una solución fácil de administrar, escalable, muy segura y de alta disponibilidad para la ejecución de sitios web de presencia. Cuando necesite tooset un sitio Web, es mejor toostart con aplicaciones Web de Azure y continuar tooCloud servicios una vez que se necesita una característica que no está disponible. Consulte Hola al final de la sección de "Proceso" hello para obtener vínculos que pueden ayudar a toochoose entre las opciones de Hola.

### <a name="cloud-services"></a>Cloud Services
![Servicio en la nube de Azure](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*Figura: Servicios de nube de Azure proporciona un toorun de contexto altamente escalable código personalizado en una plataforma como un entorno de servicio (PaaS)*

Imagine que desea toobuild una aplicación en la nube que puede admitir una gran cantidad de usuarios simultáneos, no requiere mucho administración y nunca deja de funcionar. Es posible que un fabricante de software establecida, por ejemplo, que decidió tooembrace Software como servicio (SaaS) mediante la creación de una versión de una de las aplicaciones en la nube de Hola. O bien, podría ser un principiante que desea crear una aplicación de consumidor que espera que crezca rápido. Si fuera a crear sobre Azure, ¿qué modelo de ejecución debería usar?

Aplicaciones web de Azure le permite crear esta clase de aplicación web, pero existen algunas limitaciones. No dispone de acceso administrativo, por ejemplo. Esto significa que no puede instalar software arbitrario. Máquinas virtuales de Azure ofrece mucha flexibilidad, incluido el acceso administrativo y por supuesto, puede utilizarlo toobuild una aplicación muy escalable, pero tendrá toohandle muchos aspectos de confiabilidad y administración de usted mismo. ¿Qué gustaría es una opción que le ofrece Hola control necesita, pero también administra la mayor parte del trabajo de hello necesaria para la confiabilidad y administración.

Pues esto es exactamente lo que proporciona Servicios en la nube de Azure. Esta tecnología es diseñados expresamente toosupport escalable, confiable y aplicaciones de administración de baja y es un ejemplo de lo que normalmente denomina plataforma como servicio (PaaS). toouse, se crea una aplicación con la tecnología de hello su elección, como C#, Java, PHP, Python, Node.js o algo más. El código, a continuación, se ejecuta en máquinas virtuales (instancias de tooas que se hace referencia) que se ejecutan una versión de Windows Server.

Pero estas máquinas virtuales son distintas de Hola que haya creado con máquinas virtuales de Azure. Y la diferencia es esta: Azure es quien las administra. Así, realiza tareas como instalar revisiones de sistemas operativos e implementar automáticamente las nuevas imágenes revisadas. Esto implica que la aplicación no debe mantener el estado en instancias de rol web o de trabajo; en su lugar, se debe mantener en una de las opciones de administración de datos de Azure Hola que se describe en la sección siguiente de Hola. Azure también supervisa las VM y las reinicia en caso de error. Puede establecer en la nube servicios tooautomatically crear instancias de más o menos en toodemand de respuesta. Esto permite toohandle mayor uso y, a continuación, la escala para que no se pagan tanta cuando hay menos uso.

Tiene dos toochoose roles al crear una instancia, ambos basados en Windows Server. Hola principal diferencia entre Hola dos es que una instancia de un rol web ejecuta IIS, mientras que una instancia de un rol de trabajo no. Ambos se administran Hola de mismo modo, sin embargo y la comunes para una aplicación toouse ambos. Por ejemplo, una instancia de rol web podría aceptar las solicitudes de usuarios, a continuación, pasarlas tooa instancia de rol de trabajo para su procesamiento. tooscale hacia arriba o hacia abajo de la aplicación, puede solicitar que Azure cree más instancias de cualquiera de los roles o cierre las instancias existentes. Y tooAzure similar máquinas virtuales, se le cobrará solo para el tiempo de presentación que se está ejecutando cada instancia de rol web o de trabajo.

**Escenarios de Servicios en la nube**

Servicios en la nube son toosupport ideal masivos escalada cuando necesita más control sobre la plataforma de Hola que proporciona aplicaciones Web de Azure, pero no tiene control sobre el sistema operativo subyacente de Hola.

#### <a name="choosing-a-compute-model"></a>Selección de un modelo de proceso
página de Hello [comparación de aplicaciones Web de Azure, servicios en la nube y máquinas virtuales](app-service-web/choose-web-site-cloud-service-vm.md) proporciona información más detallada sobre cómo toochoose un modelo de proceso.

## <a name="data-management"></a>Administración de datos
Las aplicaciones necesitan datos, y diferentes tipos de aplicaciones necesitan diferentes tipos de datos. Por este motivo, Azure proporciona toostore de varias maneras diferentes y administrar los datos. Azure proporciona muchas opciones de almacenamiento, todas ellas diseñadas para ofrecer un rendimiento muy duradero.  Con cualquiera de estas opciones, siempre hay 3 copias de los datos que se mantienen sincronizados en un centro de datos Azure--6 Si permite que tooback de redundancia geográfica de Azure toouse seguridad tooanother centro de datos al menos 300 millas.     

### <a name="in-virtual-machines"></a>En Máquinas virtuales
ya se ha mencionado Hola capacidad toorun SQL Server u otro DBMS en una máquina virtual que creó con máquinas virtuales de Azure. Tenga en cuenta que esta opción no está limitado toorelational sistemas; También lo tecnologías de NoSQL toorun libre como MongoDB y Casandra. La ejecución de su propio sistema de base de datos es sencillo TI replica qué estamos usa tooin nuestro propio centros de datos- pero también requiere control de administración de Hola de ese DBMS.  En otras opciones, Azure controla varios o todos de administración de Hola.

De nuevo, estado de Hola de hello Máquina Virtual y cualquier disco de datos adicionales, podrá crea o cargar respaldados por el almacenamiento de blobs (que se van a describir más adelante).  

### <a name="azure-sql-database"></a>Azure SQL Database
![Base de datos SQL de almacenamiento de Azure](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*Figura: Base de datos de SQL Azure proporciona un servicio de base de datos relacional administrado en la nube de Hola.*

Para el almacenamiento relacional, Azure proporciona Hola característica base de datos SQL. No permita que la nomenclatura de hello engañarle. Se trata de algo diferente de la típica Base de datos SQL que ofrece SQL Server y que se ejecuta sobre Windows Server.  

Anteriormente denominado SQL Azure, base de datos de SQL Azure proporciona todas Hola características clave de un base de datos relacional sistema de administración, incluidas las transacciones atómicas, acceso simultáneo a datos por varios usuarios con integridad de los datos, consultas SQL ANSI y una programación conocida modelo. Al igual que SQL Server, se puede obtener acceso a Base de datos SQL mediante Entity Framework, ADO.NET, JDBC y otras conocidas tecnologías de acceso a datos. También admite la mayoría de hello lenguaje T-SQL, junto con las herramientas de SQL Server, como SQL Server Management Studio. A todos aquellos que estén familiarizados con SQL Server (u otra base de datos relacional), el uso de Base de datos SQL les resultará muy sencillo.

Pero su base de datos SQL no es simplemente un DBMS en hello TI en la nube de un servicio de PaaS. También es controlar los datos y que puede obtener acceso a él, pero base de datos SQL se encarga de trabajo de grunt administrativas de hello, como administrar la infraestructura de hardware de Hola y mantiene automáticamente software de base de datos y el sistema operativo de hello seguridad toodate. Base de datos SQL ofrece también una alta disponibilidad, copias de seguridad automática y capacidad de restauración en el momento, y puede replicar copias entre regiones geográficas.  

**Escenarios para Base de datos SQL**

Si va a crear una aplicación de Azure (mediante cualquiera de los modelos de proceso de Hola) que necesita almacenamiento relacional, base de datos SQL puede ser una buena opción. Aplicaciones que se ejecutan en la nube Hola fuera también pueden usar este servicio, sin embargo, por lo que hay una gran cantidad de otros escenarios. Por ejemplo, se puede tener acceso a los datos almacenados en Base de datos SQL desde diferentes sistemas cliente, como equipos de escritorio, equipos portátiles, tabletas y teléfonos. Y como proporciona alta disponibilidad integrada a través de la replicación, el uso de Base de datos SQL puede ayudar a reducir el tiempo de inactividad.

### <a name="tables"></a>Tablas
![Tablas de almacenamiento de Azure](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*Figura: Tablas de Azure proporciona un plano NoSQL forma toostore que los datos.*

Esta característica recibe en ocasiones nombres diferentes porque forma parte de otra más amplia denominada "Almacenamiento de Azure". Si ve "tables", "Tablas de Azure" o "tablas de almacenamiento", es all Hola lo mismo.  

Y no se preocupe por nombre de hello: esta tecnología no proporciona almacenamiento relacional. De hecho, es un ejemplo de un enfoque NoSQL conocido como almacén de clave/valor. Tablas de Azure permite a una aplicación almacenar propiedades de diversos tipos, como cadenas, enteros y fechas. Luego, la aplicación puede recuperar un grupo de propiedades proporcionando una clave única para ese grupo. Mientras que las operaciones complejas como no se admiten las combinaciones, las tablas ofrecen datos de tootyped un acceso rápido. También son muy escalables, con un toohold capaz de tabla única tanto como un terabyte de datos. Y que coincide con su simplicidad, las tablas son toouse normalmente menos costoso que el almacenamiento relacional de la base de datos de SQL.

**Escenarios para tablas**

Suponga que desea toocreate una aplicación de Azure que necesita fast tener acceso a datos tootyped, quizá una gran cantidad de ella, pero no necesita tooperform de consultas SQL complejas en estos datos. Por ejemplo, imagine que está creando una aplicación de consumidor que necesita información de perfil de cliente toostore para cada usuario. La aplicación va toobe muy popular, por lo que debe tooallow para una gran cantidad de datos, pero no hace mucho con estos datos más allá de almacenarla, a continuación, la recuperación de varias maneras sencillas. Esto es exactamente Hola tipo de escenario donde las tablas de Azure tiene sentido.

### <a name="blobs"></a>Blobs
![Blobs de Azure Storage](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*Ilustración: Los Blobs de Azure proporcionan datos binarios sin estructurar.*  

Blobs de Azure (nuevo "Almacenamiento de blobs" y simplemente "almacenamiento de Blobs" son Hola lo mismo) es toostore diseñada datos binarios no estructurados. Al igual que las Tablas, los Blobs proporcionan almacenamiento económico, y un solo blob puede tener un tamaño hasta de 1 TB (un terabyte). Las aplicaciones de Azure pueden utilizar también unidades de Azure, que permiten a los blobs proporcionar almacenamiento persistente para un sistema de archivos de Windows montado en una instancia de Azure. aplicación Hello ve archivos normales de Windows, pero el contenido de hello realmente se almacena en un blob.

El Almacenamiento de blobs se utiliza por muchas otras características de Azure (incluidas Máquinas virtuales), así que sin duda puede manejar también sus cargas de trabajo.

**Escenarios para Blobs**

Una aplicación que almacena vídeo, archivos masivos u otra información de tipo binario puede utilizar blobs como método de almacenamiento sencillo y barato. Los Blobs suelen utilizarse junto con otros servicios como la Red de entrega de contenido, de la que hablaremos más adelante.  

### <a name="import--export"></a>Importación / Exportación
![Azure Import Export Service](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*Figura: Azure importación / exportación proporciona Hola capacidad tooship un tooor de disco duro físico de Azure para más rápido y barato datos importación o exportación.*  

A veces desea toomove una gran cantidad de datos en Azure. Esto tomaría mucho tiempo, quizá días, y utilizaría mucho ancho de banda. En estos casos, puede usar la importación y exportación de Azure, lo que permite tooship cifrada con Bitlocker 3,5" discos duros SATA directamente tooAzure centros de datos, donde Microsoft hello los datos transfieren en el almacenamiento de blobs para usted.  Una vez completada la carga de hello, Microsoft suministra hello unidades back-tooyou.  También puede solicitar que grandes cantidades de datos desde almacenamiento de blobs se exportan en unidades de disco duro y se enviarán tooyou atrás a través de correo electrónico.

**Escenarios para la importación y exportación**

* **Migración de datos de gran tamaño** : cada vez que tienen grandes cantidades de datos (Terabytes) que desea tooupload tooAzure, servicio de importación/exportación de Hola suele ser mucho más rápido y quizás más económico que transferir a través de hello internet. Una vez en los blobs de datos de hello, puede procesarlo en otras formas, como el almacenamiento de tabla o una base de datos de SQL.
* **Recuperación de datos de archivado** -puede usar la importación y exportación de toohave Microsoft transfieren grandes cantidades de datos almacenados en almacenamiento de blobs de Azure tooa de dispositivo de almacenamiento que envíe y, a continuación, tiene que el dispositivo entrega ubicación tooa espera que desee. Como esto puede tomar algún tiempo, no es una buena opción para la recuperación ante desastres. Es mejor para datos archivados a los que no necesita obtener un acceso rápido.

### <a name="file-service"></a>Servicio de archivos
![Servicio de archivos de Azure](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*Figura: Servicios de archivo de Azure proporciona SMB \\ \\ecursoCompartido las rutas de acceso para aplicaciones que se ejecutan en la nube de Hola.*

De forma local, es común toohave grandes cantidades de almacenamiento de archivos accesible a través de protocolo de bloque de mensajes del servidor (SMB) de hello mediante un \\ \\ecursoCompartido formato. Azure tiene ahora un servicio que permite toouse este protocolo en la nube de Hola. Aplicaciones que se ejecutan en Azure pueden usar archivos tooshare entre máquinas virtuales con la API como ReadFile y WriteFile del sistema de archivo conocidas. Además, los archivos de hello también pueden tener acceso en hello vez a través de una interfaz REST, lo que permite recursos compartidos de hello tooaccess del entorno local cuando también se define una red virtual. Archivos de Azure se basa en el servicio de blob de hello, por lo que hereda Hola misma disponibilidad, durabilidad, escalabilidad y redundancia geográfica integrado en el almacenamiento de Azure.

**Escenarios para Archivos de Azure**

* **Migrar nube toohello de aplicaciones existente** -su más fácil toomigrate local aplicaciones toohello en la nube que utilicen el archivo comparte datos tooshare entre las partes de la aplicación hello. Cada máquina virtual conecta a recurso compartido de archivos de toohello y, a continuación, puede leer y escribir archivos tal como haría en un archivo local recurso compartido.
* **Configuración de aplicación compartida** -un patrón común para las aplicaciones distribuidas es toohave archivos de configuración en una ubicación centralizada donde puede tener acceso desde varias máquinas virtuales. Estos archivos de configuración se pueden almacenar en un recurso compartido de archivos de Azure para que lo lean todas las instancias de la aplicación. También puede administrar la configuración de Hola a través de la interfaz REST de hello, que permite el acceso en todo el mundo toohello los archivos de configuración.
* **Recurso compartido de diagnóstico** : puede guardar y compartir archivos de diagnóstico como registros, métricas y volcados de memoria. Tener estos archivos disponibles a través de SMB de Hola y de interfaz REST permite aplicaciones toouse una variedad de herramientas de análisis para procesar y analizar datos de diagnóstico de saludo.
* **Desarrollo/pruebas/Debug** : cuando los desarrolladores o los administradores trabajan en máquinas virtuales en la nube hello, que a menudo necesitan un conjunto de herramientas o utilidades. La instalación y distribución de estas utilidades en cada una de las máquinas virtuales requiere mucho tiempo. Archivos de Azure, un desarrollador o administrador puede almacenar sus herramientas favoritas en un recurso compartido de archivos y conectarse toothem desde cualquier máquina virtual.

## <a name="networking"></a>Redes
Azure hoy en día se ejecuta en varios centros de datos repartidos Hola a todos. Al ejecutar una aplicación o almacenar los datos, puede seleccionar uno o varios de estos toouse de centros de datos. También puede conectar toothese centros de datos de varias maneras mediante servicios de Hola a continuación.

### <a name="virtual-network"></a>Virtual Network
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*Figura: Redes virtuales proporciona una red privada en la nube de Hola para que distintos servicios pueden hablar tooeach Sí o recursos locales tooon si establece una conexión VPN entre entornos.*  

Una manera útil toouse una nube pública es tootreat como una extensión de su propio centro de datos.

Como puede crear VM a petición y luego eliminarlas (y dejar de pagar) cuando ya no las necesite, puede contar con el poder de la informática solo cuando lo desee. Y desde máquinas virtuales de Azure permite crear máquinas virtuales que ejecutan SharePoint, Active Directory y otro software local familiarizado, este enfoque puede funcionar con aplicaciones de hello que ya tiene.

toomake este realmente útil, sin embargo, los usuarios debería aparecer toobe pueda tootreat estas aplicaciones como si se ejecutaran en su propio centro de datos. Esto es exactamente lo que permite Red virtual de Azure. Mediante un dispositivo de puerta de enlace VPN, un administrador puede configurar una red privada virtual (VPN) entre la red local y las máquinas virtuales que están implementados tooa red virtual de Azure. Dado que asigna su propia nube toohello de direcciones IP v4 máquinas virtuales, aparecen toobe en su propia red. Los usuarios de su organización pueden tener acceso a las aplicaciones de hello esas máquinas virtuales contienen como si se ejecutaran localmente.

Para obtener más información sobre la planificación y la creación de una red virtual idónea para usted, consulte [Red virtual](virtual-network/virtual-networks-overview.md).

### <a name="express-route"></a>ExpressRoute
![ExpressRoute](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*Figura: Utiliza ExpressRoute una red Virtual de Azure, pero las conexiones de las rutas a través de líneas en lugar de con mayor rapidez dedicadas Hola Internet pública.*  

Si necesita más ancho de banda o seguridad que la que puede ofrecer Red virtual de Azure, puede fijarse en ExpressRoute. En algunos casos, ExpressRoute puede ahorarrle también algún dinero. Tendrá una red virtual en Azure, pero Hola vínculo entre Azure y el sitio utiliza una conexión dedicada que no pasa por hello Internet pública. En orden toouse para este servicio, deberá toohave un acuerdo con un proveedor de servicios de red o un proveedor de exchange.

Configuración de una conexión de ExpressRoute requiere más tiempo y planificación, por lo que conviene toostart con una VPN de sitio a sitio, a continuación, migrar tooan conexión ExpressRoute.

Para obtener más información sobre ExpressRoute, consulte [Información general técnica sobre ExpressRoute](expressroute/expressroute-introduction.md).

### <a name="traffic-manager"></a>Administrador de tráfico
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*Figura: Azure Traffic Manager permite tooroute tráfico global tooyour servicio basado en reglas inteligentes.*

Si su aplicación de Azure se ejecuta en varios centros de datos, puede usar Azure Traffic Manager tooroute solicitudes de los usuarios cambien en todas las instancias de la aplicación hello. También puede redirigir el tráfico Hola a tooservices no se ejecutan en Azure, siempre que sean accesibles desde internet.  

Puede ejecutar una aplicación de Azure con los usuarios de solo una parte única de Hola a todos en un único centro de datos de Azure. Una aplicación con usuarios dispersos en torno a Hola a todos, sin embargo, es más probable que toorun en varios centros de datos, quizás incluso todas ellas. ¿En este segundo caso, se enfrenta a un problema: cómo inteligentemente dirigir instancias de tooapplication de los usuarios? La mayoría de casos de hello, probablemente le convenga cada usuario tooaccess Hola centro de datos más cercano tooher, ya que es probable que se le ofrecerá su mejor tiempo de respuesta Hola. Pero ¿qué ocurre si esa instancia de la aplicación hello está sobrecargado o no está disponible? En este caso, podría ser toodirect "nice" automáticamente su solicitud tooanother centro de datos. Pues esto es exactamente lo que hace el Administrador de tráfico de Azure.

propietario de Hola de una aplicación define las reglas que especifican cómo las solicitudes de usuarios deben ser dirigido toodatacenters, a continuación, se basa en Traffic Manager toocarry out estas reglas. Por ejemplo, los usuarios normalmente podrían ser dirigido toohello centro de datos de Azure más cercano, pero se envíen tooanother uno cuando el tiempo de respuesta de Hola de su centro de datos predeterminado supera el tiempo de respuesta de Hola desde otros centros de datos. Para las aplicaciones distribuidas globalmente con muchos usuarios, tiene un problema de toohandle servicio integrado como estas resulta útil.

Administrador de tráfico usa puntos de conexión de servicio de nombres de directorio (DNS) tooroute usuarios tooservice, pero aún más el tráfico no pasa a través de Traffic Manager una vez realizada esa conexión. Esto impide que el Administrador de tráfico se convierta en un cuello de botella que podría ralentizar las comunicaciones de sus servicios.

## <a name="developer-services"></a>Servicios de desarrollador
Azure ofrece una serie de herramientas toohelp que los programadores y profesionales de TI crear y mantener aplicaciones en la nube de Hola.  

### <a name="azure-sdk"></a>SDK de Azure
En 2008, hello primera versión preliminar de Azure admite solo el desarrollo. NET. En la actualidad, sin embargo, puede crear aplicaciones de Azure prácticamente con cualquier lenguaje. Microsoft proporciona actualmente SDK específicos del lenguaje para .NET, Java, PHP, Node.js, Ruby y Python. También hay un SDK general de Azure que proporciona compatibilidad básica con cualquier lenguaje, como C++.  

Estos SDK le ayudan a crear, implementar y administrar aplicaciones de Azure. Se pueden encontrar en [www.microsoftazure.com](https://azure.microsoft.com/downloads/) o GitHub, y se pueden usar con Visual Studio y Eclipse. Azure también ofrece herramientas de línea de comandos que los desarrolladores pueden usar con cualquier entorno de desarrollo o editor, incluidas las herramientas para la implementación de aplicaciones tooAzure desde sistemas Linux y Macintosh.

Además de ayudarle a crear aplicaciones de Azure, estos SDK también proporcionan bibliotecas de clientes que le ayudan a crear software que utiliza servicios de Azure. Por ejemplo, podría crear una aplicación que lee y escribe los blobs de Azure o crear una herramienta que se puede implementar aplicaciones de Azure a través de la interfaz de administración de Azure Hola.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services es un nombre de marketing que abarcan un número de servicios que ayudan a las aplicaciones de toodevelop de hello Azure.

confusión tooavoid - no proporciona una versión hospedada o basada en Web de Visual Studio. Seguirá siendo necesario que disponga de una copia local de Visual Studio en ejecución. Sin embargo, pone a disposición del usuario muchas otras herramientas que pueden resultar de gran utilidad.

Sí incluye un sistema de control de código fuente denominado Team Foundation Service, que ofrece un control de las versiones y el seguimiento de elementos de trabajo.  Aún así, puede utilizar Git para el control de versiones si lo prefiere. Y puede variar sistema de control de fuente hello que utiliza al proyecto. Se pueden crear proyectos de equipo privada ilimitados accesible desde en cualquier lugar en Hola a todos.  

Visual Studio Team Services ofrece un servicio para prueba de carga. Puede ejecutar pruebas de carga creadas en Visual Studio en las máquinas virtuales en la nube de Hola. Especifique el número total de Hola de usuarios que desee tooload prueba con, y Visual Studio Team Services automáticamente determina cuántos agentes son necesarios, las máquinas virtuales de hello necesario y ejecutará las pruebas de carga. Si está suscrito a MSDN, podrá disfrutar de miles de minutos de usuario gratuitos para prueba de carga al mes.

Visual Studio Team Services ofrece también compatibilidad con el desarrollo ágil gracias a características como compilaciones de integración continua, paneles kanban y salas para equipos virtuales.

**Escenario de Visual Studio Team Services**

Visual Studio Team Services es una buena opción para las empresas que necesitan toocollaborate en todo el mundo y todavía no tiene infraestructura de hello en lugar toodo así. Puede instalarla en minutos, seleccionar un sistema de control de código fuente y empezar a escribir código y compilar ese mismo día.  herramientas de team Hola proporcionan un lugar para la coordinación y de colaboración y herramientas adicionales de Hola proporcionan tootest necesario el análisis de Hola y ajustar la aplicación rápidamente.

Pero las organizaciones que ya tienen un sistema local pueden probar los nuevos proyectos en Visual Studio Team Services toosee si resulta más eficaz.   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*Ilustración: Application Insights supervisa el seguimiento del rendimiento y el uso de su aplicación web o para dispositivo activa.*

Cuando ha publicado su aplicación, tanto si se ejecuta en dispositivos móviles, escritorios o exploradores web, Application Insights indica qué tal funciona y lo que los usuarios hacen con ella. Le ayudará a mantener un recuento de bloqueos y la respuesta es lento, alerta si Hola figuras cross umbrales inaceptables y ayudarle a diagnosticar los problemas.

Al desarrollar una nueva característica, planee toomeasure su éxito con los usuarios. Al analizar los patrones de uso, comprenderá lo que funciona mejor para sus clientes y mejorará su aplicación en cada ciclo de desarrollo.

Aunque está hospedado en Azure, Application Insights funciona con una amplia y creciente gama de aplicaciones, tanto dentro como fuera de Azure. Abarca tanto las aplicaciones web J2EE como ASP.NET, así como las aplicaciones iOS, Android, OSX y Windows. Telemetría se envía desde un SDK que se generan con la aplicación hello, toobe analiza y muestra de Hola servicio Application Insights en Azure.

Si desea que el análisis más especializado, puede exportar Hola telemetría flujo tooa base de datos, o tooPower BI o cualquier otra herramienta.

**Escenarios de Application Insights**

Está desarrollando una aplicación. Podría ser una aplicación web, una aplicación para dispositivo o una aplicación para dispositivo con un back-end web.

* Optimizar el rendimiento de saludo de la aplicación después de haberla publicado, o mientras se encuentra en la prueba de carga.  Application Insights agrega telemetría de todas las instancias de hello instalado y muestra los gráficos de tiempos de respuesta de solicitud y recuentos de excepción, tiempos de respuesta de dependencia y otros indicadores de rendimiento. Estos ayudan a optimizar el rendimiento de la aplicación. Puede insertar código tooreport datos más específicos si lo necesita.
* Detecte y diagnostique problemas en la aplicación activa. Puede recibir alertas por correo electrónico si los indicadores de rendimiento cruzan los umbrales aceptables. Puede investigar las sesiones de usuario específico, por ejemplo toosee Hola solicitud provocó una excepción.
* Realizar un seguimiento correcto de hello tooassess de uso de cada característica nueva. Al diseñar un nuevo caso de usuario, planee toomeasure cuánto se utiliza y si los usuarios alcanzar sus objetivos previstos. Visión de la aplicación proporciona datos de uso básico como las vistas de página web, y puede insertar código tootrack Hola la experiencia del usuario con más detalle.

### <a name="automation"></a>Automation
Nadie le gusta toowaste tiempo Hola manual mismo procesa una y otra vez. Automatización de Azure proporciona una manera para toocreate, supervisar, administrar e implementar recursos en el entorno de Azure.  

La automatización utiliza "runbooks", que utiliza flujos de trabajo de Windows PowerShell (en lugar de simplemente regular PowerShell) tras los bastidores de Hola. Runbooks tienen como objetivo toobe ejecutado sin interacción del usuario. Permite que los flujos de trabajo de PowerShell estado Hola de un toobe de script guardado en puntos de comprobación a lo largo de hello forma. A continuación, si se produce un error, no tiene una secuencia de comandos desde el principio de hello toostart. Puede reiniciar en el último punto de comprobación Hola. Esto ahorra mucho trabajo tratando de identificador de secuencia de comandos de hello toomake todos los errores.

**Escenarios de Automatización**

Automatización de Azure es un manual de hello tooautomate adecuados, de larga ejecución, propensas a errores y tareas repiten con frecuencia en Azure.

### <a name="api-management"></a>API Management
Creación y publicación de Interfaces de programador de aplicaciones (API) en hello internet es un tooapplications de servicios de tooprovide de manera común. Si estos servicios están puede volver a vender (por ejemplo, los datos del tiempo), una organización puede permitir que otros terceros tooaccess esos mismos servicios por una cuota. Cuando se escala a toomore asociados, podrá normalmente necesita toooptimize y controlar el acceso.  Algunos socios incluso necesitan que los datos de hello en un formato diferente.

Administración de API de Azure facilita para las organizaciones toopublish API toopartners, los empleados y los desarrolladores de aplicaciones de terceros a escala y de forma segura. Proporciona un punto de conexión de API diferentes y actúa como un proxy toocall Hola extremo real y proporcionan servicios como almacenamiento en caché, transformación, limitación de peticiones, control de acceso y agregación de análisis.

**Escenarios de Administración de API**

Supongamos que su empresa tiene un conjunto de dispositivos que se tienen toocall tooa atrás servicio central tooget datos--por ejemplo, una compañía naviera con dispositivos en cada camión en carretera Hola.  Por supuesto, empresa Hola desearán tooset tootrack de un sistema es propias camiones para que pueda predecir y actualice los tiempos de entrega de forma confiable. Es posible conocer cuántos camiones tiene y planificar en consonancia.  Cada camión será necesario un dispositivo que devuelve la llamada tooa ubicación central con su posición y velocidad de datos y quizás mucho más.

Probablemente sea un cliente de empresa de transporte de hello también se beneficiarán de estos datos de posición.  cliente de Hello podría utilizarlo tooknow ¿qué productos tienen tootravel, donde bloquea, la cantidad que pagar a lo largo de ciertas rutas (si se combina con lo que habían pagado tooship). Si Hola trasvase empresa agrega estos datos ya, muchos clientes pueden pagar por él.  Pero, a continuación, Hola trasvase empresa necesita tooprovide forma toogive clientes Hola datos. Una vez que proporcionan acceso toocustomers, no pueden tener control sobre la frecuencia con hello se consultan datos. Tienen reglas de tooprovide sobre quién puede tener acceso a los datos. Todas estas reglas tendría toobe integrada en su API externa. Es ahí donde Administración de API puede resultar útil.  

## <a name="identity-and-access"></a>Identidad y acceso
El trabajo con identidades forma parte de la mayoría de las aplicaciones. Por ejemplo, saber quién es un usuario permite que una aplicación decida cómo debe interactuar con ese usuario. Azure proporciona servicios toohelp pista identidad así como integrar con almacenes de identidades que puede que ya esté usando.

### <a name="active-directory"></a>Active Directory
Al igual que la mayoría de los servicios de directorio, Azure Active Directory almacena información acerca de los usuarios y organizaciones de Hola que pertenecen. Permite a los usuarios iniciar sesión, a continuación, se proporciona con tokens puede presentar tooapplications tooprove su identidad. También permite sincronizar la información del usuario con Windows Server Active Directory al ejecutarse en la red local. Mientras mecanismos de Hola y formatos de datos utilizados por Azure Active Directory no son idénticos a las que se usan en Windows Server Active Directory, funciones de hello realiza son muy similares.

Es importante toounderstand que Azure Active Directory está diseñado principalmente para su uso por aplicaciones en la nube. Así por ejemplo, se puede utilizar en aplicaciones que ejecutan Azure o en otras plataformas de nube. También se usa en aplicaciones de nube de Microsoft, como las de Office 365. Sin embargo, si desea tooextend su centro de datos en la nube de hello mediante máquinas virtuales de Azure y red Virtual de Azure, Azure Active Directory no elección correcta Hola. En su lugar, le interesará toorun Windows Server Active Directory en máquinas virtuales.

aplicaciones de toolet tener acceso a información de Hola que contiene, Azure Active Directory proporciona una API de REST llama Azure Active Directory Graph. Esta API permite a las aplicaciones que se ejecutan en los objetos de directorio de acceso de plataforma y sus relaciones Hola.  Por ejemplo, una aplicación autorizada puede utilizar este toolearn API sobre un usuario, que pertenece a los grupos hello y otra información. Las aplicaciones también pueden ver las relaciones entre usuarios their social gráfico-permitir que ellos trabajar de forma más inteligente con conexiones de hello entre personas.

Otra funcionalidad de este servicio, Azure Active Directory Access Control, resulta más fácil para una aplicación tooaccept información de identidad de Facebook, Google, Windows Live ID y otros proveedores de identidad populares. En lugar de requerir Hola aplicación toounderstand Hola datos diversos formatos y protocolos utilizados por cada uno de estos proveedores, Control de acceso traduce todas ellas en un solo formato común. También permite que una aplicación acepte inicios de sesión de uno o varios dominios de Active Directory. Por ejemplo, un proveedor que proporciona una aplicación SaaS podría usar a los usuarios de Azure Active Directory Access Control toogive en cada uno de sus aplicaciones de toohello de inicio de sesión único de los clientes.

Los servicios de directorio son uno de los pilares de la informática local, No debe ser sorprendente que también son importantes en la nube de Hola.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
![Azure Multi-Factor Authentication](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*Figura: La autenticación multifactor proporciona funcionalidad de Hola para su aplicación tooverify más de una forma de identificación*

La seguridad siempre es importante. Multi-factor authentication (MFA) ayuda a garantizar que sean solo los usuarios quienes obtienen acceso a sus propias cuentas. El servicio MFA (conocido también como autenticación de dos factores o "2FA") requiere que los usuarios proporcionen dos de estos tres métodos de verificación de identidades para los inicios de sesión y las transacciones de usuario.

* Un elemento que conoce (normalmente una contraseña).
* Un elemento del que dispone (un dispositivo de confianza que no se puede duplicar con facilidad, como un teléfono).
* Un elemento físico que le identifica (biométrica).

Por lo que cuando un usuario inicia sesión, puede requerir tooalso comprobar su identidad con una aplicación móvil, una llamada de teléfono o un mensaje de texto en combinación con su contraseña. De forma predeterminada, Azure Active Directory admite el uso de Hola de contraseñas como único método de autenticación para inicios de sesión de usuario. Puede usar MFA junto con Azure AD o con aplicaciones personalizadas y directorios mediante el uso de Hola MFA SDK. Puede utilizarlo junto con aplicaciones locales utilizando el Servidor Multi-Factor Authentication.

**Escenario de MFA**

Protección de inicios de sesión sobre cuentas con información delicada como inicios de sesión de bancos y acceso de código fuente donde una entrada no autorizada podría tener un elevado coste propietario intelectual o financiero.   

## <a name="mobile"></a>Móvil
Si va a crear una aplicación para un dispositivo móvil, Azure puede ayudar a almacenar los datos en la nube de hello, autenticar a los usuarios y enviar notificaciones de inserción sin necesidad de toowrite una gran cantidad de código personalizado.

Al mismo tiempo, puede crear Hola back-end para una aplicación móvil mediante máquinas virtuales, servicios en la nube o aplicaciones Web, que pueda dedicar mucho menos Hola de escritura de tiempo subyacente componentes del servicio mediante los servicios de Azure.

### <a name="mobile-apps"></a>Mobile Apps
![Aplicaciones móviles](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*Ilustración: Aplicaciones móviles ofrece una funcionalidad que requieren habitualmente las aplicaciones que interactúan con dispositivos móviles.*

Aplicaciones móviles de Azure ofrece muchas funciones útiles que le permitirán ahorrar tiempo al generar un back-end para una aplicación móvil. Permite toodo simple aprovisionamiento y administración de los datos almacenados en una base de datos de SQL. Con código del lado servidor puede utilizar fácilmente opciones adicionales de almacenamiento de datos como almacenamiento de blobs o MongoDB. Mobile Apps brinda soporte para las notificaciones, aunque en algunos casos puede usar también para ello Notification Hubs (como se describe a continuación).  servicio de Hello tiene también una API de REST que su aplicación móvil puede llamar a tooget el trabajo hecho. Aplicaciones móviles también proporciona capacidad de hello tooauthenticate a los usuarios a través de Microsoft y Active Directory, así como otros proveedores de identidades conocidas como Google, Twitter y Facebook.   

Puede usar otros servicios de Azure como roles de trabajo y de Bus de servicio y conectar sistemas tooon locales. Incluso puede consumir los complementos entidad 3rd de hello funcionalidad adicional de tooprovide de almacén de Azure (por ejemplo, SendGrid para correo electrónico).

Bibliotecas de cliente nativo para HTML/JavaScript, tienda Windows, iOS, Android y Windows Phone, que sea más fácil toodevelop para las aplicaciones en todas las principales plataformas móviles. Una API de REST permite toouse datos de servicios móviles y funcionalidad de autenticación con las aplicaciones en distintas plataformas. Un único servicio móvil puede respaldar varias aplicaciones cliente; de este modo, puede proporcionar una experiencia de usuario coherente entre dispositivos.

Dado que Azure es compatible con escala masiva ya, puede controlar tráfico hello como la aplicación se vuelve más popular.  Se admiten la supervisión y el registro toohelp solucionar problemas y administrar el rendimiento.

### <a name="notification-hubs"></a>Notification Hubs
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*Ilustración: los Centros de notificaciones ofrecen una funcionalidad que requieren habitualmente las aplicaciones que interactúan con dispositivos móviles.*

Aunque puede escribir código toodo notificaciones en aplicaciones móviles de Azure, los centros de notificaciones es optimizado toobroadcast millones de notificaciones de inserción muy personalizada en minutos.  No es necesario tooworry sobre detalles como el operador de telefonía móvil o el fabricante del dispositivo. Puede dirigirse a individuos o millones de usuarios con una sola llamada de API.

Los centros de notificaciones es toowork diseñada con cualquier back-end. Puede utilizar aplicaciones móviles de Azure, un back-end personalizado en la nube de hello con cualquier proveedor o un servidor local.

**Escenarios de concentrador de notificación** si estuviera escribiendo un juego móvil donde reproductores tuvieron activa, puede que necesite toonotify Reproductor 2 este jugador 1 finalizado su turno. Si eso es todo lo que necesita toodo, que puede usar aplicaciones móviles. Pero si tenía 100.000 usuarios jugar a un juego y desea toosend vez tooeveryone confidencial oferta gratuita, centros de notificaciones es Hola mejor opción.

Puede enviar noticias de última hora, deportivos eventos y notificaciones toomillions de anuncio de producto de los usuarios con una latencia baja. Las empresas pueden notificar a sus empleados acerca de la nueva hora confidencial las comunicaciones, como clientes potenciales, por lo que los empleados no tienen tooconstantly comprobar correo electrónico u otro toostay aplicaciones informado. También puede enviar contraseñas válidas una sola vez requeridas para la autenticación multifactor.

## <a name="back-up"></a>Copia de seguridad
Cada empresa necesita toobackup y restaurar datos. Puede usar Azure toobackup y restaurar la aplicación ya sea en nube de Hola o de forma local. Azure ofrece diferentes opciones toohelp según tipo hello de copia de seguridad.

### <a name="site-recovery"></a>Site Recovery
Azure Site Recovery (anteriormente Administrador de recuperación de Hyper-V) puede ayudarle a proteger las aplicaciones importantes, se coordina Hola replicación y la recuperación en todos los sitios. Recuperación de sitio proporciona funcionalidad tooprotect aplicaciones basada en Hyper-v, VMWare o SAN tooyour propio sitio secundario, sitio del proveedor de hospedaje de tooa o tooAzure y evitar gastos de Hola y la complejidad de generar y administrar su propia ubicación secundaria. Azure cifra los datos y las comunicaciones y es necesario opción Hola habilite el cifrado de datos en reposo demasiado.

Supervisa continuamente el estado de Hola de los servicios y ayuda a automatizar la recuperación ordenada de hello de servicios en caso de hello de una interrupción en el sitio en el centro de datos principal de Hola. Máquinas virtuales se pueden administrar en un servicio de restauración de modo orquestaciones toohelp rápidamente, incluso para cargas de trabajo complejas de varios niveles.

Recuperación de sitios funciona con tecnologías existentes como Hyper-V Replica, System Center y SQL Server AlwaysOn. Consulte [Información general sobre Azure Site Recovery](site-recovery/site-recovery-overview.md) para obtener más detalles.

### <a name="azure-backup"></a>Copia de seguridad de Azure
![Azure Backup](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*Figura: Copia de seguridad de Azure realiza una copia de datos de servidores de Windows local en la nube de Hola.*  

Copia de seguridad de Azure realiza una copia de seguridad de los datos desde servidores locales que ejecutan Windows Server en la nube de Hola. Puede administrar las copias de seguridad directamente desde las herramientas de copia de seguridad de hello en Windows Server 2012, Windows Server 2012 Essentials o System Center 2012 - Data Protection Manager. También es posible utilizar un agente especializado de copia de seguridad.

Los datos están más seguros porque las copias de seguridad se cifran antes de la transmisión y se almacenan cifradas en Azure con la protección de un certificado que cargue. servicio de Hello usa Hola detecta que la misma protección de datos de alta disponibilidad y redundancia en el almacenamiento de Azure.  Puede hacer copias de seguridad de archivos y carpetas de manera programada o de inmediato, ejecutando copias de seguridad completas o incrementales. Después de datos se copian en la nube toohello, los usuarios autorizados pueden recuperar fácilmente server tooany de copias de seguridad. También ofrece las directivas de retención de datos configurable, compresión de datos y transferencia de datos de limitación para que pueda administrar Hola costo toostore y transferencia de datos.

**Escenarios de Copia de seguridad de Azure**

Si ya utiliza Windows Server o System Center, Copia de seguridad de Azure es la solución natural para hacer una copia de seguridad del sistema de archivos de servidores, máquinas virtuales y bases de datos de SQL Server.  Funciona con archivos cifrados, dispersos y comprimidos. Existen algunas limitaciones, por lo que debería [comprobar requisitos previos de copia de seguridad de Azure de hello](http://technet.microsoft.com/library/dn296608.aspx) primero.

## <a name="messaging-and-integration"></a>Mensajería e integración
Con independencia de lo que está haciendo, el código con frecuencia necesita toointeract con otro código.  En algunos casos, todo lo que hace falta es mensajería básica en cola. En otros, se requieren interacciones más complejas. Azure proporciona unos toosolve de maneras diferentes de estos problemas. La figura 5 muestra las opciones de Hola.

### <a name="queues"></a>Colas
![Retransmisión de bus de servicio de Azure](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*Ilustración: Las colas permiten un acoplamiento flexible entre las partes de una aplicación y facilitan el escalado.*  

Su concepto es sencillo: una aplicación coloca un mensaje en una cola y al final otra aplicación lee ese mensaje. Si la aplicación necesita este servicio de sencillo, las colas de Azure podría ser mejor opción de Hola.

Debido a Hola Hola de manera que Azure ha crecido con el tiempo, colas de almacenamiento de Azure y colas de Service Bus proporcionan servicios similares de puesta en cola. Hola razones por las que podría toouse sobre Hola otros se tratan en hello bastante notas [colas de Azure y colas de Service Bus: comparación y diferencias](http://msdn.microsoft.com/library/azure/hh767287.aspx).  En la mayoría de escenarios, cualquiera de los dos funcionará.

**Escenarios de Colas**

Un uso común de las colas de hoy en día es toolet una instancia de rol web comunicarse con una instancia de rol de trabajo dentro de Hola misma aplicación de servicios en la nube.

Por ejemplo, supongamos que crea una aplicación de Azure para compartir vídeo. aplicación Hello consta de código PHP que se ejecuta en un rol web que permite a los usuarios cargarán y ver vídeos, junto con un rol de trabajo implementado en C# que traduce cargado vídeo en varios formatos.

Cuando una instancia de rol web recibe un nuevo vídeo de un usuario, puede almacenar vídeo hello en un blob, a continuación, enviar un rol de trabajo tooa de mensaje a través de una cola indicándole que toofind este nuevo vídeo. Una instancia de rol de trabajo-it no importa qué mensaje Hola will uno, a continuación, lectura de cola de Hola y llevar a cabo traducciones de vídeo de hello necesario en segundo plano de Hola.

Al estructurar una aplicación de esta manera permite el procesamiento asincrónico y también realiza Hola aplicación tooscale más fácil, ya que el número de Hola de instancias de rol web y las instancias de rol de trabajo puede variar de forma independiente. También puede utilizar el tamaño de la cola de hello desencadenador tooscale hello en número de roles de trabajo hacia arriba y abajo. Si sube demasiado, agrega más roles. Cuando obtiene inferior, puede reducir Hola número de roles en ejecución toosave dinero.  

Puede utilizar este mismo modelo entre muchas partes diferentes de su aplicación incluso aunque no utilicen roles web y de trabajo.  Le permite tooscale partes de Hola a cada lado de la cola de hello arriba o abajo como demanda y requiere tiempo de procesamiento.

### <a name="service-bus"></a>Bus de servicio
Si se ejecutan en la nube de hello, en el centro de datos, en un dispositivo móvil o en otro lugar, las aplicaciones necesitan toointeract. objetivo de Hola de Bus de servicio de Azure es aplicaciones toolet ejecuta prácticamente desde cualquier lugar intercambian datos.

Suma toohello colas (uno a uno) se ha descrito anteriormente, Bus de servicio también proporciona tooother métodos de comunicación.

#### <a name="service-bus-relay"></a>Service Bus Relay
![Retransmisión de bus de servicio de Azure](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*Ilustración: La Retransmisión de bus de servicio permite la comunicación entre aplicaciones en diferentes lados de un firewall.*

Bus de servicio permite la comunicación directa a través de su servicio de retransmisión, proporcionando un toointeract de forma segura a través de firewalls. Retransmisiones de Bus de servicio permiten toocommunicate de aplicaciones mediante el intercambio de mensajes a través de un extremo hospedado en nube de hello, en lugar de localmente.

**Escenarios de Retransmisión de bus de servicio**

Las aplicaciones que se comunican a través del Bus de servicio pueden ser aplicaciones de Azure o software que se ejecute en alguna otra plataforma de nube. También pueden ser aplicaciones que se ejecutan fuera de hello en la nube, sin embargo. Por ejemplo, piense en una línea aérea que implementa servicios de reservas en equipos dentro de su propio centro de datos. airline Hola debe tooexpose estos servicios toomany los clientes, incluidos en el repositorio quioscos en aeropuertos, los terminales de agente de reserva y los teléfonos o incluso de los clientes. Debería usar toodo de Bus de servicio esta opción, crear interacciones con acoplamiento flexible entre Hola varias aplicaciones.

#### <a name="service-bus-topics-and-subscriptions"></a>Temas y suscripciones del Bus de servicio
![Temas de Service Bus de Azure](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *Figura: Temas de Bus de servicio permite que varias aplicaciones toopost mensajes y otras aplicaciones toosubscribe tooreceive que cumplen unos determinados criterios.*

Bus de servicio ofrece un mecanismo de publicación y suscripción denominado Temas y Suscripciones. Con publish-subscribe, una aplicación puede enviar tema tooa de mensajes, mientras que otras aplicaciones pueden crear tema toothis de suscripciones. Esto permite la comunicación de uno a varios entre un conjunto de aplicaciones, permitiendo Hola mismo mensaje ser leído por varios destinatarios.

**Escenarios de temas y suscripciones del Bus de servicio**

Cada vez que está configurando donde hay muchos mensajes que son importantes, pero varios sistemas de nivel inferiores solo necesitan toolisten toodiffering subconjuntos de las comunicaciones, el tema de Bus de servicio y las suscripciones son una buena opción.

### <a name="biztalk-services"></a>Servicios de BizTalk
![Servicios de BizTalk](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *Figura: Servicios de BizTalk proporciona formatos de mensajes de Hola capacidad tootransform XML en la nube de Hola.*

En ocasiones requiere conectar sistemas que se comunican mediante diferentes formatos de mensajería. Es común que los esquemas de base de datos diferente de toohave comerciales y mensajería formatos, incluso cuando hay un estándar común de XML. En lugar de escribir una gran cantidad de código personalizado, puede usar BizTalk Server local toointegrate varios sistemas.  Servicios de BizTalk de Azure proporciona Hola mismo tipo de servicio, pero en la nube de Hola. Puede abonar solo lo que utiliza y no se preocupe sobre la escala como tendría tooon local.

**Escenarios de servicios de BizTalk**

Normalmente, las interacciones de negocio a negocio (B2B) requieren este tipo de traducción.  Por ejemplo, una empresa crear aviones necesidades tooorder partes de él es proveedores de varias partes. Seguramente tendrá muchos proveedores de piezas.  Los pedidos deben toogo automatizada directamente desde sistemas de generadores de avión de hello en sistemas de proveedores de Hola.  Ninguna empresa desea toochange sus sistemas principales y los formatos de mensaje y es muy poco probable que estos formatos son Hola igual. Servicios de BizTalk puede tomar mensajes y traducir entre los nuevos formatos de hello ambas formas. Cualquier proveedor de avión Hola puede Hola tootranslate de trabajo u Hola varios proveedores can, dependiendo de que quiere más cantidad de hello y control de traducción que sea necesario.     

## <a name="compute-assistance"></a>Asistencia de proceso
Azure proporciona ayuda para los servicios que no es necesario toorun todo el tiempo Hola.  

### <a name="scheduler"></a>Scheduler
![Azure Scheduler](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*Figura: El programador de Azure proporciona una manera tooschedule trabajos en un momento dado para una determinada duración.*

A veces las aplicaciones solo necesitan toorun en un momento determinado. En Azure, puede ahorrar dinero con este tipo de aplicación en lugar de permitir que una aplicación solo ejecutándose esperando datos tooprocess 24 x 7. El programador de Azure permite tooschedule cuando una aplicación debe ejecutar basándose en el intervalo de tiempo o un calendario. Es confiable y verificará que un proceso se ejecuta incluso si existen errores de red, equipo o centro de datos. Utilice Hola API de REST de Scheduler toomanage estas acciones.

Cuando se produzca una alarma programada, programador envía HTTP o HTTPS mensajes tooa punto de conexión concreto o puede colocar un mensaje en una cola de almacenamiento.  Por lo que necesita toohave la aplicación tiene un punto de conexión puede tener acceso o tiene supervisar una cola de almacenamiento. A continuación, una vez que obtiene el mensaje de bienvenida, puede realizar cualquier acción que esté programado para.

**Escenarios del Programador**

* Acciones de aplicación se repiten: por ejemplo, un servicio periódicamente puede obtener datos de twitter y recopilar datos de hello en una fuente regular.
* Mantenimiento diario: procesamiento o eliminación de registros, realización de copias de seguridad y otras tareas de programación a intervalos.
* Tareas que se ejecutan de noche.
* Tareas de aplicaciones web, como eliminación diaria de registros, realización de copias de seguridad y otras tareas de programación a intervalos. Un administrador puede elegir toobackup su base de datos a la 1 A.M. cada día para hello próximo 9 meses, por ejemplo.

Hola API de Scheduler permite toocreate, actualizar, eliminar, ver y administrar colecciones de trabajos y trabajos programados mediante programación.

## <a name="performance"></a>Rendimiento
El rendimiento es siempre importante para una aplicación. Las aplicaciones suelen tooaccess Hola una y otra vez los mismos datos. Rendimiento de una manera de tooimprove se tookeep una copia de esa aplicación de datos más cerca de toohello, minimizar tiempo Hola necesita tooretrieve. Azure proporciona servicios diferentes para este fin:

### <a name="azure-caching"></a>Almacenamiento en caché de Azure
![Almacenamiento en caché de Azure](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **Ilustración: Una aplicación de Azure puede almacenar datos de caché en la memoria e incluso dividirlos entre muchos roles de trabajo**

Tener acceso a los datos almacenados en alguno de los servicios de administración de datos de Azure (Base de datos SQL, tablas o blobs) es bastante rápido. Pero tener acceso a los datos almacenados en memoria es incluso más rápido. Como consecuencia, mantener en memoria una copia de los datos a los que se tiene acceso con mayor frecuencia puede mejorar el rendimiento de la aplicación. Ya puede utilizarla toodo de almacenamiento en caché en memoria de Azure.

Una aplicación de servicios en la nube puede almacenar datos en memoria caché, a continuación, recuperar directamente sin necesidad de tooaccess el almacenamiento persistente. caché de Hola se puede mantener en la aplicación de las máquinas virtuales o proporcionarse en las máquinas virtuales dedicados exclusivamente toocaching. En cualquier caso, se puede distribuir la memoria caché de hello, con datos de Hola que contiene propagación a través de varias máquinas virtuales en un centro de datos de Azure.

Azure cuenta con varias tecnologías diferentes de caché que han cambiado con el tiempo. En el orden de Hola que se introducen, hay una compartida, en rol, administra y caché de Redis. Hola compartida el almacenamiento en caché es una tecnología antigua y no debe crear nuevas implementaciones con él. Hello memoria caché administrada tiene Hola mismas características de hello en rol de caché, pero como servicio administrado fuera de Hola Portal de administración de Azure. Hola caché en Redis está en vista previa. implementación de Redis Hola con mayor número de características de Hola y se recomienda al escribir un nuevo código de almacenamiento en caché.

**Escenarios de Caché de Azure**

Una aplicación que lee repetidamente un catálogo de productos podría beneficiarse del uso de este tipo de almacenamiento en caché, por ejemplo, ya que los datos de hello necesita estará disponible más rápidamente. tecnología de Hello también admite el bloqueo, dejar que se puede usar con la lectura/escritura, así como datos de solo lectura. Y las aplicaciones ASP.NET pueden usar datos de la sesión de hello servicio toostore con un cambio de configuración.

### <a name="content-delivery-network"></a>Content Delivery Network
![Red CDN de Azure](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **Figura: Copias de un blob pueden se almacenen en caché alrededor de Hola a todos los sitios.**

Supongamos que necesita datos de blob de toostore que vayan a tener acceso a los usuarios alrededor de Hola a todos. Quizá sea un vídeo de hello más reciente Copa del mundo coincidencia, por ejemplo, actualizaciones de controladores o un libro electrónico popular. Almacenar una copia de datos de hello en varios centros de datos de Azure le ayudará a, pero si hay una gran cantidad de usuarios, probablemente no es suficiente. Para obtener un rendimiento incluso mejor, puede usar Hola CDN de Azure.

CDN Hola tiene docenas de sitios alrededor de Hola a todos, cada uno de ellos capaz de almacenar copias de blobs de Azure. Hello primera vez que un usuario en alguna parte de Hola a todos tiene acceso a un blob determinado, información de Hola que contiene se copia desde un centro de datos de Azure en el almacenamiento local de red CDN en esa ubicación geográfica. Después de esto, accesos de ese elemento de Hola a todos utilizará la copia de blob de hello en caché en la red CDN Hola-no necesitan toogo todos los toohello de manera hello más cercano de centro de datos de Azure. resultado de Hello es más rápido acceso a datos de toofrequently tiene acceso a los usuarios en cualquier lugar de Hola a todos.

**Escenarios de red CDN**

Es común toouse CDN con vídeo de toodeliver de servicios multimedia en todo el mundo. El vídeo normalmente tiene un gran tamaño y requiere mucho ancho de banda.  Ya se ha hablado también de Servicios multimedia en esta página.

## <a name="big-data-and-big-compute"></a>Big Data y Big Compute
### <a name="hdinsight-hadoop"></a>HDInsight (Hadoop)
![HDInsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **Figura: HDInsight facilitará el proceso masivo de Hola de grandes cantidades de datos**

Durante muchos años, masiva Hola de análisis de datos se ha realizado en los datos relacionales almacenados en un almacén de datos que se generan con un DBMS relacional. Este tipo de análisis de negocios es importante y será para un toocome mucho tiempo. Pero ¿qué ocurre si están tan grandes que las bases de datos relacionales simplemente no pueden controlarla datos Hola desea tooanalyze? ¿Y suponga que los datos de hello no son relacionales? Podrían ser, por ejemplo, registros del servidor o datos de sucesos históricos de sensores o de alguna otra cosa. En este caso, tiene lo que se conoce como un problema de Big Data. Y necesita otro enfoque.

Hola la tecnología dominante hoy en día para analizar grandes cantidades de datos es Hadoop. Proyecto de código abierto de un Apache, esta tecnología almacena los datos mediante el sistema de archivos distribuido de Hadoop (HDFS) hello, y permite a los programadores crear MapReduce trabajos tooanalyze esos datos. HDFS Reparta los datos entre varios servidores, a continuación, fragmentos de ejecuciones del trabajo de MapReduce de hello en cada uno de ellos, permitiendo grandes cantidades de datos de Hola se procesan en paralelo.

HDInsight es nombre Hola Hola de Apache Hadoop-based del servicio de Azure. HDInsight permite HDFS almacenar datos en clúster de Hola y distribuir entre varias máquinas virtuales. También se propaga lógica Hola de un trabajo MapReduce a través de esas máquinas virtuales. Igual que con Hadoop local, los datos son lógica procesados localmente: hello y datos Hola funciona en Hola misma VM- y en paralelo para mejorar el rendimiento. HDInsight también puede almacenar los datos en Azure Storage Vault (ASV), que utiliza blobs.  Usar ASV podrá toosave dinero porque puede eliminar el clúster de HDInsight cuando no esté en uso, pero mantener los datos en la nube de Hola.

HDinsight es compatible con otros componentes del ecosistema de Hadoop de hello, incluidos Hive y Pig. Microsoft también ha creado los componentes que hacen que sea más fácil toowork con los datos generados por HDInsight mediante herramientas tradicionales de BI, como adaptador de HiveODBC de Hola y el Explorador de datos que funcionan con Excel.

### <a name="high-performance-computing-big-compute"></a>Informática de alto rendimiento (Big Compute)
Uno de toouse de maneras muy útil de hello una plataforma de nube es toorun informática de alto rendimiento (HPC) y otras aplicaciones "Big Compute". Algunos ejemplos son especializada toouse aplicaciones compiladas ingeniería Hola interfaz estándar del sector de paso de mensajes (MPI), así como aplicaciones embarazosamente paralelas denominadas, estos modelos de riesgos financieros.

esencia Hola de Big Compute se está ejecutando código en muchas máquinas en hello mismo tiempo. En Azure, esto significa que muchas máquinas virtuales en ejecución al mismo tiempo, todo funciona en paralelo toosolve algún problema. Esta acción requiere algunas forma tooresources y tooschedule aplicaciones, es decir, toodistribute su trabajo entre estas instancias. Módulo de HPC gratuito de Microsoft y otras soluciones de clúster de cálculo pueden realizar bien en Azure, sacar partido de los servicios de proceso y la infraestructura Azure tooadd capacidad a petición tooan local clúster de cálculo o ejecutan aplicaciones de Big Compute completamente en hello en la nube.

Azure proporciona un intervalo de VM tamaños de instancias diferentes configuraciones de núcleos de CPU, memoria, capacidad de disco y otros requisitos de características toomeet Hola de distintas aplicaciones. Hola introdujo recientemente A8 y A9 trabajo de instancias también para muchos proceso cargas de trabajo intensivas y aplicaciones MPI en paralelo en concreto, ya que tienen alta velocidad, CPU de varios núcleos y grandes cantidades de memoria. En determinadas configuraciones de instancias de hello aprovechar las ventajas de una red de aplicaciones de baja latencia y alto rendimiento en la nube de Hola que incluye tecnología de memoria directa remota (RDMA) de acceso para la máxima eficiencia de las aplicaciones de MPI paralelas.

Asimismo, Azure ofrece a socios y desarrolladores de aplicaciones de Big Compute un completo conjunto de funcionalidades de proceso, servicios, opciones de arquitectura y herramientas de desarrollo. Azure admite Big Compute flujos de trabajo personalizados que implican los flujos de trabajo de datos especializado y trabajos y tareas de programación de patrones que se pueden escalar toothousands de núcleos de proceso.

## <a name="media"></a>Multimedia
![Azure Media Services](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **Figura: Servicios multimedia es una plataforma para aplicaciones que proporcionan vídeo y otros tooclients medios alrededor de Hola a todos.**

Gran parte del tráfico de Internet actual lo constituye el vídeo, y ese porcentaje será incluso mayor en el futuro. Proporcionar aún vídeo en web de hello no es simple. Hay una gran cantidad de variables, como Hola hello y algoritmo de codificación mostrar la resolución de pantalla del usuario de Hola. Vídeo también suele toohave picos de demanda, como un pico sábado por la noche, cuando decida de muchas personas que les gustaría usar toowatch una película en línea.

Dada su popularidad, es seguro que se van crear muchas aplicaciones que utilicen vídeo. Pero todas ellas necesitará toosolve algunas de hello mismo problemas y hacer que cada uno de ellos a resolver esos problemas por sí mismo no tiene sentido. Un enfoque más adecuado es una plataforma que proporciona soluciones comunes para muchas de las aplicaciones toouse toocreate. Y la creación de esta plataforma en la nube de hello tiene algunas ventajas claras. Puede ser ampliamente disponible en forma de pago por uso, y puede controlar la variabilidad de hello en la demanda que a menudo se enfrentan a aplicaciones de vídeo.

Servicios multimedia de Azure soluciona este problema al proporcionar un conjunto de componentes de nube que permiten que la gente pueda crear y ejecutar fácilmente aplicaciones que utilizan vídeo y otro contenido multimedia.

Como se muestra en la figura hello, servicios multimedia proporciona un conjunto de componentes para las aplicaciones que funcionan con vídeo y otros archivos multimedia. Por ejemplo, incluye un medio de la ingesta de vídeo de tooupload de componente en servicios multimedia (donde se almacenan en Blobs de Azure), un componente de codificación que es compatible con diversos formatos de vídeo y audio, un componente de protección de contenido que proporciona administración de derechos digitales un componente para insertar anuncios en una secuencia de vídeo, componentes de transmisión por secuencias y mucho más. Los socios de Microsoft pueden también proporcionan componentes para la plataforma de Hola y luego tener Microsoft distribuir los componentes y se le facturará en su nombre.

Las aplicaciones que utilizan esta plataforma se pueden ejecutar en Azure o en cualquier otra plataforma. Por ejemplo, una aplicación de escritorio para una casa de producción de vídeo puede permitir que sus usuarios cargar servicios tooMedia vídeo, a continuación, procesarlo de varias maneras. Como alternativa, un servicio de administración de contenido basado en la nube que se ejecuta en Azure puede confiar en servicios multimedia tooprocess y distribuir vídeo. Donde se ejecuta y lo que lo hace, cada aplicación elige qué componentes necesita toouse, obtener acceso a ellos a través de interfaces RESTful.

toodistribute lo que produce, una aplicación puede utilizar Hola CDN de Azure, CDN otro, o enviado directamente bits toousers. Sea cual sea la forma en que llegue allí, el vídeo creado usando Servicios multimedia se puede consumir a través de varios sistemas cliente, como Windows, Macintosh, HTML 5, iOS, Android, Windows Phone, Flash y Silverlight. el objetivo de Hello es toomake sea más fácil toocreate multimedia modernas aplicaciones.

**Referencias**

Para obtener una vista más visual del funcionamiento de los servicios multimedia, descargue hello [póster de servicios multimedia de Azure][Azure Media Services Poster].

## <a name="commerce"></a>Comercio
aumento de Hola de Software como servicio está transformando ¿cómo crear aplicaciones. Y también está transformando el modo en que las vendemos. Puesto que una aplicación SaaS vive en la nube de hello, tiene sentido que sus clientes potenciales deben buscar soluciones en línea. Y aplica este cambio toodata, así como tooapplications. ¿Por qué no deben personas parecen toohello en la nube para conjuntos de datos disponibles en el mercado? Microsoft soluciona ambos de estos problemas con hello [Azure Marketplace](https://azure.microsoft.com/marketplace/).

![Comercio de Azure](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **Ilustración: Azure Marketplace y la Tienda de Azure le permiten buscar y comprar aplicaciones y conjuntos de datos comerciales de Azure y usarlos como parte de las aplicaciones de Azure.**

Hello diferencia entre Hola dos es que Marketplace es fuera Hola Portal de administración de Azure, pero Hola almacén puede tener acceso desde dentro de hello portal. Clientes potenciales pueden buscar toofind Azure aplicaciones que satisfagan sus necesidades. Los clientes también pueden buscar en cualquiera de ellos conjuntos de datos comerciales, como datos demográficos, datos financieros, datos geográficos y muchos más. Cuando encuentra algo que deseen, que pueden accedan a él desde el proveedor de hello, directamente a través de Marketplace de Hola o ubicaciones del almacén web o en algunos casos de hello Portal de administración. Aplicaciones también pueden utilizar Hola API de búsqueda de Bing a través de hello Marketplace, concederles acceso toohello resultados de búsquedas en el web.

**Escenarios de Comercio**

SendGrid es una aplicación Hola almacén de Azure que permite correo electrónico toosend. Ofrece funcionalidad adicional como estadísticas y entrega confiable.  Puede comprar esta aplicación y los servicios relacionados en lugar de pruebe toobuild dicha infraestructura usted mismo.  

## <a name="getting-started"></a>Introducción
Ahora que tiene el siguiente paso de hello panorama, hello es toowrite su primera aplicación de Azure. Elija su idioma, [obtener Hola SDK adecuado](/downloads/)y hágalo ahora. Cloud computing es el valor predeterminado nuevo de hello--empezar ahora.

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
