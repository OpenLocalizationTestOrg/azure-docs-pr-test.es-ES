---
title: "aaaConfiguring un Firewall de aplicación Web (WAFS) para el entorno del servicio de aplicaciones"
description: "Obtenga información acerca de cómo tooconfigure una aplicación web de firewall delante de su entorno de servicio de aplicación."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="0a07e-103">Configuración de un firewall de aplicaciones web (WAF) para entornos del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0a07e-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="0a07e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0a07e-104">Overview</span></span>
<span data-ttu-id="0a07e-105">Web firewalls de aplicación como hello [Barracuda WAFS para Azure](https://www.barracuda.com/programs/azure) que está disponible en hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ayuda a proteger las aplicaciones web mediante la inspección del tráfico de web entrantes tooblock SQL Inyecciones, Scripting entre sitios, cargas de malware & aplicación DDoS y otros ataques.</span><span class="sxs-lookup"><span data-stu-id="0a07e-105">Web application firewalls like hello [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic tooblock SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="0a07e-106">También examina las respuestas de Hola de servidores web back-end de Hola de prevención de pérdida de datos (DLP).</span><span class="sxs-lookup"><span data-stu-id="0a07e-106">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="0a07e-107">Combina con aislamiento de Hola y ajustar la escala adicional proporcionada por entornos del servicio de aplicación, esto proporciona un entorno ideal toohost empresariales críticas web las aplicaciones que necesitan solicitudes malintencionadas de toowithstand y el tráfico de gran volumen.</span><span class="sxs-lookup"><span data-stu-id="0a07e-107">Combined with hello isolation and additional scaling provided by App Service Environments, this provides an ideal environment toohost business critical web applications that need toowithstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="0a07e-108">Configuración</span><span class="sxs-lookup"><span data-stu-id="0a07e-108">Setup</span></span>
<span data-ttu-id="0a07e-109">De este documento que se va a configurar nuestro entorno de servicio de aplicación detrás de carga varios equilibrada instancias de Barracuda WAFS para que únicamente el tráfico de hello WAFS puede llegar a Hola entorno del servicio de aplicaciones y no será accesible desde la red Perimetral de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a07e-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from hello WAF can reach hello App Service Environment and it will not be accessible from hello DMZ.</span></span> <span data-ttu-id="0a07e-110">También tenemos Azure Traffic Manager delante de nuestro saldo de tooload Barracuda WAFS instancias a través de centros de datos de Azure y regiones.</span><span class="sxs-lookup"><span data-stu-id="0a07e-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances tooload balance across Azure data centers and regions.</span></span> <span data-ttu-id="0a07e-111">Un diagrama de alto nivel del programa de instalación de hello sería lo que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0a07e-111">A high level diagram of hello setup would look like what is shown below.</span></span>

![Arquitectura][Architecture] 

> <span data-ttu-id="0a07e-113">Nota: con la introducción de Hola de [ILB compatibilidad con el entorno del servicio de aplicación](app-service-environment-with-internal-load-balancer.md), puede configurar toobe Hola ASE inaccesible desde la red Perimetral de Hola y solo puede red privada toohello disponible.</span><span class="sxs-lookup"><span data-stu-id="0a07e-113">Note: With hello introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure hello ASE toobe inaccessible from hello DMZ and only be available toohello private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="0a07e-114">Configuración del entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0a07e-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="0a07e-115">tooconfigure un entorno de servicio de aplicaciones, consulte demasiado[nuestra documentación](app-service-web-how-to-create-an-app-service-environment.md) en asunto Hola.</span><span class="sxs-lookup"><span data-stu-id="0a07e-115">tooconfigure an App Service Environment refer too[our documentation](app-service-web-how-to-create-an-app-service-environment.md) on hello subject.</span></span> <span data-ttu-id="0a07e-116">Una vez que tenga un entorno de servicio de aplicación creado, puede crear [aplicaciones Web](app-service-web-overview.md), [aplicaciones de API](../app-service-api/app-service-api-apps-why-best-platform.md) y [aplicaciones móviles](../app-service-mobile/app-service-mobile-value-prop.md) en este entorno que se protegerán detrás de hello WAFS se configurar en la siguiente sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a07e-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind hello WAF we configure in hello next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="0a07e-117">Configuración del servicio en la nube Barracuda WAF</span><span class="sxs-lookup"><span data-stu-id="0a07e-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="0a07e-118">Barracuda tiene un [artículo detallado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre la implementación de su WAF en una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="0a07e-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="0a07e-119">Pero dado que se desea redundancia y no presentan un único punto de error, desea toodeploy al menos 2 WAFS en la instancia máquinas virtuales a Hola mismo servicio en la nube al seguir estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="0a07e-119">But because we want redundancy and not introduce a single point of failure, you want toodeploy at least 2 WAF instance VMs into hello same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-toocloud-service"></a><span data-ttu-id="0a07e-120">Agregar puntos de conexión tooCloud servicio</span><span class="sxs-lookup"><span data-stu-id="0a07e-120">Adding Endpoints tooCloud Service</span></span>
<span data-ttu-id="0a07e-121">Una vez que tiene 2 o más VM WAFS instancias de servicio en la nube puede usar hello [portal de Azure](https://portal.azure.com/) tooadd extremos HTTP y HTTPS que se usan en la aplicación como se muestra en la imagen de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="0a07e-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use hello [Azure portal](https://portal.azure.com/) tooadd HTTP and HTTPS endpoints that are used by your application as shown in hello image below.</span></span>

![Configuración de extremos][ConfigureEndpoint]

<span data-ttu-id="0a07e-123">Si las aplicaciones utilizan otros puntos de conexión, asegúrese de tooadd seguro también esos lista toothis.</span><span class="sxs-lookup"><span data-stu-id="0a07e-123">If your applications use other endpoints, make sure tooadd those toothis list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="0a07e-124">Configuración de Barracuda WAF mediante su portal de administración</span><span class="sxs-lookup"><span data-stu-id="0a07e-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="0a07e-125">Barracuda WAF utiliza el puerto TCP 8000 para la configuración a través de su portal de administración.</span><span class="sxs-lookup"><span data-stu-id="0a07e-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="0a07e-126">Puesto que tenemos varias instancias de las máquinas virtuales de hello WAFS necesitará toorepeat Hola siguientes pasos para cada instancia de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0a07e-126">Since we have multiple instances of hello WAF VMs you will need toorepeat hello steps here for each VM instance.</span></span> 

> <span data-ttu-id="0a07e-127">Nota: Una vez que haya terminado con la configuración de WAFS, quitar punto de conexión TCP/8000 Hola de su tookeep de máquinas virtuales WAFS su WAFS segura.</span><span class="sxs-lookup"><span data-stu-id="0a07e-127">Note: Once you are done with WAF configuration, remove hello TCP/8000 endpoint from all your WAF VMs tookeep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="0a07e-128">Agregar extremo de administración de hello tal como se muestra en la imagen de hello siguiente tooconfigure su WAFS Barracuda.</span><span class="sxs-lookup"><span data-stu-id="0a07e-128">Add hello management endpoint as shown in hello image below tooconfigure your Barracuda WAF.</span></span>

![Incorporación de extremos de administración][AddManagementEndpoint]

<span data-ttu-id="0a07e-130">Usar un punto de conexión de explorador toobrowse toohello administración en su servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="0a07e-130">Use a browser toobrowse toohello management endpoint on your Cloud Service.</span></span> <span data-ttu-id="0a07e-131">Si su servicio en la nube se denomina test.cloudapp.net, podría tener acceso a este punto de conexión examinando toohttp://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="0a07e-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing toohttp://test.cloudapp.net:8000.</span></span> <span data-ttu-id="0a07e-132">Debería ver una página de inicio de sesión como las siguientes que puede iniciar sesión con credenciales especificadas en fase de la instalación de hello WAFS VM.</span><span class="sxs-lookup"><span data-stu-id="0a07e-132">You should see a login page like below that you can login using credentials you specified in hello WAF VM setup phase.</span></span>

![Página de inicio de sesión de administración][ManagementLoginPage]

<span data-ttu-id="0a07e-134">Una vez inicio de sesión debería ver un panel como Hola uno en la imagen de hello siguiente presentará estadísticas básicas sobre Hola protección WAFS.</span><span class="sxs-lookup"><span data-stu-id="0a07e-134">Once you login you should see a dashboard as hello one in hello image below that will present basic statistics about hello WAF protection.</span></span>

![Panel de administración][ManagementDashboard]

<span data-ttu-id="0a07e-136">Al hacer clic en la ficha de servicios de hello le permitirá configurar su WAFS para los servicios que se protege.</span><span class="sxs-lookup"><span data-stu-id="0a07e-136">Clicking on hello Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="0a07e-137">Para obtener más información sobre cómo configurar Barracuda WAF, puede consultar [su documentación](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="0a07e-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="0a07e-138">En el ejemplo de Hola por debajo de una aplicación Web de Azure se ha configurado que sirve al tráfico de HTTP y HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0a07e-138">In hello example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Administración de agregar servicios][ManagementAddServices]

> <span data-ttu-id="0a07e-140">Nota: Según la configuración de las aplicaciones y qué características se utilizan en el entorno de servicio de aplicaciones, deberá tooforward tráfico para los puertos TCP que no sea el 80 y 443, por ejemplo, si ha configurado SSL de IP para una aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="0a07e-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need tooforward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="0a07e-141">Para obtener una lista de puertos de red usados en entornos del servicio de aplicación, consulte demasiado[documentación de controlar el tráfico de entrada](app-service-app-service-environment-control-inbound-traffic.md) sección de puertos de red.</span><span class="sxs-lookup"><span data-stu-id="0a07e-141">For a list of network ports used in App Service Environments, please refer too[Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="0a07e-142">Configuración del Administrador de tráfico de Microsoft Azure (OPCIONAL)</span><span class="sxs-lookup"><span data-stu-id="0a07e-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="0a07e-143">Si la aplicación está disponible en varias regiones, desearía saldo tooload les detrás de [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a07e-143">If your application is available in multiple regions, then you would want tooload balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="0a07e-144">toodo para que pueda agregar un punto de conexión en hello [portal de Azure clásico](https://manage.azure.com) con nombre de servicio en la nube de Hola para su WAFS perfil de Traffic Manager Hola tal y como se muestra en la imagen de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="0a07e-144">toodo so you can add an endpoint in hello [Azure classic portal](https://manage.azure.com) using hello Cloud Service name for your WAF in hello Traffic Manager profile as shown in hello image below.</span></span> 

![Extremo del Administrador de tráfico][TrafficManagerEndpoint]

<span data-ttu-id="0a07e-146">Si la aplicación requiere autenticación, asegúrese de que tiene algún recurso que no requiere la autenticación para Traffic Manager tooping para disponibilidad hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a07e-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager tooping for hello availability of your application.</span></span> <span data-ttu-id="0a07e-147">Puede configurar la dirección URL de hello en hello sección de configuración en hello [portal de Azure clásico](https://manage.azure.com) tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0a07e-147">You can configure hello URL under hello Configure section on hello [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configuración del Administrador de tráfico][ConfigureTrafficManager]

<span data-ttu-id="0a07e-149">tooforward Hola Traffic Manager comandos ping de la aplicación de tooyour WAFS, necesita las traducciones del sitio Web de toosetup en la aplicación de tooyour de Barracuda WAFS tooforward tráfico como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a07e-149">tooforward hello Traffic Manager pings from your WAF tooyour application, you need toosetup Website Translations on your Barracuda WAF tooforward traffic tooyour application as shown in hello example below.</span></span>

![Traducciones de sitios web][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="0a07e-151">Proteger el tráfico tooApp servicio entorno usando red seguridad grupos (NSG)</span><span class="sxs-lookup"><span data-stu-id="0a07e-151">Securing Traffic tooApp Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="0a07e-152">Siga hello [documentación de controlar el tráfico de entrada](app-service-app-service-environment-control-inbound-traffic.md) para obtener más información sobre la restricción de tráfico tooyour entono de hello WAFS solo por dirección de hello VIP del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="0a07e-152">Follow hello [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic tooyour App Service Environment from hello WAF only by using hello VIP address of your Cloud Service.</span></span> <span data-ttu-id="0a07e-153">A continuación se muestra un comando PowerShell de ejemplo para realizar esta tarea para el puerto TCP 80.</span><span class="sxs-lookup"><span data-stu-id="0a07e-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="0a07e-154">Reemplace hello SourceAddressPrefix por dirección de IP Virtual (VIP) del servicio de nube de su WAFS Hola.</span><span class="sxs-lookup"><span data-stu-id="0a07e-154">Replace hello SourceAddressPrefix with hello Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="0a07e-155">Nota: Hola VIP de servicio en la nube cambiará al eliminar y volver a crear Hola servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="0a07e-155">Note: hello VIP of your Cloud Service will change when you delete and re-create hello Cloud Service.</span></span> <span data-ttu-id="0a07e-156">Asegúrese de que dirección IP de tooupdate hello en el grupo de recursos de red de hello cuando lo haga.</span><span class="sxs-lookup"><span data-stu-id="0a07e-156">Make sure tooupdate hello IP address in hello Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
