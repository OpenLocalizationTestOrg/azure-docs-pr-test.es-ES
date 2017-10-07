---
title: aaaWork existente local servidores proxy y Azure AD | Documentos de Microsoft
description: "Explica cómo toowork existente local servidores proxy."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="3aec9-103">Trabajo con servidores proxy locales existentes</span><span class="sxs-lookup"><span data-stu-id="3aec9-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="3aec9-104">Este artículo se explica cómo tooconfigure toowork de conectores de Proxy de aplicación de Azure Active Directory (Azure AD) con los servidores proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="3aec9-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="3aec9-105">Está destinado a clientes con entornos de red que tienen servidores proxy en la actualidad.</span><span class="sxs-lookup"><span data-stu-id="3aec9-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="3aec9-106">Empezaremos examinando estos escenarios de implementación principales:</span><span class="sxs-lookup"><span data-stu-id="3aec9-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="3aec9-107">Configure conectores toobypass el proxy de salida local.</span><span class="sxs-lookup"><span data-stu-id="3aec9-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="3aec9-108">Configure conectores toouse un Proxy de aplicación de Azure AD tooaccess de proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="3aec9-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="3aec9-109">Para más información sobre cómo funcionan los conectores, consulte [Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="3aec9-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="3aec9-110">Configurar el proxy de salida de hello</span><span class="sxs-lookup"><span data-stu-id="3aec9-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="3aec9-111">Si tiene un proxy de salida en su entorno, use una cuenta con proxy de salida de los permisos adecuados tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="3aec9-112">Como instalador de Hola se ejecuta en el contexto de Hola Hola del usuario de que está realizando la instalación de hello, puede comprobar configuración hello mediante Microsoft Edge u otro explorador de Internet.</span><span class="sxs-lookup"><span data-stu-id="3aec9-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="3aec9-113">configuración de proxy de hello tooconfigure con Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="3aec9-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="3aec9-114">Vaya demasiado**configuración** > **configuración de vista avanzada** > **abrir la configuración de Proxy** > **Manual de instalación del Proxy** .</span><span class="sxs-lookup"><span data-stu-id="3aec9-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="3aec9-115">Establecer **utilizar un servidor proxy** demasiado**en**, seleccione hello **no usar servidor proxy de Hola para direcciones locales (intranet)** casilla de verificación y, a continuación, tooreflect de dirección y el puerto de Hola de cambio el servidor proxy local.</span><span class="sxs-lookup"><span data-stu-id="3aec9-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="3aec9-116">Rellene la configuración de proxy necesaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-116">Fill in hello necessary proxy settings.</span></span>

   ![Cuadro de diálogo de configuración del proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="3aec9-118">Omisión de servidores proxy de salida</span><span class="sxs-lookup"><span data-stu-id="3aec9-118">Bypass outbound proxies</span></span>

<span data-ttu-id="3aec9-119">Los conectores tienen componentes del sistema operativo subyacentes que realizan solicitudes salientes.</span><span class="sxs-lookup"><span data-stu-id="3aec9-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="3aec9-120">Estos componentes intentan automáticamente toolocate un servidor proxy de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="3aec9-121">Usan la detección automática de Proxy Web (WPAD), si está habilitado en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="3aec9-122">componentes del sistema operativo Hola intenten toolocate un servidor proxy llevando a cabo una búsqueda de DNS para wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="3aec9-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="3aec9-123">Si esto se resuelve en DNS, una solicitud HTTP, a continuación, se realiza toohello IP dirección wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="3aec9-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="3aec9-124">Esta solicitud se convierte en el script de configuración de proxy de hello en su entorno.</span><span class="sxs-lookup"><span data-stu-id="3aec9-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="3aec9-125">Conector de Hello usa este tooselect script un servidor proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="3aec9-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="3aec9-126">Sin embargo, tráfico de conector es posible que todavía no vaya a través, debido a una configuración adicionales necesaria en el proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="3aec9-127">Puede configurar Hola conector toobypass su tooensure de proxy local que usa dirigir conectividad toohello Azure servicios.</span><span class="sxs-lookup"><span data-stu-id="3aec9-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="3aec9-128">Se recomienda este enfoque (si lo permite la directiva de red para él), ya que significa que tiene una menor toomaintain de configuración.</span><span class="sxs-lookup"><span data-stu-id="3aec9-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="3aec9-129">toodisable uso de proxy de salida para conector de hello, Editar archivo C:\Program Files\Microsoft AAD aplicación Proxy Connector\ApplicationProxyConnectorService.exe.config de hello y agregue hello *system.net* sección se muestra en este ejemplo de código :</span><span class="sxs-lookup"><span data-stu-id="3aec9-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="3aec9-130">tooensure que el servicio de conector actualizador de hello también omite proxy hello, cree un archivo de ApplicationProxyConnectorUpdaterService.exe.config de toohello de cambio similar situado actualizador del conector del Proxy de aplicación C:\Program Files\Microsoft AAD.</span><span class="sxs-lookup"><span data-stu-id="3aec9-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="3aec9-131">Ser seguro toomake copias de archivos originales de hello, por si necesita archivos .config de toorevert toohello de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3aec9-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="3aec9-132">Utilizar un servidor proxy saliente Hola</span><span class="sxs-lookup"><span data-stu-id="3aec9-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="3aec9-133">Algunos entornos requieren que todos los toogo el tráfico saliente a través de un proxy de salida, sin excepción.</span><span class="sxs-lookup"><span data-stu-id="3aec9-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="3aec9-134">Como resultado, la omisión de proxy de hello no es una opción.</span><span class="sxs-lookup"><span data-stu-id="3aec9-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="3aec9-135">Puede configurar Hola conector tráfico toogo a través de proxy de salida de hello, como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="3aec9-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![Configuración de conector toogo de tráfico a través de un tooAzure de proxy de salida AD Proxy de aplicación](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="3aec9-137">Como resultado de tener solo el tráfico saliente, no hay ninguna necesidad de tooconfigure acceso a través de los firewalls de entrada.</span><span class="sxs-lookup"><span data-stu-id="3aec9-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="3aec9-138">Paso 1: Configurar el conector de Hola y relacionados con servicios toogo a través de proxy de salida de hello</span><span class="sxs-lookup"><span data-stu-id="3aec9-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="3aec9-139">Tal como se explicó anteriormente, si está habilitado en el entorno de Hola y configurada correctamente WPAD, conector Hola detecta automáticamente toouse de servidor y el intento de proxy de salida Hola se.</span><span class="sxs-lookup"><span data-stu-id="3aec9-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="3aec9-140">Sin embargo, puede configurar explícitamente Hola conector toogo a través de un proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="3aec9-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="3aec9-141">toodo por lo tanto, edite el C:\Program Files\Microsoft AAD aplicación Proxy Connector\ApplicationProxyConnectorService.exe.config hello y agregue hello *system.net* sección se muestra en este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="3aec9-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="3aec9-142">Cambio *proxyserver:8080* tooreflect el nombre del servidor proxy local o dirección IP, hello y el puerto que está escuchando en.</span><span class="sxs-lookup"><span data-stu-id="3aec9-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="3aec9-143">A continuación, configurar a proxy de Hola de hello actualizador del conector servicio toouse mediante la realización de un archivo de toohello cambio similar que se encuentra en C:\Program Files\Microsoft AAD aplicación Proxy conector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="3aec9-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="3aec9-144">Paso 2: Configurar el tráfico de tooallow de hello proxy del conector de Hola y servicios relacionados tooflow a través de</span><span class="sxs-lookup"><span data-stu-id="3aec9-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="3aec9-145">Hay cuatro tooconsider aspectos en el proxy de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="3aec9-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="3aec9-146">Las reglas de salida del proxy</span><span class="sxs-lookup"><span data-stu-id="3aec9-146">Proxy outbound rules</span></span>
* <span data-ttu-id="3aec9-147">La autenticación del proxy</span><span class="sxs-lookup"><span data-stu-id="3aec9-147">Proxy authentication</span></span>
* <span data-ttu-id="3aec9-148">Los puertos del proxy</span><span class="sxs-lookup"><span data-stu-id="3aec9-148">Proxy ports</span></span>
* <span data-ttu-id="3aec9-149">La inspección de SSL</span><span class="sxs-lookup"><span data-stu-id="3aec9-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="3aec9-150">Las reglas de salida del proxy</span><span class="sxs-lookup"><span data-stu-id="3aec9-150">Proxy outbound rules</span></span>
<span data-ttu-id="3aec9-151">Permitir toohello de acceso después de los puntos de conexión para el acceso del servicio de conector:</span><span class="sxs-lookup"><span data-stu-id="3aec9-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="3aec9-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="3aec9-152">*.msappproxy.net</span></span>
* <span data-ttu-id="3aec9-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3aec9-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="3aec9-154">Para el registro inicial, permitir toohello de acceso después de los puntos de conexión:</span><span class="sxs-lookup"><span data-stu-id="3aec9-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="3aec9-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="3aec9-155">login.windows.net</span></span>
* <span data-ttu-id="3aec9-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="3aec9-156">login.microsoftonline.com</span></span>

<span data-ttu-id="3aec9-157">Si no se permite una conectividad mediante el FQDN y necesita los intervalos IP toospecify en su lugar, utilice estas opciones:</span><span class="sxs-lookup"><span data-stu-id="3aec9-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="3aec9-158">Permitir el acceso de salida de conector de hello tooall destinos.</span><span class="sxs-lookup"><span data-stu-id="3aec9-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="3aec9-159">Permitir el acceso de salida de conector de hello demasiado[intervalos IP del centro de datos Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="3aec9-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="3aec9-160">desafío de Hello con el uso de la lista de Hola de intervalos IP de centro de datos de Azure es que se actualiza semanalmente.</span><span class="sxs-lookup"><span data-stu-id="3aec9-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="3aec9-161">Deberá tooput un proceso en tooensure lugar que las reglas de acceso se actualizan en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="3aec9-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="3aec9-162">La autenticación del proxy</span><span class="sxs-lookup"><span data-stu-id="3aec9-162">Proxy authentication</span></span>

<span data-ttu-id="3aec9-163">Actualmente no se admite la autenticación del proxy.</span><span class="sxs-lookup"><span data-stu-id="3aec9-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="3aec9-164">Nuestra recomendación actual es destinos de Internet toohello de tooallow Hola conector acceso anónimo.</span><span class="sxs-lookup"><span data-stu-id="3aec9-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="3aec9-165">Los puertos del proxy</span><span class="sxs-lookup"><span data-stu-id="3aec9-165">Proxy ports</span></span>

<span data-ttu-id="3aec9-166">conector Hola hace las conexiones SSL salientes mediante el método CONNECT de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="3aec9-167">Básicamente, este método establece un túnel a través de proxy de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="3aec9-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="3aec9-168">Configurar Hola proxy server tooallow túnel tooports 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="3aec9-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="3aec9-169">Service Bus, si se ejecuta a través de HTTPS, usa el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="3aec9-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="3aec9-170">Sin embargo, de forma predeterminada, Service Bus intentará establecer conexiones directas de TCP y vuelve tooHTTPS solo si se produce un error en la conexión directa.</span><span class="sxs-lookup"><span data-stu-id="3aec9-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="3aec9-171">tooensure que Hola tráfico también se envía a través de servidor proxy de salida de hello de Bus de servicio, asegúrese de que dicho conector hello no puede conectar directamente toohello servicios de Azure para los puertos 9350, 9352 y 5671.</span><span class="sxs-lookup"><span data-stu-id="3aec9-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="3aec9-172">La inspección de SSL</span><span class="sxs-lookup"><span data-stu-id="3aec9-172">SSL inspection</span></span>
<span data-ttu-id="3aec9-173">No utilice inspección de SSL para el tráfico de conector de hello, ya que causará problemas para el tráfico de conector de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="3aec9-174">Solución de problemas del proxy del conector y de conectividad del servicio</span><span class="sxs-lookup"><span data-stu-id="3aec9-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="3aec9-175">Ahora debería ver todo el tráfico que fluye a través de proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="3aec9-176">Si sigue teniendo problemas, debe hacer Hola siguiendo la información para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="3aec9-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="3aec9-177">Hola tooidentify de manera mejor y solucionar problemas de conectividad del conector de problemas es tootake una red de captura en el servicio de conector de hello al iniciar el servicio de conector de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="3aec9-178">Esta tarea puede resultar desalentadora; así pues, veamos algunas breves sugerencias sobre cómo capturar y filtrar seguimientos de red.</span><span class="sxs-lookup"><span data-stu-id="3aec9-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="3aec9-179">Puede usar Hola herramienta de su elección de supervisión.</span><span class="sxs-lookup"><span data-stu-id="3aec9-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="3aec9-180">Para fines de Hola de este artículo, hemos usado el Monitor de red 3.4 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3aec9-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="3aec9-181">Puede [descargarlo de Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="3aec9-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="3aec9-182">ejemplos de Hello y los filtros que se usan en las secciones siguientes de hello son específico tooNetwork Monitor, pero principios de hello pueden ser la herramienta de análisis de tooany aplicado.</span><span class="sxs-lookup"><span data-stu-id="3aec9-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="3aec9-183">Realización de una captura mediante el Monitor de red</span><span class="sxs-lookup"><span data-stu-id="3aec9-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="3aec9-184">toostart una captura:</span><span class="sxs-lookup"><span data-stu-id="3aec9-184">toostart a capture:</span></span>

1. <span data-ttu-id="3aec9-185">Abra el Monitor de red y haga clic en **New Capture** (Nueva captura).</span><span class="sxs-lookup"><span data-stu-id="3aec9-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="3aec9-186">Haga clic en hello **iniciar** botón.</span><span class="sxs-lookup"><span data-stu-id="3aec9-186">Click hello **Start** button.</span></span>

   ![Ventana Monitor de red](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="3aec9-188">Después de completar una captura, haga clic en hello **detener** tooend de botón.</span><span class="sxs-lookup"><span data-stu-id="3aec9-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="3aec9-189">Toma de una captura del tráfico de conector</span><span class="sxs-lookup"><span data-stu-id="3aec9-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="3aec9-190">Para solucionar el problema inicial, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3aec9-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="3aec9-191">Desde services.msc, detenga el servicio de conector del Proxy de aplicación de Azure AD de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="3aec9-192">Iniciar la captura de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-192">Start hello network capture.</span></span>
3. <span data-ttu-id="3aec9-193">Iniciar servicio de conector del Proxy de aplicación de Azure AD de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="3aec9-194">Detener la captura de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-194">Stop hello network capture.</span></span>

   ![Servicio de conector del Proxy de aplicación de Azure AD en services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="3aec9-196">Buscar en las solicitudes de Hola de servidor proxy de hello conector toohello</span><span class="sxs-lookup"><span data-stu-id="3aec9-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="3aec9-197">Ahora que tienes una captura de red, está listo toofilter lo.</span><span class="sxs-lookup"><span data-stu-id="3aec9-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="3aec9-198">Hola toolooking clave en el seguimiento de hello es entender cómo capturar toofilter Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="3aec9-199">Un filtro es el siguiente (donde 8080 es el puerto de servicio del proxy de hello):</span><span class="sxs-lookup"><span data-stu-id="3aec9-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="3aec9-200">**(http.Request o http.Response) y tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="3aec9-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="3aec9-201">Si escribe este filtro en hello **Mostrar filtro** ventana y seleccione **aplicar**, filtra el tráfico de hello capturado en función de filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="3aec9-202">Hello filtro anterior muestra solo Hola solicitudes y respuestas HTTP de puerto de proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="3aec9-203">Para un inicio de conector donde conector hello es toouse configurado un servidor proxy, filtro de hello mostraría algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="3aec9-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![Ejemplo de lista de las solicitudes y respuestas HTTP filtradas](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="3aec9-205">Está ahora específicamente buscando Hola que conectar solicita que muestran la comunicación con el servidor de proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aec9-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="3aec9-206">Si se realiza correctamente, obtiene una respuesta HTTP OK (200).</span><span class="sxs-lookup"><span data-stu-id="3aec9-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="3aec9-207">Si ve otros códigos de respuesta, como 407 o 502, proxy de hello es requerir la autenticación o no permitir el tráfico de Hola por algún otro motivo.</span><span class="sxs-lookup"><span data-stu-id="3aec9-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="3aec9-208">En este momento, póngase en contacto con el equipo de soporte técnico del servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="3aec9-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="3aec9-209">Identificación de los intentos de conexión de TCP con error</span><span class="sxs-lookup"><span data-stu-id="3aec9-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="3aec9-210">Hello otro escenario común que puede estar interesado resulta hello conector está tratando de tooconnect directamente, pero que se produzcan errores.</span><span class="sxs-lookup"><span data-stu-id="3aec9-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="3aec9-211">Otro filtro de Monitor de red que ayuda a tooeasily identificar este problema es:</span><span class="sxs-lookup"><span data-stu-id="3aec9-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="3aec9-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="3aec9-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="3aec9-213">Un paquete SYN es envía de hello primer paquete tooestablish una conexión TCP.</span><span class="sxs-lookup"><span data-stu-id="3aec9-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="3aec9-214">Si este paquete no devuelve una respuesta, se vuelve a intentar Hola SYN.</span><span class="sxs-lookup"><span data-stu-id="3aec9-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="3aec9-215">Puede usar Hola anterior filtro toosee las solicitudes de SYN retransmitidos.</span><span class="sxs-lookup"><span data-stu-id="3aec9-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="3aec9-216">A continuación, puede comprobar si estas solicitudes SYN corresponde tooany el tráfico relacionado con el conector.</span><span class="sxs-lookup"><span data-stu-id="3aec9-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="3aec9-217">Hello en el ejemplo siguiente se muestra un intento de conexión ha fallado puerto del Bus de tooService 9352:</span><span class="sxs-lookup"><span data-stu-id="3aec9-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![Ejemplo de respuesta para un intento de conexión con errores](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="3aec9-219">Si ve algo parecido a Hola anterior respuesta, conector Hola consiste en intentar toocommunicate directamente con hello service Bus de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="3aec9-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="3aec9-220">Si creas Hola conector toomake conexiones directas toohello Azure services, esta respuesta es una indicación clara de que haya un problema de red o firewall.</span><span class="sxs-lookup"><span data-stu-id="3aec9-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="3aec9-221">Si está configurado toouse un servidor proxy, esta respuesta podría significar que Service Bus intenta una conexión TCP directa antes de cambiar tooattempting una conexión a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3aec9-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="3aec9-222">El análisis de seguimiento de red no está indicado para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="3aec9-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="3aec9-223">Pero puede ser una valiosa herramienta tooget rápido más información sobre lo que ocurre con la red.</span><span class="sxs-lookup"><span data-stu-id="3aec9-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="3aec9-224">Si continúa toostruggle con problemas de conectividad del conector, crear un vale de nuestro equipo de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="3aec9-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="3aec9-225">equipo de Hello le puede ayudar a solucionar el problema más.</span><span class="sxs-lookup"><span data-stu-id="3aec9-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="3aec9-226">Para más información sobre cómo resolver errores del conector del Proxy de aplicación, consulte [Solucionar problemas de Proxy de aplicación](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="3aec9-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3aec9-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3aec9-227">Next steps</span></span>

[<span data-ttu-id="3aec9-228">Descripción de los conectores del Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3aec9-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="3aec9-229">
[¿Cómo toosilently instalar Hola conector del Proxy de aplicación de Azure AD](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="3aec9-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
