---
title: aaaService tejido e implementar contenedores | Documentos de Microsoft
description: "Hello y Service Fabric el uso de aplicaciones de microservicio toodeploy de contenedores. Este artículo describen las capacidades de hello Service Fabric proporciona contenedores y cómo toodeploy imagen de un contenedor de Windows en un clúster."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a>Implementar un tooService de contenedor de Windows Fabric
> [!div class="op_single_selector"]
> * [Implementación de un contenedor de Windows](service-fabric-deploy-container.md)
> * [Implementación de un contenedor de Docker](service-fabric-deploy-container-linux.md)
> 
> 

Este artículo le guiará por el proceso de hello de la creación de servicios en contenedores en contenedores de Windows.

Service Fabric tiene varias funcionalidades que le ayudarán a crear aplicaciones compuestas de microservicios que se ejecutan en contenedores. 

Hola capacidades incluyen:

* Activación e implementación de la imagen de contenedor
* Regulador de recursos
* Autenticación de repositorio
* Asignación de puerto a host de contenedor
* Detección y comunicación entre contenedores
* Capacidad tooconfigure y establecer variables de entorno

Echemos un vistazo a cómo las capacidades funciona cuando se está empaquetando una toobe de servicio en contenedores incluido en la aplicación.

## <a name="package-a-windows-container"></a>Empaquetado de un contenedor de Windows
Si empaqueta un contenedor, puede elegir toouse una plantilla de proyecto de Visual Studio o [crear paquete de aplicación Hola manualmente](#manually).  Si utiliza Visual Studio, la estructura del paquete de aplicación hello y archivos de manifiesto se crean mediante la plantilla de proyecto nuevo de Hola.

> [!TIP]
> toopackage de manera más fácil de Hello una imagen de contenedor existente en un servicio es toouse Visual Studio.

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>Usar Visual Studio toopackage una imagen de contenedor existente
Visual Studio proporciona a un tejido de servicio toohelp de plantilla de servicio implementa un clúster de Service Fabric tooa de contenedor.

1. Seleccione **Archivo** > **Nuevo proyecto** y cree una aplicación de Service Fabric.
2. Elija **invitado contenedor** como plantilla de servicio de Hola.
3. Elija **nombre de la imagen** y proporcionar la imagen de toohello de ruta de acceso de hello en el repositorio de contenedor. Por ejemplo, `myrepo/myimage:v1` en https://hub.docker.com
4. Asigne un nombre a su servicio y haga clic en **Aceptar**.
5. Si el servicio en contenedores, necesita un punto de conexión para la comunicación, ahora puede agregar Hola protocolo, puerto y archivo de tipo toohello ServiceManifest.xml. Por ejemplo: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Proporcionando hello `UriScheme`, Service Fabric registra automáticamente el punto de conexión de hello contenedor con servicio de nomenclatura para detectabilidad hello. puerto de Hello puede fijo (como se muestra en el anterior ejemplo de Hola) o se asigna de forma dinámica. Si no se especifica un puerto, se asigna dinámicamente de intervalo de puertos de aplicación Hola (tal y como sucedería con cualquier servicio).
    También necesita asignación de puertos de tooconfigure Hola contenedor toohost especificando un `PortBinding` directiva en el manifiesto de aplicación Hola. Para obtener más información, consulte [configurar la asignación de puerto de contenedor toohost](#Portsection).
6. Si el contenedor necesita la regulación de los recursos, agregue una directiva `ResourceGovernancePolicy`.
8. Si el contenedor necesita tooauthenticate con un repositorio privado, a continuación, agregue `RepositoryCredentials`.
7. Si está ejecutando en un equipo Windows Server 2016 con compatibilidad con el contenedor habilitado, puede usar el paquete de Hola y publicar el servicio de clúster local de acción toodeploy tooyour. 
8. Cuando esté listo, puede publicar clúster remoto de hello aplicación tooa o comprobar en el control de la solución toosource Hola. 

Para obtener un ejemplo, Hola de desprotección [ejemplos de código de contenedor de Service Fabric en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Creación de un clúster de Windows Server 2016
toodeploy la aplicación en contenedores, necesita toocreate habilitado de un clúster que ejecuta Windows Server 2016 con compatibilidad con el contenedor. El clúster puede ejecutarse localmente o implementarse en Azure mediante Azure Resource Manager. 

toodeploy un clúster mediante el Administrador de recursos de Azure, elija hello **Windows Server 2016 con contenedores** opción en Azure de la imagen. Vea el artículo de hello [crear un clúster de Service Fabric mediante Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Asegúrese de que usa Hola después de la configuración del Administrador de recursos de Azure:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
También puede usar hello [plantilla de cinco nodos Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate un clúster. Como alternativa, lea una [entrada de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) de la comunidad sobre el uso de Service Fabric y los contenedores de Windows.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Empaquetado e implementación manual de una imagen de contenedor
proceso de Hola de empaquetar manualmente un servicio en contenedores se basa en hello pasos:

1. Publicar el repositorio de tooyour de contenedores de Hola.
2. Crear estructura de directorios de paquetes de saludo.
3. Edite el archivo de manifiesto de servicio de Hola.
4. Edite el archivo de manifiesto de aplicación Hola.

## <a name="deploy-and-activate-a-container-image"></a>Implementación y activación de una imagen de contenedor
Hola Service Fabric [modelo de aplicación](service-fabric-application-model.md), un contenedor representa un host de aplicación en la que varios servicios se colocan las réplicas. toodeploy y activar un contenedor, el nombre de hello put de imagen del contenedor hello en un `ContainerHost` elemento en el manifiesto del servicio Hola.

En el manifiesto del servicio hello, agregue un `ContainerHost` Hola punto de entrada. A continuación, el conjunto de hello `ImageName` toobe nombre de Hola de repositorio de contenedor de Hola y de imagen. Hello manifiesto parcial siguiente muestra un ejemplo de cómo se denomina contenedor de hello toodeploy `myimage:v1` desde un repositorio, denominado `myrepo`:

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

Puede especificar toorun de comandos opcionales al iniciar el contenedor de hello en hello `Commands` elemento. Separe los distintos comandos con comas. 

## <a name="understand-resource-governance"></a>Descripción de la regulación de recursos
La regulación de recursos es una funcionalidad de contenedor de Hola que limita los recursos de Hola que Hola contenedor puede utilizar en el host de Hola. Hola `ResourceGovernancePolicy`, que se especifica en el manifiesto de aplicación Hola es los límites de recursos de toodeclare usado para un paquete de código de servicio. Se pueden establecer límites de recursos para hello recursos siguientes:

* Memoria
* MemorySwap
* CpuShares (peso relativo de CPU)
* MemoryReservationInMB  
* BlkioWeight (peso relativo de BlockIO).

> [!NOTE]
> Para una versión futura se ha planeado la compatibilidad para especificar límites de E/S de bloques como IOP, BPS de lectura/escritura y mucho más.
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>Autenticación de un repositorio
toodownload un contenedor, es posible que tenga repositorio de contenedor de toohello tooprovide las credenciales de inicio de sesión. Hola inicio de sesión credenciales, especificadas en el manifiesto de aplicación Hola, son utilizados toospecify Hola inicio de sesión en la información o clave SSH, para descargar la imagen de contenedor de Hola Hola repositorio de imágenes. Hello en el ejemplo siguiente se muestra una cuenta llamada *Usuarioprueba* junto con la contraseña de hello en texto no cifrado (*no* recomendado):

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

Se recomienda que cifre la contraseña hello mediante un certificado que ha implementado la máquina toohello.

Hello en el ejemplo siguiente se muestra una cuenta llamada *Usuarioprueba*, donde contraseña hello se cifró mediante el uso de un certificado denominado *MyCert*. Puede usar hello `Invoke-ServiceFabricEncryptText` texto PowerShell comando toocreate hello secreto cifrado de contraseña de Hola. Para obtener más información, vea el artículo de hello [administrar secretos en aplicaciones de Service Fabric](service-fabric-application-secret-management.md).

clave privada de Hello del certificado de Hola que ha utilizado la contraseña de hello toodecrypt debe ser implementado toohello equipo local en un método fuera de banda. (en Azure esto se logra mediante Azure Resource Manager). A continuación, cuando Service Fabric implementa la máquina de toohello de paquete de servicio de hello, puede descifrar el secreto de Hola. Mediante el secreto de hello junto con el nombre de la cuenta de hello, a continuación, se pueda autenticar con el repositorio de contenedor de Hola.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name ="Portsection"></a>Configurar la asignación de puerto de contenedor toohost
Puede configurar una toocommunicate de puerto que se utiliza de host con el contenedor de hello especificando un `PortBinding` en el manifiesto de aplicación Hola. Hola puerto enlace mapas Hola puerto toowhich Hola servicio está escuchando en hello contenedor tooa puerto en el host de Hola.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>Configuración de detección y comunicación entre contenedores
Puede usar hello `PortBinding` elemento toomap un punto de conexión de tooan de puerto del contenedor en el manifiesto del servicio Hola. En el siguiente ejemplo de Hola Hola extremo `Endpoint1` especifica un puerto fijo, 8905. También no puede especificar ningún puerto en absoluto, en cuyo caso se elige un puerto aleatorio del intervalo de puertos de aplicaciones del clúster de Hola para usted.


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
Si especifica un punto de conexión, utilizando hello `Endpoint` etiqueta en el manifiesto del servicio Hola de un contenedor de invitado, Service Fabric automáticamente puede publicar este servicio de nombres de punto de conexión toohello. Otros servicios que se ejecutan en el clúster de hello, por tanto, pueden detectar este contenedor mediante consultas REST de hello en resolver.

Registrando con servicio de nomenclatura de hello, puede realizar el contenedor a la comunicación dentro de su contenedor mediante hello [proxy inverso](service-fabric-reverseproxy.md). La comunicación se realiza proporcionando el puerto de escucha de http de proxy inverso de Hola y el nombre de hello de servicios de Hola que desee toocommunicate con como variables de entorno. Para obtener más información, vea la sección siguiente Hola. 

## <a name="configure-and-set-environment-variables"></a>Configuración y establecimiento de variables de entorno
Las variables de entorno se pueden especificar para cada paquete de código en el manifiesto del servicio Hola. Esta característica está disponible para todos los servicios, con independencia de si se implementan como contenedores, procesos o archivos ejecutables de invitado. Puede invalidar la variable de entorno valores de la aplicación hello manifiesto o especifican durante la implementación como parámetros de la aplicación.

Hello fragmento XML de manifiesto de servicio siguiente muestra un ejemplo de cómo toospecify las variables de entorno para un paquete de código:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

Estas variables de entorno pueden reemplazarse en nivel de manifiesto de aplicación Hola:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

En el ejemplo anterior de hello, se especifica un valor explícito para hello `HttpGateway` variable de entorno (19000), aunque se establezca el valor de Hola para `BackendServiceName` parámetro mediante hello `[BackendSvc]` parámetro de la aplicación. Estas opciones le permiten toospecify valor de Hola para `BackendServiceName`valor al implementar la aplicación hello y no tiene un valor fijo en el manifiesto de Hola.

## <a name="configure-isolation-mode"></a>Configuración del modo de aislamiento

Windows admite dos modos de aislamiento para contenedores: de proceso y de Hyper-V.  Con el modo de aislamiento de procesos de hello, con todos los contenedores de Hola Hola mismo host máquina recurso compartido Hola kernel con el host de Hola. Con el modo de aislamiento de hello Hyper-V, los kernels de hello están aislados entre cada contenedor de Hyper-V y host de contenedor de Hola. se especifica el modo de aislamiento de Hola Hola `ContainerHostPolicies` etiqueta en el archivo de manifiesto de aplicación Hola.  modos de aislamiento de Hola que pueden especificarse son `process`, `hyperv`, y `default`. Hola `default` el modo de aislamiento predeterminado es demasiado`process` en Windows Server hospeda y el valor predeterminado es demasiado`hyperv` en hosts de Windows 10.  Hello fragmento de código siguiente muestra cómo se especifica el modo de aislamiento de hello en el archivo de manifiesto de aplicación Hola.

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a>Ejemplos completos de manifiesto de servicio y de aplicación

Este es un ejemplo de un manifiesto de aplicación:

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

A continuación se muestra un ejemplo de manifiesto de servicio (especificado en hello anterior manifiesto de aplicación):

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha implementado un servicio en contenedores, obtenga información acerca de cómo toomanage su ciclo de vida leyendo [ciclo de vida de aplicación de Service Fabric](service-fabric-application-lifecycle.md).

* [Información general: Service Fabric y contenedores](service-fabric-containers-overview.md)
* Para un ejemplo, consulte los [ejemplos de código de contenedor de Service Fabric en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
