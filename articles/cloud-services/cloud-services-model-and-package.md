---
title: aaaWhat es un modelo de servicio en la nube y el paquete | Documentos de Microsoft
description: Describe el modelo de servicio de nube hello (.csdef, .cscfg) y el paquete (.cspkg) en Azure
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="61aff-103">¿Qué es el modelo de servicio de nube de Hola y cómo puede empaquetar?</span><span class="sxs-lookup"><span data-stu-id="61aff-103">What is hello Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="61aff-104">Se crea un servicio de nube de tres componentes, definición de servicio de Hola *(.csdef)*, la configuración de servicio de Hola *(.cscfg)*y un paquete de servicios *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="61aff-104">A cloud service is created from three components, hello service definition *(.csdef)*, hello service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="61aff-105">Ambos hello **ServiceDefinition.csdef** y **ServiceConfig.cscfg** archivos están basados en XML y describir estructura Hola del servicio de nube de Hola y cómo está configurada; denominado modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-105">Both hello **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe hello structure of hello cloud service and how it's configured; collectively called hello model.</span></span> <span data-ttu-id="61aff-106">Hola **ServicePackage.cspkg** es un archivo zip que se genera a partir de hello **ServiceDefinition.csdef** y entre otras cosas, contiene todas las dependencias de hello necesario basados en binario.</span><span class="sxs-lookup"><span data-stu-id="61aff-106">hello **ServicePackage.cspkg** is a zip file that is generated from hello **ServiceDefinition.csdef** and among other things, contains all hello required binary-based dependencies.</span></span> <span data-ttu-id="61aff-107">Azure crea un servicio de nube desde ambos hello **ServicePackage.cspkg** hello y **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="61aff-107">Azure creates a cloud service from both hello **ServicePackage.cspkg** and hello **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="61aff-108">Una vez que se ejecuta el servicio de nube de hello en Azure, puede volver a configurarlo a través de hello **ServiceConfig.cscfg** archivo, pero no se puede modificar la definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-108">Once hello cloud service is running in Azure, you can reconfigure it through hello **ServiceConfig.cscfg** file, but you cannot alter hello definition.</span></span>

## <a name="what-would-you-like-tooknow-more-about"></a><span data-ttu-id="61aff-109">¿Qué desea más información acerca de tooknow?</span><span class="sxs-lookup"><span data-stu-id="61aff-109">What would you like tooknow more about?</span></span>
* <span data-ttu-id="61aff-110">Deseo tooknow más información acerca de hello [ServiceDefinition.csdef](#csdef) y [ServiceConfig.cscfg](#cscfg) archivos.</span><span class="sxs-lookup"><span data-stu-id="61aff-110">I want tooknow more about hello [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="61aff-111">Eso ya lo sé. Deme [algunos ejemplos](#next-steps) sobre lo que puedo configurar.</span><span class="sxs-lookup"><span data-stu-id="61aff-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="61aff-112">Deseo hello toocreate [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="61aff-112">I want toocreate hello [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="61aff-113">Estoy usando Visual Studio y quiero...</span><span class="sxs-lookup"><span data-stu-id="61aff-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="61aff-114">[Crear un servicio en la nube][vs_create]</span><span class="sxs-lookup"><span data-stu-id="61aff-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="61aff-115">[Volver a configurar un servicio en la nube existente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="61aff-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="61aff-116">[Implementar un proyecto de servicio en la nube][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="61aff-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="61aff-117">[Escritorio remoto en una instancia de servicio en la nube][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="61aff-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="61aff-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="61aff-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="61aff-119">Hola **ServiceDefinition.csdef** archivo especifica valores de hello que usan Azure tooconfigure un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="61aff-119">hello **ServiceDefinition.csdef** file specifies hello settings that are used by Azure tooconfigure a cloud service.</span></span> <span data-ttu-id="61aff-120">Hola [esquema de definición de servicio de Azure (archivo de .csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) proporciona el formato permitido de Hola para un archivo de definición de servicio.</span><span class="sxs-lookup"><span data-stu-id="61aff-120">hello [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides hello allowable format for a service definition file.</span></span> <span data-ttu-id="61aff-121">Hello en el ejemplo siguiente se muestra los Hola valores que se pueden definir para hello Web y roles de trabajo:</span><span class="sxs-lookup"><span data-stu-id="61aff-121">hello following example shows hello settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="61aff-122">Puede hacer referencia a toohello [esquema de definición de servicio](https://msdn.microsoft.com/library/azure/ee758711.aspx) para entender mejor de esquema XML de hello utilizado aquí, sin embargo, aquí es una explicación rápida de algunos de los elementos de hello:</span><span class="sxs-lookup"><span data-stu-id="61aff-122">You can refer toohello [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of hello XML schema used here, however, here is a quick explanation of some of hello elements:</span></span>

<span data-ttu-id="61aff-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="61aff-123">**Sites**</span></span>  
<span data-ttu-id="61aff-124">Contiene definiciones de Hola para aplicaciones web o para sitios Web que se hospedan en IIS7.</span><span class="sxs-lookup"><span data-stu-id="61aff-124">Contains hello definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="61aff-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="61aff-125">**InputEndpoints**</span></span>  
<span data-ttu-id="61aff-126">Contiene definiciones de Hola para puntos de conexión que utiliza el servicio en la nube toocontact Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-126">Contains hello definitions for endpoints that are used toocontact hello cloud service.</span></span>

<span data-ttu-id="61aff-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="61aff-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="61aff-128">Contiene definiciones de Hola para los extremos que usan toocommunicate de instancias de rol entre sí.</span><span class="sxs-lookup"><span data-stu-id="61aff-128">Contains hello definitions for endpoints that are used by role instances toocommunicate with each other.</span></span>

<span data-ttu-id="61aff-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="61aff-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="61aff-130">Contiene definiciones de configuración de Hola para características de un rol específico.</span><span class="sxs-lookup"><span data-stu-id="61aff-130">Contains hello setting definitions for features of a specific role.</span></span>

<span data-ttu-id="61aff-131">**Certificados**</span><span class="sxs-lookup"><span data-stu-id="61aff-131">**Certificates**</span></span>  
<span data-ttu-id="61aff-132">Contiene definiciones de Hola para los certificados que son necesarios para un rol.</span><span class="sxs-lookup"><span data-stu-id="61aff-132">Contains hello definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="61aff-133">ejemplo de código anterior Hello muestra un certificado que se usa para la configuración de Hola de Connect de Azure.</span><span class="sxs-lookup"><span data-stu-id="61aff-133">hello previous code example shows a certificate that is used for hello configuration of Azure Connect.</span></span>

<span data-ttu-id="61aff-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="61aff-134">**LocalResources**</span></span>  
<span data-ttu-id="61aff-135">Contiene las definiciones de Hola para recursos de almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="61aff-135">Contains hello definitions for local storage resources.</span></span> <span data-ttu-id="61aff-136">Un recurso de almacenamiento local es un directorio reservado en sistema de archivos de Hola de máquina virtual de hello en el que está ejecutando una instancia de un rol.</span><span class="sxs-lookup"><span data-stu-id="61aff-136">A local storage resource is a reserved directory on hello file system of hello virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="61aff-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="61aff-137">**Imports**</span></span>  
<span data-ttu-id="61aff-138">Contiene las definiciones de Hola para los módulos importados.</span><span class="sxs-lookup"><span data-stu-id="61aff-138">Contains hello definitions for imported modules.</span></span> <span data-ttu-id="61aff-139">ejemplo de código anterior Hello muestra los módulos de hello para la conexión a Escritorio remoto y Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="61aff-139">hello previous code example shows hello modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="61aff-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="61aff-140">**Startup**</span></span>  
<span data-ttu-id="61aff-141">Contiene tareas que se ejecutan cuando se inicia el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-141">Contains tasks that are run when hello role starts.</span></span> <span data-ttu-id="61aff-142">Hola tareas se definen en un .cmd o un archivo ejecutable.</span><span class="sxs-lookup"><span data-stu-id="61aff-142">hello tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="61aff-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="61aff-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="61aff-144">configuración de Hola de hello para el servicio de nube está determinada por los valores de hello en hello **ServiceConfiguration.cscfg** archivo.</span><span class="sxs-lookup"><span data-stu-id="61aff-144">hello configuration of hello settings for your cloud service is determined by hello values in hello **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="61aff-145">Especificar número de Hola de instancias que desee toodeploy para cada rol en este archivo.</span><span class="sxs-lookup"><span data-stu-id="61aff-145">You specify hello number of instances that you want toodeploy for each role in this file.</span></span> <span data-ttu-id="61aff-146">se agregan valores de Hola Hola opciones de configuración que ha definido en el archivo de definición de servicio de hello toohello archivo de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="61aff-146">hello values for hello configuration settings that you defined in hello service definition file are added toohello service configuration file.</span></span> <span data-ttu-id="61aff-147">huellas digitales de Hola para los certificados de administración que están asociados con el servicio de nube de hello también se agregan archivos toohello.</span><span class="sxs-lookup"><span data-stu-id="61aff-147">hello thumbprints for any management certificates that are associated with hello cloud service are also added toohello file.</span></span> <span data-ttu-id="61aff-148">Hola [esquema de configuración de servicio de Azure (.cscfg archivo)](https://msdn.microsoft.com/library/azure/ee758710.aspx) proporciona el formato permitido de Hola para un archivo de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="61aff-148">hello [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides hello allowable format for a service configuration file.</span></span>

<span data-ttu-id="61aff-149">Hello archivo de configuración de servicio no se empaqueta con la aplicación hello, pero está cargado tooAzure como un archivo independiente y es hello tooconfigure usa el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="61aff-149">hello service configuration file is not packaged with hello application, but is uploaded tooAzure as a separate file and is used tooconfigure hello cloud service.</span></span> <span data-ttu-id="61aff-150">Puede cargar un nuevo archivo de configuración de servicio sin volver a implementar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="61aff-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="61aff-151">valores de configuración de Hola para servicio de nube de Hola se pueden cambiar mientras se ejecuta el servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-151">hello configuration values for hello cloud service can be changed while hello cloud service is running.</span></span> <span data-ttu-id="61aff-152">Hello en el ejemplo siguiente se muestra los valores de configuración de Hola que se pueden definir hello Web y roles de trabajo:</span><span class="sxs-lookup"><span data-stu-id="61aff-152">hello following example shows hello configuration settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="61aff-153">Puede hacer referencia a toohello [esquema de configuración de servicio](https://msdn.microsoft.com/library/azure/ee758710.aspx) para una mejor comprensión Hola esquema XML utilizado aquí, sin embargo, aquí es una explicación rápida de elementos de hello:</span><span class="sxs-lookup"><span data-stu-id="61aff-153">You can refer toohello [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding hello XML schema used here, however, here is a quick explanation of hello elements:</span></span>

<span data-ttu-id="61aff-154">**Instances**</span><span class="sxs-lookup"><span data-stu-id="61aff-154">**Instances**</span></span>  
<span data-ttu-id="61aff-155">Configura el número de Hola de instancias de rol de hello en ejecución.</span><span class="sxs-lookup"><span data-stu-id="61aff-155">Configures hello number of running instances for hello role.</span></span> <span data-ttu-id="61aff-156">tooprevent la nube de servicio deje de estar disponible durante las actualizaciones, se recomienda implementar más de una instancia de los roles web orientadas.</span><span class="sxs-lookup"><span data-stu-id="61aff-156">tooprevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="61aff-157">Mediante la implementación de más de una instancia, siguiendo las directrices de toohello Hola [contrato de nivel de proceso de servicio (SLA) de Azure](http://azure.microsoft.com/support/legal/sla/), lo que garantiza una conectividad externa 99,95% para los roles de conexión a Internet cuando dos o más roles se implementan instancias para un servicio.</span><span class="sxs-lookup"><span data-stu-id="61aff-157">By deploying more than one instance, you are adhering toohello guidelines in hello [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="61aff-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="61aff-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="61aff-159">Configura opciones de Hola para hello instancias en ejecución para un rol.</span><span class="sxs-lookup"><span data-stu-id="61aff-159">Configures hello settings for hello running instances for a role.</span></span> <span data-ttu-id="61aff-160">nombre de Hola de hello `<Setting>` elementos deben coincidir con las definiciones de configuración de hello en el archivo de definición de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-160">hello name of hello `<Setting>` elements must match hello setting definitions in hello service definition file.</span></span>

<span data-ttu-id="61aff-161">**Certificados**</span><span class="sxs-lookup"><span data-stu-id="61aff-161">**Certificates**</span></span>  
<span data-ttu-id="61aff-162">Configura los certificados de Hola que usan el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-162">Configures hello certificates that are used by hello service.</span></span> <span data-ttu-id="61aff-163">ejemplo de código de Hello anterior muestra cómo toodefine Hola certificado para el módulo de RemoteAccess Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-163">hello previous code example shows how toodefine hello certificate for hello RemoteAccess module.</span></span> <span data-ttu-id="61aff-164">Hola valo hello *huella digital* atributo debe establecerse la huella digital de toohello de hello certificado toouse.</span><span class="sxs-lookup"><span data-stu-id="61aff-164">hello value of hello *thumbprint* attribute must be set toohello thumbprint of hello certificate toouse.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="61aff-165">huella digital de Hello para el certificado de hello puede agregarse toohello archivo de configuración mediante un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="61aff-165">hello thumbprint for hello certificate can be added toohello configuration file by using a text editor.</span></span> <span data-ttu-id="61aff-166">O bien, se puede agregar valor hello en hello **certificados** ficha de hello **propiedades** página de rol de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61aff-166">Or, hello value can be added on hello **Certificates** tab of hello **Properties** page of hello role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="61aff-167">Definición de los puertos de las instancias de rol</span><span class="sxs-lookup"><span data-stu-id="61aff-167">Defining ports for role instances</span></span>
<span data-ttu-id="61aff-168">Azure permite solo un rol web de tooa de punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="61aff-168">Azure allows only one entry point tooa web role.</span></span> <span data-ttu-id="61aff-169">Esto significa que todo el tráfico se produce a través de una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="61aff-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="61aff-170">Puede configurar su tooshare un puerto de sitios Web mediante la configuración de hello encabezado toodirect Hola solicitud toohello correcta la ubicación del host.</span><span class="sxs-lookup"><span data-stu-id="61aff-170">You can configure your websites tooshare a port by configuring hello host header toodirect hello request toohello correct location.</span></span> <span data-ttu-id="61aff-171">También puede configurar los puertos de las aplicaciones toolisten toowell conocidos en la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-171">You can also configure your applications toolisten toowell-known ports on hello IP address.</span></span>

<span data-ttu-id="61aff-172">Hello en el ejemplo siguiente muestra hello configuración para un rol web con un sitio Web y una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="61aff-172">hello following sample shows hello configuration for a web role with a website and web application.</span></span> <span data-ttu-id="61aff-173">sitio Web de Hello está configurado como ubicación de entrada predeterminada de hello en el puerto 80, y que las aplicaciones web de hello son solicitudes de tooreceive configurado de un encabezado de host alternativo que se llama "mail.mysite.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="61aff-173">hello website is configured as hello default entry location on port 80, and hello web applications are configured tooreceive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a><span data-ttu-id="61aff-174">Cambiar la configuración de Hola de un rol</span><span class="sxs-lookup"><span data-stu-id="61aff-174">Changing hello configuration of a role</span></span>
<span data-ttu-id="61aff-175">Puede actualizar configuración de hello del servicio en la nube mientras se ejecuta en Azure, sin necesidad de desconectar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-175">You can update hello configuration of your cloud service while it is running in Azure, without taking hello service offline.</span></span> <span data-ttu-id="61aff-176">información de configuración de toochange, puede cargar un archivo de configuración o modificar el archivo de configuración de hello en colocar y aplicarlo tooyour ejecuta el servicio.</span><span class="sxs-lookup"><span data-stu-id="61aff-176">toochange configuration information, you can either upload a new configuration file, or edit hello configuration file in place and apply it tooyour running service.</span></span> <span data-ttu-id="61aff-177">Hello siguientes pueden realizarse cambios toohello configuración de un servicio:</span><span class="sxs-lookup"><span data-stu-id="61aff-177">hello following changes can be made toohello configuration of a service:</span></span>

* <span data-ttu-id="61aff-178">**Cambiar los valores de hello de valores de configuración**</span><span class="sxs-lookup"><span data-stu-id="61aff-178">**Changing hello values of configuration settings**</span></span>  
  <span data-ttu-id="61aff-179">Cuando una configuración de cambios, en la configuración una instancia de rol puede elegir tooapply Hola cambio mientras está en línea la instancia de Hola o instancia de hello toorecycle correctamente y aplicar el cambio de hello mientras Hola instancia está sin conexión.</span><span class="sxs-lookup"><span data-stu-id="61aff-179">When a configuration setting changes, a role instance can choose tooapply hello change while hello instance is online, or toorecycle hello instance gracefully and apply hello change while hello instance is offline.</span></span>
* <span data-ttu-id="61aff-180">**Cambiar la topología del servicio Hola de instancias de rol**</span><span class="sxs-lookup"><span data-stu-id="61aff-180">**Changing hello service topology of role instances**</span></span>  
  <span data-ttu-id="61aff-181">: los cambios en la topología no afectan a las instancias en ejecución, excepto donde se vaya a eliminar una instancia.</span><span class="sxs-lookup"><span data-stu-id="61aff-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="61aff-182">Todas las instancias restantes por lo general no es necesario toobe recicle; Sin embargo, puede elegir toorecycle instancias de rol en el cambio de topología de respuesta tooa.</span><span class="sxs-lookup"><span data-stu-id="61aff-182">All remaining instances generally do not need toobe recycled; however, you can choose toorecycle role instances in response tooa topology change.</span></span>
* <span data-ttu-id="61aff-183">**Cambio de huella digital del certificado Hola**</span><span class="sxs-lookup"><span data-stu-id="61aff-183">**Changing hello certificate thumbprint**</span></span>  
  <span data-ttu-id="61aff-184">: solo puede actualizar un certificado cuando una instancia de rol está sin conexión.</span><span class="sxs-lookup"><span data-stu-id="61aff-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="61aff-185">Si un certificado es agregado, eliminado o cambiado mientras una instancia de rol está en línea, Azure correctamente toma certificado Hola de hello instancia tooupdate sin conexión y volver a iniciarlo en línea una vez completado el cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes hello instance offline tooupdate hello certificate and bring it back online after hello change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="61aff-186">Control de los cambios de configuración con eventos de tiempo de ejecución de servicio</span><span class="sxs-lookup"><span data-stu-id="61aff-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="61aff-187">Hola [biblioteca en tiempo de ejecución de Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) incluye hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) espacio de nombres, que proporciona clases para interactuar con hello entorno de Azure desde un rol.</span><span class="sxs-lookup"><span data-stu-id="61aff-187">hello [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with hello Azure environment from a role.</span></span> <span data-ttu-id="61aff-188">Hola [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) clase define Hola después de eventos que se producen antes y después de un cambio de configuración:</span><span class="sxs-lookup"><span data-stu-id="61aff-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines hello following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="61aff-189">**[Cambiar](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) evento**</span><span class="sxs-lookup"><span data-stu-id="61aff-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="61aff-190">Esto se produce antes de cambio de configuración de hello tooa aplicada la instancia especificada de un rol de ofrecerle una tootake oportunidad hacia abajo de instancias de rol de hello si es necesario.</span><span class="sxs-lookup"><span data-stu-id="61aff-190">This occurs before hello configuration change is applied tooa specified instance of a role giving you a chance tootake down hello role instances if necessary.</span></span>
* <span data-ttu-id="61aff-191">**[Evento](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) cambiado**</span><span class="sxs-lookup"><span data-stu-id="61aff-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="61aff-192">Se produce después del cambio de configuración de hello tooa aplicada la instancia especificada de un rol.</span><span class="sxs-lookup"><span data-stu-id="61aff-192">Occurs after hello configuration change is applied tooa specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="61aff-193">Dado que cambios en el certificado siempre tienen instancias de Hola de un rol sin conexión, no producen eventos RoleEnvironment.Changing o RoleEnvironment.Changed de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-193">Because certificate changes always take hello instances of a role offline, they do not raise hello RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="61aff-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="61aff-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="61aff-195">toodeploy una aplicación como un servicio de nube en Azure, primero debe primera aplicación Hola de paquete en formato adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-195">toodeploy an application as a cloud service in Azure, you must first package hello application in hello appropriate format.</span></span> <span data-ttu-id="61aff-196">Puede usar hello **CSPack** herramienta de línea de comandos (instalado con hello [Azure SDK](https://azure.microsoft.com/downloads/)) archivo de paquete de hello toocreate como una alternativa tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="61aff-196">You can use hello **CSPack** command-line tool (installed with hello [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello package file as an alternative tooVisual Studio.</span></span>

<span data-ttu-id="61aff-197">**CSPack** usa Hola contenido de hello servicio definición servicios de archivos y configuración toodefine Hola contenido del archivo de paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="61aff-197">**CSPack** uses hello contents of hello service definition file and service configuration file toodefine hello contents of hello package.</span></span> <span data-ttu-id="61aff-198">**CSPack** genera un archivo de paquete de aplicación (.cspkg) que se puede cargar tooAzure mediante hello [portal de Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="61aff-198">**CSPack** generates an application package file (.cspkg) that you can upload tooAzure by using hello [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="61aff-199">De forma predeterminada, se denomina paquete hello `[ServiceDefinitionFileName].cspkg`, pero puede especificar un nombre diferente mediante el uso de hello `/out` opción de **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="61aff-199">By default, hello package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using hello `/out` option of **CSPack**.</span></span>

<span data-ttu-id="61aff-200">**CSPack** se encuentra en:</span><span class="sxs-lookup"><span data-stu-id="61aff-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="61aff-201">CSPack.exe (en windows) está disponible mediante la ejecución de hello **Microsoft Azure Command Prompt** acceso directo que se instala con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="61aff-201">CSPack.exe (on windows) is available by running hello **Microsoft Azure Command Prompt** shortcut that is installed with hello SDK.</span></span>  
> 
> <span data-ttu-id="61aff-202">Ejecutar programa de hello CSPack.exe toosee documentación sobre todos los conmutadores de hello posibles y los comandos.</span><span class="sxs-lookup"><span data-stu-id="61aff-202">Run hello CSPack.exe program by itself toosee documentation about all hello possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="61aff-203">Ejecutar su servicio en la nube localmente en hello **emulador de proceso de Microsoft Azure**, usar hello **/copyonly** opción.</span><span class="sxs-lookup"><span data-stu-id="61aff-203">Run your cloud service locally in hello **Microsoft Azure Compute Emulator**, use hello **/copyonly** option.</span></span> <span data-ttu-id="61aff-204">Esta opción copia los archivos binarios de hello para el diseño de directorio tooa Hola aplicación desde el que se pueden ejecutar en el emulador de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-204">This option copies hello binary files for hello application tooa directory layout from which they can be run in hello compute emulator.</span></span>
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a><span data-ttu-id="61aff-205">Comando de ejemplo toopackage un servicio de nube</span><span class="sxs-lookup"><span data-stu-id="61aff-205">Example command toopackage a cloud service</span></span>
<span data-ttu-id="61aff-206">Hello en el ejemplo siguiente se crea un paquete de aplicación que contiene información de Hola para un rol web.</span><span class="sxs-lookup"><span data-stu-id="61aff-206">hello following example creates an application package that contains hello information for a web role.</span></span> <span data-ttu-id="61aff-207">comando Hello especifica toouse de archivo de definición de servicio de hello, directory Hola donde pueden ser archivos binarios encuentra y Hola nombre del archivo de paquete de hello.</span><span class="sxs-lookup"><span data-stu-id="61aff-207">hello command specifies hello service definition file toouse, hello directory where binary files can be found, and hello name of hello package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="61aff-208">Si la aplicación hello contiene un rol web y un rol de trabajo, hello siguiente comando se utiliza:</span><span class="sxs-lookup"><span data-stu-id="61aff-208">If hello application contains both a web role and a worker role, hello following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="61aff-209">Donde las variables de Hola se definen como sigue:</span><span class="sxs-lookup"><span data-stu-id="61aff-209">Where hello variables are defined as follows:</span></span>

| <span data-ttu-id="61aff-210">Variable</span><span class="sxs-lookup"><span data-stu-id="61aff-210">Variable</span></span> | <span data-ttu-id="61aff-211">Valor</span><span class="sxs-lookup"><span data-stu-id="61aff-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="61aff-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="61aff-212">\[DirectoryName\]</span></span> |<span data-ttu-id="61aff-213">Hola subdirectorio en hello directorio raíz del proyecto que contiene el archivo de .csdef Hola de hello proyecto de Azure.</span><span class="sxs-lookup"><span data-stu-id="61aff-213">hello subdirectory under hello root project directory that contains hello .csdef file of hello Azure project.</span></span> |
| <span data-ttu-id="61aff-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="61aff-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="61aff-215">nombre de Hola Hola servicio del archivo de definición.</span><span class="sxs-lookup"><span data-stu-id="61aff-215">hello name of hello service definition file.</span></span> <span data-ttu-id="61aff-216">De forma predeterminada, este archivo se denomina ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="61aff-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="61aff-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="61aff-217">\[OutputFileName\]</span></span> |<span data-ttu-id="61aff-218">nombre de Hola para hello genera el archivo de paquete.</span><span class="sxs-lookup"><span data-stu-id="61aff-218">hello name for hello generated package file.</span></span> <span data-ttu-id="61aff-219">Normalmente, esto se establece toohello nombre de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="61aff-219">Typically, this is set toohello name of hello application.</span></span> <span data-ttu-id="61aff-220">Si no se especifica ningún nombre de archivo, el paquete de aplicación Hola se crea como \[ApplicationName\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="61aff-220">If no file name is specified, hello application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="61aff-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="61aff-221">\[RoleName\]</span></span> |<span data-ttu-id="61aff-222">nombre de Hello del rol de hello tal como se define en el archivo de definición de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-222">hello name of hello role as defined in hello service definition file.</span></span> |
| <span data-ttu-id="61aff-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="61aff-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="61aff-224">ubicación de Hola de archivos binarios de hello para el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-224">hello location of hello binary files for hello role.</span></span> |
| <span data-ttu-id="61aff-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="61aff-225">\[VirtualPath\]</span></span> |<span data-ttu-id="61aff-226">directorios físicos de Hola para cada ruta de acceso virtual definida en hello sitios sección de definición de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-226">hello physical directories for each virtual path defined in hello Sites section of hello service definition.</span></span> |
| <span data-ttu-id="61aff-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="61aff-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="61aff-228">Hola directorios físicos del contenido de Hola para cada ruta de acceso virtual definidos en el nodo de sitio de Hola de definición de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-228">hello physical directories of hello contents for each virtual path defined in hello site node of hello service definition.</span></span> |
| <span data-ttu-id="61aff-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="61aff-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="61aff-230">nombre de Hello del archivo binario de hello para el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="61aff-230">hello name of hello binary file for hello role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61aff-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61aff-231">Next steps</span></span>
<span data-ttu-id="61aff-232">Voy a crear un paquete de servicio en la nube y quiero...</span><span class="sxs-lookup"><span data-stu-id="61aff-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="61aff-233">[Configurar Escritorio remoto para una instancia de servicio en la nube][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="61aff-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="61aff-234">[Implementar un proyecto de servicio en la nube][deploy]</span><span class="sxs-lookup"><span data-stu-id="61aff-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="61aff-235">Estoy usando Visual Studio y quiero...</span><span class="sxs-lookup"><span data-stu-id="61aff-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="61aff-236">[Crear un nuevo servicio en la nube][vs_create]</span><span class="sxs-lookup"><span data-stu-id="61aff-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="61aff-237">[Volver a configurar un servicio en la nube existente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="61aff-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="61aff-238">[Implementar un proyecto de servicio en la nube][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="61aff-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="61aff-239">[Configurar Escritorio remoto para una instancia de servicio en la nube][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="61aff-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
