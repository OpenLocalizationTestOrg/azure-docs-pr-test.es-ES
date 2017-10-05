---
title: Trabajo con servidores proxy locales existentes y Azure AD | Microsoft Docs
description: "Se explica cómo trabajar con servidores proxy locales existentes."
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="2129d-103">Trabajo con servidores proxy locales existentes</span><span class="sxs-lookup"><span data-stu-id="2129d-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="2129d-104">En este artículo se explica cómo configurar conectores del proxy de aplicación de Azure Active Directory (Azure AD) para que funcionen con servidores proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="2129d-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="2129d-105">Está destinado a clientes con entornos de red que tienen servidores proxy en la actualidad.</span><span class="sxs-lookup"><span data-stu-id="2129d-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="2129d-106">Empezaremos examinando estos escenarios de implementación principales:</span><span class="sxs-lookup"><span data-stu-id="2129d-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="2129d-107">Configuración de conectores para omitir los proxy de salida locales.</span><span class="sxs-lookup"><span data-stu-id="2129d-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="2129d-108">Configuración de conectores para usar un proxy de salida para obtener acceso al Proxy de aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2129d-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="2129d-109">Para más información sobre cómo funcionan los conectores, consulte [Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="2129d-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="2129d-110">Configuración del proxy de salida</span><span class="sxs-lookup"><span data-stu-id="2129d-110">Configure the outbound proxy</span></span>

<span data-ttu-id="2129d-111">Si tiene un proxy de salida en su entorno, use una cuenta con permisos adecuados para configurar al proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="2129d-111">If you have an outbound proxy in your environment, use an account with appropriate permissions to configure the outbound proxy.</span></span> <span data-ttu-id="2129d-112">Puesto que el programa de instalación se ejecuta en el contexto del usuario que lleva a cabo la instalación, puede comprobar la configuración mediante Microsoft Edge u otro explorador de Internet.</span><span class="sxs-lookup"><span data-stu-id="2129d-112">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="2129d-113">Para configurar el proxy en Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="2129d-113">To configure the proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="2129d-114">Vaya a **Configuración** > **Ver configuración avanzada** > **Abrir la configuración de proxy** > **Configuración manual del proxy**.</span><span class="sxs-lookup"><span data-stu-id="2129d-114">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="2129d-115">Establezca **Utilizar un servidor proxy** en **Activado**, active la casilla **No usar el servidor proxy para direcciones locales (intranet)** y cambie la dirección y el puerto para reflejar su servidor proxy local.</span><span class="sxs-lookup"><span data-stu-id="2129d-115">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="2129d-116">Rellene la configuración del proxy necesaria.</span><span class="sxs-lookup"><span data-stu-id="2129d-116">Fill in the necessary proxy settings.</span></span>

   ![Cuadro de diálogo de configuración del proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="2129d-118">Omisión de servidores proxy de salida</span><span class="sxs-lookup"><span data-stu-id="2129d-118">Bypass outbound proxies</span></span>

<span data-ttu-id="2129d-119">Los conectores tienen componentes del sistema operativo subyacentes que realizan solicitudes salientes.</span><span class="sxs-lookup"><span data-stu-id="2129d-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="2129d-120">Estos componentes intentan automáticamente encontrar un servidor proxy en la red.</span><span class="sxs-lookup"><span data-stu-id="2129d-120">These components automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="2129d-121">Usan la detección automática de proxy web, si está habilitada en el entorno.</span><span class="sxs-lookup"><span data-stu-id="2129d-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="2129d-122">Los componentes del sistema operativo intentan localizar un servidor proxy llevando a cabo una búsqueda de DNS para wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="2129d-122">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="2129d-123">Si esto se resuelve en DNS, se realiza una solicitud HTTP para la dirección IP para wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="2129d-123">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="2129d-124">Esta solicitud se convierte en el script de configuración de proxy en su entorno.</span><span class="sxs-lookup"><span data-stu-id="2129d-124">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="2129d-125">El conector lo usará para seleccionar un servidor proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="2129d-125">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="2129d-126">Sin embargo, es posible que el tráfico del conector no pase aún porque se requiera una configuración adicional en el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="2129d-126">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="2129d-127">Puede configurar el conector para omitir el proxy local a fin de garantizar que utilice conectividad directa a los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="2129d-127">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="2129d-128">Se recomienda este método (siempre que lo permita la directiva de red), ya que significa que tendrá una configuración menos que mantener.</span><span class="sxs-lookup"><span data-stu-id="2129d-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="2129d-129">Para deshabilitar el uso del proxy de salida para el conector, edite el archivo C:\Archivos de programa\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config y agregue la sección *system.net* que se muestra en este ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2129d-129">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

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
<span data-ttu-id="2129d-130">Para asegurarse de que el servicio de actualización de los conectores también omite el proxy, realice un cambio similar en el archivo ApplicationProxyConnectorUpdaterService.exe.config, que se encuentra en C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span><span class="sxs-lookup"><span data-stu-id="2129d-130">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="2129d-131">Asegúrese de realizar copias de los archivos originales por si fuera necesario revertir a los archivos .config predeterminados.</span><span class="sxs-lookup"><span data-stu-id="2129d-131">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="2129d-132">Uso del servidor proxy saliente</span><span class="sxs-lookup"><span data-stu-id="2129d-132">Use the outbound proxy server</span></span>

<span data-ttu-id="2129d-133">Algunos entornos requieren que todo el tráfico saliente atraviese sin excepciones un proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="2129d-133">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="2129d-134">Por lo tanto, no se contempla la opción de omitir el proxy.</span><span class="sxs-lookup"><span data-stu-id="2129d-134">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="2129d-135">Puede configurar el tráfico del conector de manera que vaya a través del proxy de salida, tal y como se muestra en el diagrama siguiente:</span><span class="sxs-lookup"><span data-stu-id="2129d-135">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![Configuración del tráfico del conector para pasar a través de un proxy de salida para acceder al Proxy de aplicación de Azure AD](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="2129d-137">Como solo se tiene tráfico saliente, no es necesario configurar el acceso entrante a través de los firewalls.</span><span class="sxs-lookup"><span data-stu-id="2129d-137">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="2129d-138">Paso 1: Configurar el conector y los servicios relacionados para que vayan a través del proxy de salida</span><span class="sxs-lookup"><span data-stu-id="2129d-138">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="2129d-139">Tal como se explicó anteriormente, si WPAD está habilitado en el entorno y se ha configurado correctamente, el conector detectará automáticamente el servidor del proxy de salida y tratará de usarlo.</span><span class="sxs-lookup"><span data-stu-id="2129d-139">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="2129d-140">Sin embargo, puede configurar explícitamente el conector para que vaya a través de un proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="2129d-140">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="2129d-141">Para ello, edite el archivo C:\Archivos de programa\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config y agregue la sección *system.net* que se muestra en este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="2129d-141">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="2129d-142">Cambie *proxyserver:8080* para que refleje el nombre o la dirección IP del servidor proxy local y el puerto en el que está escuchando.</span><span class="sxs-lookup"><span data-stu-id="2129d-142">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

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

<span data-ttu-id="2129d-143">A continuación, configure el servicio de actualización de los conectores para que use el proxy; para ello, haga un cambio similar en el archivo que se encuentra en C:\Archivos de programa\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="2129d-143">Next, configure the Connector Updater service to use the proxy by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="2129d-144">Paso 2: Configurar el proxy para permitir que pase el tráfico desde el conector y los servicios relacionados</span><span class="sxs-lookup"><span data-stu-id="2129d-144">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="2129d-145">Hay cuatro aspectos que se deben tener en cuenta en el servidor proxy saliente:</span><span class="sxs-lookup"><span data-stu-id="2129d-145">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="2129d-146">Las reglas de salida del proxy</span><span class="sxs-lookup"><span data-stu-id="2129d-146">Proxy outbound rules</span></span>
* <span data-ttu-id="2129d-147">La autenticación del proxy</span><span class="sxs-lookup"><span data-stu-id="2129d-147">Proxy authentication</span></span>
* <span data-ttu-id="2129d-148">Los puertos del proxy</span><span class="sxs-lookup"><span data-stu-id="2129d-148">Proxy ports</span></span>
* <span data-ttu-id="2129d-149">La inspección de SSL</span><span class="sxs-lookup"><span data-stu-id="2129d-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="2129d-150">Las reglas de salida del proxy</span><span class="sxs-lookup"><span data-stu-id="2129d-150">Proxy outbound rules</span></span>
<span data-ttu-id="2129d-151">Permita el acceso a los siguientes puntos de conexión para servicio de conector:</span><span class="sxs-lookup"><span data-stu-id="2129d-151">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="2129d-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="2129d-152">*.msappproxy.net</span></span>
* <span data-ttu-id="2129d-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="2129d-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="2129d-154">Para el registro inicial, permita el acceso a los siguientes puntos de conexión:</span><span class="sxs-lookup"><span data-stu-id="2129d-154">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="2129d-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="2129d-155">login.windows.net</span></span>
* <span data-ttu-id="2129d-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="2129d-156">login.microsoftonline.com</span></span>

<span data-ttu-id="2129d-157">Si no puede permitir la conectividad mediante el FQDN y debe especificar intervalos de direcciones IP en su lugar, use estas opciones:</span><span class="sxs-lookup"><span data-stu-id="2129d-157">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="2129d-158">Permitir el acceso de salida del conector a todos los destinos.</span><span class="sxs-lookup"><span data-stu-id="2129d-158">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="2129d-159">Permitir el acceso de salida del conector a los [intervalos IP del centro de datos de Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="2129d-159">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="2129d-160">El desafío de usar la lista de intervalos IP del centro de datos de Azure es que se actualiza semanalmente.</span><span class="sxs-lookup"><span data-stu-id="2129d-160">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="2129d-161">Es necesario colocar un proceso para garantizar que las reglas de acceso se actualizan en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="2129d-161">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="2129d-162">La autenticación del proxy</span><span class="sxs-lookup"><span data-stu-id="2129d-162">Proxy authentication</span></span>

<span data-ttu-id="2129d-163">Actualmente no se admite la autenticación del proxy.</span><span class="sxs-lookup"><span data-stu-id="2129d-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="2129d-164">Nuestra recomendación actual es permitir el acceso anónimo de conector a los destinos de Internet.</span><span class="sxs-lookup"><span data-stu-id="2129d-164">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="2129d-165">Los puertos del proxy</span><span class="sxs-lookup"><span data-stu-id="2129d-165">Proxy ports</span></span>

<span data-ttu-id="2129d-166">El conector realiza las conexiones salientes basadas en SSL con el método CONNECT.</span><span class="sxs-lookup"><span data-stu-id="2129d-166">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="2129d-167">Básicamente, este método configura un túnel a través del proxy de salida.</span><span class="sxs-lookup"><span data-stu-id="2129d-167">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="2129d-168">Configure el servidor proxy para permitir la tunelización a los puertos no estándar 443 y 80.</span><span class="sxs-lookup"><span data-stu-id="2129d-168">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="2129d-169">Service Bus, si se ejecuta a través de HTTPS, usa el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="2129d-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="2129d-170">Sin embargo, de forma predeterminada, Service Bus intenta crear conexiones TCP directas y recurrir a HTTPS solo si se produce un error en la conectividad directa.</span><span class="sxs-lookup"><span data-stu-id="2129d-170">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="2129d-171">Para asegurarse de que el tráfico de Service Bus también se envía a través del servidor proxy de salida, debe asegurarse de que el conector no puede conectar directamente con los servicios de Azure para los puertos 9350, 9352 y 5671.</span><span class="sxs-lookup"><span data-stu-id="2129d-171">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="2129d-172">La inspección de SSL</span><span class="sxs-lookup"><span data-stu-id="2129d-172">SSL inspection</span></span>
<span data-ttu-id="2129d-173">No utilice la inspección de SSL para el tráfico del conector, ya que le causa problemas.</span><span class="sxs-lookup"><span data-stu-id="2129d-173">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="2129d-174">Solución de problemas del proxy del conector y de conectividad del servicio</span><span class="sxs-lookup"><span data-stu-id="2129d-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="2129d-175">Ahora debería ver todo el tráfico pasando a través del proxy.</span><span class="sxs-lookup"><span data-stu-id="2129d-175">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="2129d-176">Si tiene problemas, la siguiente información debería ayudar.</span><span class="sxs-lookup"><span data-stu-id="2129d-176">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="2129d-177">La mejor manera de identificar y solucionar problemas de conectividad del conector es realizar una captura de red en el servicio de conector cuando se inicia.</span><span class="sxs-lookup"><span data-stu-id="2129d-177">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="2129d-178">Esta tarea puede resultar desalentadora; así pues, veamos algunas breves sugerencias sobre cómo capturar y filtrar seguimientos de red.</span><span class="sxs-lookup"><span data-stu-id="2129d-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="2129d-179">Puede usar la herramienta de supervisión que prefiera.</span><span class="sxs-lookup"><span data-stu-id="2129d-179">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="2129d-180">En este artículo, hemos usado la versión 3.4 del Monitor de red de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2129d-180">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="2129d-181">Puede [descargarlo de Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="2129d-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="2129d-182">Los ejemplos y los filtros que se utilizan en las siguientes secciones son específicos del Monitor de red, pero los principios se pueden aplicar a cualquier herramienta de análisis.</span><span class="sxs-lookup"><span data-stu-id="2129d-182">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="2129d-183">Realización de una captura mediante el Monitor de red</span><span class="sxs-lookup"><span data-stu-id="2129d-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="2129d-184">Para iniciar una captura:</span><span class="sxs-lookup"><span data-stu-id="2129d-184">To start a capture:</span></span>

1. <span data-ttu-id="2129d-185">Abra el Monitor de red y haga clic en **New Capture** (Nueva captura).</span><span class="sxs-lookup"><span data-stu-id="2129d-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="2129d-186">Haga clic en el botón **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="2129d-186">Click the **Start** button.</span></span>

   ![Ventana Monitor de red](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="2129d-188">Después de completar una captura, haga clic en el botón **Stop** (Detener) para finalizarla.</span><span class="sxs-lookup"><span data-stu-id="2129d-188">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="2129d-189">Toma de una captura del tráfico de conector</span><span class="sxs-lookup"><span data-stu-id="2129d-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="2129d-190">Para solucionar el problema inicial, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2129d-190">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="2129d-191">Desde services.msc, detenga el servicio de conector del Proxy de aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2129d-191">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="2129d-192">Inicie la captura de red.</span><span class="sxs-lookup"><span data-stu-id="2129d-192">Start the network capture.</span></span>
3. <span data-ttu-id="2129d-193">Inicie el servicio de conector del Proxy de aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2129d-193">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="2129d-194">Detenga la captura de red.</span><span class="sxs-lookup"><span data-stu-id="2129d-194">Stop the network capture.</span></span>

   ![Servicio de conector del Proxy de aplicación de Azure AD en services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="2129d-196">Consulta las solicitudes del conector al servidor proxy</span><span class="sxs-lookup"><span data-stu-id="2129d-196">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="2129d-197">Ahora que tiene una captura de red, puede filtrarla.</span><span class="sxs-lookup"><span data-stu-id="2129d-197">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="2129d-198">La clave para buscar el seguimiento es comprender cómo se filtra la captura.</span><span class="sxs-lookup"><span data-stu-id="2129d-198">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="2129d-199">Un filtro como el siguiente (donde 8080 es el puerto del servicio de proxy):</span><span class="sxs-lookup"><span data-stu-id="2129d-199">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="2129d-200">**(http.Request o http.Response) y tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="2129d-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="2129d-201">Si escribe este filtro en la ventana **Mostrar filtro** y selecciona **Aplicar**, se filtra el tráfico capturado en función del filtro.</span><span class="sxs-lookup"><span data-stu-id="2129d-201">If you enter this filter in the **Display Filter** window and select **Apply**, it filters the captured traffic based on the filter.</span></span>

<span data-ttu-id="2129d-202">El filtro anterior solo muestra las solicitudes y respuestas HTTP hacia o desde el puerto proxy.</span><span class="sxs-lookup"><span data-stu-id="2129d-202">The preceding filter shows just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="2129d-203">Para un inicio de conector en el que el conector está configurado para utilizar un servidor proxy, habría que utilizar un filtro similar a este:</span><span class="sxs-lookup"><span data-stu-id="2129d-203">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![Ejemplo de lista de las solicitudes y respuestas HTTP filtradas](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="2129d-205">Ahora está buscando específicamente las solicitudes de CONNECT que muestren que la comunicación con el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="2129d-205">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="2129d-206">Si se realiza correctamente, obtiene una respuesta HTTP OK (200).</span><span class="sxs-lookup"><span data-stu-id="2129d-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="2129d-207">Si ve otros códigos de respuesta, como 407 o 502, el proxy requiere autenticación o no permite el tráfico por algún otro motivo.</span><span class="sxs-lookup"><span data-stu-id="2129d-207">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="2129d-208">En este momento, póngase en contacto con el equipo de soporte técnico del servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="2129d-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="2129d-209">Identificación de los intentos de conexión de TCP con error</span><span class="sxs-lookup"><span data-stu-id="2129d-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="2129d-210">El otro escenario habitual que quizá le interese es cuando el conector está intentando conectarse directamente, pero no lo consigue.</span><span class="sxs-lookup"><span data-stu-id="2129d-210">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="2129d-211">Otro filtro del Monitor de red que le ayuda a identificar este problema fácilmente es:</span><span class="sxs-lookup"><span data-stu-id="2129d-211">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="2129d-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="2129d-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="2129d-213">Un paquete SYN es el primer paquete enviado para establecer una conexión TCP.</span><span class="sxs-lookup"><span data-stu-id="2129d-213">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="2129d-214">Si este paquete no devuelve ninguna respuesta, se intenta de nuevo el envío de SYN.</span><span class="sxs-lookup"><span data-stu-id="2129d-214">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="2129d-215">Puede utilizar el filtro anterior para ver las solicitudes de SYN retransmitidas.</span><span class="sxs-lookup"><span data-stu-id="2129d-215">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="2129d-216">A continuación, puede comprobar si estas solicitudes SYN corresponden a cualquier tráfico relacionado con el conector.</span><span class="sxs-lookup"><span data-stu-id="2129d-216">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="2129d-217">En el ejemplo siguiente se muestra un intento de conexión con error al puerto de Service Bus 9352:</span><span class="sxs-lookup"><span data-stu-id="2129d-217">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![Ejemplo de respuesta para un intento de conexión con errores](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="2129d-219">Si ve algo parecido a la respuesta anterior, el conector está intentando comunicarse directamente con el servicio Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2129d-219">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="2129d-220">Si el conector debería estar realizando conexiones directas a los servicios de Azure, esta respuesta es un claro indicio de que tiene un problema de red o firewall.</span><span class="sxs-lookup"><span data-stu-id="2129d-220">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="2129d-221">Si la configuración está establecida para usar un servidor proxy, esta respuesta puede significar que Service Bus está intentando realizar una conexión TCP directa antes de cambiar a intentar conectarse a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2129d-221">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="2129d-222">El análisis de seguimiento de red no está indicado para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="2129d-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="2129d-223">Sin embargo, puede ser una herramienta valiosa para obtener información rápida sobre lo que ocurre con la red.</span><span class="sxs-lookup"><span data-stu-id="2129d-223">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="2129d-224">Si sigue experimentando problemas de conectividad del conector, cree un vale para nuestro equipo de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="2129d-224">If you continue to struggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="2129d-225">El equipo puede ayudarle a solucionar otros problemas.</span><span class="sxs-lookup"><span data-stu-id="2129d-225">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="2129d-226">Para más información sobre cómo resolver errores del conector del Proxy de aplicación, consulte [Solucionar problemas de Proxy de aplicación](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="2129d-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2129d-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2129d-227">Next steps</span></span>

[<span data-ttu-id="2129d-228">Descripción de los conectores del Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2129d-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="2129d-229">
[Cómo instalar de forma silenciosa el conector de Proxy de aplicación de Azure AD](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="2129d-229">
[How to silently install the Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
