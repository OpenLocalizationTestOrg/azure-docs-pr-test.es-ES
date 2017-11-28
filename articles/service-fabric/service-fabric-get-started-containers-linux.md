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
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="85561-104">Cree la primera aplicación contenedora de Service Fabric en Linux</span><span class="sxs-lookup"><span data-stu-id="85561-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="85561-105">Windows</span><span class="sxs-lookup"><span data-stu-id="85561-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="85561-106">Linux</span><span class="sxs-lookup"><span data-stu-id="85561-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="85561-107">Ejecuta una aplicación existente en un contenedor de Linux en un clúster de Service Fabric no requiere ninguna aplicación de tooyour de cambios.</span><span class="sxs-lookup"><span data-stu-id="85561-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="85561-108">Este artículo le guiará por la creación de una imagen de Docker que contiene un Python [matraz](http://flask.pocoo.org/) implementación de clúster de Service Fabric tooa y aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="85561-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="85561-109">También compartirá la aplicación en el contenedor mediante [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="85561-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="85561-110">Este artículo supone que el usuario tiene un conocimiento básico de Docker.</span><span class="sxs-lookup"><span data-stu-id="85561-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="85561-111">Puede obtener información sobre Docker leer hello [Introducción a Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="85561-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85561-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="85561-112">Prerequisites</span></span>
* <span data-ttu-id="85561-113">Un equipo de desarrollo en el que se ejecute:</span><span class="sxs-lookup"><span data-stu-id="85561-113">A development computer running:</span></span>
  * <span data-ttu-id="85561-114">[SDK y herramientas de Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="85561-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="85561-115">[Docker CE para Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="85561-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="85561-116">CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="85561-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="85561-117">Un registro de Azure Container Registry: [cree un registro de contenedor](../container-registry/container-registry-get-started-portal.md) en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="85561-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="85561-118">Definir el contenedor de Docker Hola</span><span class="sxs-lookup"><span data-stu-id="85561-118">Define hello Docker container</span></span>
<span data-ttu-id="85561-119">Crear una imagen basada en hello [imagen de Python](https://hub.docker.com/_/python/) ubicado en Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="85561-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="85561-120">Defina el contenedor de Docker en un archivo Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="85561-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="85561-121">Hola Dockerfile contiene instrucciones para configurar el entorno de hello dentro de su contenedor, cargar aplicación hello desea toorun y asignación de puertos.</span><span class="sxs-lookup"><span data-stu-id="85561-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="85561-122">Hola Dockerfile es Hola entrada toohello `docker build` comando, que crea la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="85561-123">Cree un directorio vacío y cree el archivo hello *Dockerfile* (con ninguna extensión de archivo).</span><span class="sxs-lookup"><span data-stu-id="85561-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="85561-124">Agregue la Hola siguiente demasiado*Dockerfile* y guarde los cambios:</span><span class="sxs-lookup"><span data-stu-id="85561-124">Add hello following too*Dockerfile* and save your changes:</span></span>

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

<span data-ttu-id="85561-125">Hola de lectura [referencia sobre Dockerfile](https://docs.docker.com/engine/reference/builder/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="85561-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="85561-126">Creación de una aplicación web simple</span><span class="sxs-lookup"><span data-stu-id="85561-126">Create a simple web application</span></span>
<span data-ttu-id="85561-127">Cree una aplicación web de Flask que escucha en el puerto 80 y devuelve "Hola mundo".</span><span class="sxs-lookup"><span data-stu-id="85561-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="85561-128">En el mismo directorio de Hola, crear archivo hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="85561-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="85561-129">Agregue los siguiente hello y guarde los cambios:</span><span class="sxs-lookup"><span data-stu-id="85561-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="85561-130">Crear hello *app.py* de archivos y agregue Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="85561-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="85561-131">Crear imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="85561-131">Build hello image</span></span>
<span data-ttu-id="85561-132">Ejecute hello `docker build` imagen de hello toocreate de comando que se ejecuta la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="85561-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="85561-133">Abra una ventana de PowerShell y navegue demasiado*c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="85561-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="85561-134">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="85561-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="85561-135">Este comando compilaciones Hola nueva imagen siguiendo las instrucciones de hello en el Dockerfile, nomenclatura (-t etiquetado) imagen Hola "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="85561-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="85561-136">Creación de una imagen extrae la imagen base Hola hacia abajo de Docker Hub y crea una nueva imagen que agrega la aplicación encima de la imagen base Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="85561-137">Una vez completado el comando de compilación de hello, ejecute hello `docker images` toosee información en la nueva imagen de Hola de comandos:</span><span class="sxs-lookup"><span data-stu-id="85561-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="85561-138">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="85561-138">Run hello application locally</span></span>
<span data-ttu-id="85561-139">Compruebe que se ejecuta la aplicación en contenedores localmente antes de Insertar registro de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="85561-140">Ejecutar la aplicación hello, asignación del contenedor de su equipo puerto 4000 toohello expone el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="85561-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="85561-141">*nombre* ofrece un toohello de nombre ejecutando contenedor (en lugar de Id. de contenedor de hello).</span><span class="sxs-lookup"><span data-stu-id="85561-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="85561-142">Conectar toohello ejecutando el contenedor.</span><span class="sxs-lookup"><span data-stu-id="85561-142">Connect toohello running container.</span></span>  <span data-ttu-id="85561-143">Abra un explorador web que señala la dirección IP toohello devuelta en el puerto 4000, por ejemplo "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="85561-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="85561-144">Debería ver Hola encabezado "¡Hello World!"</span><span class="sxs-lookup"><span data-stu-id="85561-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="85561-145">mostrar en Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-145">display in hello browser.</span></span>

!["¡Hola mundo!"][hello-world]

<span data-ttu-id="85561-147">toostop su contenedor, ejecute:</span><span class="sxs-lookup"><span data-stu-id="85561-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="85561-148">Eliminar el contenedor de Hola desde el equipo de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="85561-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="85561-149">Registro de contenedor de inserción Hola imagen toohello</span><span class="sxs-lookup"><span data-stu-id="85561-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="85561-150">Después de comprobar que la aplicación hello se ejecuta en Docker, Insertar registro de hello imágenes tooyour en el registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="85561-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="85561-151">Ejecutar `docker login` toolog en tooyour del registro de contenedor con su [las credenciales del registro](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="85561-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="85561-152">Hello en el ejemplo siguiente se pasa Hola ID y la contraseña de Azure Active Directory [entidad de servicio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="85561-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="85561-153">Por ejemplo, que puede que haya asignado un registro de tooyour principal de servicio para un escenario de automatización.</span><span class="sxs-lookup"><span data-stu-id="85561-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="85561-154">O bien, puede iniciar sesión con su nombre de usuario y contraseña del registro.</span><span class="sxs-lookup"><span data-stu-id="85561-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="85561-155">Hello comando siguiente crea una etiqueta o un alias de imagen de hello, con un registro de tooyour de ruta de acceso completa.</span><span class="sxs-lookup"><span data-stu-id="85561-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="85561-156">En este ejemplo lugares Hola imagen Hola `samples` desorden de tooavoid de espacio de nombres en la raíz de hello del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="85561-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="85561-157">Registro de contenedor de inserción Hola imagen tooyour:</span><span class="sxs-lookup"><span data-stu-id="85561-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="85561-158">Imagen de Docker de paquete Hola con Yeoman</span><span class="sxs-lookup"><span data-stu-id="85561-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="85561-159">Hola servicio SDK de tejido para Linux incluye un [Yeoman](http://yeoman.io/) generador que hace más fácil toocreate la aplicación y agregar una imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="85561-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="85561-160">Vamos a usar Yeoman toocreate llama a una aplicación con un único contenedor de Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="85561-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="85561-161">toocreate una aplicación de contenedor de Service Fabric, abra una ventana de terminal y ejecute `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="85561-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="85561-162">Dé nombre a la aplicación (por ejemplo, "mycontainer").</span><span class="sxs-lookup"><span data-stu-id="85561-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="85561-163">Proporcionar Hola URL de imagen de contenedor de hello en un registro de contenedor (por ejemplo, "").</span><span class="sxs-lookup"><span data-stu-id="85561-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="85561-164">Esta imagen tiene una carga de trabajo definido de punto de entrada, por lo que necesitan tooexplicitly especificar comandos de entrada (los comandos ejecutados en el contenedor de hello, que se mantendrá el contenedor de Hola que se ejecuta después del inicio).</span><span class="sxs-lookup"><span data-stu-id="85561-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="85561-165">Especifique un número de instancias de "1".</span><span class="sxs-lookup"><span data-stu-id="85561-165">Specify an instance count of "1".</span></span>

![Generador Yeoman de Service Fabric para contenedores][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="85561-167">Configuración de la asignación de puertos y la autenticación de repositorios de contenedor</span><span class="sxs-lookup"><span data-stu-id="85561-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="85561-168">El servicio en contenedor necesita un punto de conexión para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="85561-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="85561-169">Ahora agregue Hola protocolo, puerto y tipo tooan `Endpoint` en el archivo de hello ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="85561-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="85561-170">En este artículo, servicio de hello en contenedores escucha en el puerto 4000:</span><span class="sxs-lookup"><span data-stu-id="85561-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="85561-171">Proporcionar hello `UriScheme` automáticamente registros Hola punto de conexión de contenedor con servicio de nomenclatura de tejido de servicio de detectabilidad hello.</span><span class="sxs-lookup"><span data-stu-id="85561-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="85561-172">Se proporciona un archivo de ejemplo completo de ServiceManifest.xml final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="85561-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="85561-173">Configurar la asignación de puerto de host de puerto del contenedor de hello especificando un `PortBinding` directiva en `ContainerHostPolicies` del archivo de ApplicationManifest.xml Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="85561-174">En este artículo, `ContainerPort` es 80 (contenedor de hello expone el puerto 80, como Hola especificado en Dockerfile) y `EndpointRef` es "myserviceTypeEndpoint" (extremo de hello definido en el manifiesto de servicio de hello).</span><span class="sxs-lookup"><span data-stu-id="85561-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="85561-175">Las solicitudes entrantes que el servicio en el puerto 4000 toohello están asignan tooport 80 en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="85561-176">Si el contenedor necesita tooauthenticate con un repositorio privado, a continuación, agregue `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="85561-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="85561-177">En este artículo, Agregar nombre de la cuenta de hello y una contraseña para el registro de hello myregistry.azurecr.io contenedor.</span><span class="sxs-lookup"><span data-stu-id="85561-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="85561-178">Compilación y paquete de aplicación de Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="85561-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="85561-179">plantillas de servicio tejido Yeoman Hola incluyen un script de compilación para [Gradle](https://gradle.org/), que puede usar toobuild aplicación Hola Hola terminal.</span><span class="sxs-lookup"><span data-stu-id="85561-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="85561-180">toobuild y el paquete de aplicación hello, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="85561-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="85561-181">Implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="85561-181">Deploy hello application</span></span>
<span data-ttu-id="85561-182">Una vez que se compila la aplicación hello, puede implementarla con hello CLI de tejido de servicio de clúster local toohello.</span><span class="sxs-lookup"><span data-stu-id="85561-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="85561-183">Conectar el clúster de Service Fabric local toohello.</span><span class="sxs-lookup"><span data-stu-id="85561-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="85561-184">Hola usar script de instalación proporcionado por el almacén de imágenes del clúster toohello del paquete en hello plantilla toocopy aplicación hello, registrar el tipo de aplicación Hola y cree una instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="85561-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="85561-185">Abra un explorador y navegue tooService Fabric Explorer en el Explorador de http://localhost:19080 / (sustituya localhost con la dirección IP privada de Hola de hello VM si usa a Vagrant en Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="85561-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="85561-186">Expanda el nodo de aplicaciones de hello y observe que ahora hay una entrada para el tipo de aplicación y otro para hello primera instancia de ese tipo.</span><span class="sxs-lookup"><span data-stu-id="85561-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="85561-187">Conectar toohello ejecutando el contenedor.</span><span class="sxs-lookup"><span data-stu-id="85561-187">Connect toohello running container.</span></span>  <span data-ttu-id="85561-188">Abra un explorador web que señala la dirección IP toohello devuelta en el puerto 4000, por ejemplo "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="85561-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="85561-189">Debería ver Hola encabezado "¡Hello World!"</span><span class="sxs-lookup"><span data-stu-id="85561-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="85561-190">mostrar en Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-190">display in hello browser.</span></span>

!["¡Hola mundo!"][hello-world]

## <a name="clean-up"></a><span data-ttu-id="85561-192">Limpieza</span><span class="sxs-lookup"><span data-stu-id="85561-192">Clean up</span></span>
<span data-ttu-id="85561-193">Usar secuencia de comandos de desinstalación de hello proporcionadas en hello plantilla toodelete Hola instancia de la aplicación de clúster de desarrollo local de Hola y anular el registro del tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="85561-194">Después de insertar el registro de contenedor de hello imagen toohello puede eliminar imagen local Hola desde el equipo de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="85561-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="85561-195">Manifiestos de servicio y de aplicación de Service Fabric de ejemplo completos</span><span class="sxs-lookup"><span data-stu-id="85561-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="85561-196">Estas son servicio completo de Hola y manifiestos de aplicación que se usan en este artículo.</span><span class="sxs-lookup"><span data-stu-id="85561-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="85561-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="85561-197">ServiceManifest.xml</span></span>
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
### <a name="applicationmanifestxml"></a><span data-ttu-id="85561-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="85561-198">ApplicationManifest.xml</span></span>
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
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="85561-199">Agregar más servicios tooan existente aplicación</span><span class="sxs-lookup"><span data-stu-id="85561-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="85561-200">llevar a cabo otra aplicación de tooan de servicio de contenedor ya creado mediante yeoman, tooadd Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="85561-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="85561-201">Cambiar toohello raíz del directorio de aplicación existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="85561-202">Por ejemplo, `cd ~/YeomanSamples/MyApplication`si `MyApplication` es aplicación Hola creado por Yeoman.</span><span class="sxs-lookup"><span data-stu-id="85561-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="85561-203">Ejecute `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="85561-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="85561-204">Configuración del intervalo de tiempo antes de hacer que se termine el contenedor</span><span class="sxs-lookup"><span data-stu-id="85561-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="85561-205">Puede configurar un intervalo de tiempo para hello en tiempo de ejecución toowait antes de quita el contenedor de hello después hello eliminación de servicio (o un nodo de tooanother de movimiento) se haya iniciado.</span><span class="sxs-lookup"><span data-stu-id="85561-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="85561-206">Intervalo de tiempo de configuración Hola envía hello `docker stop <time in seconds>` contenedor toohello de comando.</span><span class="sxs-lookup"><span data-stu-id="85561-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="85561-207">Para más detalles, consulte [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="85561-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="85561-208">toowait de intervalo de tiempo de Hola se especifica en hello `Hosting` sección.</span><span class="sxs-lookup"><span data-stu-id="85561-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="85561-209">Hola siguiente fragmento de manifiesto de clúster muestra cómo hello tooset el intervalo de espera:</span><span class="sxs-lookup"><span data-stu-id="85561-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="85561-210">Hello intervalo de tiempo predeterminado se establece too10 segundos.</span><span class="sxs-lookup"><span data-stu-id="85561-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="85561-211">Puesto que esta configuración es dinámica, una configuración solo actualizar en tiempo de espera de hello clúster actualizaciones Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="85561-212">Configurar hello en tiempo de ejecución tooremove imágenes del contenedor sin usar</span><span class="sxs-lookup"><span data-stu-id="85561-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="85561-213">Puede configurar tooremove de clúster de Service Fabric Hola imágenes del contenedor sin usar del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="85561-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="85561-214">Esta configuración permite toobe de espacio en disco recuperado si están presentes en el nodo de hello demasiadas imágenes del contenedor.</span><span class="sxs-lookup"><span data-stu-id="85561-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="85561-215">tooenable esta función, la actualización hello `Hosting` sección manifiesto de clúster de hello tal y como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="85561-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="85561-216">Para las imágenes que no se deben eliminar, puede especificar en hello `ContainerImagesToSkip` parámetro.</span><span class="sxs-lookup"><span data-stu-id="85561-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="85561-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="85561-217">Next steps</span></span>
* <span data-ttu-id="85561-218">Más información acerca de cómo ejecutar [contenedores en Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85561-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="85561-219">Hola de lectura [implementar una aplicación de .NET en un contenedor](service-fabric-host-app-in-a-container.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="85561-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="85561-220">Obtenga información acerca de Service Fabric hello [ciclo de vida de la aplicación](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="85561-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="85561-221">Hola de desprotección [ejemplos de código de contenedor de Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="85561-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
