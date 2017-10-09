---
title: aaaService tejido e implementar contenedores de Linux | Documentos de Microsoft
description: "Hello y Service Fabric el uso de aplicaciones de microservicio de toodeploy de contenedores de Linux. Este artículo describen las capacidades de hello Service Fabric proporciona contenedores y cómo toodeploy imagen de un contenedor de Linux en un clúster"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a>Implementar un tooService de contenedor Linux tejido
> [!div class="op_single_selector"]
> * [Implementación de un contenedor de Windows](service-fabric-deploy-container.md)
> * [Implementar un contenedor de Linux](service-fabric-deploy-container-linux.md)
>
>

Este artículo lo guiará a través de la creación de servicios de contenedor en contenedores de Docker en Linux.

Service Fabric tiene varias funcionalidades de contenedor que le ayudarán a crear aplicaciones que se componen de microservicios en contenedores. Son los llamados servicios en contenedores.

incluyen capacidades de Hello;

* Activación e implementación de la imagen de contenedor
* Regulador de recursos
* Autenticación de repositorio
* Asignación de puertos de puerto del contenedor toohost
* Detección y comunicación entre contenedores
* Capacidad tooconfigure y establecer variables de entorno

## <a name="packaging-a-docker-container-with-yeoman"></a>Empaquetado de un contenedor de Docker con Yeoman
Al empaquetar un contenedor en Linux, puede elegir cualquier toouse una plantilla de yeoman o [crear paquete de aplicación Hola manualmente](#manually).

Una aplicación de Service Fabric puede contener uno o varios contenedores, cada uno con un rol específico en la entrega de la funcionalidad de la aplicación hello. Hola servicio SDK de tejido para Linux incluye un [Yeoman](http://yeoman.io/) generador que hace más fácil toocreate la aplicación y agregar una imagen de contenedor. Vamos a usar Yeoman toocreate llama a una aplicación con un único contenedor de Docker *SimpleContainerApp*. Puede agregar más servicios más adelante mediante la edición de archivos de manifiesto de hello generado.

## <a name="install-docker-on-your-development-box"></a>Instalación de un contenedor de Docker en el cuadro de desarrollo

Siguiente ejecución Hola comandos docker tooinstall en el cuadro de desarrollo de Linux (si está usando imágenes vagrant hello en OSX, ya está instalado docker):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>Crear aplicación hello
1. En un terminal, escriba `yo azuresfcontainer`.
2. Dé nombre a la aplicación; por ejemplo, mycontainerap.
3. Proporcionar Hola URL de imagen de contenedor de Hola desde un repositorio de DockerHub. Hola imagen parámetro toma Hola formulario [repositorio] / [nombre de imagen]
4. Si Hola imagen no tiene un carga de trabajo-punto de entrada definido, deberá tooexplicitly especificar comandos de entrada con un conjunto delimitado por comas de toorun de comandos en el contenedor de hello, que se mantendrá el contenedor de Hola que se ejecuta después del inicio.

![Generador Yeoman de Service Fabric para contenedores][sf-yeoman]

## <a name="deploy-hello-application"></a>Implementar la aplicación hello

### <a name="using-xplat-cli"></a>Uso de la CLI multiplataforma
Una vez que se compila la aplicación hello, puede implementarlo toohello clúster local con hello CLI de Azure.

1. Conectar el clúster de Service Fabric local toohello.

    ```bash
    azure servicefabric cluster connect
    ```

2. Hola usar script de instalación proporcionado por el almacén de imágenes del clúster toohello del paquete en hello plantilla toocopy aplicación hello, registrar el tipo de aplicación Hola y cree una instancia de la aplicación hello.

    ```bash
    ./install.sh
    ```

3. Abra un explorador y navegue tooService Fabric Explorer en el Explorador de http://localhost:19080 / (sustituya localhost con la dirección IP privada de Hola de hello VM si usa a Vagrant en Mac OS X).
4. Expanda el nodo de aplicaciones de hello y observe que ahora hay una entrada para el tipo de aplicación y otro para hello primera instancia de ese tipo.
5. Usar scripts de desinstalación de hello proporcionado en la instancia de la aplicación de hello plantilla toodelete hello y anular el registro del tipo de aplicación Hola.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Uso de la CLI de Azure 2.0

Consulte la documentación de referencia de hello sobre la administración de un [ciclo de vida de aplicación mediante Hola CLI de Azure 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).

Para una aplicación de ejemplo, [Hola de extracción del repositorio código de contenedor de Service Fabric los ejemplos en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>Agregar más servicios tooan existente aplicación

tooadd otro contenedor de servicio aplicación tooan ya creado mediante `yo`, realizar Hola pasos:

1. Cambiar toohello raíz del directorio de aplicación existente de Hola.  Por ejemplo, `cd ~/YeomanSamples/MyApplication`si `MyApplication` es aplicación Hola creado por Yeoman.
2. Ejecute `yo azuresfcontainer:AddService`

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

Puede proporcionar los comandos de entrada mediante la especificación de hello opcional `Commands` elemento con un conjunto delimitado por comas de toorun de comandos en el contenedor de Hola.

> [!NOTE]
> Si Hola imagen no tiene un carga de trabajo-punto de entrada definido, deberá tooexplicitly especificar comandos entradas dentro de `Commands` elemento con un conjunto delimitado por comas de toorun de comandos en el contenedor de hello, que se mantendrá el contenedor de Hola que se ejecuta después de inicio.

## <a name="understand-resource-governance"></a>Descripción de la regulación de recursos
La regulación de recursos es una funcionalidad de contenedor de Hola que limita los recursos de Hola que Hola contenedor puede utilizar en el host de Hola. Hola `ResourceGovernancePolicy`, que se especifica en el manifiesto de aplicación Hola es los límites de recursos de toodeclare usado para un paquete de código de servicio. Se pueden establecer límites de recursos para hello recursos siguientes:

* Memoria
* MemorySwap
* CpuShares (peso relativo de CPU)
* MemoryReservationInMB  
* BlkioWeight (peso relativo de BlockIO).

> [!NOTE]
> En una versión futura, se incluirá compatibilidad para especificar límites de E/S de bloques como IOP, BPS de lectura/escritura y mucho más.
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

## <a name="configure-container-port-to-host-port-mapping"></a>Configuración de la asignación de puerto a host de contenedor
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
Mediante el uso de hello `PortBinding` directiva, puede asignar un puerto de contenedor tooan `Endpoint` en el manifiesto del servicio Hola. Hola extremo `Endpoint1` puede especificar un puerto fijo (por ejemplo, el puerto 80). También no puede especificar ningún puerto en absoluto, en cuyo caso se elige un puerto aleatorio del intervalo de puertos de aplicaciones del clúster de Hola para usted.

Si especifica un punto de conexión, utilizando hello `Endpoint` etiqueta en el manifiesto del servicio Hola de un contenedor de invitado, Service Fabric automáticamente puede publicar este servicio de nombres de punto de conexión toohello. Otros servicios que se ejecutan en el clúster de hello, por tanto, pueden detectar este contenedor mediante consultas REST de hello en resolver.

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

Registrando con servicio de nomenclatura de hello, puede hacer fácilmente un contenedor a la comunicación en el código de hello dentro de su contenedor mediante el uso de hello [proxy inverso](service-fabric-reverseproxy.md). La comunicación se realiza proporcionando el puerto de escucha de http de proxy inverso de Hola y el nombre de hello de servicios de Hola que desee toocommunicate con como variables de entorno. Para obtener más información, vea la sección siguiente Hola.

## <a name="configure-and-set-environment-variables"></a>Configuración y establecimiento de variables de entorno
Las variables de entorno se pueden especificar para cada paquete de código en el manifiesto del servicio hello, tanto para los servicios que se implementan en contenedores o para los servicios que se implementan como archivos ejecutables de procesos e invitados. Estos valores de variable de entorno se pueden invalidar específicamente en el manifiesto de aplicación Hola o especificados durante la implementación como parámetros de la aplicación.

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
* [Interactuar con los clústeres de Service Fabric usando Hola CLI de Azure](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>Artículos relacionados

* [Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Introducción a Service Fabric y la CLI de Azure 2.0)
* [Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Introducción a la CLI de XPlat de Service Fabric)
