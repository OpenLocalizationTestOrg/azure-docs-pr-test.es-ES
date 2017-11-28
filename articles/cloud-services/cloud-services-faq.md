---
title: "Preguntas más frecuentes sobre roles de Azure Cloud Services | Microsoft Docs"
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
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="cfca7-104">P+F de Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="cfca7-104">Cloud Services FAQ</span></span>
<span data-ttu-id="cfca7-105">En este artículo se responden algunas preguntas frecuentes sobre Servicios en la nube de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cfca7-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="cfca7-106">También puede visitar [Preguntas más frecuentes de soporte técnico de Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para información general sobre los precios y el soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="cfca7-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="cfca7-107">También puede consultar la [página Tamaños de los servicios en la nube](cloud-services-sizes-specs.md) para obtener información de tamaño.</span><span class="sxs-lookup"><span data-stu-id="cfca7-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="cfca7-108">Certificados</span><span class="sxs-lookup"><span data-stu-id="cfca7-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="cfca7-109">¿Dónde debo instalar mi certificado?</span><span class="sxs-lookup"><span data-stu-id="cfca7-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="cfca7-110">**My**</span><span class="sxs-lookup"><span data-stu-id="cfca7-110">**My**</span></span>  
  <span data-ttu-id="cfca7-111">Certificado de aplicación con clave privada (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="cfca7-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="cfca7-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="cfca7-112">**CA**</span></span>  
  <span data-ttu-id="cfca7-113">Todos los certificados intermedios van a este almacén (entidades de certificación de directivas y secundarias).</span><span class="sxs-lookup"><span data-stu-id="cfca7-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="cfca7-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="cfca7-114">**ROOT**</span></span>  
  <span data-ttu-id="cfca7-115">El almacén de entidades de certificación raíz, por lo que la mayoría de certificados de entidades de certificación raíz van aquí.</span><span class="sxs-lookup"><span data-stu-id="cfca7-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="cfca7-116">No se puede quitar el certificado expirado</span><span class="sxs-lookup"><span data-stu-id="cfca7-116">I can't remove expired certificate</span></span>
<span data-ttu-id="cfca7-117">Azure impide quitar un certificado mientras está en uso.</span><span class="sxs-lookup"><span data-stu-id="cfca7-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="cfca7-118">Debe eliminar la implementación que utiliza el certificado o actualizar la implementación con un certificado diferente o renovado.</span><span class="sxs-lookup"><span data-stu-id="cfca7-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="cfca7-119">Eliminar un certificado expirado</span><span class="sxs-lookup"><span data-stu-id="cfca7-119">Delete an expired certificate</span></span>
<span data-ttu-id="cfca7-120">Siempre que el certificado no esté en uso, podrá usar el cmdlet de PowerShell [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) para quitar un certificado.</span><span class="sxs-lookup"><span data-stu-id="cfca7-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="cfca7-121">Tengo certificados expirados denominados Administración de servicios de Microsoft Azure para Extensiones</span><span class="sxs-lookup"><span data-stu-id="cfca7-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="cfca7-122">Estos certificados se crean siempre que se agrega una extensión al servicio en la nube, como la extensión de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="cfca7-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="cfca7-123">Estos certificados solo se utilizan para cifrar y descifrar la configuración privada de la extensión.</span><span class="sxs-lookup"><span data-stu-id="cfca7-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="cfca7-124">No importa si estos certificados expiran.</span><span class="sxs-lookup"><span data-stu-id="cfca7-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="cfca7-125">La fecha de expiración no se comprueba.</span><span class="sxs-lookup"><span data-stu-id="cfca7-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="cfca7-126">Siguen apareciendo certificados que he eliminado</span><span class="sxs-lookup"><span data-stu-id="cfca7-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="cfca7-127">Estos siguen reapareciendo muy probablemente a causa de una herramienta que esté utilizando, como Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cfca7-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="cfca7-128">Cada vez que vuelva a conectar con una herramienta que esté utilizando un certificado, este se volverá a cargar en Azure.</span><span class="sxs-lookup"><span data-stu-id="cfca7-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="cfca7-129">Mis certificados siguen desapareciendo</span><span class="sxs-lookup"><span data-stu-id="cfca7-129">My certificates keep disappearing</span></span>
<span data-ttu-id="cfca7-130">Cuando se recicla la instancia de máquina virtual, se pierden todos los cambios locales.</span><span class="sxs-lookup"><span data-stu-id="cfca7-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="cfca7-131">Use una [tarea de inicio](cloud-services-startup-tasks.md) para instalar certificados en la máquina virtual cada vez que se inicie el rol.</span><span class="sxs-lookup"><span data-stu-id="cfca7-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="cfca7-132">No encuentro mis certificados de administración en el portal</span><span class="sxs-lookup"><span data-stu-id="cfca7-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="cfca7-133">Los [certificados de administración](../azure-api-management-certs.md) solo están disponibles en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="cfca7-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="cfca7-134">La versión actual de Azure Portal no utiliza certificados de administración.</span><span class="sxs-lookup"><span data-stu-id="cfca7-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="cfca7-135">¿Cómo puedo deshabilitar un certificado de administración?</span><span class="sxs-lookup"><span data-stu-id="cfca7-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="cfca7-136">[certificados de administración](../azure-api-management-certs.md) .</span><span class="sxs-lookup"><span data-stu-id="cfca7-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="cfca7-137">Se eliminan en el Portal de Azure clásico cuando ya no quiera utilizarlos más.</span><span class="sxs-lookup"><span data-stu-id="cfca7-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="cfca7-138">¿Cómo puedo crear un certificado SSL para una dirección IP específica?</span><span class="sxs-lookup"><span data-stu-id="cfca7-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="cfca7-139">Siga las instrucciones del [tutorial de creación de un tutorial](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="cfca7-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="cfca7-140">Utilice la dirección IP como el nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="cfca7-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="cfca7-141">Seguridad</span><span class="sxs-lookup"><span data-stu-id="cfca7-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="cfca7-142">Deshabilitar SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="cfca7-142">Disable SSL 3.0</span></span>
<span data-ttu-id="cfca7-143">Para deshabilitar SSL 3.0 y usar la seguridad TLS, cree una tarea de inicio que se documente en esta entrada de blog: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="cfca7-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="cfca7-144">Agregue **nosniff** a su sitio web</span><span class="sxs-lookup"><span data-stu-id="cfca7-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="cfca7-145">Para evitar que los clientes curioseen en los tipos MIME, agregue un ajuste a su archivo *web.config*.</span><span class="sxs-lookup"><span data-stu-id="cfca7-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="cfca7-146">También puede agregarlo como un ajuste en IIS.</span><span class="sxs-lookup"><span data-stu-id="cfca7-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="cfca7-147">Use el comando siguiente con el artículo [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) (tareas comunes de inicio).</span><span class="sxs-lookup"><span data-stu-id="cfca7-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="cfca7-148">Personalización de IIS para un rol web</span><span class="sxs-lookup"><span data-stu-id="cfca7-148">Customize IIS for a web role</span></span>
<span data-ttu-id="cfca7-149">Use el script de inicio de IIS del artículo [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) (tareas comunes de inicio).</span><span class="sxs-lookup"><span data-stu-id="cfca7-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="cfca7-150">Escalado</span><span class="sxs-lookup"><span data-stu-id="cfca7-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="cfca7-151">No puedo escalar más allá de X instancias</span><span class="sxs-lookup"><span data-stu-id="cfca7-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="cfca7-152">La suscripción de Azure tiene un límite en el número de núcleos que se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="cfca7-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="cfca7-153">El escalado no funcionará si ha usado todos los núcleos disponibles.</span><span class="sxs-lookup"><span data-stu-id="cfca7-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="cfca7-154">Por ejemplo, si tiene un límite de 100 núcleos, esto significa que podría tener 100 instancias de máquina virtual de tamaño A1 para su servicio en la nube o 50 instancias de máquina virtual de tamaño A2.</span><span class="sxs-lookup"><span data-stu-id="cfca7-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="cfca7-155">Redes</span><span class="sxs-lookup"><span data-stu-id="cfca7-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="cfca7-156">No se puede reservar una dirección IP en un servicio en la nube con varias direcciones IP virtuales</span><span class="sxs-lookup"><span data-stu-id="cfca7-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="cfca7-157">En primer lugar, asegúrese de que la instancia de máquina virtual para la que está intentando reservar la dirección IP está activada.</span><span class="sxs-lookup"><span data-stu-id="cfca7-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="cfca7-158">En segundo lugar, asegúrese de que utiliza direcciones IP reservadas para las implementaciones de ensayo y de producción.</span><span class="sxs-lookup"><span data-stu-id="cfca7-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="cfca7-159">**No** cambie la configuración mientras se está actualizando la implementación.</span><span class="sxs-lookup"><span data-stu-id="cfca7-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="cfca7-160">Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="cfca7-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="cfca7-161">¿Cómo se usa el escritorio remoto con un NSG?</span><span class="sxs-lookup"><span data-stu-id="cfca7-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="cfca7-162">Agregue reglas al NSG que permitan el tráfico en los puertos **3389** y **20000**.</span><span class="sxs-lookup"><span data-stu-id="cfca7-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="cfca7-163">El Escritorio remoto usa el puerto **3389**.</span><span class="sxs-lookup"><span data-stu-id="cfca7-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="cfca7-164">Las instancias del servicio en la nube tienen la carga equilibrada, por lo que no se puede controlar directamente a qué instancia conectarse.</span><span class="sxs-lookup"><span data-stu-id="cfca7-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="cfca7-165">Los agentes *RemoteForwarder* y *RemoteAccess* administran el tráfico RDP y permiten al cliente enviar una cookie de RDP y especificar una instancia concreta a la que conectarse.</span><span class="sxs-lookup"><span data-stu-id="cfca7-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="cfca7-166">Los agentes *RemoteForwarder* y *RemoteAccess* requieren que ese puerto **20000*** se abra (y puede estar bloqueado en el caso de que tenga un NSG).</span><span class="sxs-lookup"><span data-stu-id="cfca7-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
