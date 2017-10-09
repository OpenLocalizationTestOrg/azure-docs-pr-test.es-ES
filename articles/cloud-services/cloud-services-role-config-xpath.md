---
title: "hoja de referencia de XPath de configuración de rol de servicios de aaaCloud | Documentos de Microsoft"
description: "Hola distintas configuraciones de XPath que se puede utilizar en valores tooexpose de configuración de rol de servicio de hello en la nube como una variable de entorno."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="449d1-103">Exponer los valores de configuración de rol como una variable de entorno con XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="449d1-104">En el trabajo de servicio de nube de Hola o archivo de definición de servicio de rol web, puede exponer los valores de configuración en tiempo de ejecución como variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="449d1-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="449d1-105">Hola después de los valores de XPath se admite (que corresponden a los valores de tooAPI).</span><span class="sxs-lookup"><span data-stu-id="449d1-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="449d1-106">Estos valores de XPath también están disponibles a través de hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="449d1-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="449d1-107">Aplicación en ejecución en el emulador</span><span class="sxs-lookup"><span data-stu-id="449d1-107">App running in emulator</span></span>
<span data-ttu-id="449d1-108">Indica que la aplicación Hola se ejecuta en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="449d1-109">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-109">Type</span></span> | <span data-ttu-id="449d1-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-111">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-111">XPath</span></span> |<span data-ttu-id="449d1-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="449d1-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="449d1-113">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-113">Code</span></span> |<span data-ttu-id="449d1-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="449d1-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="449d1-115">Id. de implementación</span><span class="sxs-lookup"><span data-stu-id="449d1-115">Deployment ID</span></span>
<span data-ttu-id="449d1-116">Recupera el identificador de implementación de hello para la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="449d1-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-117">Type</span></span> | <span data-ttu-id="449d1-118">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-119">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-119">XPath</span></span> |<span data-ttu-id="449d1-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="449d1-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="449d1-121">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-121">Code</span></span> |<span data-ttu-id="449d1-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="449d1-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="449d1-123">Id. de rol</span><span class="sxs-lookup"><span data-stu-id="449d1-123">Role ID</span></span>
<span data-ttu-id="449d1-124">Recupera el identificador de rol actual de hello para la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="449d1-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-125">Type</span></span> | <span data-ttu-id="449d1-126">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-127">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-127">XPath</span></span> |<span data-ttu-id="449d1-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="449d1-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="449d1-129">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-129">Code</span></span> |<span data-ttu-id="449d1-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="449d1-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="449d1-131"> Actualizar dominio</span><span class="sxs-lookup"><span data-stu-id="449d1-131">Update domain</span></span>
<span data-ttu-id="449d1-132">Recupera el dominio de actualización de Hola de instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="449d1-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-133">Type</span></span> | <span data-ttu-id="449d1-134">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-135">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-135">XPath</span></span> |<span data-ttu-id="449d1-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="449d1-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="449d1-137">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-137">Code</span></span> |<span data-ttu-id="449d1-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="449d1-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="449d1-139">Dominio de error</span><span class="sxs-lookup"><span data-stu-id="449d1-139">Fault domain</span></span>
<span data-ttu-id="449d1-140">Recupera el dominio de error de Hola de instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="449d1-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-141">Type</span></span> | <span data-ttu-id="449d1-142">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-143">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-143">XPath</span></span> |<span data-ttu-id="449d1-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="449d1-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="449d1-145">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-145">Code</span></span> |<span data-ttu-id="449d1-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="449d1-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="449d1-147">Nombre de rol</span><span class="sxs-lookup"><span data-stu-id="449d1-147">Role name</span></span>
<span data-ttu-id="449d1-148">Recupera el nombre de la función hello de instancias de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="449d1-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-149">Type</span></span> | <span data-ttu-id="449d1-150">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-151">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-151">XPath</span></span> |<span data-ttu-id="449d1-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="449d1-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="449d1-153">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-153">Code</span></span> |<span data-ttu-id="449d1-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="449d1-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="449d1-155">Opción de configuración</span><span class="sxs-lookup"><span data-stu-id="449d1-155">Config setting</span></span>
<span data-ttu-id="449d1-156">Recupera Hola valo Hola especifica valor de configuración.</span><span class="sxs-lookup"><span data-stu-id="449d1-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="449d1-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-157">Type</span></span> | <span data-ttu-id="449d1-158">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-159">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-159">XPath</span></span> |<span data-ttu-id="449d1-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="449d1-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="449d1-161">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-161">Code</span></span> |<span data-ttu-id="449d1-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="449d1-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="449d1-163">Ruta de acceso de almacenamiento local</span><span class="sxs-lookup"><span data-stu-id="449d1-163">Local storage path</span></span>
<span data-ttu-id="449d1-164">Recupera la ruta de acceso de almacenamiento local de hello para la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="449d1-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-165">Type</span></span> | <span data-ttu-id="449d1-166">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-167">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-167">XPath</span></span> |<span data-ttu-id="449d1-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="449d1-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="449d1-169">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-169">Code</span></span> |<span data-ttu-id="449d1-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="449d1-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="449d1-171">Tamaño del almacenamiento local</span><span class="sxs-lookup"><span data-stu-id="449d1-171">Local storage size</span></span>
<span data-ttu-id="449d1-172">Recupera el tamaño de Hola de almacenamiento local de hello para la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="449d1-173">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-173">Type</span></span> | <span data-ttu-id="449d1-174">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-175">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-175">XPath</span></span> |<span data-ttu-id="449d1-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="449d1-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="449d1-177">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-177">Code</span></span> |<span data-ttu-id="449d1-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="449d1-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="449d1-179">Protocolo del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="449d1-179">Endpoint protocol</span></span>
<span data-ttu-id="449d1-180">Recupera el protocolo de extremo de hello para la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="449d1-181">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-181">Type</span></span> | <span data-ttu-id="449d1-182">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-183">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-183">XPath</span></span> |<span data-ttu-id="449d1-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="449d1-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="449d1-185">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-185">Code</span></span> |<span data-ttu-id="449d1-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="449d1-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="449d1-187">IP del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="449d1-187">Endpoint IP</span></span>
<span data-ttu-id="449d1-188">Hola Obtiene la dirección IP del punto de conexión especificada.</span><span class="sxs-lookup"><span data-stu-id="449d1-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="449d1-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-189">Type</span></span> | <span data-ttu-id="449d1-190">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-191">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-191">XPath</span></span> |<span data-ttu-id="449d1-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="449d1-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="449d1-193">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-193">Code</span></span> |<span data-ttu-id="449d1-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="449d1-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="449d1-195">Puerto del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="449d1-195">Endpoint port</span></span>
<span data-ttu-id="449d1-196">Recupera el puerto de extremo de hello para la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="449d1-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="449d1-197">Tipo</span><span class="sxs-lookup"><span data-stu-id="449d1-197">Type</span></span> | <span data-ttu-id="449d1-198">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="449d1-199">XPath</span><span class="sxs-lookup"><span data-stu-id="449d1-199">XPath</span></span> |<span data-ttu-id="449d1-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="449d1-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="449d1-201">Código</span><span class="sxs-lookup"><span data-stu-id="449d1-201">Code</span></span> |<span data-ttu-id="449d1-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="449d1-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="449d1-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="449d1-203">Example</span></span>
<span data-ttu-id="449d1-204">Este es un ejemplo de un rol de trabajo que crea una tarea de inicio con una variable de entorno denominada `TestIsEmulated` establecer toohello [ @emulated valor xpath](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="449d1-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a><span data-ttu-id="449d1-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="449d1-205">Next steps</span></span>
<span data-ttu-id="449d1-206">Obtener más información sobre hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) archivo.</span><span class="sxs-lookup"><span data-stu-id="449d1-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="449d1-207">Cree un paquete [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .</span><span class="sxs-lookup"><span data-stu-id="449d1-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="449d1-208">Habilite [Escritorio remoto](cloud-services-role-enable-remote-desktop.md) para un rol.</span><span class="sxs-lookup"><span data-stu-id="449d1-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

