---
title: "una aplicación de contenedor de Azure Service Fabric en Linux aaaCreate | Documentos de Microsoft"
description: "Cree la primera aplicación contenedora en Linux en Azure Service Fabric.  Crear una imagen de Docker con la aplicación, del registro de hello imagen tooa contenedor de inserción, compilar e implementar una aplicación de contenedor de Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>Cree la primera aplicación contenedora de Service Fabric en Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Ejecuta una aplicación existente en un contenedor de Linux en un clúster de Service Fabric no requiere ninguna aplicación de tooyour de cambios. Este artículo le guiará por la creación de una imagen de Docker que contiene un Python [matraz](http://flask.pocoo.org/) implementación de clúster de Service Fabric tooa y aplicaciones web.  También compartirá la aplicación en el contenedor mediante [Azure Container Registry](/azure/container-registry/).  Este artículo supone que el usuario tiene un conocimiento básico de Docker. Puede obtener información sobre Docker leer hello [Introducción a Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Requisitos previos
* Un equipo de desarrollo en el que se ejecute:
  * [SDK y herramientas de Service Fabric](service-fabric-get-started-linux.md).
  * [Docker CE para Linux](https://docs.docker.com/engine/installation/#prior-releases). 
  * [CLI de Service Fabric](service-fabric-cli.md)

* Un registro de Azure Container Registry: [cree un registro de contenedor](../container-registry/container-registry-get-started-portal.md) en la suscripción de Azure. 

## <a name="define-hello-docker-container"></a>Definir el contenedor de Docker Hola
Crear una imagen basada en hello [imagen de Python](https://hub.docker.com/_/python/) ubicado en Docker Hub. 

Defina el contenedor de Docker en un archivo Dockerfile. Hola Dockerfile contiene instrucciones para configurar el entorno de hello dentro de su contenedor, cargar aplicación hello desea toorun y asignación de puertos. Hola Dockerfile es Hola entrada toohello `docker build` comando, que crea la imagen de Hola. 

Cree un directorio vacío y cree el archivo hello *Dockerfile* (con ninguna extensión de archivo). Agregue la Hola siguiente demasiado*Dockerfile* y guarde los cambios:

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
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

## <a name="build-hello-image"></a>Crear imagen de Hola
Ejecute hello `docker build` imagen de hello toocreate de comando que se ejecuta la aplicación web. Abra una ventana de PowerShell y navegue demasiado*c:\temp\helloworldapp*. Ejecute el siguiente comando de hello:

```bash
docker build -t helloworldapp .
```

Este comando compilaciones Hola nueva imagen siguiendo las instrucciones de hello en el Dockerfile, nomenclatura (-t etiquetado) imagen Hola "helloworldapp". Creación de una imagen extrae la imagen base Hola hacia abajo de Docker Hub y crea una nueva imagen que agrega la aplicación encima de la imagen base Hola.  

Una vez completado el comando de compilación de hello, ejecute hello `docker images` toosee información en la nueva imagen de Hola de comandos:

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>Ejecutar la aplicación hello localmente
Compruebe que se ejecuta la aplicación en contenedores localmente antes de Insertar registro de contenedor de Hola.  

Ejecutar la aplicación hello, asignación del contenedor de su equipo puerto 4000 toohello expone el puerto 80:

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*nombre* ofrece un toohello de nombre ejecutando contenedor (en lugar de Id. de contenedor de hello).

Conectar toohello ejecutando el contenedor.  Abra un explorador web que señala la dirección IP toohello devuelta en el puerto 4000, por ejemplo "http://localhost:4000". Debería ver Hola encabezado "¡Hello World!" mostrar en Explorador de Hola.

!["¡Hola mundo!"][hello-world]

toostop su contenedor, ejecute:

```bash
docker stop my-web-site
```

Eliminar el contenedor de Hola desde el equipo de desarrollo:

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>Registro de contenedor de inserción Hola imagen toohello
Después de comprobar que la aplicación hello se ejecuta en Docker, Insertar registro de hello imágenes tooyour en el registro de contenedor de Azure.

Ejecutar `docker login` toolog en tooyour del registro de contenedor con su [las credenciales del registro](../container-registry/container-registry-authentication.md).

Hello en el ejemplo siguiente se pasa Hola ID y la contraseña de Azure Active Directory [entidad de servicio](../active-directory/active-directory-application-objects.md). Por ejemplo, que puede que haya asignado un registro de tooyour principal de servicio para un escenario de automatización.  O bien, puede iniciar sesión con su nombre de usuario y contraseña del registro.

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hello comando siguiente crea una etiqueta o un alias de imagen de hello, con un registro de tooyour de ruta de acceso completa. En este ejemplo lugares Hola imagen Hola `samples` desorden de tooavoid de espacio de nombres en la raíz de hello del registro de hello.

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Registro de contenedor de inserción Hola imagen tooyour:

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>Imagen de Docker de paquete Hola con Yeoman
Hola servicio SDK de tejido para Linux incluye un [Yeoman](http://yeoman.io/) generador que hace más fácil toocreate la aplicación y agregar una imagen de contenedor. Vamos a usar Yeoman toocreate llama a una aplicación con un único contenedor de Docker *SimpleContainerApp*.

toocreate una aplicación de contenedor de Service Fabric, abra una ventana de terminal y ejecute `yo azuresfcontainer`.  

Dé nombre a la aplicación (por ejemplo, "mycontainer"). 

Proporcionar Hola URL de imagen de contenedor de hello en un registro de contenedor (por ejemplo, ""). 

Esta imagen tiene una carga de trabajo definido de punto de entrada, por lo que necesitan tooexplicitly especificar comandos de entrada (los comandos ejecutados en el contenedor de hello, que se mantendrá el contenedor de Hola que se ejecuta después del inicio). 

Especifique un número de instancias de "1".

![Generador Yeoman de Service Fabric para contenedores][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>Configuración de la asignación de puertos y la autenticación de repositorios de contenedor
El servicio en contenedor necesita un punto de conexión para la comunicación.  Ahora agregue Hola protocolo, puerto y tipo tooan `Endpoint` en el archivo de hello ServiceManifest.xml. En este artículo, servicio de hello en contenedores escucha en el puerto 4000: 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
Proporcionar hello `UriScheme` automáticamente registros Hola punto de conexión de contenedor con servicio de nomenclatura de tejido de servicio de detectabilidad hello. Se proporciona un archivo de ejemplo completo de ServiceManifest.xml final Hola de este artículo. 

Configurar la asignación de puerto de host de puerto del contenedor de hello especificando un `PortBinding` directiva en `ContainerHostPolicies` del archivo de ApplicationManifest.xml Hola.  En este artículo, `ContainerPort` es 80 (contenedor de hello expone el puerto 80, como Hola especificado en Dockerfile) y `EndpointRef` es "myserviceTypeEndpoint" (extremo de hello definido en el manifiesto de servicio de hello).  Las solicitudes entrantes que el servicio en el puerto 4000 toohello están asignan tooport 80 en el contenedor de Hola.  Si el contenedor necesita tooauthenticate con un repositorio privado, a continuación, agregue `RepositoryCredentials`.  En este artículo, Agregar nombre de la cuenta de hello y una contraseña para el registro de hello myregistry.azurecr.io contenedor. 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>Compilación y paquete de aplicación de Service Fabric hello
plantillas de servicio tejido Yeoman Hola incluyen un script de compilación para [Gradle](https://gradle.org/), que puede usar toobuild aplicación Hola Hola terminal. toobuild y el paquete de aplicación hello, ejecute hello siguiente:

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>Implementar la aplicación hello
Una vez que se compila la aplicación hello, puede implementarla con hello CLI de tejido de servicio de clúster local toohello.

Conectar el clúster de Service Fabric local toohello.

```bash
sfctl cluster select --endpoint http://localhost:19080
```

Hola usar script de instalación proporcionado por el almacén de imágenes del clúster toohello del paquete en hello plantilla toocopy aplicación hello, registrar el tipo de aplicación Hola y cree una instancia de la aplicación hello.

```bash
./install.sh
```

Abra un explorador y navegue tooService Fabric Explorer en el Explorador de http://localhost:19080 / (sustituya localhost con la dirección IP privada de Hola de hello VM si usa a Vagrant en Mac OS X). Expanda el nodo de aplicaciones de hello y observe que ahora hay una entrada para el tipo de aplicación y otro para hello primera instancia de ese tipo.

Conectar toohello ejecutando el contenedor.  Abra un explorador web que señala la dirección IP toohello devuelta en el puerto 4000, por ejemplo "http://localhost:4000". Debería ver Hola encabezado "¡Hello World!" mostrar en Explorador de Hola.

!["¡Hola mundo!"][hello-world]

## <a name="clean-up"></a>Limpieza
Usar secuencia de comandos de desinstalación de hello proporcionadas en hello plantilla toodelete Hola instancia de la aplicación de clúster de desarrollo local de Hola y anular el registro del tipo de aplicación Hola.

```bash
./uninstall.sh
```

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
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a>Agregar más servicios tooan existente aplicación

llevar a cabo otra aplicación de tooan de servicio de contenedor ya creado mediante yeoman, tooadd Hola lo siguiente:

1. Cambiar toohello raíz del directorio de aplicación existente de Hola.  Por ejemplo, `cd ~/YeomanSamples/MyApplication`si `MyApplication` es aplicación Hola creado por Yeoman.
2. Ejecute `yo azuresfcontainer:AddService`

<a id="manually"></a>


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

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
