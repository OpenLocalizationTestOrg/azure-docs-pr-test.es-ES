---
title: "Administración de varios entornos en Service Fabric | Microsoft Docs"
description: "Las aplicaciones de Service Fabric se pueden ejecutar en clústeres cuyo tamaño oscila entre una y miles de máquinas. En algunos casos, deseará configurar su aplicación de forma diferente para cada uno de los entornos. Este artículo explica cómo definir distintos parámetros de aplicación por entorno."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 9317b3f0b7984e795c4205360ed58e2c4f3fbcb1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="6c19d-105">Administración de los parámetros de la aplicación en varios entornos</span><span class="sxs-lookup"><span data-stu-id="6c19d-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="6c19d-106">Puede crear clústeres de Service Fabric de Azure con cualquier número de máquinas, desde una sola máquina hasta miles de ellas.</span><span class="sxs-lookup"><span data-stu-id="6c19d-106">You can create Azure Service Fabric clusters by using anywhere from one to many thousands of machines.</span></span> <span data-ttu-id="6c19d-107">Aunque los archivos binarios de una aplicación pueden ejecutarse sin modificación alguna en este amplio espectro de entornos, con frecuencia se desea configurar la aplicación de manera diferente, en función del número de máquinas donde se vaya a implementar.</span><span class="sxs-lookup"><span data-stu-id="6c19d-107">While application binaries can run without modification across this wide spectrum of environments, you often want to configure the application differently, depending on the number of machines you're deploying to.</span></span>

<span data-ttu-id="6c19d-108">A modo de ejemplo simple, considere `InstanceCount` en un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="6c19d-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="6c19d-109">Cuando se ejecutan las aplicaciones de Azure, normalmente se prefiere establecer este parámetro en el valor especial "-1".</span><span class="sxs-lookup"><span data-stu-id="6c19d-109">When you are running applications in Azure, you generally want to set this parameter to the special value of "-1".</span></span> <span data-ttu-id="6c19d-110">Esta configuración garantiza que el servicio se ejecute en todos los nodos del clúster (o en todos los nodos de ese tipo, si ha establecido una restricción de colocación).</span><span class="sxs-lookup"><span data-stu-id="6c19d-110">This configuration ensures that your service is running on every node in the cluster (or every node in the node type if you have set a placement constraint).</span></span> <span data-ttu-id="6c19d-111">Sin embargo, no es adecuada para un clúster de una sola máquina, ya que no puede haber varios procesos que escuchen el mismo punto de conexión en una máquina individual.</span><span class="sxs-lookup"><span data-stu-id="6c19d-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on the same endpoint on a single machine.</span></span> <span data-ttu-id="6c19d-112">En su lugar, normalmente se establece `InstanceCount` en "1".</span><span class="sxs-lookup"><span data-stu-id="6c19d-112">Instead, you typically set `InstanceCount` to "1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="6c19d-113">Especificación de parámetros concretos del entorno</span><span class="sxs-lookup"><span data-stu-id="6c19d-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="6c19d-114">La solución a este problema de configuración es un conjunto de servicios predeterminados con parámetros y los archivos de parámetros de la aplicación que rellene los valores de dichos parámetros para un entorno determinado.</span><span class="sxs-lookup"><span data-stu-id="6c19d-114">The solution to this configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="6c19d-115">Los parámetros predeterminados de los servicios y las aplicaciones se configuran en los manifiestos de servicio y aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c19d-115">Default services and application parameters are configured in the application and service manifests.</span></span> <span data-ttu-id="6c19d-116">La definición de esquema para los archivos ApplicationManifest.xml y ServiceManifest.xml se instala con el SDK y las herramientas de Service Fabric en *C:\Archivos de programa\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="6c19d-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml files is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="6c19d-117">Servicios predeterminados</span><span class="sxs-lookup"><span data-stu-id="6c19d-117">Default services</span></span>
<span data-ttu-id="6c19d-118">Las aplicaciones de Service Fabric constan de una colección de instancias de servicio.</span><span class="sxs-lookup"><span data-stu-id="6c19d-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="6c19d-119">Aunque se puede crear una aplicación vacía y, a continuación, crear todas las instancias del servicio de forma dinámica, la mayoría de las aplicaciones tienen un conjunto de servicios principales que se deben crear siempre que se crea una instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c19d-119">While it is possible for you to create an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when the application is instantiated.</span></span> <span data-ttu-id="6c19d-120">Estos se conocen como "servicios predeterminados".</span><span class="sxs-lookup"><span data-stu-id="6c19d-120">These are referred to as "default services".</span></span> <span data-ttu-id="6c19d-121">Se especifican en el manifiesto de aplicación con marcadores de posición para la configuración de cada entorno entre corchetes:</span><span class="sxs-lookup"><span data-stu-id="6c19d-121">They are specified in the application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="6c19d-122">Todos los parámetros con nombre deben definirse dentro del elemento Parameters del manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="6c19d-122">Each of the named parameters must be defined within the Parameters element of the application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="6c19d-123">El atributo DefaultValue especifica el valor que se usará en ausencia de un parámetro más específico para un entorno determinado.</span><span class="sxs-lookup"><span data-stu-id="6c19d-123">The DefaultValue attribute specifies the value to be used in the absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="6c19d-124">No todos los parámetros de instancias de servicio son adecuados para la configuración de cada entorno.</span><span class="sxs-lookup"><span data-stu-id="6c19d-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="6c19d-125">En el ejemplo anterior, los valores LowKey y HighKey del esquema de partición del servicio se definen explícitamente para todas las instancias del servicio, ya que el intervalo de partición es una función del dominio de datos, no del entorno.</span><span class="sxs-lookup"><span data-stu-id="6c19d-125">In the example above, the LowKey and HighKey values for the service's partitioning scheme are explicitly defined for all instances of the service since the partition range is a function of the data domain, not the environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="6c19d-126">Opciones de configuración del servicio de cada entorno</span><span class="sxs-lookup"><span data-stu-id="6c19d-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="6c19d-127">El [modelo de aplicación de Service Fabric](service-fabric-application-model.md) permite a los servicios incluir paquetes de configuración que contienen pares clave-valor personalizados que se pueden leer en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6c19d-127">The [Service Fabric application model](service-fabric-application-model.md) enables services to include configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="6c19d-128">Los valores de estas opciones también se pueden diferenciar por entorno, para lo que se debe especificar `ConfigOverride` en el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c19d-128">The values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in the application manifest.</span></span>

<span data-ttu-id="6c19d-129">Suponga que tiene la siguiente opción en Config\Settings.xml para el servicio `Stateful1`:</span><span class="sxs-lookup"><span data-stu-id="6c19d-129">Suppose that you have the following setting in the Config\Settings.xml file for the `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="6c19d-130">Para reemplazar este valor para un par entorno/aplicación específico, cree `ConfigOverride` al importar el manifiesto de servicio en el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c19d-130">To override this value for a specific application/environment pair, create a `ConfigOverride` when you import the service manifest in the application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="6c19d-131">Este parámetro se puede configurar después por entorno, tal como se mostró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6c19d-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="6c19d-132">Puede hacerlo declarándolo en la sección de parámetros del manifiesto de aplicación y especificar valores específicos del entorno en el archivo de parámetros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c19d-132">You can do this by declaring it in the parameters section of the application manifest and specifying environment-specific values in the application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="6c19d-133">En el caso de las opciones de configuración, hay tres lugares donde se puede establecer el valor de una clave: el paquete de configuración del servicio, el manifiesto de aplicación y el archivo de parámetros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c19d-133">In the case of service configuration settings, there are three places where the value of a key can be set: the service configuration package, the application manifest, and the application parameter file.</span></span> <span data-ttu-id="6c19d-134">Service Fabric siempre elegirá entre el archivo de parámetros de la aplicación en primer lugar (si se especifica), luego el manifiesto de aplicación y, finalmente, el paquete de configuración.</span><span class="sxs-lookup"><span data-stu-id="6c19d-134">Service Fabric will always choose from the application parameter file first (if specified), then the application manifest, and finally the configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="6c19d-135">Establecimiento y uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="6c19d-135">Setting and using environment variables</span></span> 
<span data-ttu-id="6c19d-136">Puede especificar y establecer variables de entorno en el archivo ServiceManifest.xml y, luego, invalidarlas por instancia en el archivo ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="6c19d-136">You can specify and set environment variables in the ServiceManifest.xml file and then override these in the ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="6c19d-137">En el ejemplo siguiente se muestran dos variables de entorno, una con un valor definido y el de la otra, invalidado.</span><span class="sxs-lookup"><span data-stu-id="6c19d-137">The example below shows two environment variables, one with a value set and the other is overridden.</span></span> <span data-ttu-id="6c19d-138">Puede usar parámetros de aplicación para establecer los valores de las variables de entorno del mismo modo que se usaron para las invalidaciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="6c19d-138">You can use application parameters to set environment variables values in the same way that these were used for config overrides.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
<span data-ttu-id="6c19d-139">Para invalidar las variables de entorno del archivo ApplicationManifest.xml, haga referencia al paquete de código en el archivo ServiceManifest con el elemento `EnvironmentOverrides`.</span><span class="sxs-lookup"><span data-stu-id="6c19d-139">To override the environment variables in the ApplicationManifest.xml, reference the code package in the ServiceManifest with the `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="6c19d-140">Una vez que se cree la instancia de servicio con nombre, puede tener acceso a las variables de entorno desde el código.</span><span class="sxs-lookup"><span data-stu-id="6c19d-140">Once the named service instance is created you can access the environment variables from code.</span></span> <span data-ttu-id="6c19d-141">Por ejemplo, en C# puede hacer lo siguiente</span><span class="sxs-lookup"><span data-stu-id="6c19d-141">e.g. In C# you can do the following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="6c19d-142">Variables de entorno de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6c19d-142">Service Fabric environment variables</span></span>
<span data-ttu-id="6c19d-143">Service Fabric tiene variables de entorno integradas que se establecen para cada instancia del servicio.</span><span class="sxs-lookup"><span data-stu-id="6c19d-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="6c19d-144">A continuación se muestra la lista completa de variables de entorno; las que están en negrita son las que se utilizarán en el servicio y las otras por el tiempo de ejecución de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6c19d-144">The full list of environment variables is below, where the ones in bold are the ones that you will use in your service, the other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="6c19d-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="6c19d-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="6c19d-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="6c19d-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="6c19d-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="6c19d-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="6c19d-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="6c19d-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="6c19d-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="6c19d-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="6c19d-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="6c19d-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="6c19d-151">**Fabric_Endpoint_[SuNombreDeServicio]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="6c19d-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="6c19d-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="6c19d-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="6c19d-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="6c19d-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="6c19d-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="6c19d-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="6c19d-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="6c19d-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="6c19d-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="6c19d-156">Fabric_NodeId</span></span>
* <span data-ttu-id="6c19d-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="6c19d-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="6c19d-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="6c19d-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="6c19d-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="6c19d-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="6c19d-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="6c19d-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="6c19d-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="6c19d-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="6c19d-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="6c19d-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="6c19d-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="6c19d-163">FabricPackageFileName</span></span>

<span data-ttu-id="6c19d-164">El código siguiente muestra cómo enumerar las variables de entorno de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6c19d-164">The code belows shows how to list the Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="6c19d-165">Los siguientes son ejemplos de variable de entorno para un tipo de aplicación denominado `GuestExe.Application` con un tipo de servicio denominado `FrontEndService` cuando se ejecuta en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="6c19d-165">The following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="6c19d-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="6c19d-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="6c19d-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="6c19d-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="6c19d-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="6c19d-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="6c19d-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="6c19d-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="6c19d-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="6c19d-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="6c19d-171">Archivos de parámetros de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6c19d-171">Application parameter files</span></span>
<span data-ttu-id="6c19d-172">El proyecto de aplicación de Service Fabric puede incluir uno o más archivos de parámetro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c19d-172">The Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="6c19d-173">Cada uno de ellos define valores concretos para los parámetros que se definen en el manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="6c19d-173">Each of them defines the specific values for the parameters that are defined in the application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="6c19d-174">De forma predeterminada, una aplicación nueva incluye tres archivos de parámetros de aplicación, denominados Local.1Node.xml, Local.5Node.xml y Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="6c19d-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Archivos de parámetros de la aplicación en el Explorador de soluciones][app-parameters-solution-explorer]

<span data-ttu-id="6c19d-176">Para crear un archivo de parámetros, basta con copiar y pegar uno existente y asignarle un nombre nuevo.</span><span class="sxs-lookup"><span data-stu-id="6c19d-176">To create a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="6c19d-177">Identificación de parámetros específicos del entorno durante la implementación</span><span class="sxs-lookup"><span data-stu-id="6c19d-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="6c19d-178">En el momento de la implementación, es preciso elegir el archivo de parámetros apropiado que se aplicará en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c19d-178">At deployment time, you need to choose the appropriate parameter file to apply with your application.</span></span> <span data-ttu-id="6c19d-179">Esto se puede realizar desde el cuadro de diálogo Publicar de Visual Studio o a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c19d-179">You can do this through the Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="6c19d-180">Implementación desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6c19d-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="6c19d-181">Al publicar una aplicación en Visual Studio, puede elegir en la lista de archivos de parámetros disponibles.</span><span class="sxs-lookup"><span data-stu-id="6c19d-181">You can choose from the list of available parameter files when you publish your application in Visual Studio.</span></span>

![Elección de un archivo de parámetros en el cuadro de diálogo Publicar][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="6c19d-183">Implementación a partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c19d-183">Deploy from PowerShell</span></span>
<span data-ttu-id="6c19d-184">El script de PowerShell `Deploy-FabricApplication.ps1` incluido en la plantilla de proyecto de aplicación acepta un perfil de publicación como un parámetro, y el elemento PublishProfile contiene una referencia al archivo de parámetros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c19d-184">The `Deploy-FabricApplication.ps1` PowerShell script included in the application project template accepts a publish profile as a parameter and the PublishProfile contains a reference to the application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="6c19d-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c19d-185">Next steps</span></span>
<span data-ttu-id="6c19d-186">Para obtener más información sobre algunos de los conceptos principales descritos en este tema, vea la [Información técnica de Service Fabric](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c19d-186">To learn more about some of the core concepts that are discussed in this topic, see the [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="6c19d-187">Para obtener más información sobre otras funcionalidades de administración de aplicaciones disponibles en Visual Studio, vea [Administración de aplicaciones de Service Fabric en Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="6c19d-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
