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
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="7e47b-104">Cree la primera aplicación contenedora en Service Fabric en Windows</span><span class="sxs-lookup"><span data-stu-id="7e47b-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7e47b-105">Windows</span><span class="sxs-lookup"><span data-stu-id="7e47b-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="7e47b-106">Linux</span><span class="sxs-lookup"><span data-stu-id="7e47b-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="7e47b-107">Ejecutar una aplicación existente en un contenedor de Windows en un clúster de Service Fabric no requiere ninguna aplicación de tooyour de cambios.</span><span class="sxs-lookup"><span data-stu-id="7e47b-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="7e47b-108">Este artículo le guiará por la creación de una imagen de Docker que contiene un Python [matraz](http://flask.pocoo.org/) implementación de clúster de Service Fabric tooa y aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="7e47b-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="7e47b-109">También compartirá la aplicación en el contenedor mediante [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="7e47b-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="7e47b-110">Este artículo supone que el usuario tiene un conocimiento básico de Docker.</span><span class="sxs-lookup"><span data-stu-id="7e47b-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="7e47b-111">Puede obtener información sobre Docker leer hello [Introducción a Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="7e47b-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e47b-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7e47b-112">Prerequisites</span></span>
<span data-ttu-id="7e47b-113">Un equipo de desarrollo en el que se ejecute:</span><span class="sxs-lookup"><span data-stu-id="7e47b-113">A development computer running:</span></span>
* <span data-ttu-id="7e47b-114">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7e47b-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="7e47b-115">[SDK y herramientas de Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7e47b-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="7e47b-116">Docker para Windows.</span><span class="sxs-lookup"><span data-stu-id="7e47b-116">Docker for Windows.</span></span>  <span data-ttu-id="7e47b-117">[Obtener Docker CE para Windows (estable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="7e47b-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="7e47b-118">Después de instalar e iniciar Docker, haga doble clic en el icono de bandeja de Hola y seleccione **cambiar contenedores tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="7e47b-118">After installing and starting Docker, right-click on hello tray icon and select **Switch tooWindows containers**.</span></span> <span data-ttu-id="7e47b-119">Se trata de imágenes de Docker de toorun requiere basadas en Windows.</span><span class="sxs-lookup"><span data-stu-id="7e47b-119">This is required toorun Docker images based on Windows.</span></span>

<span data-ttu-id="7e47b-120">Un clúster de Windows con tres, o más, nodos que se ejecute en Windows Server 2016 con contenedores: [Creación del primer clúster de Service Fabric en Azure](service-fabric-cluster-creation-via-portal.md) o [Prueba gratis de Service Fabric](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="7e47b-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="7e47b-121">Un registro de Azure Container Registry: [cree un registro de contenedor](../container-registry/container-registry-get-started-portal.md) en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e47b-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-hello-docker-container"></a><span data-ttu-id="7e47b-122">Definir el contenedor de Docker Hola</span><span class="sxs-lookup"><span data-stu-id="7e47b-122">Define hello Docker container</span></span>
<span data-ttu-id="7e47b-123">Crear una imagen basada en hello [imagen de Python](https://hub.docker.com/_/python/) ubicado en Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="7e47b-123">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="7e47b-124">Defina el contenedor de Docker en un archivo Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="7e47b-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="7e47b-125">Hola Dockerfile contiene instrucciones para configurar el entorno de hello dentro de su contenedor, cargar aplicación hello desea toorun y asignación de puertos.</span><span class="sxs-lookup"><span data-stu-id="7e47b-125">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="7e47b-126">Hola Dockerfile es Hola entrada toohello `docker build` comando, que crea la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-126">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span>

<span data-ttu-id="7e47b-127">Cree un directorio vacío y cree el archivo hello *Dockerfile* (con ninguna extensión de archivo).</span><span class="sxs-lookup"><span data-stu-id="7e47b-127">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="7e47b-128">Agregue la Hola siguiente demasiado*Dockerfile* y guarde los cambios:</span><span class="sxs-lookup"><span data-stu-id="7e47b-128">Add hello following too*Dockerfile* and save your changes:</span></span>

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

<span data-ttu-id="7e47b-129">Hola de lectura [referencia sobre Dockerfile](https://docs.docker.com/engine/reference/builder/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7e47b-129">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="7e47b-130">Creación de una aplicación web simple</span><span class="sxs-lookup"><span data-stu-id="7e47b-130">Create a simple web application</span></span>
<span data-ttu-id="7e47b-131">Cree una aplicación web de Flask que escucha en el puerto 80 y devuelve "Hola mundo".</span><span class="sxs-lookup"><span data-stu-id="7e47b-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="7e47b-132">En el mismo directorio de Hola, crear archivo hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="7e47b-132">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="7e47b-133">Agregue los siguiente hello y guarde los cambios:</span><span class="sxs-lookup"><span data-stu-id="7e47b-133">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="7e47b-134">Crear hello *app.py* de archivos y agregue Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e47b-134">Also create hello *app.py* file and add hello following:</span></span>

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
## <a name="build-hello-image"></a><span data-ttu-id="7e47b-135">Crear imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="7e47b-135">Build hello image</span></span>
<span data-ttu-id="7e47b-136">Ejecute hello `docker build` imagen de hello toocreate de comando que se ejecuta la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7e47b-136">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="7e47b-137">Abra una ventana de PowerShell y navegue directory toohello que contiene hello Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="7e47b-137">Open a PowerShell window and navigate toohello directory containing hello Dockerfile.</span></span> <span data-ttu-id="7e47b-138">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7e47b-138">Run hello following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="7e47b-139">Este comando compilaciones Hola nueva imagen siguiendo las instrucciones de hello en el Dockerfile, nomenclatura (-t etiquetado) imagen Hola "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="7e47b-139">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="7e47b-140">Creación de una imagen extrae la imagen base Hola hacia abajo de Docker Hub y crea una nueva imagen que agrega la aplicación encima de la imagen base Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-140">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="7e47b-141">Una vez completado el comando de compilación de hello, ejecute hello `docker images` toosee información en la nueva imagen de Hola de comandos:</span><span class="sxs-lookup"><span data-stu-id="7e47b-141">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="7e47b-142">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="7e47b-142">Run hello application locally</span></span>
<span data-ttu-id="7e47b-143">Compruebe la imagen localmente antes de Insertar registro de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-143">Verify your image locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="7e47b-144">Ejecute la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="7e47b-144">Run hello application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="7e47b-145">*nombre* ofrece un toohello de nombre ejecutando contenedor (en lugar de Id. de contenedor de hello).</span><span class="sxs-lookup"><span data-stu-id="7e47b-145">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="7e47b-146">Una vez que se inicia el contenedor de hello, encontrar su dirección IP para que puedan conectarse tooyour ejecutando el contenedor desde un explorador:</span><span class="sxs-lookup"><span data-stu-id="7e47b-146">Once hello container starts, find its IP address so that you can connect tooyour running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="7e47b-147">Conectar toohello ejecutando el contenedor.</span><span class="sxs-lookup"><span data-stu-id="7e47b-147">Connect toohello running container.</span></span>  <span data-ttu-id="7e47b-148">Abra un explorador web que apunte toohello dirección IP que devuelve, por ejemplo "http://172.31.194.61".</span><span class="sxs-lookup"><span data-stu-id="7e47b-148">Open a web browser pointing toohello IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="7e47b-149">Debería ver Hola encabezado "¡Hello World!"</span><span class="sxs-lookup"><span data-stu-id="7e47b-149">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="7e47b-150">mostrar en Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-150">display in hello browser.</span></span>

<span data-ttu-id="7e47b-151">toostop su contenedor, ejecute:</span><span class="sxs-lookup"><span data-stu-id="7e47b-151">toostop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="7e47b-152">Eliminar el contenedor de Hola desde el equipo de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="7e47b-152">Delete hello container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="7e47b-153">Registro de contenedor de inserción Hola imagen toohello</span><span class="sxs-lookup"><span data-stu-id="7e47b-153">Push hello image toohello container registry</span></span>
<span data-ttu-id="7e47b-154">Después de comprobar que el contenedor de Hola se ejecuta en el equipo de desarrollo, Insertar registro de hello imágenes tooyour en el registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e47b-154">After you verify that hello container runs on your development machine, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="7e47b-155">Ejecutar ``docker login`` toolog en tooyour del registro de contenedor con su [las credenciales del registro](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7e47b-155">Run ``docker login`` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="7e47b-156">Hello en el ejemplo siguiente se pasa Hola ID y la contraseña de Azure Active Directory [entidad de servicio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="7e47b-156">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="7e47b-157">Por ejemplo, que puede que haya asignado un registro de tooyour principal de servicio para un escenario de automatización.</span><span class="sxs-lookup"><span data-stu-id="7e47b-157">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span> <span data-ttu-id="7e47b-158">O bien, puede iniciar sesión con su nombre de usuario y contraseña del registro.</span><span class="sxs-lookup"><span data-stu-id="7e47b-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="7e47b-159">Hello comando siguiente crea una etiqueta o un alias de imagen de hello, con un registro de tooyour de ruta de acceso completa.</span><span class="sxs-lookup"><span data-stu-id="7e47b-159">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="7e47b-160">En este ejemplo lugares Hola imagen Hola ```samples``` desorden de tooavoid de espacio de nombres en la raíz de hello del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="7e47b-160">This example places hello image in hello ```samples``` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="7e47b-161">Registro de contenedor de inserción Hola imagen tooyour:</span><span class="sxs-lookup"><span data-stu-id="7e47b-161">Push hello image tooyour container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a><span data-ttu-id="7e47b-162">Crear servicio de hello en contenedores en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7e47b-162">Create hello containerized service in Visual Studio</span></span>
<span data-ttu-id="7e47b-163">Hello SDK del servicio de Fabric y herramientas proporcionan una toohelp de plantilla de servicio se crea una aplicación en contenedores.</span><span class="sxs-lookup"><span data-stu-id="7e47b-163">hello Service Fabric SDK and tools provide a service template toohelp you create a containerized application.</span></span>

1. <span data-ttu-id="7e47b-164">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7e47b-164">Start Visual Studio.</span></span>  <span data-ttu-id="7e47b-165">Seleccione **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7e47b-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="7e47b-166">Seleccione **Aplicación de Service Fabric**, asígnele el nombre "MyFirstContainer" y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7e47b-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="7e47b-167">Seleccione **invitado contenedor** de lista de Hola de **plantillas de servicio**.</span><span class="sxs-lookup"><span data-stu-id="7e47b-167">Select **Guest Container** from hello list of **service templates**.</span></span>
4. <span data-ttu-id="7e47b-168">En **nombre de la imagen** escriba "myregistry.azurecr.io/samples/helloworldapp", imagen Hola inserta tooyour repositorio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="7e47b-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", hello image you pushed tooyour container repository.</span></span>
5. <span data-ttu-id="7e47b-169">Asigne un nombre a su servicio y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7e47b-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="7e47b-170">Configuración de la comunicación</span><span class="sxs-lookup"><span data-stu-id="7e47b-170">Configure communication</span></span>
<span data-ttu-id="7e47b-171">servicio de Hello en contenedores, necesita un punto de conexión para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="7e47b-171">hello containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="7e47b-172">Agregar un `Endpoint` elemento con protocolo de hello, el puerto y el archivo de tipo toohello ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="7e47b-172">Add an `Endpoint` element with hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="7e47b-173">En este artículo, el servicio de hello en contenedores escucha en el puerto 8081.</span><span class="sxs-lookup"><span data-stu-id="7e47b-173">For this article, hello containerized service listens on port 8081.</span></span>  <span data-ttu-id="7e47b-174">En este ejemplo, se usa un puerto fijo 8081.</span><span class="sxs-lookup"><span data-stu-id="7e47b-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="7e47b-175">Si no se especifica ningún puerto, se elige un puerto aleatorio del intervalo de puertos de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-175">If no port is specified, a random port from hello application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="7e47b-176">Al definir un punto de conexión, Service Fabric publica Hola extremo toohello servicio de nombres.</span><span class="sxs-lookup"><span data-stu-id="7e47b-176">By defining an endpoint, Service Fabric publishes hello endpoint toohello Naming service.</span></span>  <span data-ttu-id="7e47b-177">Otros servicios que se ejecutan en el clúster de hello pueden resolver este contenedor.</span><span class="sxs-lookup"><span data-stu-id="7e47b-177">Other services running in hello cluster can resolve this container.</span></span>  <span data-ttu-id="7e47b-178">También puede realizar la comunicación de contenedor a otro mediante hello [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="7e47b-178">You can also perform container-to-container communication using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="7e47b-179">La comunicación se realiza proporcionando el puerto de escucha de proxy inverso HTTP de Hola y el nombre de hello de servicios de Hola que desee toocommunicate con como variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="7e47b-179">Communication is performed by providing hello reverse proxy HTTP listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="7e47b-180">Configuración y establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="7e47b-180">Configure and set environment variables</span></span>
<span data-ttu-id="7e47b-181">Las variables de entorno se pueden especificar para cada paquete de código en el manifiesto del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-181">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="7e47b-182">Esta característica está disponible para todos los servicios, con independencia de si se implementan como contenedores, procesos o archivos ejecutables de invitado.</span><span class="sxs-lookup"><span data-stu-id="7e47b-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="7e47b-183">Puede invalidar la variable de entorno valores de la aplicación hello manifiesto o especifican durante la implementación como parámetros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e47b-183">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="7e47b-184">Hello fragmento XML de manifiesto de servicio siguiente muestra un ejemplo de cómo toospecify las variables de entorno para un paquete de código:</span><span class="sxs-lookup"><span data-stu-id="7e47b-184">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="7e47b-185">Estas variables de entorno se pueden invalidar en el manifiesto de aplicación Hola:</span><span class="sxs-lookup"><span data-stu-id="7e47b-185">These environment variables can be overridden in hello application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="7e47b-186">Configurar la asignación de puerto de puerto a host del contenedor y la detección de contenedor a contenedor</span><span class="sxs-lookup"><span data-stu-id="7e47b-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="7e47b-187">Configurar una toocommunicate de puerto que se utiliza de host con el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-187">Configure a host port used toocommunicate  with hello container.</span></span> <span data-ttu-id="7e47b-188">enlace de puerto de Hello asigna el puerto de hello en qué Hola servicio está escuchando en hello contenedor tooa puerto en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-188">hello port binding maps hello port on which hello service is listening inside hello container tooa port on hello host.</span></span> <span data-ttu-id="7e47b-189">Agregar un `PortBinding` elemento `ContainerHostPolicies` elemento del archivo de ApplicationManifest.xml Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-189">Add a `PortBinding` element in `ContainerHostPolicies` element of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="7e47b-190">En este artículo, `ContainerPort` es 80 (contenedor de hello expone el puerto 80, como Hola especificado en Dockerfile) y `EndpointRef` es "Guest1TypeEndpoint" (Hola extremo previamente definido en el manifiesto del servicio de Hola).</span><span class="sxs-lookup"><span data-stu-id="7e47b-190">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (hello endpoint previously defined in hello service manifest).</span></span>  <span data-ttu-id="7e47b-191">Las solicitudes entrantes que el servicio en el puerto 8081 toohello están asignan tooport 80 en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-191">Incoming requests toohello service on port 8081 are mapped tooport 80 on hello container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="7e47b-192">Configurar la autenticación de Container Registry</span><span class="sxs-lookup"><span data-stu-id="7e47b-192">Configure container registry authentication</span></span>
<span data-ttu-id="7e47b-193">Configurar la autenticación de registro del contenedor mediante la adición de `RepositoryCredentials` demasiado`ContainerHostPolicies` del archivo de ApplicationManifest.xml Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-193">Configure container registry authentication by adding `RepositoryCredentials` too`ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span> <span data-ttu-id="7e47b-194">Agregar cuenta de hello y una contraseña para el registro de hello myregistry.azurecr.io contenedor, lo que permite la imagen del contenedor de Hola Hola servicio toodownload del repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-194">Add hello account and password for hello myregistry.azurecr.io container registry, which allows hello service toodownload hello container image from hello repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="7e47b-195">Se recomienda que cifrar contraseñas de repositorio de hello mediante un certificado de cifrado que ha implementado tooall nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-195">We recommend that you encrypt hello repository password by using an encipherment certificate that's deployed tooall nodes of hello cluster.</span></span> <span data-ttu-id="7e47b-196">Cuando Service Fabric implementa el clúster de toohello de paquete de servicio de hello, certificado de cifrado de hello es texto de cifrado usado toodecrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-196">When Service Fabric deploys hello service package toohello cluster, hello encipherment certificate is used toodecrypt hello cipher text.</span></span>  <span data-ttu-id="7e47b-197">cmdlet Invoke-ServiceFabricEncryptText de Hello es texto de cifrado de hello toocreate usado para contraseña de hello, que se agrega el archivo de ApplicationManifest.xml toohello.</span><span class="sxs-lookup"><span data-stu-id="7e47b-197">hello Invoke-ServiceFabricEncryptText cmdlet is used toocreate hello cipher text for hello password, which is added toohello ApplicationManifest.xml file.</span></span>

<span data-ttu-id="7e47b-198">Hello script siguiente crea un nuevo certificado autofirmado y exporta el archivo PFX de tooa.</span><span class="sxs-lookup"><span data-stu-id="7e47b-198">hello following script creates a new self-signed certificate and exports it tooa PFX file.</span></span>  <span data-ttu-id="7e47b-199">certificado de Hola se importa en un almacén de claves existente y, a continuación, implementa el clúster de Service Fabric toohello.</span><span class="sxs-lookup"><span data-stu-id="7e47b-199">hello certificate is imported into an existing key vault and then deployed toohello Service Fabric cluster.</span></span>

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
<span data-ttu-id="7e47b-200">Cifrar la contraseña de hello mediante hello [ServiceFabricEncryptText Invoke](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7e47b-200">Encrypt hello password using hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="7e47b-201">Reemplace contraseña Hola con texto de cifrado de hello devolviendo hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet y establecer `PasswordEncrypted` demasiado "true".</span><span class="sxs-lookup"><span data-stu-id="7e47b-201">Replace hello password with hello cipher text returned by hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` too"true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="7e47b-202">Configuración del modo de aislamiento</span><span class="sxs-lookup"><span data-stu-id="7e47b-202">Configure isolation mode</span></span>
<span data-ttu-id="7e47b-203">Windows admite dos modos de aislamiento para contenedores: de proceso y de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7e47b-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="7e47b-204">Con el modo de aislamiento de procesos de hello, con todos los contenedores de Hola Hola mismo host máquina recurso compartido Hola kernel con el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-204">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="7e47b-205">Con el modo de aislamiento de hello Hyper-V, los kernels de hello están aislados entre cada contenedor de Hyper-V y host de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-205">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="7e47b-206">se especifica el modo de aislamiento de Hola Hola `ContainerHostPolicies` elemento en el archivo de manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-206">hello isolation mode is specified in hello `ContainerHostPolicies` element in hello application manifest file.</span></span> <span data-ttu-id="7e47b-207">modos de aislamiento de Hola que pueden especificarse son `process`, `hyperv`, y `default`.</span><span class="sxs-lookup"><span data-stu-id="7e47b-207">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="7e47b-208">modo de aislamiento predeterminado de Hello, valor predeterminado es demasiado`process` en Windows Server hospeda y el valor predeterminado es demasiado`hyperv` en hosts de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7e47b-208">hello default isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="7e47b-209">Hello fragmento de código siguiente muestra cómo se especifica el modo de aislamiento de hello en el archivo de manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-209">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="7e47b-210">Configuración de la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="7e47b-210">Configure resource governance</span></span>
<span data-ttu-id="7e47b-211">[La regulación de recursos](service-fabric-resource-governance.md) restringe Hola recursos Hola contenedor pueden usar en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-211">[Resource governance](service-fabric-resource-governance.md) restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="7e47b-212">Hola `ResourceGovernancePolicy` elemento, que se especifica en el manifiesto de aplicación Hola, es los límites de recursos toodeclare usado para un paquete de código de servicio.</span><span class="sxs-lookup"><span data-stu-id="7e47b-212">hello `ResourceGovernancePolicy` element, which is specified in hello application manifest, is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="7e47b-213">Se pueden establecer límites de recursos para hello recursos siguientes: memoria, MemorySwap, CpuShares (peso relativo de CPU), MemoryReservationInMB, BlkioWeight (peso relativo de BlockIO).</span><span class="sxs-lookup"><span data-stu-id="7e47b-213">Resource limits can be set for hello following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="7e47b-214">En este ejemplo, el paquete de servicio Guest1Pkg Obtiene un núcleo en nodos de clúster de Hola donde se coloca.</span><span class="sxs-lookup"><span data-stu-id="7e47b-214">In this example, service package Guest1Pkg gets one core on hello cluster nodes where it is placed.</span></span>  <span data-ttu-id="7e47b-215">Límites de memoria son absolutos, por lo que el paquete de código de hello es limitado too1024 MB de memoria (y una reserva de garantía de software del mismo Hola).</span><span class="sxs-lookup"><span data-stu-id="7e47b-215">Memory limits are absolute, so hello code package is limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="7e47b-216">Paquetes de código (contenedores o procesos) no son tooallocate capaz de más memoria que este límite e intentar toodo que se producirá una excepción de memoria insuficiente.</span><span class="sxs-lookup"><span data-stu-id="7e47b-216">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="7e47b-217">Para toowork de cumplimiento del límite de recursos, todos los paquetes de código dentro de un paquete de servicio deben tener límites de memoria especificados.</span><span class="sxs-lookup"><span data-stu-id="7e47b-217">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a><span data-ttu-id="7e47b-218">Implementar la aplicación de contenedor de hello</span><span class="sxs-lookup"><span data-stu-id="7e47b-218">Deploy hello container application</span></span>
<span data-ttu-id="7e47b-219">Guarde todos los cambios y genere la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7e47b-219">Save all your changes and build hello application.</span></span> <span data-ttu-id="7e47b-220">toopublish la aplicación, el botón secundario en **MyFirstContainer** en el Explorador de soluciones y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="7e47b-220">toopublish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="7e47b-221">En **extremo de la conexión**, escriba el extremo de administración de Hola para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-221">In **Connection Endpoint**, enter hello management endpoint for hello cluster.</span></span>  <span data-ttu-id="7e47b-222">Por ejemplo, "containercluster.westus2.cloudapp.azure.com:19000".</span><span class="sxs-lookup"><span data-stu-id="7e47b-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="7e47b-223">Puede encontrar la conexión de cliente de hello extremo en la hoja de información general de hello para el clúster en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7e47b-223">You can find hello client connection endpoint in hello Overview blade for your cluster in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="7e47b-224">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="7e47b-224">Click **Publish**.</span></span>

<span data-ttu-id="7e47b-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) es una herramienta web para inspeccionar y administrar aplicaciones y nodos en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7e47b-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="7e47b-226">Abra un explorador y navegue toohttp://containercluster.westus2.cloudapp.azure.com:19080/explorador/y siga la implementación de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7e47b-226">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow hello application deployment.</span></span>  <span data-ttu-id="7e47b-227">aplicación Hello implementa pero está en un estado de error hasta que se descarga la imagen de hello en nodos de clúster de hello (que pueden tardar algún tiempo, según el tamaño de la imagen de hello): ![Error][1]</span><span class="sxs-lookup"><span data-stu-id="7e47b-227">hello application deploys but is in an error state until hello image is downloaded on hello cluster nodes (which can take some time, depending on hello image size): ![Error][1]</span></span>

<span data-ttu-id="7e47b-228">aplicación Hello está listo cuando se encuentra en ```Ready``` estado: ![listo][2]</span><span class="sxs-lookup"><span data-stu-id="7e47b-228">hello application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="7e47b-229">Abra un explorador y navegue toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="7e47b-229">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="7e47b-230">Debería ver Hola encabezado "¡Hello World!"</span><span class="sxs-lookup"><span data-stu-id="7e47b-230">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="7e47b-231">mostrar en Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-231">display in hello browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="7e47b-232">Limpieza</span><span class="sxs-lookup"><span data-stu-id="7e47b-232">Clean up</span></span>
<span data-ttu-id="7e47b-233">Continuar tooincur cargos mientras se está ejecutando el clúster de hello, considere la posibilidad de [eliminar el clúster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="7e47b-233">You continue tooincur charges while hello cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="7e47b-234">Los [clústeres de la entidad](http://tryazureservicefabric.westus.cloudapp.azure.com/) se eliminan automáticamente a las pocas horas.</span><span class="sxs-lookup"><span data-stu-id="7e47b-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="7e47b-235">Después de insertar el registro de contenedor de hello imagen toohello puede eliminar imagen local Hola desde el equipo de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="7e47b-235">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="7e47b-236">Manifiestos de servicio y de aplicación de Service Fabric de ejemplo completos</span><span class="sxs-lookup"><span data-stu-id="7e47b-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="7e47b-237">Estas son servicio completo de Hola y manifiestos de aplicación que se usan en este artículo.</span><span class="sxs-lookup"><span data-stu-id="7e47b-237">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="7e47b-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="7e47b-238">ServiceManifest.xml</span></span>
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
### <a name="applicationmanifestxml"></a><span data-ttu-id="7e47b-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="7e47b-239">ApplicationManifest.xml</span></span>
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

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="7e47b-240">Configuración del intervalo de tiempo antes de hacer que se termine el contenedor</span><span class="sxs-lookup"><span data-stu-id="7e47b-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="7e47b-241">Puede configurar un intervalo de tiempo para hello en tiempo de ejecución toowait antes de quita el contenedor de hello después hello eliminación de servicio (o un nodo de tooanother de movimiento) se haya iniciado.</span><span class="sxs-lookup"><span data-stu-id="7e47b-241">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="7e47b-242">Intervalo de tiempo de configuración Hola envía hello `docker stop <time in seconds>` contenedor toohello de comando.</span><span class="sxs-lookup"><span data-stu-id="7e47b-242">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="7e47b-243">Para más detalles, consulte [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="7e47b-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="7e47b-244">toowait de intervalo de tiempo de Hola se especifica en hello `Hosting` sección.</span><span class="sxs-lookup"><span data-stu-id="7e47b-244">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="7e47b-245">Hola siguiente fragmento de manifiesto de clúster muestra cómo hello tooset el intervalo de espera:</span><span class="sxs-lookup"><span data-stu-id="7e47b-245">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="7e47b-246">Hello intervalo de tiempo predeterminado se establece too10 segundos.</span><span class="sxs-lookup"><span data-stu-id="7e47b-246">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="7e47b-247">Puesto que esta configuración es dinámica, una configuración solo actualizar en tiempo de espera de hello clúster actualizaciones Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-247">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="7e47b-248">Configurar hello en tiempo de ejecución tooremove imágenes del contenedor sin usar</span><span class="sxs-lookup"><span data-stu-id="7e47b-248">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="7e47b-249">Puede configurar tooremove de clúster de Service Fabric Hola imágenes del contenedor sin usar del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e47b-249">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="7e47b-250">Esta configuración permite toobe de espacio en disco recuperado si están presentes en el nodo de hello demasiadas imágenes del contenedor.</span><span class="sxs-lookup"><span data-stu-id="7e47b-250">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="7e47b-251">tooenable esta función, la actualización hello `Hosting` sección manifiesto de clúster de hello tal y como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="7e47b-251">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="7e47b-252">Para las imágenes que no se deben eliminar, puede especificar en hello `ContainerImagesToSkip` parámetro.</span><span class="sxs-lookup"><span data-stu-id="7e47b-252">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="7e47b-253">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7e47b-253">Next steps</span></span>
* <span data-ttu-id="7e47b-254">Más información acerca de cómo ejecutar [contenedores en Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e47b-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="7e47b-255">Hola de lectura [implementar una aplicación de .NET en un contenedor](service-fabric-host-app-in-a-container.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7e47b-255">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="7e47b-256">Obtenga información acerca de Service Fabric hello [ciclo de vida de la aplicación](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="7e47b-256">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="7e47b-257">Hola de desprotección [ejemplos de código de contenedor de Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="7e47b-257">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
