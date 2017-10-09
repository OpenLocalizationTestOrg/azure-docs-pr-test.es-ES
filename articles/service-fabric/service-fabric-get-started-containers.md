---
title: "una aplicación de contenedor de Azure Service Fabric aaaCreate | Documentos de Microsoft"
description: "Cree la primera aplicación contenedora en Windows en Azure Service Fabric.  Crear una imagen de Docker con una aplicación de Python, registro de hello imagen tooa contenedor de inserción, compilar e implementar una aplicación de contenedor de Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Cree la primera aplicación contenedora en Service Fabric en Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Ejecutar una aplicación existente en un contenedor de Windows en un clúster de Service Fabric no requiere ninguna aplicación de tooyour de cambios. Este artículo le guiará por la creación de una imagen de Docker que contiene un Python [matraz](http://flask.pocoo.org/) implementación de clúster de Service Fabric tooa y aplicaciones web.  También compartirá la aplicación en el contenedor mediante [Azure Container Registry](/azure/container-registry/).  Este artículo supone que el usuario tiene un conocimiento básico de Docker. Puede obtener información sobre Docker leer hello [Introducción a Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Requisitos previos
Un equipo de desarrollo en el que se ejecute:
* Visual Studio 2015 o Visual Studio 2017.
* [SDK y herramientas de Service Fabric](service-fabric-get-started.md).
*  Docker para Windows.  [Obtener Docker CE para Windows (estable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description). Después de instalar e iniciar Docker, haga doble clic en el icono de bandeja de Hola y seleccione **cambiar contenedores tooWindows**. Se trata de imágenes de Docker de toorun requiere basadas en Windows.

Un clúster de Windows con tres, o más, nodos que se ejecute en Windows Server 2016 con contenedores: [Creación del primer clúster de Service Fabric en Azure](service-fabric-cluster-creation-via-portal.md) o [Prueba gratis de Service Fabric](https://aka.ms/tryservicefabric).

Un registro de Azure Container Registry: [cree un registro de contenedor](../container-registry/container-registry-get-started-portal.md) en la suscripción de Azure.

## <a name="define-hello-docker-container"></a>Definir el contenedor de Docker Hola
Crear una imagen basada en hello [imagen de Python](https://hub.docker.com/_/python/) ubicado en Docker Hub.

Defina el contenedor de Docker en un archivo Dockerfile. Hola Dockerfile contiene instrucciones para configurar el entorno de hello dentro de su contenedor, cargar aplicación hello desea toorun y asignación de puertos. Hola Dockerfile es Hola entrada toohello `docker build` comando, que crea la imagen de Hola.

Cree un directorio vacío y cree el archivo hello *Dockerfile* (con ninguna extensión de archivo). Agregue la Hola siguiente demasiado*Dockerfile* y guarde los cambios:

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

Hola de lectura [referencia sobre Dockerfile](https://docs.docker.com/engine/reference/builder/) para obtener más información.

## <a name="create-a-simple-web-application"></a>Creación de una aplicación web simple
Cree una aplicación web de Flask que escucha en el puerto 80 y devuelve "Hola mundo".  En el mismo directorio de Hola, crear archivo hello *requirements.txt*.  Agregue los siguiente hello y guarde los cambios:
```
Flask
```

Crear hello *app.py* de archivos y agregue Hola siguiente:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>Crear imagen de Hola
Ejecute hello `docker build` imagen de hello toocreate de comando que se ejecuta la aplicación web. Abra una ventana de PowerShell y navegue directory toohello que contiene hello Dockerfile. Ejecute el siguiente comando de hello:

```
docker build -t helloworldapp .
```

Este comando compilaciones Hola nueva imagen siguiendo las instrucciones de hello en el Dockerfile, nomenclatura (-t etiquetado) imagen Hola "helloworldapp". Creación de una imagen extrae la imagen base Hola hacia abajo de Docker Hub y crea una nueva imagen que agrega la aplicación encima de la imagen base Hola.  

Una vez completado el comando de compilación de hello, ejecute hello `docker images` toosee información en la nueva imagen de Hola de comandos:

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>Ejecutar la aplicación hello localmente
Compruebe la imagen localmente antes de Insertar registro de contenedor de Hola.  

Ejecute la aplicación hello:

```
docker run -d --name my-web-site helloworldapp
```

*nombre* ofrece un toohello de nombre ejecutando contenedor (en lugar de Id. de contenedor de hello).

Una vez que se inicia el contenedor de hello, encontrar su dirección IP para que puedan conectarse tooyour ejecutando el contenedor desde un explorador:
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

Conectar toohello ejecutando el contenedor.  Abra un explorador web que apunte toohello dirección IP que devuelve, por ejemplo "http://172.31.194.61". Debería ver Hola encabezado "¡Hello World!" mostrar en Explorador de Hola.

toostop su contenedor, ejecute:

```
docker stop my-web-site
```

Eliminar el contenedor de Hola desde el equipo de desarrollo:

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>Registro de contenedor de inserción Hola imagen toohello
Después de comprobar que el contenedor de Hola se ejecuta en el equipo de desarrollo, Insertar registro de hello imágenes tooyour en el registro de contenedor de Azure.

Ejecutar ``docker login`` toolog en tooyour del registro de contenedor con su [las credenciales del registro](../container-registry/container-registry-authentication.md).

Hello en el ejemplo siguiente se pasa Hola ID y la contraseña de Azure Active Directory [entidad de servicio](../active-directory/active-directory-application-objects.md). Por ejemplo, que puede que haya asignado un registro de tooyour principal de servicio para un escenario de automatización. O bien, puede iniciar sesión con su nombre de usuario y contraseña del registro.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hello comando siguiente crea una etiqueta o un alias de imagen de hello, con un registro de tooyour de ruta de acceso completa. En este ejemplo lugares Hola imagen Hola ```samples``` desorden de tooavoid de espacio de nombres en la raíz de hello del registro de hello.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Registro de contenedor de inserción Hola imagen tooyour:

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Crear servicio de hello en contenedores en Visual Studio
Hello SDK del servicio de Fabric y herramientas proporcionan una toohelp de plantilla de servicio se crea una aplicación en contenedores.

1. Inicie Visual Studio.  Seleccione **Archivo** > **Nuevo** > **Proyecto**.
2. Seleccione **Aplicación de Service Fabric**, asígnele el nombre "MyFirstContainer" y haga clic en **Aceptar**.
3. Seleccione **invitado contenedor** de lista de Hola de **plantillas de servicio**.
4. En **nombre de la imagen** escriba "myregistry.azurecr.io/samples/helloworldapp", imagen Hola inserta tooyour repositorio de contenedor.
5. Asigne un nombre a su servicio y haga clic en **Aceptar**.

## <a name="configure-communication"></a>Configuración de la comunicación
servicio de Hello en contenedores, necesita un punto de conexión para la comunicación. Agregar un `Endpoint` elemento con protocolo de hello, el puerto y el archivo de tipo toohello ServiceManifest.xml. En este artículo, el servicio de hello en contenedores escucha en el puerto 8081.  En este ejemplo, se usa un puerto fijo 8081.  Si no se especifica ningún puerto, se elige un puerto aleatorio del intervalo de puertos de aplicación Hola.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

Al definir un punto de conexión, Service Fabric publica Hola extremo toohello servicio de nombres.  Otros servicios que se ejecutan en el clúster de hello pueden resolver este contenedor.  También puede realizar la comunicación de contenedor a otro mediante hello [proxy inverso](service-fabric-reverseproxy.md).  La comunicación se realiza proporcionando el puerto de escucha de proxy inverso HTTP de Hola y el nombre de hello de servicios de Hola que desee toocommunicate con como variables de entorno.

## <a name="configure-and-set-environment-variables"></a>Configuración y establecimiento de variables de entorno
Las variables de entorno se pueden especificar para cada paquete de código en el manifiesto del servicio Hola. Esta característica está disponible para todos los servicios, con independencia de si se implementan como contenedores, procesos o archivos ejecutables de invitado. Puede invalidar la variable de entorno valores de la aplicación hello manifiesto o especifican durante la implementación como parámetros de la aplicación.

Hello fragmento XML de manifiesto de servicio siguiente muestra un ejemplo de cómo toospecify las variables de entorno para un paquete de código:
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Estas variables de entorno se pueden invalidar en el manifiesto de aplicación Hola:

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>Configurar la asignación de puerto de puerto a host del contenedor y la detección de contenedor a contenedor
Configurar una toocommunicate de puerto que se utiliza de host con el contenedor de Hola. enlace de puerto de Hello asigna el puerto de hello en qué Hola servicio está escuchando en hello contenedor tooa puerto en el host de Hola. Agregar un `PortBinding` elemento `ContainerHostPolicies` elemento del archivo de ApplicationManifest.xml Hola.  En este artículo, `ContainerPort` es 80 (contenedor de hello expone el puerto 80, como Hola especificado en Dockerfile) y `EndpointRef` es "Guest1TypeEndpoint" (Hola extremo previamente definido en el manifiesto del servicio de Hola).  Las solicitudes entrantes que el servicio en el puerto 8081 toohello están asignan tooport 80 en el contenedor de Hola.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>Configurar la autenticación de Container Registry
Configurar la autenticación de registro del contenedor mediante la adición de `RepositoryCredentials` demasiado`ContainerHostPolicies` del archivo de ApplicationManifest.xml Hola. Agregar cuenta de hello y una contraseña para el registro de hello myregistry.azurecr.io contenedor, lo que permite la imagen del contenedor de Hola Hola servicio toodownload del repositorio de Hola.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

Se recomienda que cifrar contraseñas de repositorio de hello mediante un certificado de cifrado que ha implementado tooall nodos de clúster de Hola. Cuando Service Fabric implementa el clúster de toohello de paquete de servicio de hello, certificado de cifrado de hello es texto de cifrado usado toodecrypt Hola.  cmdlet Invoke-ServiceFabricEncryptText de Hello es texto de cifrado de hello toocreate usado para contraseña de hello, que se agrega el archivo de ApplicationManifest.xml toohello.

Hello script siguiente crea un nuevo certificado autofirmado y exporta el archivo PFX de tooa.  certificado de Hola se importa en un almacén de claves existente y, a continuación, implementa el clúster de Service Fabric toohello.

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
Cifrar la contraseña de hello mediante hello [ServiceFabricEncryptText Invoke](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Reemplace contraseña Hola con texto de cifrado de hello devolviendo hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet y establecer `PasswordEncrypted` demasiado "true".

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a>Configuración del modo de aislamiento
Windows admite dos modos de aislamiento para contenedores: de proceso y de Hyper-V. Con el modo de aislamiento de procesos de hello, con todos los contenedores de Hola Hola mismo host máquina recurso compartido Hola kernel con el host de Hola. Con el modo de aislamiento de hello Hyper-V, los kernels de hello están aislados entre cada contenedor de Hyper-V y host de contenedor de Hola. se especifica el modo de aislamiento de Hola Hola `ContainerHostPolicies` elemento en el archivo de manifiesto de aplicación Hola. modos de aislamiento de Hola que pueden especificarse son `process`, `hyperv`, y `default`. modo de aislamiento predeterminado de Hello, valor predeterminado es demasiado`process` en Windows Server hospeda y el valor predeterminado es demasiado`hyperv` en hosts de Windows 10. Hello fragmento de código siguiente muestra cómo se especifica el modo de aislamiento de hello en el archivo de manifiesto de aplicación Hola.

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>Configuración de la regulación de recursos
[La regulación de recursos](service-fabric-resource-governance.md) restringe Hola recursos Hola contenedor pueden usar en el host de Hola. Hola `ResourceGovernancePolicy` elemento, que se especifica en el manifiesto de aplicación Hola, es los límites de recursos toodeclare usado para un paquete de código de servicio. Se pueden establecer límites de recursos para hello recursos siguientes: memoria, MemorySwap, CpuShares (peso relativo de CPU), MemoryReservationInMB, BlkioWeight (peso relativo de BlockIO).  En este ejemplo, el paquete de servicio Guest1Pkg Obtiene un núcleo en nodos de clúster de Hola donde se coloca.  Límites de memoria son absolutos, por lo que el paquete de código de hello es limitado too1024 MB de memoria (y una reserva de garantía de software del mismo Hola). Paquetes de código (contenedores o procesos) no son tooallocate capaz de más memoria que este límite e intentar toodo que se producirá una excepción de memoria insuficiente. Para toowork de cumplimiento del límite de recursos, todos los paquetes de código dentro de un paquete de servicio deben tener límites de memoria especificados.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>Implementar la aplicación de contenedor de hello
Guarde todos los cambios y genere la aplicación hello. toopublish la aplicación, el botón secundario en **MyFirstContainer** en el Explorador de soluciones y seleccione **publicar**.

En **extremo de la conexión**, escriba el extremo de administración de Hola para clúster Hola.  Por ejemplo, "containercluster.westus2.cloudapp.azure.com:19000". Puede encontrar la conexión de cliente de hello extremo en la hoja de información general de hello para el clúster en hello [portal de Azure](https://portal.azure.com).

Haga clic en **Publicar**.

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) es una herramienta web para inspeccionar y administrar aplicaciones y nodos en un clúster de Service Fabric. Abra un explorador y navegue toohttp://containercluster.westus2.cloudapp.azure.com:19080/explorador/y siga la implementación de la aplicación hello.  aplicación Hello implementa pero está en un estado de error hasta que se descarga la imagen de hello en nodos de clúster de hello (que pueden tardar algún tiempo, según el tamaño de la imagen de hello): ![Error][1]

aplicación Hello está listo cuando se encuentra en ```Ready``` estado: ![listo][2]

Abra un explorador y navegue toohttp://containercluster.westus2.cloudapp.azure.com:8081. Debería ver Hola encabezado "¡Hello World!" mostrar en Explorador de Hola.

## <a name="clean-up"></a>Limpieza
Continuar tooincur cargos mientras se está ejecutando el clúster de hello, considere la posibilidad de [eliminar el clúster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).  Los [clústeres de la entidad](http://tryazureservicefabric.westus.cloudapp.azure.com/) se eliminan automáticamente a las pocas horas.

Después de insertar el registro de contenedor de hello imagen toohello puede eliminar imagen local Hola desde el equipo de desarrollo:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Manifiestos de servicio y de aplicación de Service Fabric de ejemplo completos
Estas son servicio completo de Hola y manifiestos de aplicación que se usan en este artículo.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a>Configuración del intervalo de tiempo antes de hacer que se termine el contenedor

Puede configurar un intervalo de tiempo para hello en tiempo de ejecución toowait antes de quita el contenedor de hello después hello eliminación de servicio (o un nodo de tooanother de movimiento) se haya iniciado. Intervalo de tiempo de configuración Hola envía hello `docker stop <time in seconds>` contenedor toohello de comando.   Para más detalles, consulte [docker stop](https://docs.docker.com/engine/reference/commandline/stop/). toowait de intervalo de tiempo de Hola se especifica en hello `Hosting` sección. Hola siguiente fragmento de manifiesto de clúster muestra cómo hello tooset el intervalo de espera:

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
Hello intervalo de tiempo predeterminado se establece too10 segundos. Puesto que esta configuración es dinámica, una configuración solo actualizar en tiempo de espera de hello clúster actualizaciones Hola. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Configurar hello en tiempo de ejecución tooremove imágenes del contenedor sin usar

Puede configurar tooremove de clúster de Service Fabric Hola imágenes del contenedor sin usar del nodo de Hola. Esta configuración permite toobe de espacio en disco recuperado si están presentes en el nodo de hello demasiadas imágenes del contenedor.  tooenable esta función, la actualización hello `Hosting` sección manifiesto de clúster de hello tal y como se muestra en el siguiente fragmento de código de hello: 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

Para las imágenes que no se deben eliminar, puede especificar en hello `ContainerImagesToSkip` parámetro. 



## <a name="next-steps"></a>Pasos siguientes
* Más información acerca de cómo ejecutar [contenedores en Service Fabric](service-fabric-containers-overview.md).
* Hola de lectura [implementar una aplicación de .NET en un contenedor](service-fabric-host-app-in-a-container.md) tutorial.
* Obtenga información acerca de Service Fabric hello [ciclo de vida de la aplicación](service-fabric-application-lifecycle.md).
* Hola de desprotección [ejemplos de código de contenedor de Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) en GitHub.

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
