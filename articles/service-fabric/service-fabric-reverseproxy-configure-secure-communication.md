---
title: "aaaAzure Service Fabric invertir una comunicación segura proxy | Documentos de Microsoft"
description: "Configurar la comunicación segura de extremo a extremo de proxy inverso tooenable."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a><span data-ttu-id="a4ab2-103">Conectar el servicio seguro tooa con proxy inverso Hola</span><span class="sxs-lookup"><span data-stu-id="a4ab2-103">Connect tooa secure service with hello reverse proxy</span></span>

<span data-ttu-id="a4ab2-104">Este artículo explica cómo tooestablish conexión segura entre proxy inverso de Hola y servicios, lo que permite un canal seguro de tooend final.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-104">This article explains how tooestablish secure connection between hello reverse proxy and services, thus enabling an end tooend secure channel.</span></span>

<span data-ttu-id="a4ab2-105">Conectar servicios toosecure se admite solo una vez proxy inverso toolisten configurado en HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-105">Connecting toosecure services is supported only when reverse proxy is configured toolisten on HTTPS.</span></span> <span data-ttu-id="a4ab2-106">Resto del documento de Hola se da por supuesto que éste es el caso de hello.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-106">Rest of hello document assumes this is hello case.</span></span>
<span data-ttu-id="a4ab2-107">Consulte demasiado[proxy en Azure Service Fabric inverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) proxy inverso de hello tooconfigure en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-107">Refer too[Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a><span data-ttu-id="a4ab2-108">Establecimiento de conexión segura entre el proxy inverso de Hola y servicios</span><span class="sxs-lookup"><span data-stu-id="a4ab2-108">Secure connection establishment between hello reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-tooservices"></a><span data-ttu-id="a4ab2-109">Invertir tooservices de autenticación de proxy:</span><span class="sxs-lookup"><span data-stu-id="a4ab2-109">Reverse proxy authenticating tooservices:</span></span>
<span data-ttu-id="a4ab2-110">Hello proxy inverso identifica a sí mismo tooservices usando su certificado, especificada con ***reverseProxyCertificate*** propiedad Hola **clúster** [sección de tipo de recurso](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a4ab2-110">hello reverse proxy identifies itself tooservices using its certificate, specified with ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a4ab2-111">Los servicios pueden implementar Hola lógica tooverify Hola certificado de proxy inverso de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-111">Services can implement hello logic tooverify hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="a4ab2-112">Servicios de Hello pueden especificar detalles del certificado de cliente de hello aceptado como valores de configuración en el paquete de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-112">hello services can specify hello accepted client certificate details as configuration settings in hello configuration package.</span></span> <span data-ttu-id="a4ab2-113">Esto se puede leer en tiempo de ejecución y usó toovalidate Hola certificado presentado por el proxy inverso Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-113">This can be read at runtime and used toovalidate hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="a4ab2-114">Consulte demasiado[administrar parámetros de la aplicación](service-fabric-manage-multiple-environment-app-configuration.md) valores de configuración de tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-114">Refer too[Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a><span data-ttu-id="a4ab2-115">Invertir la verificación de identidad del servicio de hello mediante certificado Hola presentado por el servicio de Hola de proxy:</span><span class="sxs-lookup"><span data-stu-id="a4ab2-115">Reverse proxy verifying hello service's identity via hello certificate presented by hello service:</span></span>
<span data-ttu-id="a4ab2-116">tooperform validación de certificados de servidor de certificados de hello presentado por servicios de hello, proxy inverso es compatible con una de las siguientes opciones de hello: ninguno, ServiceCommonNameAndIssuer y ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-116">tooperform server certificate validation of hello certificates presented by hello services, reverse proxy supports one of hello following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="a4ab2-117">tooselect una de estas tres opciones, especifique hello **ApplicationCertificateValidationPolicy** de sección de parámetros de Hola de elemento de ApplicationGateway/Http bajo [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="a4ab2-117">tooselect one of these three options, specify hello **ApplicationCertificateValidationPolicy** in hello parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="a4ab2-118">Consulte toohello siguiente sección para obtener más información sobre la configuración adicional para cada una de estas opciones.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-118">Refer toohello next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="a4ab2-119">Opciones de validación de certificados de servicio</span><span class="sxs-lookup"><span data-stu-id="a4ab2-119">Service certificate validation options</span></span> 

- <span data-ttu-id="a4ab2-120">**Ninguno**: proxy inverso omite la comprobación del certificado de proxy de servicio de Hola y establece la conexión segura de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-120">**None**: Reverse proxy skips verification of hello proxied service certificate and establishes hello secure connection.</span></span> <span data-ttu-id="a4ab2-121">Se trata del comportamiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-121">This is hello default behavior.</span></span>
<span data-ttu-id="a4ab2-122">Especificar hello **ApplicationCertificateValidationPolicy** con valor **ninguno** en la sección de parámetros de hello del elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-122">Specify hello **ApplicationCertificateValidationPolicy** with value **None** in hello parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="a4ab2-123">**ServiceCommonNameAndIssuer**: proxy inverso comprueba el certificado de hello presentado por servicio de hello en función de nombre común del certificado y la huella digital del emisor inmediato: especificar hello **ApplicationCertificateValidationPolicy**  con valor **ServiceCommonNameAndIssuer** en la sección de parámetros de hello del elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies hello certificate presented by hello service based on certificate's common name and immediate issuer's thumbprint: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in hello parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="a4ab2-124">lista de hello toospecify de nombre común de servicio y las huellas digitales de emisor, agregue un **ApplicationGateway/Http/ServiceCommonNameAndIssuer** elemento bajo fabricSettings, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-124">toospecify hello list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="a4ab2-125">En el elemento de matriz de parámetros de hello, pueden agregarse varios pares de huella digital de emisor y nombre común del certificado.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-125">Multiple certificate common name and issuer thumbprint pairs can be added in hello parameters array element.</span></span> 

<span data-ttu-id="a4ab2-126">Si está conectando proxy inverso de punto de conexión de hello toopresents un certificado que es común huella digital del emisor y el nombre coincide con alguno de los valores de hello especificados aquí, se establece el canal SSL.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-126">If hello endpoint reverse proxy is connecting toopresents a certificate who's common name and  issuer thumbprint matches any of hello values specified here, SSL channel is established.</span></span> <span data-ttu-id="a4ab2-127">En detalles del error toomatch Hola certificado, proxy inverso produce un error de solicitud del cliente de hello con un código de estado 502 (puerta de enlace incorrecta).</span><span class="sxs-lookup"><span data-stu-id="a4ab2-127">Upon failure toomatch hello certificate details, reverse proxy fails hello client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="a4ab2-128">Hola línea de estado HTTP también contendrá frase Hola "Certificado SSL no válido".</span><span class="sxs-lookup"><span data-stu-id="a4ab2-128">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span> 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- <span data-ttu-id="a4ab2-129">**ServiceCertificateThumbprints**: proxy inverso comprobará el certificado del servicio proxy de hello en función de su huella digital.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-129">**ServiceCertificateThumbprints**: Reverse proxy will verify hello proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="a4ab2-130">Puede elegir a toogo esta ruta cuando Hola servicios se configuran con certificados autofirmados: especificar hello **ApplicationCertificateValidationPolicy** con valor **ServiceCertificateThumbprints**en la sección de parámetros de hello del elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-130">You can choose toogo this route when hello services are configured with self signed certificates: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in hello parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="a4ab2-131">Especificar huellas digitales de hello con un **ServiceCertificateThumbprints** entrada en la sección de parámetros del elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-131">Also specify hello thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="a4ab2-132">Huellas digitales varios pueden especificarse como una lista separada por comas en el campo de valor de hello, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="a4ab2-132">Multiple thumbprints can be specified as a comma-separated list in hello value field, as shown below:</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="a4ab2-133">Si Hola huella del certificado de servidor hello aparece en esta entrada de configuración, proxy inverso éxito conexión de SSL de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-133">If hello thumbprint of hello server certificate is listed in this config entry, reverse proxy succeeds hello SSL connection.</span></span> <span data-ttu-id="a4ab2-134">En caso contrario, termina la conexión de Hola y se produce un error Hola solicitud del cliente con un 502 (puerta de enlace incorrecta).</span><span class="sxs-lookup"><span data-stu-id="a4ab2-134">Otherwise, it terminates hello connection and fails hello client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="a4ab2-135">Hola línea de estado HTTP también contendrá frase Hola "Certificado SSL no válido".</span><span class="sxs-lookup"><span data-stu-id="a4ab2-135">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="a4ab2-136">Lógica de selección de punto de conexión cuando los servicios exponen tanto puntos de conexión seguros como no seguros</span><span class="sxs-lookup"><span data-stu-id="a4ab2-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="a4ab2-137">Service Fabric admite la configuración de varios puntos de conexión para un servicio.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="a4ab2-138">Consulte [Especificación de los recursos en un manifiesto de servicio](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="a4ab2-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="a4ab2-139">Proxy inverso selecciona uno de hello extremos tooforward Hola solicitud en función de hello **ListenerName** parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-139">Reverse proxy selects one of hello endpoints tooforward hello request based on hello  **ListenerName** query parameter.</span></span> <span data-ttu-id="a4ab2-140">Si no se especifica, se puede elegir cualquier punto de conexión de lista de puntos de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-140">If this is not specified, it can pick any endpoint from hello endpoints list.</span></span> <span data-ttu-id="a4ab2-141">Ahora puede ser un punto de conexión HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="a4ab2-142">Puede haber escenarios o requisitos en la que desea toooperate de proxy inverso de hello en un "único modo seguro", es decir</span><span class="sxs-lookup"><span data-stu-id="a4ab2-142">There might be scenarios/requirements where you want hello reverse proxy toooperate in a "secure only mode", i.e</span></span> <span data-ttu-id="a4ab2-143">no desea Hola segura proxy inverso tooforward solicitudes toounsecured los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-143">you don't want hello secure reverse proxy tooforward requests toounsecured endpoints.</span></span> <span data-ttu-id="a4ab2-144">Esto puede lograrse mediante la especificación de hello **SecureOnlyMode** entrada de configuración con el valor **true** en la sección de parámetros de hello del elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-144">This can be achieved by specifying hello **SecureOnlyMode** configuration entry with value **true** in hello parameters section of ApplicationGateway/Http element.</span></span>   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> <span data-ttu-id="a4ab2-145">Cuando se trabaja en **SecureOnlyMode**, si el cliente ha especificado un **ListenerName** correspondiente punto de conexión de tooan HTTP(unsecured), proxy inverso produce un error en solicitud de hello con un código de estado 404 de HTTP (no encontrado).</span><span class="sxs-lookup"><span data-stu-id="a4ab2-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding tooan HTTP(unsecured) endpoint, reverse proxy fails hello request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a><span data-ttu-id="a4ab2-146">Configurar la autenticación de certificado de cliente a través de proxy inverso de Hola</span><span class="sxs-lookup"><span data-stu-id="a4ab2-146">Setting up client certificate authentication through hello reverse proxy</span></span>
<span data-ttu-id="a4ab2-147">Terminación SSL se produce en el proxy inverso de Hola y se pierden todos los datos del certificado de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-147">SSL termination happens at hello reverse proxy and all hello client certificate data is lost.</span></span> <span data-ttu-id="a4ab2-148">Para la autenticación de certificado de cliente de hello servicios tooperform, establecer hello **ForwardClientCertificate** en la sección de parámetros de hello del elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-148">For hello services tooperform client certificate authentication, set hello **ForwardClientCertificate** setting in hello parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="a4ab2-149">Cuando **ForwardClientCertificate** se establece demasiado**false**, invertir la dirección proxy no se solicitará certificado de cliente de Hola durante su protocolo de enlace SSL con cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-149">When **ForwardClientCertificate** is set too**false**, reverse proxy will not request for hello client certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="a4ab2-150">Se trata del comportamiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-150">This is hello default behavior.</span></span>

2. <span data-ttu-id="a4ab2-151">Cuando **ForwardClientCertificate** se establece demasiado**true**, invertir las solicitudes de proxy para el certificado del cliente de Hola durante su protocolo de enlace SSL con cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-151">When **ForwardClientCertificate** is set too**true**, reverse proxy requests for hello client's certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="a4ab2-152">A continuación, reenvía cliente hello datos del certificado en un encabezado HTTP personalizado denominado **certificado de cliente X**.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-152">It will then forward hello client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="a4ab2-153">el valor del encabezado de Hello es la cadena de formato PEM Hola con codificación base64 del certificado del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-153">hello header value is hello base64 encoded PEM format string of hello client's certificate.</span></span> <span data-ttu-id="a4ab2-154">servicio Hola puede correctamente o no superado solicitud Hola con código de estado adecuado después de inspeccionar los datos del certificado Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-154">hello service can succeed/fail hello request with appropriate status code after inspecting hello certificate data.</span></span>
<span data-ttu-id="a4ab2-155">Si el cliente de hello no presenta un certificado, proxy inverso reenvía un encabezado vacío y deje que caso de hello servicio identificador hello.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-155">If hello client does not present a certificate, reverse proxy forwards an empty header and let hello service handle hello case.</span></span>

> <span data-ttu-id="a4ab2-156">El proxy inverso es un simple reenviador.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="a4ab2-157">No llevará a cabo ninguna validación de certificado del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-157">It will not perform any validation of hello client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a4ab2-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4ab2-158">Next steps</span></span>
* <span data-ttu-id="a4ab2-159">Consulte demasiado[configurar los servicios de proxy inverso tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) ejemplos de plantilla para el Administrador de recursos de Azure tooconfigure proxy inverso seguro con opciones de validación de certificados de servicio diferente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4ab2-159">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="a4ab2-160">Vea un ejemplo de comunicación HTTP entre los servicios de un [proyecto de ejemplo en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a4ab2-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="a4ab2-161">Llamadas a procedimiento remoto con la comunicación remota de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a4ab2-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="a4ab2-162">API web que usa OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a4ab2-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="a4ab2-163">Administración de certificados del clúster</span><span class="sxs-lookup"><span data-stu-id="a4ab2-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
