---
title: "Service Fabric e implementación de contenedores | Microsoft Docs"
description: "Service Fabric y el uso de contenedores para implementar aplicaciones de microservicios. En este artículo se describen las funcionalidades que ofrece Service Fabric para los contenedores y cómo implementar una imagen de contenedor de Windows en un clúster."
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
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a>Implementación de un contenedor de Windows en Service Fabric
> [!div class="op_single_selector"]
> * [Implementación de un contenedor de Windows](service-fabric-deploy-container.md)
> * [Implementación de un contenedor de Docker](service-fabric-deploy-container-linux.md)
> 
> 

Este artículo le guiará a través del proceso de creación de servicios de contenedor en contenedores de Windows.

Service Fabric tiene varias funcionalidades que le ayudarán a crear aplicaciones compuestas de microservicios que se ejecutan en contenedores. 

Entre estas funcionalidades, cabe destacar:

* Activación e implementación de la imagen de contenedor
* Regulador de recursos
* Autenticación de repositorio
* Asignación de puerto a host de contenedor
* Detección y comunicación entre contenedores
* Capacidad de configurar y establecer variables de entorno

Echemos un vistazo a cada una de las funcionalidades al empaquetar un servicio en contenedor que desea incluir en la aplicación.

## <a name="package-a-windows-container"></a>Empaquetado de un contenedor de Windows
Al empaquetar un contenedor, puede usar una plantilla de proyecto de Visual Studio o [crear el paquete de aplicación manualmente](#manually).  Con Visual Studio, la estructura del paquete de aplicación y los archivos de manifiesto se crean mediante la plantilla para nuevos proyectos.

> [!TIP]
> La forma más sencilla de empaquetar una imagen de contenedor en un servicio es mediante Visual Studio.

## <a name="use-visual-studio-to-package-an-existing-container-image"></a>Uso de Visual Studio para empaquetar una imagen de contenedor existente
Visual Studio proporciona una plantilla de servicio de Service Fabric para ayudarle a implementar un contenedor en un clúster de Service Fabric.

1. Seleccione **Archivo** > **Nuevo proyecto** y cree una aplicación de Service Fabric.
2. Elija **Contenedor invitado** como la plantilla de servicio.
3. Elija el **Nombre de imagen** y proporcione la ruta de acceso a la imagen en el repositorio de contenedores. Por ejemplo, `myrepo/myimage:v1` en https://hub.docker.com
4. Asigne un nombre a su servicio y haga clic en **Aceptar**.
5. Si el servicio en contenedores necesita un punto de conexión para establecer comunicación, ahora podrá agregar el protocolo, el puerto y el tipo al archivo ServiceManifest.xml. Por ejemplo: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Si se especifica `UriScheme`, Service Fabric registra automáticamente el punto de conexión del contenedor con el servicio de nombres de Service Fabric para facilitar la detección. El puerto puede fijarse (como se muestra en el ejemplo anterior) o asignarse dinámicamente. Si no se especifica un puerto, se asigna dinámicamente desde el intervalo de puertos de la aplicación (como ocurre con cualquier otro servicio).
    También puede configurar la asignación de puerto a host del contenedor si especifica una directiva `PortBinding` en el manifiesto de aplicación. Para más información, consulte [Configuración de la asignación de puerto a host del contenedor](#Portsection).
6. Si el contenedor necesita la regulación de los recursos, agregue una directiva `ResourceGovernancePolicy`.
8. Si el contenedor necesita autenticarse con un repositorio privado, agregue `RepositoryCredentials`.
7. Si utiliza una máquina con Windows Server 2016 compatible con el contenedor habilitado, puede usar la acción de empaquetar y publicar para la implementación del clúster local. 
8. Cuando esté listo puede publicar la aplicación en un clúster remoto o comprobar la solución en el control de código fuente. 

Para un ejemplo, consulte los [ejemplos de código de contenedor de Service Fabric en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).

## <a name="creating-a-windows-server-2016-cluster"></a>Creación de un clúster de Windows Server 2016
Para implementar la aplicación en contenedores, debe crear un clúster que ejecute Windows Server 2016 con la compatibilidad con contenedores habilitada. El clúster puede ejecutarse localmente o implementarse en Azure mediante Azure Resource Manager. 

Para implementar un clúster con Azure Resource Manager, elija la opción de imagen **Windows Server 2016 with Containers** (Windows Server 2016 con contenedores) en Azure. Vea el artículo [Creación de un clúster de Service Fabric con Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Asegúrese de usar la configuración de Azure Resource Manager siguiente:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
También puede usar la [plantilla de cinco nodos de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) para crear un clúster. Como alternativa, lea una [entrada de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) de la comunidad sobre el uso de Service Fabric y los contenedores de Windows.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Empaquetado e implementación manual de una imagen de contenedor
El proceso de empaquetado manual de un servicio en contenedor se basa en los siguientes pasos:

1. Publicar los contenedores en el repositorio.
2. Crear la estructura de directorios del paquete.
3. Editar el archivo de manifiesto de servicio.
4. Editar el archivo de manifiesto de aplicación.

## <a name="deploy-and-activate-a-container-image"></a>Implementación y activación de una imagen de contenedor
En el [modelo de aplicación](service-fabric-application-model.md)de Service Fabric, un contenedor representa un host de la aplicación en el que se colocan varias réplicas de servicio. Para implementar y activar un contenedor, ponga el nombre de la imagen de contenedor en un elemento `ContainerHost` en el manifiesto de servicio.

En el manifiesto de servicio, añada un elemento `ContainerHost` para el punto de entrada. A continuación, establezca el elemento `ImageName` como nombre de la imagen y el repositorio del contenedor. El siguiente manifiesto parcial muestra un ejemplo de cómo implementar el contenedor llamado `myimage:v1` desde un repositorio denominado `myrepo`:

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

Puede especificar comandos opcionales para que se ejecuten al iniciar el contenedor en el elemento `Commands`. Separe los distintos comandos con comas. 

## <a name="understand-resource-governance"></a>Descripción de la regulación de recursos
La regulación de recursos es una funcionalidad del contenedor que permite restringir los recursos que puede usar el contenedor en el host. El elemento `ResourceGovernancePolicy`, especificado en el manifiesto de la aplicación, se utiliza para declarar los límites de recursos para un paquete de código de servicio. Es posible establecer límites para los siguientes recursos:

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
Para descargar un contenedor, puede que tenga que proporcionar credenciales de inicio de sesión para el repositorio de contenedor. Las credenciales de inicio de sesión incluidas en el manifiesto de la aplicación se usan para especificar la información de inicio de sesión, o clave SSH, para descargar la imagen del contenedor desde el repositorio de imágenes. En el ejemplo siguiente se muestra una cuenta llamada *TestUser* junto con la contraseña no cifrada (*no* recomendado):

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

Se recomienda cifrar la contraseña mediante un certificado implementado en la máquina.

El ejemplo siguiente muestra una cuenta denominada *TestUser* con la contraseña cifrada mediante un certificado llamado *MyCert*. Puede usar el comando de PowerShell `Invoke-ServiceFabricEncryptText` para crear el texto cifrado secreto de la contraseña. Para más información, consulte el artículo [Administración de secretos en aplicaciones de Service Fabric](service-fabric-application-secret-management.md).

La clave privada del certificado que se usa para descifrar la contraseña se debe implementar en la máquina local con un método fuera de banda (en Azure esto se logra mediante Azure Resource Manager). Posteriormente, cuando Service Fabric implementa el paquete de servicio en la máquina, es capaz de descifrar el secreto. Al usar el secreto junto con el nombre de cuenta, puede autenticarse con el repositorio de contenedor.

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

## <a name ="Portsection"></a> Configuración de la asignación de puerto a host del contenedor
Puede configurar un puerto de host utilizado para comunicarse con el contenedor mediante la especificación de un elemento `PortBinding` en el manifiesto de aplicación. El enlace de puerto asigna el puerto que el servicio está escuchando dentro del contenedor a un puerto en el host.

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
Puede usar el elemento `PortBinding` para asignar un puerto del contenedor a un punto de conexión del manifiesto de servicio. En el ejemplo siguiente, el punto de conexión `Endpoint1` especifica un puerto fijo, 8905. También puede no especificar ningún puerto, en cuyo caso se elegirá un puerto aleatorio del intervalo de puertos de la aplicación del clúster.


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
Si especifica un punto de conexión, al usar la etiqueta `Endpoint` en el manifiesto de servicio de un contenedor invitado, Service Fabric puede publicar automáticamente este punto de conexión en el servicio de nombres. De este modo, otros servicios que se ejecutan en el clúster podrán detectar que este contenedor usa las consultas REST para la resolución.

Al registrarse con el servicio de nombres, se puede establecer la comunicación de contenedor a contenedor dentro del contenedor mediante el [proxy inverso](service-fabric-reverseproxy.md). La comunicación se establece al proporcionar el puerto de escucha http de proxy inverso y el nombre de los servicios con los que desea comunicarse como variables de entorno. Para más información, consulte la siguiente sección. 

## <a name="configure-and-set-environment-variables"></a>Configuración y establecimiento de variables de entorno
En el manifiesto de servicio, las variables de entorno se pueden especificar para cada paquete de código. Esta característica está disponible para todos los servicios, con independencia de si se implementan como contenedores, procesos o archivos ejecutables de invitado. Estos valores de variable de entorno se invalidan en el manifiesto de aplicación o se especifican durante la implementación como parámetros de la aplicación.

El siguiente fragmento de código XML del manifiesto de servicio muestra un ejemplo de cómo especificar variables de entorno para un paquete de código:

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

Estas variables de entorno se pueden invalidar en el nivel del manifiesto de aplicación:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

En el ejemplo anterior, se ha especificado un valor explícito para la variable de entorno `HttpGateway` (19000), mientras que el valor del parámetro `BackendServiceName` se ha establecido a través del parámetro de la aplicación `[BackendSvc]`. Esta configuración permite especificar el valor de `BackendServiceName` al implementar la aplicación sin necesidad de tener un valor fijo en el manifiesto.

## <a name="configure-isolation-mode"></a>Configuración del modo de aislamiento

Windows admite dos modos de aislamiento para contenedores: de proceso y de Hyper-V.  Con el modo de aislamiento de proceso, todos los contenedores que se ejecutan en la misma máquina host comparten el kernel con el host. Con el modo de aislamiento de Hyper-V, los kernels se aíslan entre los contenedores de Hyper-V y el host del contenedor. El modo de aislamiento se especifica en la etiqueta `ContainerHostPolicies` del archivo de manifiesto de aplicación.  Los modos de aislamiento que se pueden especificar son `process`, `hyperv` y `default`. `default` es `process` en los hosts de Windows Server y `hyperv` en los hosts de Windows 10 de forma predeterminada.  El siguiente fragmento de código muestra cómo el modo de aislamiento se especifica en el archivo de manifiesto de aplicación.

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

Este es un ejemplo de manifiesto de servicio (especificado en el manifiesto de aplicación anterior):

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
Ahora que ha implementado un servicio en contenedor, consulte [Ciclo de vida de la aplicación de Service Fabric](service-fabric-application-lifecycle.md) para saber cómo administrar su ciclo de vida.

* [Información general: Service Fabric y contenedores](service-fabric-containers-overview.md)
* Para un ejemplo, consulte los [ejemplos de código de contenedor de Service Fabric en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
