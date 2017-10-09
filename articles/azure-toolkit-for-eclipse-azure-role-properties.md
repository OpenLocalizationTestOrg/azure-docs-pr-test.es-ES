---
title: "Propiedades de la función aaaAzure"
description: "Obtenga información acerca de cómo toouse Hola Kit de herramientas de Azure para la configuración de rol de Azure tooconfigure de Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a>Propiedades de roles de Azure
Diversas opciones de configuración para el rol de Azure pueden establecerse en hello Azure Toolkit for Eclipse.

## <a name="configuring-azure-role-properties"></a>Configuración de propiedades de roles de Azure
Configurar las propiedades de rol de Azure se logra a través de los cuadros de diálogo de propiedades de hello para el rol de trabajo. Menú contextual de hello abierto para rol de hello en hello select y el panel del explorador de proyectos de Eclipse **Azure** submenú. (Si no ve el rol de Hola Hola Explorador de proyectos de Eclipse, expanda el proyecto de Azure en el Explorador de proyectos).

![][ic789599]

Hola varias propiedades que pueden establecerse entre hello **propiedades** en este tema se describen los cuadros de diálogo. Tenga en cuenta que muchas de las propiedades se rellenan automáticamente al crear un nuevo proyecto de implementación de Azure.

Hola después de páginas de propiedades está disponible para roles de Azure.

* [Propiedades de máquina virtual](#virtual_machine_properties)
* [Propiedades de almacenamiento en caché](#caching_properties)
* [Propiedades de certificados](#certificates_properties)
* [Propiedades de componentes](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [Propiedades de puntos de conexión](#endpoints_properties)
* [Propiedades de variables de entorno](#environment_variables_properties)
* [Propiedades de equilibrio de carga y de afinidad de la sesión (conocidas también como "sesiones temporales")](#session_affinity_properties)
* [Propiedades de almacenamiento local](#local_storage_properties)
* [Propiedades de configuración de servidor](#server_configuration_properties)
* [Propiedades de la descarga de SSL](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>Propiedades de máquina virtual
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **propiedades**, y se tiene el tamaño de máquina virtual de hello capacidad toochange hello así como cambiar número de Hola de instancias, como se muestra en hello después de la imagen.

![][ic719499]

> [!NOTE]
> Solo Windows: cuando se establece Hola número de instancias tooa valor mayor que 1 y también configurar un servidor de aplicaciones, el Kit de herramientas de hello permite solo 1 toorun de instancia de rol en el emulador de Windows hello, independientemente de esta configuración. Se trata de conflictos de enlace de puerto de tooavoid entre Hola distintas instancias de servidor (por ejemplo, todos los tratar toobind tooport 8080) cuando se ejecutan en hello mismo equipo. Se conserva el configuración del número de instancia que desee, pero solo entra en vigor solo cuando se implementa en la nube toohello.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Propiedades de almacenamiento en caché
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **almacenamiento en caché**. En este cuadro de diálogo, puede habilitar colocadas compatibles con memcache memorias caché con nombre, lo que le toohelp velocidad a las aplicaciones web.

![][ic719483]

Dentro de hello **Caching** página de propiedades, puede especificar la configuración global para hello siguientes:

* Si el almacenamiento en caché colocado está habilitado.
* tamaño de caché de Hola como un porcentaje de memoria.
* nombre de cuenta de almacenamiento de Hola para guardar el estado de la caché de hello cuando la aplicación se ejecuta como un servicio en la nube o none si no desea que toosave Hola caché. (nombre de cuenta de almacenamiento de hello no se usa al ejecutar la aplicación en el emulador de proceso de hello). Si establece el nombre de cuenta de almacenamiento de hello demasiado**(auto)** (que es la predeterminada de hello), la configuración de almacenamiento en caché usará automáticamente Hola la misma cuenta de almacenamiento como uno que seleccione en Hola Hola **publicar tooAzure**cuadro de diálogo.

> [!NOTE]
> Hola **(auto)** configuración tendrá efecto de hello deseado solo si se publica la implementación mediante Hola Eclipse toolkit Asistente para la publicación. Si en su lugar publica el archivo de hello .cspkg manualmente mediante un mecanismo externo, como Hola [Portal de administración de Azure][Azure Management Portal], implementación de hello no funcionará correctamente.
> 
> 

Hola después el cuadro de diálogo muestra las propiedades de Hola de una memoria caché.

![][ic719501]

* **Nombre:** nombre Hola de hello colocados caché.
* **Número de puerto:** Hola toouse de número de puerto para caché de Hola.
* **Directiva de caducidad:** uno Hola después valores que especifica cuándo expira una clave de caché de Hola.
  * **Absoluto:** clave Hola expira cuando lo especifica el tiempo de hello **minutos toolive** se alcanza.
  * **NeverExpires:** Hola clave no tiene una fecha de caducidad.
  * **SlidingWindow:** clave Hola expira si no se ha accedido durante Hola de tiempo especificado por **toolive minutos**; cada vez que se tiene acceso, se restablece el reloj de expiración de Hola.
* **Minutos toolive:** número máximo de minutos de una clave de memcached toolive, toohello la directiva de expiración del firmante.
* **Alta disponibilidad con copias de seguridad replicadas en distintas instancias de rol:** si esta opción está habilitada, ayuda a proporcionar alta disponibilidad mediante copias de seguridad replicadas en distintas instancias de rol. Tenga en cuenta que al menos dos instancias de rol deben estar en vigor para la implementación para esta característica toowork.

tooadd una nueva memoria caché, haga clic en hello **agregar** botón en hello **Caching** página de propiedades y un **Configure Named Cache** se abrirá el cuadro de diálogo. Proporcionar valores para las propiedades de Hola que se describen anteriormente.

toomodify una caché con nombre, seleccione la caché hello y haga clic en hello **editar** botón en hello **Caching** página de propiedades. Se abrirá un cuadro de diálogo Permitir toomodify Hola propiedades de caché. Presione **Aceptar** valores de caché toosave Hola.

toodelete una memoria caché, seleccione la caché hello y haga clic en hello **quitar** botón en hello **Caching** página de propiedades y, a continuación, haga clic en **Sí** eliminación de hello tooconfirm.

Para obtener más información acerca de cómo toouse almacenamiento en caché, vea [cómo tooUse colocados Caching][How tooUse Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Propiedades de certificados
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **certificados**.

![][ic710964]

En este cuadro de diálogo, puede agregar o quitar certificados a los que se haga en el proyecto de Eclipse. Tenga en cuenta que los certificados de hello enumerados aquí no se almacenan automáticamente en cualquier almacén de claves de Java y por lo tanto, no estarán disponibles automáticamente para ningún uso desde dentro de una aplicación de Java. Solo se registran con Azure para que se puedan precargar en hello Windows almacenar en máquinas virtuales de hello ejecutando la implementación de certificado y se utilizará posteriormente con otro software de Windows. Hola actualmente, solo la característica del Kit de herramientas de Hola que utiliza certificados de hello hace referencia a esta forma en hello **certificados** cuadro de diálogo es [la descarga de SSL][SSL Offloading], debido tooits dependencia de los servicios de Internet Information Server (IIS) y la aplicación de enrutamiento de solicitud (ARR), que requieren Hola toobe certificado adecuado a disposición de esta manera.

Al implementar su tooAzure de proyecto mediante el Asistente para publicación de hello, será toopoint solicitada en hello Personal Information Exchange (PFX) archivos correspondientes certificados toothese, junto con sus contraseñas, en orden tooautomatically cargarlos toohello Servicio de Azure, pero solo si ha no se han cargado previamente.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Propiedades de componentes
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **componentes**. Dentro de este cuadro de diálogo, se tiene Hola capacidad tooadd, modificar, o quitar componentes de Hola de su rol, así como cambiar orden de hello en el que se procesan.

![][ic719502]

característica de componentes de Hello permite proyecto de implementación de Azure de tooyour de tooadd dependencias, como proyectos de aplicaciones Java, archivos especiales y las instrucciones de línea de comandos ejecutable que son necesarios para la implementación.

Para cada componente, se puede especificar:

* paso de Hello toobe seguirse al importar el componente de hello en el proyecto de implementación de Azure cuando se crea.
* paso de Hello toobe cuidado al implementar ese componente en hello nube de Azure.

> [!NOTE]
> Al especificar archivos de componentes o líneas de comandos, tenga en cuenta que la implementación de máquina virtual de Windows de tooa publicado, por lo que los pasos personalizados deben ser válidos para un sistema operativo basado en Windows. 
> 
> 

Los componentes tienen Hola propiedades siguientes:

* **Importación:** método que indica cómo se importarán los componente de hello en proyecto de hello cuando se compila el proyecto de Hola. Esto puede ser uno de hello siguientes valores:
  * **copia:** se copia el componente de Hola Hola ruta de acceso local especificada por hello **de** propiedad en función de hello **approot** directory.
  * **EAR:** componente hello es un archivo de empresa de Java (EAR) importado de un proyecto de aplicación de empresa en la ruta local Hola especificado por hello **de** propiedad. (Esto se detecta automáticamente por el Kit de herramientas de hello en función de hello naturaleza del proyecto de hello en esa ubicación).
  * **JAR:** componente hello es un archivo de Java (JAR) y se importa desde un proyecto de Java en hello ruta de acceso local especificada por hello **de** propiedad. (Esto se detecta automáticamente por el Kit de herramientas de hello en función de hello naturaleza del proyecto de hello en esa ubicación).
  * **Ninguno:** se realiza ninguna acción componente de hello tooimport. Esto es aplicable cuando se supone que el componente de hello tooalready estar presentes en el rol de hello **approot** directorio, o cuando el componente de hello es simplemente una instrucción ejecutable de línea de comandos, como Hola especificado en **como**propiedad cuando hello **implementar** método es **exec**.
  * **WAR:** componente hello es un archivo de aplicación web de Java (WAR) y se importa desde un proyecto Web dinámico en hello ruta de acceso local especificada por hello **de** propiedad. (Esto se detecta automáticamente por el Kit de herramientas de hello en función de hello naturaleza del proyecto de hello en esa ubicación).
  * **ZIP:** componente hello es un archivo zip y se importa por zip de Hola de directorio o archivo especificado por hello **de** propiedad.
* **Desde:** ruta de acceso de origen en la carpeta de toohello del equipo local o un archivo que representa la implementación de hello elementos tooimport tooyour. Las variables de entorno de Windows se pueden usar en esta propiedad. Todos los componentes se importará en función de hello **approot** directorio cuando se compila el proyecto de Hola.
  
    Tenga en cuenta que tiene Hola capacidad toodeploy un componente desde una descarga cuando se implementa en la nube toohello (no el emulador de proceso hello). Consulte la información relacionada que aparece a continuación relativa a la adición de componentes.    
* **Al igual que:** nombre de archivo bajo qué Hola componente se importará al rol de Hola **approot** directorio y en última instancia implementada en hello nube de Azure. Deje esta tookeep en blanco de la propiedad Hola Hola nombre igual que lo es en la máquina local Hola. (Para los componentes ejecutables, es decir, aquellos cuyo **implementar** método está establecido demasiado**exec**, puede tratarse de una instrucción de línea de comandos de Windows arbitraria.)
  
  > [!IMPORTANT]
  > Si utiliza caracteres de espacio para este valor, se controlarán forma distinta dependiendo de hello implementar el método. Si Hola implementa el método es **exec**, espacios se interpretarán como separadores de argumentos de línea de comandos y no como parte del nombre de archivo de Hola. Para todos los demás métodos de implementación, los espacios se interpretarán como parte del nombre de archivo de Hola.
  > 
  > 
* **Implementar:** método que indica la acción de hello aplica toohello componente cuando se inicia la implementación de Hola. Esto puede ser uno de hello siguientes valores:
  
  * **copia:** componente hello es toohello copiada de ruta de acceso de destino especificada por hello **a** propiedad.
  * **exec:** componente hello es una instrucción ejecutable de línea de comandos de Windows ejecutada en el contexto de Hola de ruta de acceso de hello especificada hello **a** propiedad en tiempo de Hola Hola implementación se inicia.
  * **Ninguno:** intervención del usuario es el componente de toohello aplicado cuando se inicia la implementación de Hola.
  * **ZIP:** componente hello es toohello descomprimida de ruta de acceso de destino especificada por hello **a** propiedad. Este método solo está disponible al hello **importación** propiedad es **postal**.
* **Para:** ruta de acceso de destino en la máquina virtual de Hola donde se implementará el componente de Hola. Las variables de entorno de Windows se pueden usar en esta propiedad y las rutas de acceso de archivo son relativas demasiado**approot**.

tooadd un nuevo componente, haga clic en hello **agregar** botón en hello **componentes** página de propiedades y un **componente de rol de Azure** se abrirá el cuadro de diálogo. Proporcionar valores para las propiedades de Hola que se describen anteriormente. 

Hola continuación, muestra un ejemplo para agregar un nuevo componente WAR.

![][ic719503]

Al implementar en la nube toohello (no Hola emulador de proceso), si desea que el componente de hello toodeploy desde una descarga, asegúrese que **en la nube, en lugar de incluir en el paquete de hello, implementar desde** está activada. Si desea toodownload de su cuenta de almacenamiento de Azure, seleccione cuenta de almacenamiento de Hola de hello **cuenta de almacenamiento** lista desplegable (puede hacer clic en hello **cuentas** vincular toomodify lo que aparece en la lista de hello), que se rellenará parcialmente en hello **URL** campo y, a continuación, rellene Hola parte restante de la dirección URL de Hola. Si no desea toouse almacenamiento de Azure, seleccione **(ninguno)** de hello **cuenta de almacenamiento** lista desplegable lista y escriba el componente de tooyour de dirección URL de Hola Hola **URL** campo. Especifique uno de los siguientes métodos de hello:

* **copia:** componente de descarga de hello es toohello copiada de ruta de acceso de destino especificada por hello **tooDirectory** ruta de acceso.
* **mismo:** Hola el mismo método usado para **implementar desde una descarga** como para **implementar desde el paquete**.
* **ZIP:** componente de descarga de hello es toohello descomprimida de ruta de acceso de destino especificada por hello **tooDirectory** ruta de acceso.

un componente, seleccione Hola componente y haga clic en Hola toomodify **editar** botón en hello **componentes** página de propiedades. Se abrirá un cuadro de diálogo Permitir toomodify Hola propiedades del componente. Presione **Aceptar** valores de los componentes toosave Hola.

toodelete un componente, seleccione Hola componente y haga clic en Hola **quitar** botón en hello **componentes** página de propiedades y, a continuación, haga clic en **Sí** eliminación de hello tooconfirm.

Los componentes se procesan en orden de Hola. Hola de uso **Subir** y **mover hacia abajo** botones orden de hello tooarrange.

> [!NOTE]
> característica de configuración de servidor de Hola se basa también en componentes. No puede quitar ni modificarse sin quitar la configuración de servidor correspondiente de Hola dichos componentes. Se le pedirá información cuando se intente toomake cambios toosuch componentes.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Propiedades de puntos de conexión
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **extremos**. En este cuadro de diálogo, tiene Hola capacidad toocreate un punto de conexión, así como editar o quitar un punto de conexión, como se muestra en hello después de la imagen.

![][ic719505]

tooadd un extremo, haga clic en hello **agregar** botón en hello **extremos** página de propiedades y un **Agregar extremo** se abrirá el cuadro de diálogo.

![][ic710897]

Escriba un nombre para el punto de conexión de hello, seleccione el tipo de hello (ya sea **entrada**, **interno**, o **InstanceInput**) y especifique el puerto público y privado de Hola. Presione **Aceptar** toosave Hola nuevos valores de punto de conexión.

Según el tipo de saludo de punto de conexión, puede utilizar intervalos de puertos de la siguiente manera:

* Para un extremo de instancia de entrada, puerto público de hello puede ser un intervalo de puertos (por ejemplo **2000-2010**) y puerto privado hello es un valor fijo.
* Para un extremo interno, no se utiliza el puerto público de Hola y puerto privado de hello puede ser un intervalo, o estar en blanco o conjunto tooan asterisco tooindicate se establece automáticamente en Azure.
* Para los extremos de entrada, puerto público Hola solo puede ser un valor fijo y puerto privado de hello puede ser un valor fijo, o estar en blanco o conjunto tooan asterisco tooindicate se establece automáticamente en Azure.

Si desea que toouse un número de puerto único en lugar de un intervalo, deje el cuadro de texto de hello para el fin de Hola de intervalo de Hola en blanco.

Para los puertos que están tooautomatic de conjunto, si necesita toodetermine el puerto que se utiliza en tiempo de ejecución, la aplicación puede usar API de tiempo de ejecución de servicios de Azure, que se documenta en Hola Hola [paquete com.microsoft.windowsazure.serviceruntime resumen][com.microsoft.windowsazure.serviceruntime package summary].

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

toomodify un punto de conexión, seleccione el punto de conexión de Hola y haga clic en hello **editar** botón en hello **extremos** página de propiedades. Se abrirá un cuadro de diálogo que le permite puertos públicos y privados, tipo y nombre de punto de conexión de toomodify Hola. Presione **Aceptar** toosave Hola modifica valores de punto de conexión.

toodelete un punto de conexión, seleccione el punto de conexión de Hola y haga clic en hello **quitar** botón en hello **extremos** página de propiedades y, a continuación, haga clic en **Sí** eliminación de hello tooconfirm.

En orden tooproperly configurar algunas de las características de hello (por ejemplo, la descarga de almacenamiento en caché, afinidad de la sesión o SSL) habilitado por el usuario de hello en un rol, el Kit de herramientas de hello puede configurar automáticamente los extremos especiales que se mostrarán junto con los extremos definidos por el usuario. Kit de herramientas de Hello evita que el usuario Hola editen o eliminar estos puntos de conexión generadas automáticamente como Hola asociados característica está habilitado.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Propiedades de variables de entorno
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **Variables de entorno**. En este cuadro de diálogo, tiene Hola capacidad toocreate una variable de entorno, así como modificar o quitar una variable de entorno, como se muestra en hello después de la imagen.

![][ic719506]

Las variables de entorno son secuencias de comandos de inicio de tooyour disponibles cuando se inicia el rol de Hola.

> [!NOTE]
> Al especificar las variables de entorno, tenga en cuenta que la implementación de máquina virtual de Windows de tooa publicado, por lo que las variables de entorno deben ser válidas para un sistema operativo de Windows.
> 
> 

Como ejemplo de una variable de entorno que está disponible cuando se inicia el rol de hello, cree una nueva variable de entorno haciendo clic en hello **agregar** botón. Hello siguiente muestra una variable de entorno denominada **MyRoleVersion** que se crea y asigna el valor de hello **1.0**.

![][ic659268]

Dentro del código jsp, podría mostrar valor de hello mediante hello `System.getenv` método:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Lo que genera este resultado cuando se ejecuta la aplicación:

![][ic552233]

toomodify una variable de entorno, seleccione la variable de entorno de Hola y haga clic en hello **editar** botón en hello **Variables de entorno** página de propiedades. Se abrirá un cuadro de diálogo Permitir toomodify Hola variable propiedades del entorno. Presione **Aceptar** valores de la variable de entorno toosave Hola.

toodelete una variable de entorno, seleccione la variable de entorno de Hola y haga clic en hello **quitar** botón en hello **Variables de entorno** página de propiedades y, a continuación, haga clic en **Sí**eliminación de hello tooconfirm.

En orden tooproperly configurar algunas de las características de hello (por ejemplo, la configuración del servidor, la depuración remota o almacenamiento Local) habilitada por el usuario de hello en un rol, el Kit de herramientas de hello puede configurar automáticamente las variables de entorno especiales que se mostrarán junto con variables de entorno definida por el usuario. Kit de herramientas de Hello impide a editar usuario Hola o eliminar dichas variables de entorno generado automáticamente como Hola asociados característica está habilitado.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Propiedades de equilibrio de carga y de afinidad de la sesión (conocidas también como "sesiones temporales")
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **equilibrio de carga**. En este cuadro de diálogo, tiene tooenable de capacidad de Hola o deshabilite la afinidad de sesión, como se muestra en hello después de la imagen.

![][ic719492]

Para más información relacionada, consulte [Habilitar la afinidad de la sesión][Session Affinity]. Además, observe el comportamiento de esta característica en el contexto de Hola de descarga de SSL, como se describe en [la descarga de SSL][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Propiedades de almacenamiento local
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **almacenamiento Local**. En este cuadro de diálogo, tiene toocreate de capacidad de hello, modificar o quitar almacenamiento local temporal para la máquina virtual de Hola que está ejecutando la aplicación. Valores específicos se pueden establecer para el tamaño de Hola de almacenamiento local de hello, así como si contenido Hola se conserva cuando se recicla, rol de hello como se muestra en hello después de la imagen.

![][ic719508]

Opcionalmente, también puede especificar una variable de entorno correspondiente toohello de almacenamiento local.

De forma predeterminada, todo lo que se implementa en Azure se colocan (y se han descomprimido) en hello **approot** carpeta de instancia de rol de Hola. Mientras que la mayoría de las implementaciones sencillas se ajustarán incluso después de la descompresión, espacio de hello asignado para hello **approot** directorio es limitado y no está bien definido (menos de 1 GB es una regla general razonable). Por lo tanto, tooensure Azure asigna suficiente espacio en disco para implementaciones más grandes que podrían no caber en hello **approot** carpeta, debe configurar un recurso de almacenamiento local mediante hello **almacenamiento Local** cuadro de diálogo. Para una toodo de forma sencilla, vea [implementar implementaciones a gran escala][Deploying Large Deployments].

Puede hacer referencia fácilmente a recursos de almacenamiento de Hola desde scripts de inicio (por ejemplo, el **startup.cmd**) mediante la variable de entorno de hello asociado automáticamente por el Kit de herramientas de Eclipse Hola Hola recurso, como se muestra en hello  **Almacenamiento local** cuadro de diálogo. Esa variable de entorno contendrá la ruta de acceso completa de Hola de recurso local Hola que se ha configurado en tiempo de presentación que se ejecuta el script de inicio. 

toomodify un recurso de almacenamiento local, seleccione el recurso de almacenamiento local de Hola y haga clic en hello **editar** botón en hello **almacenamiento Local** página de propiedades. Se abrirá un cuadro de diálogo Permitir toomodify Hola recursos propiedades de almacenamiento local. Presione **Aceptar** valores de recursos de almacenamiento local de toosave Hola.

toodelete un recurso de almacenamiento local, seleccione el recurso de almacenamiento local de Hola y haga clic en hello **quitar** botón en hello **almacenamiento Local** página de propiedades y, a continuación, haga clic en **Sí** eliminación de hello tooconfirm.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Propiedades de configuración de servidor
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **configuración del servidor**. En este cuadro de diálogo, tiene tooadd de capacidad de hello, quitar y modificar Hola JDK y el servidor de aplicaciones de Java que use la implementación, así como agregar o quitar las aplicaciones de hello (como archivos WAR, JAR o EAR) utilizadas por la implementación.

### <a name="jdk-configuration"></a>Configuración de JDK
Este cuadro de diálogo le permite toospecify Hola JDK paquete toouse para su implementación. Si está usando Eclipse en Windows, puede especificar Hola JDK paquete toouse localmente cuando se ejecuta en hello emulador de Azure y tiene Hola opción toodeploy ese tooAzure instalación local. En sistemas operativos que no son de Windows, configuración de JDK del emulador hello no es aplicable y no se puede implementar localmente Hola instalado JDK, ya que no es compatible con Windows. Sin embargo, independientemente del sistema operativo de Hola que está usando, siempre puede elegir entre Hola 3ª parte JDK paquetes toodeploy tooAzure o apuntar a su propio paquete JDK compatible con Windows desde una ubicación de descarga alternativa.

Hola te mostramos un ejemplo de cómo se puede especificar un JDK en Windows:

![][ic780647]

Si está usando Eclipse en Windows, puede especificar un toouse JDK con hello proceso emulador; por lo tanto, asegúrese de toodo **Hola uso JDK desde esta ruta de acceso de archivo para las pruebas localmente** está activada en hello **Emulator deployment** sección. A continuación, especifique la ruta de acceso local de hello tooyour JDK; puede examinar toodifferent JDK si hello que desea toouse no se selecciona automáticamente. También tiene Hola opción toodeploy su servicio de nube de Azure; tooyour JDK toodo por lo tanto, seleccione hello **implementar mi JDK local (auto-upload toocloud almacenamiento)** opción Hola **implementación de nube** sección.

Nota: En sistemas operativos que no son Windows, Hola **Emulator deployment** hello y configuración **implementar mi JDK local** opción no están disponibles. Hello en el ejemplo siguiente se muestra cómo especificar un JDK en un equipo Mac o sí admite el sistema operativo Windows no:

![][ic789643]

Independientemente de que se encuentra en el sistema de operativo hello, tienes Hola siguiendo dos **implementación de nube** opciones de origen de Hola y el tipo de su paquete de JDK:

* **Implementar un paquete JDK de terceros disponible en Azure** 
* **Implementar desde una descarga personalizada** 

Si usas hello **implementar un paquete JDK de terceros 3rd disponible de Azure** opción:

1. Active casilla Hola llamada **implementar un paquete JDK de terceros 3rd disponible de Azure**.
2. Desde la lista desplegable de hello, seleccione Hola 3ª parte paquete de JDK que está disponible en Azure.
3. Su **JDK** ficha tendrá un aspecto similar siguiente toohello en Windows: ![][ic780648] y tendrá una apariencia similar siguiente toohello en Mac OS o sí admite sistemas operativos que no son de Windows:![][ic789643]
4. Haga clic en **Aceptar** toosave los cambios.
5. Cuando tooaccept solicitada hello contrato de licencia de proveedor de paquetes de hello 3ª parte JDK, revise los términos de licencia de Hola. Suponiendo que acepta los términos de hello, haga clic en **Sí** tooclose hello **Aceptar el contrato de licencia** cuadro de diálogo.
    Tenga en cuenta que Hola subyacente lógica para el que los elementos aparecen en la lista desplegable de Hola para hello **implementar un paquete JDK de terceros 3rd disponible de Azure** opción puede personalizarse. elementos de hello toocustomize, Hola **JDK** cuadro de diálogo, haga clic en hello **personalizar** vínculo. Esto cerrará hello **JDK** hello abierto y página de propiedades **componentsets.xml** archivo en Eclipse, que, a continuación, se puede modificar según sea necesario. Documentación de **componentsets.xml** se incluye en hello **componentsets.xml** propio archivo.

Si usas hello **implementar un JDK desde una descarga personalizada** opción:

1. Crear un archivo ZIP de su directorio de instalación de JDK, asegurándose de que propio nodo de directorio de hello es el elemento secundario de hello de la estructura del archivo ZIP hello y no su contenido. Tome nota del nombre de hello del directorio de hello, tal y como se necesite más adelante y tenga en cuenta este JDK instalación será la máquina virtual de Windows tooa implementado.
2. Cargar Hola ZIP en su cuenta de almacenamiento de Azure como un blob. Puede hacerlo mediante una herramienta disponible externamente para cargar blobs tooAzure almacenamiento. Es recomendable toouse un blob privado. Tome nota de la dirección URL del blob Hola de contenido de hello ZIP.
3. Active casilla Hola llamada **implementar un JDK desde una descarga personalizada**.
    Si desea toodownload de su cuenta de almacenamiento de Azure, seleccione cuenta de almacenamiento de Hola de hello **cuenta de almacenamiento** lista desplegable (puede hacer clic en hello **cuentas** vincular toomodify lo que aparece en la lista de hello), que se rellenará parcialmente en hello **URL** campo y, a continuación, rellene Hola parte restante de la dirección URL de Hola. Si no desea toouse almacenamiento de Azure, seleccione **(ninguno)** de hello **cuenta de almacenamiento** lista desplegable lista y escriba Hola URL tooyour descarga de JDK en hello **URL** campo. Si usa el almacenamiento de Azure, nombres de blob de dirección URL de hello deben estar en minúsculas.
4. Asegúrese de que hello **JAVA_HOME** cuadro de texto hace referencia toohello nombre de directorio correcto. De forma predeterminada, hará referencia a Hola el mismo nombre de directorio JDK como valor de Hola que eligió para su uso local. Sin embargo, si el directorio Hola contenido en hello ZIP tiene un nombre distinto (por ejemplo, due toousing una versión diferente), nombre de directorio de actualización Hola Hola **JAVA_HOME** textbox en consecuencia, ya que esta configuración se usarán en hello en la nube () no en el emulador de proceso hello).
5. Haga clic en **Aceptar** toosave los cambios.

Eso es todo. Ahora, cuando se compila para la nube de hello, observará será mucho menor tamaño de paquete de hello, normalmente tardará menos tiempo de proceso de compilación de Hola y Hola propia implementación al publicar en la nube toohello también debería tardar menos tiempo. Tenga en cuenta que hello **implementar mi JDK local (auto-upload toocloud almacenamiento)** o **implementar un JDK desde una descarga personalizada** opciones están en vigor solo cuando la aplicación se implementa en la nube de Hola. No tienen ningún efecto sobre su experiencia de emulador de proceso; versión local de Hola de componentes de hello todavía se utilizará cuando se implementa toohello del emulador de proceso. 

### <a name="server-configuration"></a>Configuración del servidor
Hola aquí te mostramos un ejemplo de cómo se puede especificar un servidor de aplicaciones.

![][ic796926]

Compruebe que hello **implementar un servidor de este tipo** casilla de verificación está seleccionada y, a continuación, elija el tipo de saludo del servidor de aplicaciones que desea toouse.

Para especificar un toouse de servidor para la implementación de nube, puede aprovechar las ventajas de hello siguientes opciones:

1. **Implementar un servidor de entidad 3rd disponible en Azure** -esto es especialmente relevante en escenarios de desarrollo y pruebas donde la eficacia de la implementación y la simplicidad es una prioridad y servidor hello no requiere una configuración personalizada. O bien, cuando se desea toouse uno de esos servidores como punto de partida de hello pero incluye pasos de personalización de servidor adecuado en la lógica de inicio de su implementación.
2. **Implementar desde una descarga personalizada** -esto es especialmente relevante en escenarios de producción cuando se tiene un servidor especialmente configurado y preparado que quiere que toouse en la nube de Hola.
3. **Implementar mi instalación de servidor local** : se aplica especialmente si la configuración de instalación del servidor local está personalizada para el usuario. Si elige esta opción, también debe especificar la ruta de acceso de su servidor local en hello **ruta de acceso del servidor Local** siguiente cuadro de texto.

Si usas hello **implementar un servidor de entidad 3rd disponible en Azure** opción:

1. Active casilla Hola llamada **implementar un servidor de entidad 3rd disponible en Azure**.
2. Desde el menú desplegable de hello, seleccione Hola deseado toouse de software de servidor con la implementación en la nube de Hola. Tenga en cuenta que si ya ha especificado un tipo de servidor toouse anteriormente, estará limitado toochoosing sólo un servidor de nube que se encuentra en hello misma familia que ese tipo de servidor. Pero si no seleccionó un tipo de servidor, puede elegir entre cualquiera de los servidores de Hola que están actualmente disponibles en Azure y tipo de servidor de Hola se seleccionará automáticamente para usted.
3. Haga clic en **Aceptar** toosave los cambios.

Si usa hello **implementar desde una descarga personalizada** opción:

1. Asegúrese de que ya ha seleccionado un tipo de servidor según toohello pasos anteriores. Esto indica a Hola complemento cómo debe ser servidor de hello toodeploy desde la descarga personalizada, tal y como de hello misma familia que su tipo de servidor seleccionado.
2. Active casilla Hola llamada **implementar desde una descarga personalizada**.
    Si desea toodownload de su cuenta de almacenamiento de Azure, seleccione cuenta de almacenamiento de Hola de hello **cuenta de almacenamiento** lista desplegable (puede hacer clic en hello **cuentas** vincular toomodify lo que aparece en la lista de hello), que se rellenará parcialmente en hello **URL** campo y, a continuación, rellene Hola parte restante de servidor de hello URL tooyour descargar ZIP (cuando se usa almacenamiento de Azure, nombres de blob de dirección URL de hello debe estar en minúscula). Si no desea toouse almacenamiento de Azure, seleccione **(ninguno)** de hello **cuenta de almacenamiento** lista desplegable lista y escriba Hola URL tooyour servidor al descargar ZIP en hello **URL** campo. Hola ZIP contendría una carpeta secundaria que representa el directorio de instalación del servidor de aplicaciones. Por ejemplo, si está utilizando un archivo zip para Apache Tomcat 7.0.35, dentro de hello zip sería Hola secundarios carpeta que representan Hola directorio de instalación, como **apache-tomcat-7.0.35**. 
3. Especificar valor de hello para la variable de entorno del directorio particular de Hola. El valor predeterminado será valor toohello usado para el servidor de aplicaciones local, si existe, pero puede especificar un valor diferente si el servidor de aplicaciones de nube es distinto de su servidor de aplicaciones local. Sin embargo, debe asegurarse de que el servidor de aplicaciones de nube es de hello toomake misma familia como tipo de servidor hello seleccionado con anterioridad.
    Si actualiza el código postal de servidor de nube aplicación Hola futuro, puede cambiar manualmente la configuración del directorio particular de Hola o toohave vuelva a coincidir con la configuración local (si se cambia el servidor de aplicaciones local demasiado).
4. Haga clic en **Aceptar** toosave los cambios.

Hola subyacente lógica para que los elementos aparecen en hello **Server** ficha de hello **configuración del servidor** se puede personalizar la página de propiedades. Se trata de una característica avanzada que podría necesitar si sus necesidades van más allá de los valores predeterminados de Hola o si desea tooadd otros servidores. lógica de hello toocustomize, Hola **Server** cuadro de diálogo, haga clic en hello **personalizar** vínculo. Esto cerrará hello **configuración del servidor** hello abierto y página de propiedades **componentsets.xml** archivo en Eclipse, que, a continuación, se puede modificar como plantilla de configuración de servidor de hello tooextend necesarios. Documentación de **componentsets.xml** se incluye en hello **componentsets.xml** propio archivo.

Si usas hello **implementar mi servidor local (auto-upload toocloud almacenamiento)** opción:

1. Active casilla Hola llamada **implementar mi servidor local (auto-upload toocloud almacenamiento)**.
2. Con hello **cuenta de almacenamiento** lista desplegable, seleccione **(auto)**. Si especifica **(auto)** aquí, Hola Eclipse toolkit usará Hola misma cuenta de almacenamiento para el servidor como Hola uno que seleccione para su implementación en hello **publicar tooAzure** cuadro de diálogo.
3. Haga clic en **Aceptar** toosave los cambios.

Seleccione una ruta de acceso de instalación de servidor en el equipo en hello **ruta de acceso del servidor Local** cuadro de texto si se cumple alguna de hello condiciones siguientes:

* Desea tootest la implementación en el emulador de hello (se aplica solo tooWindows).
* Desea toodeploy en la nube de toohello de servidor instalada localmente.
* Si desea toouse una descarga de servidor personalizado de su propia en nube hello, en cuyo caso, asegúrese también de hello **implementar mi servidor local (auto-upload toocloud almacenamiento)** opción está seleccionada anteriormente.

Si aplica ninguno de hello anterior opciones tooyour situación, configuración de servidor local de hello es opcional.

### <a name="applications-configuration"></a>Configuración de aplicaciones
Hola aquí te mostramos un ejemplo de cómo se puede especificar una aplicación.

![][ic719512]

Haga clic en **agregar** tooadd otra aplicación, o **quitar** tooremove una aplicación. Por motivos de eficiencia, si desea toouse una descarga para el origen de Hola de una aplicación cuando se implementa en la nube toohello, usar hello [propiedades de los componentes](#components_properties) toospecify una dirección URL, la cuenta de almacenamiento, etcetera. 

A partir de la versión de abril de 2014 hello, las aplicaciones se cargan automáticamente en hello misma cuenta de almacenamiento (en hello **eclipsedeploy** contenedor) como Hola seleccionada para su implementación. lógica de inicio de saludo de la implementación contiene un paso que descarga primero esas aplicaciones desde esa cuenta de almacenamiento. Esto significa que puede actualizar las aplicaciones en la implementación sin necesidad de toorebuild y volver a implementar el paquete completo de hello, mediante la carga manual de las versiones más recientes de la aplicación hello directamente en esa cuenta de almacenamiento (por ejemplo mediante el Hola portal de Azure) , reemplazando archivos WAR de hello cargado originalmente ahí Hola Kit de herramientas. A continuación, simplemente inicie Hola reciclado de todas esas instancias de rol mediante el portal de administración de Azure nuevo, o a través de utilidades de línea de comandos. (Activar rol reciclaje directamente desde dentro de Kit de herramientas de Eclipse hello no se admite actualmente.)

### <a name="notes-about-server-configuration"></a>Notas sobre la configuración del servidor
Los cambios realizados a través de hello **configuración del servidor** página de propiedades se reflejan en hello `<component>` elementos del archivo package.xml de Hola.

Cuando usas hello **se cargue automáticamente...**  o **implementar desde una descarga...**  opciones hello JDK o servidor de aplicaciones, y se va a crear para la nube hello (no Hola emulador de proceso) y está conectado toohello red, puede notar crear mensajes como siguiente hello en la salida de la consola de Hola Hola Ant generador comprueba la disponibilidad de la descarga de hello:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Si seleccionó hello **implementar desde una descarga...**  opción, es posible que aparezcan Hola después de advertencia, pero Hola compilación continuará:

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

Esta advertencia es indicación solo Hola que Hola disponibilidad de la descarga no se ha comprobado. Por lo que si una implementación en la nube de Hola se produce un error por algún motivo, comprobar toosee si ha recibido esta advertencia.

Si desea toodisable comprobación de la descarga de hello (por ejemplo, si cree que ralentiza innecesariamente compilación hello), hello establezca `verifydownloads` atributo demasiado`false` en hello `<windowsazurepackage>` elemento de package.xml: 

`<windowsazurepackage verifydownloads="false" ...>` 

Si seleccionó hello **se cargue automáticamente...**  opción, a continuación, en la ventana de la consola de hello verá informar del progreso Hola carga Hola cada 5 segundos, siempre que sea necesaria una carga de los mensajes de compilación.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>Propiedades de la descarga de SSL
Abra el menú contextual de hello para el rol de hello en el panel Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **la descarga de SSL**. 

![][ic719481]

En este cuadro de diálogo, puede habilitar SSL descarga, lo que permite habilitar tooeasily admite la transferencia de hipertexto protocolo seguro (HTTPS) en su implementación de Java en Azure, sin necesidad de tooconfigure SSL en el servidor de aplicaciones Java. Para obtener más información, consulte [la descarga de SSL] [ SSL Offloading] y [cómo tooUse la descarga de SSL][How tooUse SSL Offloading].

## <a name="see-also"></a>Otras referencias
[kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]

[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]

[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Propiedades del proyecto de Azure][Azure Project Properties]

[Lista de cuentas de Azure Storage][Azure Storage Account List]

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
