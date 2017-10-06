---
title: aaaDeploy un tooAzure ejecutable existente Service Fabric | Documentos de Microsoft
description: "Tutorial sobre la implementación de clúster de Service Fabric tooa toopackage una aplicación existente como un ejecutable de invitado, por lo que puede ser"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>Implementar un tejido de invitado ejecutable tooService
Puede ejecutar cualquier tipo de código, como Node.js, Java o C++ en Azure Service Fabric como servicio. Service Fabric hace referencia a tipos de toothese de servicios como archivos ejecutables de invitado.

Los ejecutables invitados se tratan por Service Fabric como servicios sin estado. Por ello, se colocan en los nodos de un clúster, en función de la disponibilidad y otras métricas. Este artículo se describe cómo toopackage e implementar un clúster de Service Fabric tooa ejecutable de invitado, mediante Visual Studio o una utilidad de línea de comandos.

En este artículo, se cubre Hola pasos toopackage un invitado ejecutable e impleméntela tooService tejido.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Ventajas de ejecutar un ejecutable invitado en Service Fabric
Hay varias toorunning ventajas un ejecutable en un clúster de Service Fabric invitado:

* Alta disponibilidad. Las aplicaciones que se ejecutan en Service Fabric se crean con alta disponibilidad. Service Fabric garantiza que se están ejecutando instancias de una aplicación.
* Supervisión del estado. La supervisión del mantenimiento de Service Fabric detecta si hay una aplicación en funcionamiento y proporciona información de diagnóstico si se produce un error.   
* Administración del ciclo de vida de las aplicaciones. Además de proporcionar actualizaciones sin tiempo de inactividad, Service Fabric proporciona versión anterior de toohello de reversión automática si se produce un evento de mal estado notificado durante la actualización.    
* Densidad. Puede ejecutar varias aplicaciones en un clúster, lo que elimina la necesidad de Hola de cada toorun de aplicación en su propio hardware.
* Detectabilidad: Con REST se puede llamar a toofind del servicio de nomenclatura de tejido de servicio de hello otros servicios en clúster de Hola. 

## <a name="samples"></a>Muestras
* [Ejemplo para empaquetar e implementar un archivo ejecutable invitado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Ejemplo de dos archivos ejecutables (C# y nodejs) de invitado comunicarse a través del servicio de nomenclatura de hello con REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Información general de los archivos de manifiesto de servicio y aplicación
Como parte de la implementación de un archivo ejecutable de invitado, resulta empaquetado de Service Fabric hello toounderstand útil y modelo de implementación tal y como se describe en [modelo de aplicación](service-fabric-application-model.md). modelo de empaquetado de Service Fabric Hola se basa en dos archivos XML: Hola manifiestos de aplicación y de servicio. Hello definición de esquema para archivos ApplicationManifest.xml y ServiceManifest.xml hello está instalado una con Hola SDK del servicio de Fabric en *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **Manifiesto de aplicación** manifiesto de aplicación de hello es aplicación de hello toodescribe usado. Enumeran los servicios de Hola que lo componen y otros parámetros que son utilizado toodefine deben implementarse cómo uno o varios servicios, como el número de Hola de instancias.

  En Service Fabric, una aplicación es una unidad de implementación y actualización. Una aplicación se puede actualizar como una sola unidad donde se administran los posibles errores y reversiones. Service Fabric garantiza que el proceso de actualización de hello es ya sea correcta, o bien, si se produce un error en la actualización de hello, no deje aplicación hello en un estado inestable o desconocido.
* **Manifiesto del servicio** manifiesto del servicio Hola describe los componentes de Hola de un servicio. Incluye datos, como el nombre de Hola y tipo de servicio y su código y configuración. Hello manifiesto del servicio también incluye algunos parámetros adicionales que se pueden usar servicio de hello tooconfigure una vez que se implementa.

## <a name="application-package-file-structure"></a>Estructura de archivo del paquete de aplicación
un tejido de aplicación tooService toodeploy, aplicación hello debe seguir una estructura de directorios predefinidos. Hola aquí te mostramos un ejemplo de esa estructura.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

Hola ApplicationPackageRoot contiene el archivo ApplicationManifest.xml hello que define la aplicación hello. Un subdirectorio para cada servicio incluido en la aplicación hello es toocontain usado todos Hola artefactos que requiere el servicio de Hola. Estos subdirectorios son hello ServiceManifest.xml y, por lo general, Hola siguientes:

* *Code*. Este directorio contiene el código del servicio de Hola.
* *Config*. Este directorio contiene un archivo Settings.xml (y otros archivos si es necesario) que puede tener acceso servicio de hello en Opciones de configuración específicas de tooretrieve en tiempo de ejecución.
* *Data*. Se trata de un directorio adicional toostore local datos adicionales que Hola servicio puede necesitar. Datos deben estar toostore utilizados efímera solo datos. Service Fabric no copia ni replicar el directorio de datos de cambios toohello si servicio de hello necesita toobe reubicado (por ejemplo, durante la conmutación por error).

> [!NOTE]
> No tienes hello toocreate `config` y `data` directorios si no los necesite.
>
>

## <a name="package-an-existing-executable"></a>Empaquetado de un ejecutable existente
Al empaquetar un archivo ejecutable de invitado, puede elegir cualquier toouse una plantilla de proyecto de Visual Studio o demasiado[crear paquete de aplicación Hola manualmente](#manually). Con Visual Studio, Hola estructura del paquete de aplicación y se crean archivos de manifiesto por la nueva plantilla de proyecto Hola automáticamente.

> [!TIP]
> toopackage de manera más fácil de Hello un ejecutable a un servicio de Windows existente es toouse Visual Studio y en Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Usar Visual Studio toopackage e implementar un archivo ejecutable existente
Visual Studio proporciona a un tejido de servicio toohelp de plantilla de servicio implementar un clúster de Service Fabric tooa ejecutable de invitado.

1. Seleccione **Archivo** > **Nuevo proyecto** y cree una aplicación de Service Fabric.
2. Elija **invitado ejecutable** como plantilla de servicio de Hola.
3. Haga clic en **examinar** carpeta de hello tooselect con el archivo ejecutable y rellene el resto de hello del servicio de hello parámetros toocreate Hola.
   * *Comportamiento del paquete de código*. Puede ser conjunto toocopy todo el contenido de Hola de su toohello carpeta del proyecto de Visual Studio, lo que resulta útil si ejecutable hello no cambia. Si espera toochange ejecutable hello y desea Hola capacidad toopick de nuevas compilaciones dinámicamente, puede elegir toolink toohello carpeta en su lugar. Puede usar carpetas vinculadas al crear el proyecto de aplicación de hello en Visual Studio. Esto vincula la ubicación de origen toohello desde dentro de proyecto de hello, lo que permite invitado hello tooupdate ejecutable en su destino de origen. Esas actualizaciones se convierten en parte del paquete de aplicación hello en la compilación.
   * *Programa* especifica Hola ejecutable que se debe ejecutar el servicio de hello toostart.
   * *Argumentos* especifica los argumentos de Hola que deben pasarse a toohello ejecutable. Puede ser una lista de parámetros con argumentos.
   * *WorkingFolder* especifica Hola el directorio de trabajo de proceso de Hola que queda toobe iniciado. Puede especificar tres valores:
     * `CodeBase`especifica ese directorio de trabajo de hello va toobe establecer directorio de código de toohello en el paquete de aplicación Hola (`Code` directory mostrado en hello delante de la estructura de archivos).
     * `CodePackage`especifica ese directorio de trabajo de hello va toobe establece toohello directorio raíz del paquete de aplicación Hola (`GuestService1Pkg` se muestra en hello delante de la estructura de archivos).
     * `Work`Especifica que los archivos de saludo se colocan en un subdirectorio denominado trabajo.
4. Asigne un nombre a su servicio y haga clic en **Aceptar**.
5. Si el servicio necesita un punto de conexión para la comunicación, ahora puede agregar Hola protocolo, puerto y archivo de tipo toohello ServiceManifest.xml. Por ejemplo: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. Ahora puede usar el paquete de Hola y acción de publicación en el grupo local mediante la depuración de la solución de hello en Visual Studio. Cuando esté listo, puede publicar clúster remoto de hello aplicación tooa o comprobar en el control de la solución toosource Hola.
7. Ir al final de toohello de este artículo toosee cómo tooview su servicio ejecutable invitado ejecuta en el Explorador de Service Fabric.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Usar Yoeman toopackage e implementar un archivo ejecutable existente en Linux

procedimiento de Hola para crear e implementar un invitado ejecutable en Linux es Hola igual que implementar una aplicación de csharp o java.

1. En un terminal, escriba `yo azuresfguest`.
2. Asigne un nombre a la aplicación.
3. El servicio de nombres y proporcionar detalles de hello como ruta de acceso del ejecutable hello y parámetros de Hola con que se debe invocar.

Yeoman crea un paquete de aplicación con la aplicación apropiada de Hola y archivos de manifiesto junto con instalación y desinstalación las secuencias de comandos.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>Empaquetado e implementación manuales de un archivo ejecutable existente
proceso de Hola de empaquetar manualmente un archivo ejecutable de invitado se basa en hello siguiendo los pasos generales:

1. Crear estructura de directorios de paquetes de saludo.
2. Agregar archivos de código y la configuración de la aplicación hello.
3. Edite el archivo de manifiesto de servicio de Hola.
4. Edite el archivo de manifiesto de aplicación Hola.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Crear estructura de directorios del paquete de Hola
Puede iniciar mediante la creación de la estructura de directorios de hello, como se describe en hello anterior sección "Estructura de archivos de paquete de aplicación".

### <a name="add-hello-applications-code-and-configuration-files"></a>Agregar archivos de código y la configuración de la aplicación hello
Una vez haya creado la estructura de directorios de hello, puede agregar archivos de código y la configuración de la aplicación hello en los directorios de código y la configuración de Hola. También puede crear directorios adicionales o varios subdirectorios en los directorios de código o configuración de Hola.

Service Fabric un `xcopy` del contenido de Hola Hola directorio raíz de aplicación, así que no hay ningún toouse estructura predefinida aparte de la creación de dos directorios principales, código y configuración. (Puede elegir diferentes nombres si lo desea. Más detalles se encuentran en la sección siguiente Hola.)

> [!NOTE]
> Asegúrese de que incluye todos los archivos de Hola y dependencias que Hola necesidades de la aplicación. Service Fabric copia Hola contenido del paquete de aplicación hello en todos los nodos de clúster de Hola que Servicios de la aplicación hello están toobe continuo implementado. paquete de Hello debe contener todo el código de hello que la aplicación hello necesita toorun. No se da por supuesto que ya están instaladas las dependencias de Hola.
>
>

### <a name="edit-hello-service-manifest-file"></a>Editar el archivo de manifiesto de servicio de Hola
Hola siguiente paso es tooedit Hola servicio archivo de manifiesto tooinclude Hola siguiente información:

* nombre de Hola Hola del tipo de servicio. Se trata de un identificador que Service Fabric usa tooidentify un servicio.
* Hola comando toouse toolaunch Hola la aplicación (ExeHost).
* Cualquier secuencia de comandos que necesita tooset toobe ejecutar una aplicación hello (SetupEntrypoint).

Hello aquí te mostramos un ejemplo de un `ServiceManifest.xml` archivo:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

Hola las secciones siguientes se pasa por partes diferentes de hello del archivo de Hola que necesita tooupdate.

#### <a name="update-servicetypes"></a>Actualización de ServiceTypes
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* Puede elegir cualquier nombre que desee para `ServiceTypeName`. se utiliza el valor de Hola Hola `ApplicationManifest.xml` tooidentify Hola servicio de archivos.
* Especifique `UseImplicitHost="true"`. Este atributo indica a Service Fabric que el servicio de Hola se basa en una aplicación independiente, por lo que todos los Service Fabric debe toodo es toolaunch como un proceso y supervisar su estado.

#### <a name="update-codepackage"></a>Actualización de CodePackage
elemento de Hello CodePackage especifica la ubicación de hello (y versión) de código de servicio de Hola.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

Hola `Name` elemento es toospecify usado Hola nombre del directorio de Hola Hola paquete de aplicación que contiene el código de servicio de Hola. `CodePackage`También tiene hello `version` atributo. Esto puede ser usado toospecify Hola versión de código de hello y también podrían ser usa código de servicio de tooupgrade hello mediante la infraestructura de administración de ciclo de vida de aplicación hello en Service Fabric.

#### <a name="optional-update-setupentrypoint"></a>Opcional: Actualización de SetupEntryPoint
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
elemento de Hello SetupEntryPoint es toospecify usa cualquier archivo ejecutable o por lotes que se debe ejecutar antes de que se inicia el código de servicio de Hola. Es un paso opcional, por lo que no es necesario toobe incluyen si no hay ninguna inicialización necesaria. Hola SetupEntryPoint se ejecuta cada vez que se reinicie el servicio de Hola.

Hay solo un SetupEntryPoint, por lo que las secuencias de comandos del programa de instalación necesitan toobe agrupada en un archivo por lotes solo si el programa de instalación de la aplicación hello requiere varias secuencias de comandos. Hola SetupEntryPoint puede ejecutar cualquier tipo de archivo: archivos ejecutables, archivos por lotes y cmdlets de PowerShell. Para más información, vea cómo [configurar SetupEntryPoint](service-fabric-application-runas-security.md).

En el anterior ejemplo de Hola Hola SetupEntryPoint ejecuta un archivo por lotes denominado `LaunchConfig.cmd` decir Hola ubicada en `scripts` subdirectorio del directorio de código de hello (suponiendo que se establece el elemento de WorkingFolder de hello tooCodeBase).

#### <a name="update-entrypoint"></a>Actualización de EntryPoint
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

Hola `EntryPoint` elemento de archivo de manifiesto de servicio de hello es toospecify usado cómo servicio de hello toolaunch. Hola `ExeHost` elemento especifica ejecutable hello (y argumentos) que debe ser utilizado toolaunch Hola servicio.

* `Program`Especifica el nombre de hello del archivo ejecutable de Hola que debe iniciar el servicio de Hola.
* `Arguments`Especifica los argumentos de Hola que deben pasarse toohello ejecutable. Puede ser una lista de parámetros con argumentos.
* `WorkingFolder`Especifica el directorio de trabajo de Hola de proceso de Hola que queda toobe iniciado. Puede especificar tres valores:
  * `CodeBase`especifica ese directorio de trabajo de hello va toobe establecer directorio de código de toohello en el paquete de aplicación Hola (`Code` directorio Hola delante de la estructura de archivos).
  * `CodePackage`especifica ese directorio de trabajo de hello va toobe establece toohello directorio raíz del paquete de aplicación Hola (`GuestService1Pkg` Hola delante de la estructura de archivos).
    * `Work`Especifica que los archivos de saludo se colocan en un subdirectorio denominado trabajo.

Hola WorkingFolder es directorio de trabajo correcto de tooset útil Hola para que las rutas de acceso relativas pueden utilizarse cualquier secuencias de comandos hello, aplicación o inicialización.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Actualización de puntos de conexión y registro mediante el servicio de nombres para la comunicación
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
En el anterior ejemplo de Hola Hola `Endpoint` elemento especifica los extremos de Hola que puede escuchar aplicación hello. En este ejemplo, hello aplicación Node.js escucha en http en el puerto 3000.

Además puede pedir toopublish Service Fabric este servicio de nombres de punto de conexión toohello para que otros servicios puedan detectar el servicio de toothis de dirección de punto de conexión de Hola. Esto le permite toobe toocommunicate capaz de entre los servicios que son ejecutables de invitado.
Hello publicado dirección del extremo es del formulario de hello `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme` y `PathSuffix` son atributos opcionales. `IPAddressOrFQDN`es Hola dirección IP o nombre de dominio completo de este ejecutable se coloca en el nodo de Hola y se calcula automáticamente.

En hello siguiente ejemplo, servicio de hello una vez implementada, en el Explorador de Service Fabric verá un punto de conexión similar demasiado`http://10.1.4.92:3000/myapp/` publica para la instancia de servicio de Hola. Si se trata de un equipo local, verá `http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
Puede usar estas direcciones con [proxy inverso](service-fabric-reverseproxy.md) toocommunicate entre servicios.

### <a name="edit-hello-application-manifest-file"></a>Editar el archivo de manifiesto de aplicación Hola
Una vez haya configurado hello `Servicemanifest.xml` archivo, necesita algunos cambios toohello toomake `ApplicationManifest.xml` correcta se usan el tipo de servicio y el nombre de archivo tooensure que Hola.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
Hola `ServiceManifestImport` elemento, puede especificar uno o varios servicios que desea que tooinclude en la aplicación hello. Se hace referencia a servicios con `ServiceManifestName`, que especifica el nombre de hello del directorio de Hola donde hello `ServiceManifest.xml` archivo se encuentra.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Configuración de los registros
Para los ejecutables de invitado, resulta útil toobe toosee capaz de consola registros toofind out si los scripts de configuración de aplicación y de hello muestran los errores.
Redirección de la consola puede configurarse en hello `ServiceManifest.xml` archivo mediante hello `ConsoleRedirection` elemento.

> [!WARNING]
> Nunca use Directiva de redirección de consola de hello en una aplicación que se implementa en producción porque esto puede afectar a la conmutación por error de aplicación de Hola. *Solo* debe usarla con fines de depuración y desarrollo local.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`puede ser el directorio de trabajo de tooa de tooredirect usado consola resultado (stdout y stderr). Esto proporciona Hola capacidad tooverify que no hay ningún error durante la instalación de Hola o ejecución de la aplicación hello en clúster de Service Fabric Hola.

`FileRetentionCount`Determina cuántos archivos se guardan en el directorio de trabajo de Hola. Un valor de 5, por ejemplo, significa que los archivos de registro de hello para ejecuciones de cinco anterior Hola se almacenan en el directorio de trabajo de Hola.

`FileMaxSizeInKb`Especifica el tamaño máximo de Hola Hola de archivos de registro.

Archivos de registro se guardan en uno de los directorios de trabajo del servicio de Hola. toodetermine donde hello encontrará los archivos, utilice Service Fabric Explorer toodetermine qué servicio de Hola de nodo se ejecuta en, y qué directorio de trabajo está usándola. Este proceso se trata más adelante en este artículo.

## <a name="deployment"></a>Implementación
último paso de Hello es demasiado[implementar su aplicación](service-fabric-deploy-remove-applications.md). Hola después de la muestra de script de PowerShell toodeploy su clúster de desarrollo local de aplicación toohello e inicie un nuevo servicio de Service Fabric.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Comprimir el paquete de hello](service-fabric-package-apps.md#compress-a-package) antes de copiar el almacén de imágenes de toohello si el paquete de hello es demasiado grande o tiene muchos archivos. Obtenga más información [aquí](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Se puede implementar un servicio Service Fabric en diversas "configuraciones". Por ejemplo, se puede implementar como una o varias instancias o pueden implementarse de forma que hay una instancia del servicio de hello en cada nodo del clúster de Service Fabric Hola.

Hola `InstanceCount` parámetro de hello `New-ServiceFabricService` cmdlet es usado toospecify cuántas instancias del servicio de hello deben iniciarse en el clúster de Service Fabric Hola. Puede establecer hello `InstanceCount` valor, según el tipo de Hola de aplicación que se va a implementar. Hola dos los escenarios más comunes son:

* `InstanceCount = "1"`. En este caso, solo una instancia del servicio de Hola se implementa en el clúster de Hola. Programador de Service Fabric determina qué servicio de hello nodo queda toobe implementada en.
* `InstanceCount ="-1"`. En este caso, se implementa una instancia del servicio de hello en todos los nodos de clúster de Service Fabric Hola. resultado de Hello tiene uno (y sólo una) instancia del servicio de Hola para cada nodo de clúster de Hola.

Se trata de una configuración resulta útil para las aplicaciones front-end (por ejemplo, un extremo REST), porque las aplicaciones cliente demasiado necesitan "conectar" tooany de nodos de hello en el punto de conexión de hello clúster toouse Hola. Esta configuración también se puede utilizar cuando, por ejemplo, todos los nodos del clúster de Service Fabric Hola de equilibrador de carga conectado tooa. Tráfico de cliente, a continuación, se puede distribuir en servicio de Hola que se ejecuta en todos los nodos de clúster de Hola.

## <a name="check-your-running-application"></a>Comprobación de la aplicación en ejecución
En el Explorador de Service Fabric, identificar el nodo de Hola donde se ejecuta el servicio de Hola. En este ejemplo, se ejecuta en el nodo 1:

![Nodo donde se ejecuta el servicio](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Si desplazarse por los nodos toohello y explorar aplicación toohello, verá información del nodo esenciales de hello, incluida su ubicación en el disco.

![Ubicación en el disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

Si examina toohello directorio mediante el Explorador de servidores, puede encontrar el directorio de trabajo de Hola y de carpeta de registro del servicio de hello, tal y como se muestra en la siguiente captura de pantalla de hello: 

![Ubicación del registro](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo toopackage un ejecutable de invitado e implementarlo tooService tejido. Vea Hola siguientes artículos para obtener información relacionada y tareas.

* [Ejemplo para empaquetar e implementar un archivo ejecutable de invitado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), incluida una versión preliminar de toohello de vínculo de la herramienta de empaquetado de Hola
* [Ejemplo de dos archivos ejecutables (C# y nodejs) de invitado comunicarse a través del servicio de nomenclatura de hello con REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [Implementación de varios ejecutables invitados](service-fabric-deploy-multiple-apps.md)
* [Creación de la primera aplicación de Service Fabric en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
