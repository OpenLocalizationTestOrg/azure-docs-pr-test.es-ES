---
title: "Configuración de un firewall de aplicaciones web (WAF) para entornos del Servicio de aplicaciones"
description: "Obtenga información sobre cómo configurar un firewall de aplicaciones web delante del entorno del Servicio de aplicaciones."
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
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="50501-103">Configuración de un firewall de aplicaciones web (WAF) para entornos del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="50501-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="50501-104">Información general</span><span class="sxs-lookup"><span data-stu-id="50501-104">Overview</span></span>
<span data-ttu-id="50501-105">Los firewalls de aplicaciones web como [Barracuda WAF para Azure](https://www.barracuda.com/programs/azure), que está disponible en [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ayuda a proteger las aplicaciones web mediante la inspección del tráfico web entrante para bloquear las inyecciones de código SQL, scripts de sitios, cargas de malware, DDoS de aplicaciones y otros ataques.</span><span class="sxs-lookup"><span data-stu-id="50501-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="50501-106">También examina las respuestas de los servidores web back-end para prevención de pérdida de datos (DLP).</span><span class="sxs-lookup"><span data-stu-id="50501-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="50501-107">Combinado con el aislamiento y la escala adicional proporcionados por los entornos del Servicio de aplicaciones, esto proporciona un entorno ideal para hospedar importantes aplicaciones web empresariales que deben soportar peticiones malintencionadas y tráfico de gran volumen.</span><span class="sxs-lookup"><span data-stu-id="50501-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="50501-108">Configuración</span><span class="sxs-lookup"><span data-stu-id="50501-108">Setup</span></span>
<span data-ttu-id="50501-109">Para este documento, configuraremos nuestro entorno del Servicio de aplicaciones detrás de varias instancias de equilibrio de carga de Barracuda WAF para que únicamente el tráfico del WAF pueda ponerse en contacto con el entorno del Servicio de aplicaciones, y no se podrá obtener acceso desde la red perimetral.</span><span class="sxs-lookup"><span data-stu-id="50501-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="50501-110">También dispondremos del Administrador de tráfico de Azure delante de nuestras instancias de Barracuda WAF para equilibrar la carga entre las regiones y los centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="50501-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="50501-111">Un diagrama de alto nivel del programa de instalación tendría el aspecto que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="50501-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Architecture][Architecture] 

> <span data-ttu-id="50501-113">Nota: con la introducción de [la compatibilidad de ILB con el entorno de App Service](app-service-environment-with-internal-load-balancer.md), puede configurar el ASE para que no pueda accederse desde la red perimetral y solo está disponible en la red privada.</span><span class="sxs-lookup"><span data-stu-id="50501-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="50501-114">Configuración del entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="50501-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="50501-115">Para configurar un entorno del Servicio de aplicaciones, consulte [nuestra documentación](app-service-web-how-to-create-an-app-service-environment.md) sobre el tema.</span><span class="sxs-lookup"><span data-stu-id="50501-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="50501-116">Después de crear una instancia de App Service Environment, puede crear en él [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) y [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) que se protegerán detrás del WAF que se configurará en la próxima sección.</span><span class="sxs-lookup"><span data-stu-id="50501-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="50501-117">Configuración del servicio en la nube Barracuda WAF</span><span class="sxs-lookup"><span data-stu-id="50501-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="50501-118">Barracuda tiene un [artículo detallado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre la implementación de su WAF en una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="50501-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="50501-119">No obstante, habida cuenta de que queremos redundancia y no introducir un único punto de error, hay que implementar al menos dos máquinas virtuales de la instancia de WAF en el mismo servicio en la nube al seguir estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="50501-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="50501-120">Incorporación de extremos al servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="50501-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="50501-121">Cuando ya tenga dos o más instancias de máquina virtual de WAF en el servicio en la nube, puede usar el [Portal de Azure](https://portal.azure.com/) para agregar puntos de conexión HTTP y HTTPS que la aplicación use, como se muestra en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="50501-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![Configuración de extremos][ConfigureEndpoint]

<span data-ttu-id="50501-123">Si las aplicaciones utilizan otros extremos, asegúrese de agregarlos a esta lista.</span><span class="sxs-lookup"><span data-stu-id="50501-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="50501-124">Configuración de Barracuda WAF mediante su portal de administración</span><span class="sxs-lookup"><span data-stu-id="50501-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="50501-125">Barracuda WAF utiliza el puerto TCP 8000 para la configuración a través de su portal de administración.</span><span class="sxs-lookup"><span data-stu-id="50501-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="50501-126">Como tenemos varias instancias de máquinas virtuales de WAF, tendrá que repetir los pasos siguientes para cada instancia de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="50501-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="50501-127">Nota: Una vez que haya terminado con la configuración de WAF, quite el extremo TCP/8000 de todas las máquinas virtuales de WAF para preservar la seguridad del WAF.</span><span class="sxs-lookup"><span data-stu-id="50501-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="50501-128">Agregue el extremo de administración como se muestra en la imagen siguiente para configurar Barracuda WAF.</span><span class="sxs-lookup"><span data-stu-id="50501-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![Incorporación de extremos de administración][AddManagementEndpoint]

<span data-ttu-id="50501-130">Utilice un explorador para examinar el extremo de administración en el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="50501-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="50501-131">Si el servicio en la nube se llama test.cloudapp.net, para acceder a este punto de conexión sería preciso dirigirse a http://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="50501-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="50501-132">Debería ver una página de inicio de sesión como la siguiente en la que puede iniciar sesión con las credenciales especificadas en la fase de instalación de la máquina virtual de WAF.</span><span class="sxs-lookup"><span data-stu-id="50501-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![Página de inicio de sesión de administración][ManagementLoginPage]

<span data-ttu-id="50501-134">Tras iniciar sesión, debe aparecer un panel de información como el de la imagen siguiente que presentará estadísticas básicas sobre la protección de WAF.</span><span class="sxs-lookup"><span data-stu-id="50501-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![Panel de administración][ManagementDashboard]

<span data-ttu-id="50501-136">Al hacer clic en la pestaña Servicios, le permitirá configurar el WAF para los servicios que protege.</span><span class="sxs-lookup"><span data-stu-id="50501-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="50501-137">Para obtener más información sobre cómo configurar Barracuda WAF, puede consultar [su documentación](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="50501-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="50501-138">En el ejemplo siguiente, se ha configurado una aplicación web de Azure que atiende el tráfico en HTTP y HTTPS.</span><span class="sxs-lookup"><span data-stu-id="50501-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Administración de agregar servicios][ManagementAddServices]

> <span data-ttu-id="50501-140">Nota: Dependiendo de cómo se configuran las aplicaciones y qué características se utilizan en el entorno del Servicio de aplicaciones, deberá reenviar el tráfico para los puertos TCP distintos del 80 y el 443, por ejemplo, si ha configurado SSL de IP para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="50501-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="50501-141">Para obtener una lista de los puertos de red usados en entornos del Servicio de aplicaciones, vea la sección dedicada a los puertos de red en la [documentación del control del tráfico de entrada](app-service-app-service-environment-control-inbound-traffic.md) .</span><span class="sxs-lookup"><span data-stu-id="50501-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="50501-142">Configuración del Administrador de tráfico de Microsoft Azure (OPCIONAL)</span><span class="sxs-lookup"><span data-stu-id="50501-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="50501-143">Si la aplicación se encuentra disponible en varias regiones, debe equilibrar la carga entre ellas detrás del [Administrador de tráfico de Azure](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50501-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="50501-144">Para ello, puede agregar un punto de conexión en el [Portal de Azure clásico](https://manage.azure.com) con el nombre del servicio en la nube de su WAF en el perfil del Administrador de tráfico, como se muestra en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="50501-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![Extremo del Administrador de tráfico][TrafficManagerEndpoint]

<span data-ttu-id="50501-146">Si la aplicación requiere autenticación, asegúrese de que tiene algún recurso que no requiere ninguna autenticación para que el Administrador de tráfico haga ping para la disponibilidad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50501-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="50501-147">Puede configurar la dirección URL en la sección Configuración del [Portal de Azure clásico](https://manage.azure.com) , como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="50501-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configuración del Administrador de tráfico][ConfigureTrafficManager]

<span data-ttu-id="50501-149">Para reenviar los pings del Administrador de tráfico desde el WAF a la aplicación, debe configurar las traducciones de sitios web en Barracuda WAF para reenviar el tráfico a la aplicación, tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="50501-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![Traducciones de sitios web][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="50501-151">Protección del tráfico en el entorno del Servicio de aplicaciones mediante grupos de recursos de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="50501-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="50501-152">Vea la [documentación sobre el control del tráfico de entrada](app-service-app-service-environment-control-inbound-traffic.md) para obtener detalles sobre la restricción del tráfico en el entorno del Servicio de aplicaciones desde el WAF solo mediante la utilización de la dirección IP virtual del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="50501-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="50501-153">A continuación se muestra un comando PowerShell de ejemplo para realizar esta tarea para el puerto TCP 80.</span><span class="sxs-lookup"><span data-stu-id="50501-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="50501-154">Reemplace SourceAddressPrefix con la dirección IP virtual (VIP) del servicio en la nube del WAF.</span><span class="sxs-lookup"><span data-stu-id="50501-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="50501-155">Nota: La dirección VIP del servicio en la nube cambiará al eliminar y volver a crear el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="50501-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="50501-156">Asegúrese de actualizar la dirección IP en el grupo de recursos de red una vez hecho esto.</span><span class="sxs-lookup"><span data-stu-id="50501-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
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
