---
title: "una aplicación de Node.js que usa MongoDB aaaDeploy | Documentos de Microsoft"
description: "Tutorial sobre cómo toopackage varios clúster invitado ejecutables toodeploy tooan Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a>Implementación de varios ejecutables invitados
Este artículo se muestra cómo toopackage e implementar varios invitado ejecutables tooAzure Service Fabric. Para compilar e implementar un único paquete de Service Fabric leen cómo demasiado[implementar un tejido de invitado ejecutable tooService](service-fabric-deploy-existing-app.md).

Aunque este tutorial muestra cómo toodeploy una aplicación con un front-end Node.js que usa MongoDB como almacén de datos de hello, puede aplicar aplicación tooany de hello pasos que tiene dependencias en otra aplicación.   

Puede usar el paquete de aplicación de Hola de tooproduce de Visual Studio que contiene varios archivos ejecutables de invitado. Vea [toopackage en Visual Studio una aplicación existente](service-fabric-deploy-existing-app.md). Después de haber agregado el primer ejecutable de invitado hello, haga clic en proyecto de aplicación de Hola y Hola seleccione **Agregar -> servicio de Fabric de servicio nueva** tooadd Hola segunda invitado proyecto ejecutable toohello solución. Nota: Si elige toolink origen de Hola Hola proyecto de Visual Studio, compilar la solución de Visual Studio de hello, asegurará de que el paquete de aplicación es una toodate con cambios en el origen de Hola. 

## <a name="samples"></a>Muestras
* [Ejemplo para empaquetar e implementar un archivo ejecutable invitado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Ejemplo de dos archivos ejecutables (C# y nodejs) de invitado comunicarse a través del servicio de nomenclatura de hello con REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>Manualmente el paquete Hola varias aplicaciones ejecutables de invitado
O bien puede empaquetar manualmente invitado Hola ejecutable. Para hacer el empaquetado manual de hello, este artículo usa la herramienta de empaquetado de Service Fabric hello, que está disponible en [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

### <a name="packaging-hello-nodejs-application"></a>Hola de empaquetado aplicación Node.js
En este artículo se da por supuesto que no está instalado Node.js en nodos de hello en clúster de Service Fabric Hola. En consecuencia, es necesario tooadd Node.exe el directorio de raíz de toohello de la aplicación de nodo antes de empaquetar. estructura de directorios de Hola de aplicación de Node.js de hello (mediante el marco de trabajo de web Express y motor de plantillas Jade) debería ser similar toohello uno a continuación:

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

El siguiente paso, creará un paquete de aplicación para hello aplicación Node.js. código de Hello siguiente crea un paquete de aplicación de Service Fabric que contiene la aplicación de Node.js Hola.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

A continuación se muestra una descripción de los parámetros de Hola que se utilizan:

* **/ source** puntos toohello directorio de aplicación Hola que debe empaquetarse.
* **/ target** define directorio hello en qué Hola se debe crear el paquete. Este directorio tiene toobe diferente hello directorio de origen.
* **/ appname** define el nombre de la aplicación hello de aplicación existente de Hola. Es importante toounderstand que esto traduce toohello nombre del servicio en el manifiesto de hello y no toohello nombre de aplicación de Service Fabric.
* **/exe** define Hola ejecutable que Service Fabric es ya debería estar toolaunch, en este caso `node.exe`.
* **/maen** define el argumento de Hola que está siendo usado toolaunch Hola ejecutable. A medida que no está instalado Node.js, Service Fabric debe servidor web de toolaunch hello Node.js ejecutando `node.exe bin/www`.  `/ma:'bin/www'`indica a toouse de herramienta de empaquetado de hello `bin/ma` como argumento de Hola para node.exe.
* **/ AppType** define el nombre del tipo de aplicación de hello Service Fabric.

Si examina el directorio toohello que especificó en el parámetro de hello/Target, puede ver que esa herramienta Hola ha creado un paquete de Service Fabric totalmente operativo tal y como se muestra a continuación:

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Hola ServiceManifest.xml generado tiene ahora una sección que describe cómo debería iniciarse servidor web de Node.js de hello, como se muestra en el siguiente fragmento de código de hello:

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
En este ejemplo, servidor web de Node.js de hello escucha a tooport 3000, por lo que necesita información de extremo de hello tooupdate en archivo de hello ServiceManifest.xml tal y como se muestra a continuación.   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>Hola empaquetar aplicación de MongoDB
Ahora que ha empaquetado aplicación Node.js de hello, puede seguir adelante y MongoDB del paquete. Como se mencionó antes, pasos de Hola que atraviesan ahora no son tooNode.js específico y MongoDB. De hecho, se aplican a las aplicaciones de tooall que pretenden toobe empaquetada como una aplicación de Service Fabric.  

toopackage MongoDB, desea toomake seguro que empaquetar Mongod.exe y Mongo.exe. Ambos archivos binarios se encuentran en hello `bin` directorio de su directorio de instalación de MongoDB. estructura de directorios de Hello tiene un aspecto similar toohello uno a continuación.

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Service Fabric necesita toostart MongoDB con un toohello similar de comando uno siguiente, por lo que necesita toouse hello `/ma` parámetro al empaquetar MongoDB.

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> no se va a conservar datos Hello en caso de hello de un error de nodo si coloca el directorio de datos de MongoDB hello en el directorio local de hello del nodo de Hola. Debe usar almacenamiento duradero o implementar una réplica de MongoDB establecer orden tooprevent pérdida de datos.  
>
>

En el shell de comandos de PowerShell o hello, ejecutamos la herramienta de empaquetado de hello con hello parámetros siguientes:

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

Orden tooadd MongoDB tooyour Service Fabric paquete de aplicación, deberá toomake seguro ese parámetro / Target Hola señala toohello mismo directorio que ya contiene el manifiesto de aplicación Hola junto con la aplicación de hello Node.js. También necesita toomake seguro de que está usando Hola ApplicationType homónimas.

Vamos a examinar el directorio toohello y examine qué herramienta Hola creada.

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Como puede ver, herramienta de hello agrega un nuevo directorio de toohello de carpeta, MongoDB, que contiene los archivos binarios de hello MongoDB. Si abre hello `ApplicationManifest.xml` archivo, puede ver ese paquete Hola ahora contiene aplicación Node.js de hello y MongoDB. siguiente de código de Hello muestra el contenido del manifiesto de aplicación Hola Hola.

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a>Publicar aplicación de hello
Hola último paso es clúster de Service Fabric local de toopublish Hola aplicación toohello mediante scripts de PowerShell de Hola a continuación:

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

Una vez aplicación hello clúster local toohello se publicó correctamente, puede tener acceso a aplicación Node.js de hello en el puerto de Hola que se ha introducido en el manifiesto del servicio Hola de aplicación de Node.js hello, por ejemplo http://localhost:3000.

En este tutorial, ha visto cómo tooeasily paquete dos aplicaciones existentes como una aplicación de Service Fabric. También ha aprendido cómo toodeploy se tooService tejido para que TI puedan beneficiarse de algunas de hello características de Service Fabric, como la integración de sistema de estado y disponibilidad alta.


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>Agregar más invitado ejecutables tooan aplicación existente mediante Yeoman en Linux

tooadd otra aplicación de tooan de servicio ya creado mediante `yo`, realizar Hola pasos: 
1. Cambiar toohello raíz del directorio de aplicación existente de Hola.  Por ejemplo, `cd ~/YeomanSamples/MyApplication`si `MyApplication` es aplicación Hola creado por Yeoman.
2. Ejecute `yo azuresfguest:AddService` y proporcionar detalles necesarios de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Obtener información acerca de la implementación de contenedores con [información general de Service Fabric y contenedores](service-fabric-containers-overview.md)
* [Ejemplo para empaquetar e implementar un archivo ejecutable invitado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Ejemplo de dos archivos ejecutables (C# y nodejs) de invitado comunicarse a través del servicio de nomenclatura de hello con REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
