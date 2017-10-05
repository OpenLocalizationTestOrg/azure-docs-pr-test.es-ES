---
title: "Creación de una aplicación contenedora en Azure Service Fabric | Microsoft Docs"
description: "Cree la primera aplicación contenedora en Windows en Azure Service Fabric.  Cree una imagen de Docker con una aplicación en Python, inserte la imagen en un registro de contenedores y compile e implemente una aplicación contenedora en Service Fabric."
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
ms.openlocfilehash: 025bde02b3f342ec3399d51819d1fa8a91f11374
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="e7c40-104">Cree la primera aplicación contenedora en Service Fabric en Windows</span><span class="sxs-lookup"><span data-stu-id="e7c40-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7c40-105">Windows</span><span class="sxs-lookup"><span data-stu-id="e7c40-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="e7c40-106">Linux</span><span class="sxs-lookup"><span data-stu-id="e7c40-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="e7c40-107">Para ejecutar una aplicación que existe en un contenedor de Windows en un clúster de Service Fabric no hay que hacer ningún cambio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7c40-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="e7c40-108">Este artículo le guiará por la creación de una imagen de Docker que contiene una aplicación web [Flask](http://flask.pocoo.org/) en Python y su implementación en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e7c40-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="e7c40-109">También compartirá la aplicación en el contenedor mediante [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="e7c40-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="e7c40-110">Este artículo supone que el usuario tiene un conocimiento básico de Docker.</span><span class="sxs-lookup"><span data-stu-id="e7c40-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="e7c40-111">Para obtener información acerca de Docker, lea la [introducción a Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="e7c40-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7c40-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e7c40-112">Prerequisites</span></span>
<span data-ttu-id="e7c40-113">Un equipo de desarrollo en el que se ejecute:</span><span class="sxs-lookup"><span data-stu-id="e7c40-113">A development computer running:</span></span>
* <span data-ttu-id="e7c40-114">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e7c40-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="e7c40-115">[SDK y herramientas de Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e7c40-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="e7c40-116">Docker para Windows.</span><span class="sxs-lookup"><span data-stu-id="e7c40-116">Docker for Windows.</span></span>  <span data-ttu-id="e7c40-117">[Obtener Docker CE para Windows (estable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="e7c40-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="e7c40-118">Después de instalar e iniciar Docker, haga clic con el botón derecho en el icono de la bandeja y seleccione **Switch to Windows containers** (Conmutar a contenedores de Windows),</span><span class="sxs-lookup"><span data-stu-id="e7c40-118">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="e7c40-119">algo que es necesario para ejecutar imágenes de Docker basadas en Windows.</span><span class="sxs-lookup"><span data-stu-id="e7c40-119">This is required to run Docker images based on Windows.</span></span>

<span data-ttu-id="e7c40-120">Un clúster de Windows con tres, o más, nodos que se ejecute en Windows Server 2016 con contenedores: [Creación del primer clúster de Service Fabric en Azure](service-fabric-cluster-creation-via-portal.md) o [Prueba gratis de Service Fabric](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="e7c40-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="e7c40-121">Un registro de Azure Container Registry: [cree un registro de contenedor](../container-registry/container-registry-get-started-portal.md) en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7c40-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-the-docker-container"></a><span data-ttu-id="e7c40-122">Definición del contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="e7c40-122">Define the Docker container</span></span>
<span data-ttu-id="e7c40-123">Compile una imagen basada en la [imagen de Python](https://hub.docker.com/_/python/) ubicada en Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="e7c40-123">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="e7c40-124">Defina el contenedor de Docker en un archivo Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="e7c40-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="e7c40-125">El archivo Dockerfile contiene instrucciones para la configuración del entorno dentro del contenedor, la carga de la aplicación que desea ejecutar y la asignación de puertos.</span><span class="sxs-lookup"><span data-stu-id="e7c40-125">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="e7c40-126">El Dockerfile es la entrada para el comando `docker build`, que crea la imagen.</span><span class="sxs-lookup"><span data-stu-id="e7c40-126">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span>

<span data-ttu-id="e7c40-127">Cree un directorio vacío y cree el archivo *Dockerfile* (sin extensión de archivo).</span><span class="sxs-lookup"><span data-stu-id="e7c40-127">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="e7c40-128">Agregue lo siguiente al archivo *Dockerfile* y guarde los cambios:</span><span class="sxs-lookup"><span data-stu-id="e7c40-128">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="e7c40-129">Para más información, lea la [referencia de Dockerfile](https://docs.docker.com/engine/reference/builder/).</span><span class="sxs-lookup"><span data-stu-id="e7c40-129">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="e7c40-130">Creación de una aplicación web simple</span><span class="sxs-lookup"><span data-stu-id="e7c40-130">Create a simple web application</span></span>
<span data-ttu-id="e7c40-131">Cree una aplicación web de Flask que escucha en el puerto 80 y devuelve "Hola mundo".</span><span class="sxs-lookup"><span data-stu-id="e7c40-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="e7c40-132">En el mismo directorio, cree el archivo *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="e7c40-132">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="e7c40-133">Agregue lo siguiente y guarde los cambios:</span><span class="sxs-lookup"><span data-stu-id="e7c40-133">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="e7c40-134">Cree también el archivo *app.py* y agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7c40-134">Also create the *app.py* file and add the following:</span></span>

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
## <a name="build-the-image"></a><span data-ttu-id="e7c40-135">Compilación de la imagen</span><span class="sxs-lookup"><span data-stu-id="e7c40-135">Build the image</span></span>
<span data-ttu-id="e7c40-136">Ejecute el comando `docker build` para crear la imagen que ejecuta la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e7c40-136">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="e7c40-137">Abra una ventana de PowerShell y navegue hasta el directorio que contiene el archivo Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="e7c40-137">Open a PowerShell window and navigate to the directory containing the Dockerfile.</span></span> <span data-ttu-id="e7c40-138">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e7c40-138">Run the following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="e7c40-139">Este comando crea la imagen nueva con las instrucciones del Dockerfile y asígnele el nombre (etiqueta -t) "helloworldapp" a la imagen.</span><span class="sxs-lookup"><span data-stu-id="e7c40-139">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="e7c40-140">La creación de una imagen extrae la imagen base de Docker Hub y crea una nueva imagen que agrega la aplicación sobre la imagen base.</span><span class="sxs-lookup"><span data-stu-id="e7c40-140">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="e7c40-141">Una vez que se complete el comando de compilación, ejecute el comando `docker images` para ver información sobre la nueva imagen:</span><span class="sxs-lookup"><span data-stu-id="e7c40-141">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="e7c40-142">Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="e7c40-142">Run the application locally</span></span>
<span data-ttu-id="e7c40-143">Compruebe la imagen localmente antes de insertarla en el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="e7c40-143">Verify your image locally before pushing it the container registry.</span></span>  

<span data-ttu-id="e7c40-144">Ejecute la aplicación:</span><span class="sxs-lookup"><span data-stu-id="e7c40-144">Run the application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="e7c40-145">*name* asigna un nombre al contenedor en ejecución (en lugar del identificador del contenedor).</span><span class="sxs-lookup"><span data-stu-id="e7c40-145">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="e7c40-146">Una vez que el contenedor se inicia, busque su dirección IP para que pueda conectarse a su contenedor en ejecución desde un explorador:</span><span class="sxs-lookup"><span data-stu-id="e7c40-146">Once the container starts, find its IP address so that you can connect to your running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="e7c40-147">Conéctese al contenedor en ejecución.</span><span class="sxs-lookup"><span data-stu-id="e7c40-147">Connect to the running container.</span></span>  <span data-ttu-id="e7c40-148">Abra un explorador web que apunte a la dirección IP devuelta; por ejemplo, "http://172.31.194.61".</span><span class="sxs-lookup"><span data-stu-id="e7c40-148">Open a web browser pointing to the IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="e7c40-149">Debería ver que el título "¡Hola mundo!"</span><span class="sxs-lookup"><span data-stu-id="e7c40-149">You should see the heading "Hello World!"</span></span> <span data-ttu-id="e7c40-150">se muestra en el explorador.</span><span class="sxs-lookup"><span data-stu-id="e7c40-150">display in the browser.</span></span>

<span data-ttu-id="e7c40-151">Para detener el contenedor, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e7c40-151">To stop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="e7c40-152">Elimine el contenedor del equipo de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="e7c40-152">Delete the container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="e7c40-153">Inserción de la imagen en el registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="e7c40-153">Push the image to the container registry</span></span>
<span data-ttu-id="e7c40-154">Después de comprobar que el contenedor se ejecuta en el equipo de desarrollo, inserte la imagen en el registro de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="e7c40-154">After you verify that the container runs on your development machine, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="e7c40-155">Ejecute ``docker login`` para iniciar sesión en el registro de contenedor con sus [credenciales de registro](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e7c40-155">Run ``docker login`` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="e7c40-156">En el ejemplo siguiente se pasa el identificador y la contraseña de una [entidad de servicio](../active-directory/active-directory-application-objects.md) de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e7c40-156">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="e7c40-157">Por ejemplo, puede que haya asignado una entidad de servicio al registro para ver un escenario de automatización.</span><span class="sxs-lookup"><span data-stu-id="e7c40-157">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span> <span data-ttu-id="e7c40-158">O bien, puede iniciar sesión con su nombre de usuario y contraseña del registro.</span><span class="sxs-lookup"><span data-stu-id="e7c40-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="e7c40-159">El siguiente comando crea una etiqueta, o alias, de la imagen, con una ruta de acceso completa al registro.</span><span class="sxs-lookup"><span data-stu-id="e7c40-159">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="e7c40-160">Este ejemplo coloca la imagen en el espacio de nombres ```samples``` para evitar el desorden en la raíz del registro.</span><span class="sxs-lookup"><span data-stu-id="e7c40-160">This example places the image in the ```samples``` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="e7c40-161">Inserte la imagen en el registro de contenedor:</span><span class="sxs-lookup"><span data-stu-id="e7c40-161">Push the image to your container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-the-containerized-service-in-visual-studio"></a><span data-ttu-id="e7c40-162">Creación del servicio en contenedor en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e7c40-162">Create the containerized service in Visual Studio</span></span>
<span data-ttu-id="e7c40-163">Las herramientas y el SDK de Service Fabric proporcionan una plantilla de servicio que le ayuda a crear una aplicación en contenedor.</span><span class="sxs-lookup"><span data-stu-id="e7c40-163">The Service Fabric SDK and tools provide a service template to help you create a containerized application.</span></span>

1. <span data-ttu-id="e7c40-164">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e7c40-164">Start Visual Studio.</span></span>  <span data-ttu-id="e7c40-165">Seleccione **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e7c40-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="e7c40-166">Seleccione **Aplicación de Service Fabric**, asígnele el nombre "MyFirstContainer" y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e7c40-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="e7c40-167">Seleccione **Contenedor de invitado**  en la lista de **plantillas del servicio**.</span><span class="sxs-lookup"><span data-stu-id="e7c40-167">Select **Guest Container** from the list of **service templates**.</span></span>
4. <span data-ttu-id="e7c40-168">En **Nombre de la imagen** escriba "myregistry.azurecr.io/samples/helloworldapp", la imagen que insertó en el repositorio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="e7c40-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", the image you pushed to your container repository.</span></span>
5. <span data-ttu-id="e7c40-169">Asigne un nombre a su servicio y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e7c40-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="e7c40-170">Configuración de la comunicación</span><span class="sxs-lookup"><span data-stu-id="e7c40-170">Configure communication</span></span>
<span data-ttu-id="e7c40-171">El servicio en contenedor necesita un punto de conexión para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="e7c40-171">The containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="e7c40-172">Agregar un elemento `Endpoint` con el protocolo, el puerto y el tipo en el archivo ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e7c40-172">Add an `Endpoint` element with the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="e7c40-173">Para este artículo, el servicio en contenedor realiza escuchas en el puerto 8081.</span><span class="sxs-lookup"><span data-stu-id="e7c40-173">For this article, the containerized service listens on port 8081.</span></span>  <span data-ttu-id="e7c40-174">En este ejemplo, se usa un puerto fijo 8081.</span><span class="sxs-lookup"><span data-stu-id="e7c40-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="e7c40-175">Si no se especifica ningún puerto, se elige un puerto aleatorio dentro del intervalo de puertos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7c40-175">If no port is specified, a random port from the application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="e7c40-176">Al definir un punto de conexión, Service Fabric publica el punto de conexión en el servicio de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="e7c40-176">By defining an endpoint, Service Fabric publishes the endpoint to the Naming service.</span></span>  <span data-ttu-id="e7c40-177">Otros servicios que se ejecuten en el clúster pueden resolver este contenedor.</span><span class="sxs-lookup"><span data-stu-id="e7c40-177">Other services running in the cluster can resolve this container.</span></span>  <span data-ttu-id="e7c40-178">También puede realizar la comunicación de contenedor a contenedor utilizando el [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="e7c40-178">You can also perform container-to-container communication using the [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="e7c40-179">La comunicación se establece al proporcionar el puerto de escucha HTTP del proxy inverso y el nombre de los servicios con los que desea comunicarse como variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="e7c40-179">Communication is performed by providing the reverse proxy HTTP listening port and the name of the services that you want to communicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="e7c40-180">Configuración y establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="e7c40-180">Configure and set environment variables</span></span>
<span data-ttu-id="e7c40-181">En el manifiesto de servicio, las variables de entorno se pueden especificar para cada paquete de código.</span><span class="sxs-lookup"><span data-stu-id="e7c40-181">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="e7c40-182">Esta característica está disponible para todos los servicios, con independencia de si se implementan como contenedores, procesos o archivos ejecutables de invitado.</span><span class="sxs-lookup"><span data-stu-id="e7c40-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="e7c40-183">Estos valores de variable de entorno se invalidan en el manifiesto de aplicación o se especifican durante la implementación como parámetros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7c40-183">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="e7c40-184">El siguiente fragmento de código XML del manifiesto de servicio muestra un ejemplo de cómo especificar variables de entorno para un paquete de código:</span><span class="sxs-lookup"><span data-stu-id="e7c40-184">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="e7c40-185">Estas variables de entorno se pueden invalidar en el manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="e7c40-185">These environment variables can be overridden in the application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="e7c40-186">Configurar la asignación de puerto de puerto a host del contenedor y la detección de contenedor a contenedor</span><span class="sxs-lookup"><span data-stu-id="e7c40-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="e7c40-187">Configurar un puerto de host que se utiliza para comunicarse con el contenedor.</span><span class="sxs-lookup"><span data-stu-id="e7c40-187">Configure a host port used to communicate  with the container.</span></span> <span data-ttu-id="e7c40-188">El enlace de puerto asigna el puerto en el que el servicio está escuchando dentro del contenedor a un puerto en el host.</span><span class="sxs-lookup"><span data-stu-id="e7c40-188">The port binding maps the port on which the service is listening inside the container to a port on the host.</span></span> <span data-ttu-id="e7c40-189">Agregar un elemento `PortBinding` en el elemento `ContainerHostPolicies` del archivo ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e7c40-189">Add a `PortBinding` element in `ContainerHostPolicies` element of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="e7c40-190">Para este artículo, `ContainerPort` es 80 (el contenedor expone el puerto 80, como se especifica en el Dockerfile) y `EndpointRef` es "Guest1TypeEndpoint" (el punto de conexión definido previamente en el manifiesto de servicio).</span><span class="sxs-lookup"><span data-stu-id="e7c40-190">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (the endpoint previously defined in the service manifest).</span></span>  <span data-ttu-id="e7c40-191">Las solicitudes entrantes para el servicio en el puerto 8081 se asignan al puerto 80 del contenedor.</span><span class="sxs-lookup"><span data-stu-id="e7c40-191">Incoming requests to the service on port 8081 are mapped to port 80 on the container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="e7c40-192">Configurar la autenticación de Container Registry</span><span class="sxs-lookup"><span data-stu-id="e7c40-192">Configure container registry authentication</span></span>
<span data-ttu-id="e7c40-193">Configure la autenticación de Container Registry mediante la adición de `RepositoryCredentials` a `ContainerHostPolicies` en el archivo ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e7c40-193">Configure container registry authentication by adding `RepositoryCredentials` to `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span> <span data-ttu-id="e7c40-194">Agregue la cuenta y contraseña para el registro de contenedores myregistry.azurecr.io, que permite al servicio descargar la imagen de contenedor del repositorio.</span><span class="sxs-lookup"><span data-stu-id="e7c40-194">Add the account and password for the myregistry.azurecr.io container registry, which allows the service to download the container image from the repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="e7c40-195">Se recomienda cifrar la contraseña del repositorio con un certificado de cifrado que se implementa en todos los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="e7c40-195">We recommend that you encrypt the repository password by using an encipherment certificate that's deployed to all nodes of the cluster.</span></span> <span data-ttu-id="e7c40-196">Cuando Service Fabric implementa el paquete de servicio en el clúster, el certificado de cifrado se utiliza para descifrar el texto cifrado.</span><span class="sxs-lookup"><span data-stu-id="e7c40-196">When Service Fabric deploys the service package to the cluster, the encipherment certificate is used to decrypt the cipher text.</span></span>  <span data-ttu-id="e7c40-197">El cmdlet Invoke-ServiceFabricEncryptText se usa para crear el texto cifrado para la contraseña, que se agrega al archivo ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e7c40-197">The Invoke-ServiceFabricEncryptText cmdlet is used to create the cipher text for the password, which is added to the ApplicationManifest.xml file.</span></span>

<span data-ttu-id="e7c40-198">El script siguiente crea un nuevo certificado autofirmado y lo exporta a un archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="e7c40-198">The following script creates a new self-signed certificate and exports it to a PFX file.</span></span>  <span data-ttu-id="e7c40-199">El certificado se importa en un almacén de claves existente y, a continuación, se implementa en el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e7c40-199">The certificate is imported into an existing key vault and then deployed to the Service Fabric cluster.</span></span>

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

# Create a self signed cert, export to PFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import the certificate to an existing key vault.  The key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add the certificate to all the VMs in the cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="e7c40-200">Cifre la contraseña mediante el cmdlet [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="e7c40-200">Encrypt the password using the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="e7c40-201">Reemplace la contraseña con el texto cifrado devuelto por el cmdlet [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) y establezca `PasswordEncrypted` en "true".</span><span class="sxs-lookup"><span data-stu-id="e7c40-201">Replace the password with the cipher text returned by the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` to "true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="e7c40-202">Configuración del modo de aislamiento</span><span class="sxs-lookup"><span data-stu-id="e7c40-202">Configure isolation mode</span></span>
<span data-ttu-id="e7c40-203">Windows admite dos modos de aislamiento para contenedores: de proceso y de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e7c40-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="e7c40-204">Con el modo de aislamiento de proceso, todos los contenedores que se ejecutan en la misma máquina host comparten el kernel con el host.</span><span class="sxs-lookup"><span data-stu-id="e7c40-204">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="e7c40-205">Con el modo de aislamiento de Hyper-V, los kernels se aíslan entre los contenedores de Hyper-V y el host del contenedor.</span><span class="sxs-lookup"><span data-stu-id="e7c40-205">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="e7c40-206">El modo de aislamiento se especifica en el elemento `ContainerHostPolicies` del archivo de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7c40-206">The isolation mode is specified in the `ContainerHostPolicies` element in the application manifest file.</span></span> <span data-ttu-id="e7c40-207">Los modos de aislamiento que se pueden especificar son `process`, `hyperv` y `default`.</span><span class="sxs-lookup"><span data-stu-id="e7c40-207">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="e7c40-208">El modo de aislamiento predeterminado es `process` en hosts con Windows Server e `hyperv` en hosts con Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e7c40-208">The default isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="e7c40-209">El siguiente fragmento de código muestra cómo el modo de aislamiento se especifica en el archivo de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7c40-209">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="e7c40-210">Configuración de la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="e7c40-210">Configure resource governance</span></span>
<span data-ttu-id="e7c40-211">La [regulación de recursos](service-fabric-resource-governance.md) restringe los recursos que el contenedor puede usar en el host.</span><span class="sxs-lookup"><span data-stu-id="e7c40-211">[Resource governance](service-fabric-resource-governance.md) restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="e7c40-212">El elemento `ResourceGovernancePolicy`, especificado en el manifiesto de la aplicación, se utiliza para declarar los límites de recursos para un paquete de código de servicio.</span><span class="sxs-lookup"><span data-stu-id="e7c40-212">The `ResourceGovernancePolicy` element, which is specified in the application manifest, is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="e7c40-213">Se pueden establecer límites de recursos para los siguientes recursos: memoria, MemorySwap, CpuShares (peso relativo de CPU), MemoryReservationInMB, BlkioWeight (peso relativo de BlockIO).</span><span class="sxs-lookup"><span data-stu-id="e7c40-213">Resource limits can be set for the following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="e7c40-214">En este ejemplo, el paquete de servicio Guest1Pkg obtiene un núcleo en los nodos del clúster en los que es situado.</span><span class="sxs-lookup"><span data-stu-id="e7c40-214">In this example, service package Guest1Pkg gets one core on the cluster nodes where it is placed.</span></span>  <span data-ttu-id="e7c40-215">Los límites de memoria son absolutos, por lo que el paquete de código está limitado a 1024 MB de memoria (con una reserva de garantía flexible de dicha capacidad).</span><span class="sxs-lookup"><span data-stu-id="e7c40-215">Memory limits are absolute, so the code package is limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="e7c40-216">Los paquetes de código (contenedores o procesos) no pueden asignar más memoria de la que establece este límite; si se intenta, el resultado es una excepción de memoria insuficiente.</span><span class="sxs-lookup"><span data-stu-id="e7c40-216">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="e7c40-217">Para que la aplicación del límite de recursos funcione, es necesario haber definido límites de memoria en todos los paquetes de código de un paquete de servicio.</span><span class="sxs-lookup"><span data-stu-id="e7c40-217">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-the-container-application"></a><span data-ttu-id="e7c40-218">Implementación de la aplicación contenedora</span><span class="sxs-lookup"><span data-stu-id="e7c40-218">Deploy the container application</span></span>
<span data-ttu-id="e7c40-219">Guarde todos los cambios y compile la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7c40-219">Save all your changes and build the application.</span></span> <span data-ttu-id="e7c40-220">Para publicar la aplicación, haga clic con el botón derecho en **MyFirstContainer** en el Explorador de soluciones y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e7c40-220">To publish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="e7c40-221">En **Punto de conexión de la conexión**, escriba el punto de conexión de administración del clúster.</span><span class="sxs-lookup"><span data-stu-id="e7c40-221">In **Connection Endpoint**, enter the management endpoint for the cluster.</span></span>  <span data-ttu-id="e7c40-222">Por ejemplo, "containercluster.westus2.cloudapp.azure.com:19000".</span><span class="sxs-lookup"><span data-stu-id="e7c40-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="e7c40-223">El punto de conexión del cliente se puede encontrar en la hoja de información general del clúster en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7c40-223">You can find the client connection endpoint in the Overview blade for your cluster in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e7c40-224">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e7c40-224">Click **Publish**.</span></span>

<span data-ttu-id="e7c40-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) es una herramienta web para inspeccionar y administrar aplicaciones y nodos en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e7c40-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="e7c40-226">Abra un explorador, navegue hasta http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ y siga la implementación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7c40-226">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow the application deployment.</span></span>  <span data-ttu-id="e7c40-227">La aplicación se implementa, pero está en estado de error hasta que la imagen se descarga en los nodos del clúster (lo que pueden tardar un tiempo, según el tamaño de imagen): ![Error][1]</span><span class="sxs-lookup"><span data-stu-id="e7c40-227">The application deploys but is in an error state until the image is downloaded on the cluster nodes (which can take some time, depending on the image size): ![Error][1]</span></span>

<span data-ttu-id="e7c40-228">La aplicación está lista cuando está en el estado ```Ready```: ![Ready][2]</span><span class="sxs-lookup"><span data-stu-id="e7c40-228">The application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="e7c40-229">Abra un explorador y navegue hasta http://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="e7c40-229">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="e7c40-230">Debería ver que el título "¡Hola mundo!"</span><span class="sxs-lookup"><span data-stu-id="e7c40-230">You should see the heading "Hello World!"</span></span> <span data-ttu-id="e7c40-231">se muestra en el explorador.</span><span class="sxs-lookup"><span data-stu-id="e7c40-231">display in the browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="e7c40-232">Limpieza</span><span class="sxs-lookup"><span data-stu-id="e7c40-232">Clean up</span></span>
<span data-ttu-id="e7c40-233">Mientras el clúster esté en ejecución seguirá generando cargos, así que debería considerar la posibilidad de [eliminar el clúster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="e7c40-233">You continue to incur charges while the cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="e7c40-234">Los [clústeres de la entidad](http://tryazureservicefabric.westus.cloudapp.azure.com/) se eliminan automáticamente a las pocas horas.</span><span class="sxs-lookup"><span data-stu-id="e7c40-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="e7c40-235">Después de insertar la imagen en el registro de contenedor puede eliminar la imagen local del equipo de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="e7c40-235">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="e7c40-236">Manifiestos de servicio y de aplicación de Service Fabric de ejemplo completos</span><span class="sxs-lookup"><span data-stu-id="e7c40-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="e7c40-237">Estos son los manifiestos de servicio y de aplicación completos que se usan en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e7c40-237">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="e7c40-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="e7c40-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="e7c40-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="e7c40-239">ApplicationManifest.xml</span></span>
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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
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
    <!-- The section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="e7c40-240">Configuración del intervalo de tiempo antes de hacer que se termine el contenedor</span><span class="sxs-lookup"><span data-stu-id="e7c40-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="e7c40-241">Puede configurar un intervalo de tiempo para que el entorno de ejecución espere antes de que el contenedor se quite una vez que la eliminación del servicio (o el movimiento a otro nodo) se haya iniciado.</span><span class="sxs-lookup"><span data-stu-id="e7c40-241">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="e7c40-242">Si se configura el intervalo de tiempo, se envía el comando `docker stop <time in seconds>` al contenedor.</span><span class="sxs-lookup"><span data-stu-id="e7c40-242">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="e7c40-243">Para más detalles, consulte [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="e7c40-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="e7c40-244">El intervalo de tiempo de espera se especifica en la sección `Hosting`.</span><span class="sxs-lookup"><span data-stu-id="e7c40-244">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="e7c40-245">El siguiente fragmento de manifiesto de clúster muestra cómo establecer el intervalo de espera:</span><span class="sxs-lookup"><span data-stu-id="e7c40-245">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="e7c40-246">El intervalo de tiempo predeterminado se establece en diez segundos.</span><span class="sxs-lookup"><span data-stu-id="e7c40-246">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="e7c40-247">Puesto que esta configuración es dinámica, una actualización de solo configuración en el clúster actualiza el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="e7c40-247">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="e7c40-248">Configuración del entorno de ejecución para quitar imágenes de contenedor sin usar</span><span class="sxs-lookup"><span data-stu-id="e7c40-248">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="e7c40-249">Puede configurar el clúster de Service Fabric para quitar del nodo las imágenes de contenedor sin usar.</span><span class="sxs-lookup"><span data-stu-id="e7c40-249">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="e7c40-250">Esta configuración permite recuperar el espacio en disco si hay demasiadas imágenes de contenedor en el nodo.</span><span class="sxs-lookup"><span data-stu-id="e7c40-250">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="e7c40-251">Para habilitar esta característica, actualice la sección `Hosting` en el manifiesto de clúster, tal como se muestra en el fragmento siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7c40-251">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="e7c40-252">Puede especificar las imágenes que no se deben eliminar en el parámetro `ContainerImagesToSkip`.</span><span class="sxs-lookup"><span data-stu-id="e7c40-252">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="e7c40-253">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e7c40-253">Next steps</span></span>
* <span data-ttu-id="e7c40-254">Más información acerca de cómo ejecutar [contenedores en Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7c40-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="e7c40-255">Consulte el tutorial [Implementación de una aplicación .NET en un contenedor](service-fabric-host-app-in-a-container.md).</span><span class="sxs-lookup"><span data-stu-id="e7c40-255">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="e7c40-256">Más información acerca del [ciclo de vida de aplicaciones](service-fabric-application-lifecycle.md) de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e7c40-256">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="e7c40-257">Consulte [los ejemplos de código de contenedor de Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="e7c40-257">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
