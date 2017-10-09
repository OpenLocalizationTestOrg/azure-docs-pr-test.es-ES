---
title: "roles de servicios en la nube aaaAzure preguntas más frecuentes | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre Azure Cloud Services. Responde a algunas preguntas comunes sobre certificados, roles web y roles de trabajo."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="ff911-104">P+F de Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="ff911-104">Cloud Services FAQ</span></span>
<span data-ttu-id="ff911-105">En este artículo se responden algunas preguntas frecuentes sobre Servicios en la nube de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ff911-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="ff911-106">También puede visitar hello [preguntas frecuentes de soporte de Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para información general de precios y soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff911-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="ff911-107">También puede consultar hello [página de tamaño de máquina virtual de servicios de nube](cloud-services-sizes-specs.md) para obtener información de tamaño.</span><span class="sxs-lookup"><span data-stu-id="ff911-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="ff911-108">Certificados</span><span class="sxs-lookup"><span data-stu-id="ff911-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="ff911-109">¿Dónde debo instalar mi certificado?</span><span class="sxs-lookup"><span data-stu-id="ff911-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="ff911-110">**My**</span><span class="sxs-lookup"><span data-stu-id="ff911-110">**My**</span></span>  
  <span data-ttu-id="ff911-111">Certificado de aplicación con clave privada (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="ff911-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="ff911-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="ff911-112">**CA**</span></span>  
  <span data-ttu-id="ff911-113">Todos los certificados intermedios van a este almacén (entidades de certificación de directivas y secundarias).</span><span class="sxs-lookup"><span data-stu-id="ff911-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="ff911-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="ff911-114">**ROOT**</span></span>  
  <span data-ttu-id="ff911-115">almacén de CA raíz de Hola, por lo que el certificado de CA raíz principal aquí debe ir.</span><span class="sxs-lookup"><span data-stu-id="ff911-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="ff911-116">No se puede quitar el certificado expirado</span><span class="sxs-lookup"><span data-stu-id="ff911-116">I can't remove expired certificate</span></span>
<span data-ttu-id="ff911-117">Azure impide quitar un certificado mientras está en uso.</span><span class="sxs-lookup"><span data-stu-id="ff911-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="ff911-118">Se necesita tooeither eliminación hello de la implementación que utiliza certificados de Hola o parche Hola con un certificado diferente o renovado.</span><span class="sxs-lookup"><span data-stu-id="ff911-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="ff911-119">Eliminar un certificado expirado</span><span class="sxs-lookup"><span data-stu-id="ff911-119">Delete an expired certificate</span></span>
<span data-ttu-id="ff911-120">Como certificado de hello no está en uso, puede usar hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove de cmdlet de PowerShell un certificado.</span><span class="sxs-lookup"><span data-stu-id="ff911-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="ff911-121">Tengo certificados expirados denominados Administración de servicios de Microsoft Azure para Extensiones</span><span class="sxs-lookup"><span data-stu-id="ff911-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="ff911-122">Estos certificados se crean cada vez que se agrega una extensión toohello servicio en la nube como Hola extensión de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="ff911-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="ff911-123">Estos certificados sólo se utilizan para cifrar y descifrar la configuración privada de Hola de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff911-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="ff911-124">No importa si estos certificados expiran.</span><span class="sxs-lookup"><span data-stu-id="ff911-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="ff911-125">no se comprueba la fecha de expiración de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff911-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="ff911-126">Siguen apareciendo certificados que he eliminado</span><span class="sxs-lookup"><span data-stu-id="ff911-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="ff911-127">Estos siguen reapareciendo muy probablemente a causa de una herramienta que esté utilizando, como Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff911-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="ff911-128">Cada vez que se vuelve a conectar con una herramienta que está utilizando un certificado, nuevo será tooAzure cargado.</span><span class="sxs-lookup"><span data-stu-id="ff911-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="ff911-129">Mis certificados siguen desapareciendo</span><span class="sxs-lookup"><span data-stu-id="ff911-129">My certificates keep disappearing</span></span>
<span data-ttu-id="ff911-130">Cuando se recicla la instancia de la máquina virtual de hello, se pierden todos los cambios locales.</span><span class="sxs-lookup"><span data-stu-id="ff911-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="ff911-131">Use un [tarea de inicio](cloud-services-startup-tasks.md) tooinstall certificados toohello virtual machine se inicia cada rol de Hola de tiempo.</span><span class="sxs-lookup"><span data-stu-id="ff911-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="ff911-132">No encuentro mi certificados de administración en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="ff911-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="ff911-133">[Certificados de administración](../azure-api-management-certs.md) sólo están disponibles en hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff911-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="ff911-134">portal de Azure actual Hello no utiliza certificados de administración.</span><span class="sxs-lookup"><span data-stu-id="ff911-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="ff911-135">¿Cómo puedo deshabilitar un certificado de administración?</span><span class="sxs-lookup"><span data-stu-id="ff911-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="ff911-136">[certificados de administración](../azure-api-management-certs.md) .</span><span class="sxs-lookup"><span data-stu-id="ff911-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="ff911-137">Eliminarlas a través de hello Portal clásico de Azure si no quiere toobe usar más.</span><span class="sxs-lookup"><span data-stu-id="ff911-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="ff911-138">¿Cómo puedo crear un certificado SSL para una dirección IP específica?</span><span class="sxs-lookup"><span data-stu-id="ff911-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="ff911-139">Siga las instrucciones de Hola Hola [crear un tutorial de certificado](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="ff911-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="ff911-140">Usar dirección IP de hello como Hola nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="ff911-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="ff911-141">Seguridad</span><span class="sxs-lookup"><span data-stu-id="ff911-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="ff911-142">Deshabilitar SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="ff911-142">Disable SSL 3.0</span></span>
<span data-ttu-id="ff911-143">toodisable SSL 3.0 y utilizar la seguridad TLS, cree una tarea de inicio que se describe en esta entrada de blog: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="ff911-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="ff911-144">Agregar **nosniff** sitio Web de tooyour</span><span class="sxs-lookup"><span data-stu-id="ff911-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="ff911-145">los clientes de tooprevent de examen de los tipos MIME hello, agregar una configuración en su *web.config* archivo.</span><span class="sxs-lookup"><span data-stu-id="ff911-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="ff911-146">También puede agregarlo como un ajuste en IIS.</span><span class="sxs-lookup"><span data-stu-id="ff911-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="ff911-147">Comando siguiente de Hola de uso con hello [tareas comunes de inicio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artículo.</span><span class="sxs-lookup"><span data-stu-id="ff911-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="ff911-148">Personalización de IIS para un rol web</span><span class="sxs-lookup"><span data-stu-id="ff911-148">Customize IIS for a web role</span></span>
<span data-ttu-id="ff911-149">Usar script de inicio IIS de Hola de hello [tareas comunes de inicio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artículo.</span><span class="sxs-lookup"><span data-stu-id="ff911-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="ff911-150">Escalado</span><span class="sxs-lookup"><span data-stu-id="ff911-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="ff911-151">No puedo escalar más allá de X instancias</span><span class="sxs-lookup"><span data-stu-id="ff911-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="ff911-152">La suscripción de Azure tiene un límite en número de Hola de núcleos que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="ff911-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="ff911-153">Ajuste de escala no funcionará si ha utilizado todos los núcleos de hello disponibles.</span><span class="sxs-lookup"><span data-stu-id="ff911-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="ff911-154">Por ejemplo, si tiene un límite de 100 núcleos, esto significa que podría tener 100 instancias de máquina virtual de tamaño A1 para su servicio en la nube o 50 instancias de máquina virtual de tamaño A2.</span><span class="sxs-lookup"><span data-stu-id="ff911-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="ff911-155">Redes</span><span class="sxs-lookup"><span data-stu-id="ff911-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="ff911-156">No se puede reservar una dirección IP en un servicio en la nube con varias direcciones IP virtuales</span><span class="sxs-lookup"><span data-stu-id="ff911-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="ff911-157">En primer lugar, asegúrese de que esa instancia de máquina virtual de Hola que intentas tooreserve Hola IP para está activada.</span><span class="sxs-lookup"><span data-stu-id="ff911-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="ff911-158">En segundo lugar, asegúrese de que está usando direcciones IP reservadas para implementaciones de ensayo y producción de hello molestarse en.</span><span class="sxs-lookup"><span data-stu-id="ff911-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="ff911-159">**No** cambiar la configuración de hello mientras se actualiza la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff911-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="ff911-160">Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="ff911-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="ff911-161">¿Cómo se usa el escritorio remoto con un NSG?</span><span class="sxs-lookup"><span data-stu-id="ff911-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="ff911-162">Agregar reglas toohello NSG que permitan el tráfico en puertos **3389** y **20000**.</span><span class="sxs-lookup"><span data-stu-id="ff911-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="ff911-163">Escritorio remoto usa el puerto **3389**.</span><span class="sxs-lookup"><span data-stu-id="ff911-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="ff911-164">Instancias de servicio en la nube son carga equilibrada, por lo que directamente no se puede controlar qué tooconnect de instancia a.</span><span class="sxs-lookup"><span data-stu-id="ff911-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="ff911-165">Hola *RemoteForwarder* y *RemoteAccess* agentes administrar el tráfico RDP y permitir Hola cliente toosend una cookie RDP y especificar un tooconnect de una instancia individual a.</span><span class="sxs-lookup"><span data-stu-id="ff911-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="ff911-166">Hola *RemoteForwarder* y *RemoteAccess* agentes requieren ese puerto **20000*** abrirse, que pueden bloquearse si tienes un NSG.</span><span class="sxs-lookup"><span data-stu-id="ff911-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
