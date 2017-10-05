---
title: "Comunicación segura con proxy inverso de Azure Service Fabric | Microsoft Docs"
description: "Configure el proxy inverso para habilitar la comunicación segura de un extremo a otro."
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
ms.openlocfilehash: 568f9638c59282bcd7d3fae058a1588a889c22dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-secure-service-with-the-reverse-proxy"></a><span data-ttu-id="56118-103">Conexión a un servicio seguro con el proxy inverso</span><span class="sxs-lookup"><span data-stu-id="56118-103">Connect to a secure service with the reverse proxy</span></span>

<span data-ttu-id="56118-104">En este artículo se explica cómo establecer una conexión segura entre el proxy inverso y los servicios, lo que crea un canal seguro de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="56118-104">This article explains how to establish secure connection between the reverse proxy and services, thus enabling an end to end secure channel.</span></span>

<span data-ttu-id="56118-105">La conexión a servicios seguros solo se admite cuando se configura el proxy inverso para escuchar en HTTPS.</span><span class="sxs-lookup"><span data-stu-id="56118-105">Connecting to secure services is supported only when reverse proxy is configured to listen on HTTPS.</span></span> <span data-ttu-id="56118-106">En el resto del documento se da por supuesto que esto es así.</span><span class="sxs-lookup"><span data-stu-id="56118-106">Rest of the document assumes this is the case.</span></span>
<span data-ttu-id="56118-107">Consulte [Proxy inverso en Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) para configurar el proxy inverso en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="56118-107">Refer to [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) to configure the reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-the-reverse-proxy-and-services"></a><span data-ttu-id="56118-108">Establecimiento de una conexión segura entre el proxy inverso y los servicios</span><span class="sxs-lookup"><span data-stu-id="56118-108">Secure connection establishment between the reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-to-services"></a><span data-ttu-id="56118-109">Autenticación del proxy inverso con los servicios:</span><span class="sxs-lookup"><span data-stu-id="56118-109">Reverse proxy authenticating to services:</span></span>
<span data-ttu-id="56118-110">El proxy inverso se identifica a sí mismo ante los servicios mediante su certificado, especificado con la propiedad ***reverseProxyCertificate*** en la [sección de tipos de recursos](../azure-resource-manager/resource-group-authoring-templates.md) del **clúster**.</span><span class="sxs-lookup"><span data-stu-id="56118-110">The reverse proxy identifies itself to services using its certificate, specified with ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="56118-111">Los servicios pueden implementar la lógica para comprobar el certificado presentado por el proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="56118-111">Services can implement the logic to verify the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="56118-112">Los servicios pueden especificar los detalles del certificado de cliente aceptado como valores de configuración en el paquete de configuración.</span><span class="sxs-lookup"><span data-stu-id="56118-112">The services can specify the accepted client certificate details as configuration settings in the configuration package.</span></span> <span data-ttu-id="56118-113">Esto se puede leer en tiempo de ejecución y puede utilizarse para validar el certificado presentado por el proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="56118-113">This can be read at runtime and used to validate the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="56118-114">Consulte [Administración de los parámetros de la aplicación en varios entornos](service-fabric-manage-multiple-environment-app-configuration.md) para agregar los valores de configuración.</span><span class="sxs-lookup"><span data-stu-id="56118-114">Refer to [Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) to add the configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-the-services-identity-via-the-certificate-presented-by-the-service"></a><span data-ttu-id="56118-115">Comprobación por parte del proxy inverso de la identidad del servicio mediante el certificado presentado por el servicio:</span><span class="sxs-lookup"><span data-stu-id="56118-115">Reverse proxy verifying the service's identity via the certificate presented by the service:</span></span>
<span data-ttu-id="56118-116">Para realizar la validación de certificados de servidor de los certificados presentados por los servicios, el proxy inverso es compatible con una de las siguientes opciones: Ninguno, ServiceCommonNameAndIssuer y ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="56118-116">To perform server certificate validation of the certificates presented by the services, reverse proxy supports one of the following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="56118-117">Para seleccionar una de estas tres opciones, especifique el **ApplicationCertificateValidationPolicy** en la sección de parámetros del elemento ApplicationGateway/Http bajo [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="56118-117">To select one of these three options, specify the **ApplicationCertificateValidationPolicy** in the parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="56118-118">Consulte la sección siguiente para obtener más información sobre la configuración adicional para cada una de estas opciones.</span><span class="sxs-lookup"><span data-stu-id="56118-118">Refer to the next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="56118-119">Opciones de validación de certificados de servicio</span><span class="sxs-lookup"><span data-stu-id="56118-119">Service certificate validation options</span></span> 

- <span data-ttu-id="56118-120">**Ninguno**: el proxy inverso omite la comprobación del certificado de los servicios con proxy y establece la conexión segura.</span><span class="sxs-lookup"><span data-stu-id="56118-120">**None**: Reverse proxy skips verification of the proxied service certificate and establishes the secure connection.</span></span> <span data-ttu-id="56118-121">Este es el comportamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="56118-121">This is the default behavior.</span></span>
<span data-ttu-id="56118-122">Especifique **ApplicationCertificateValidationPolicy** con el valor **Ninguno** en la sección de parámetros del elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="56118-122">Specify the **ApplicationCertificateValidationPolicy** with value **None** in the parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="56118-123">**ServiceCommonNameAndIssuer**: el proxy inverso comprueba que el certificado presentado por el servicio basándose en el nombre común del certificado y la huella digital del emisor inmediato. Para ello, especifique **ApplicationCertificateValidationPolicy** con valor **ServiceCommonNameAndIssuer** en la sección de parámetros del elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="56118-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies the certificate presented by the service based on certificate's common name and immediate issuer's thumbprint: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="56118-124">Para especificar la lista de nombres comunes de servicio y huellas digitales de emisor, agregue un elemento **ApplicationGateway/Http/ServiceCommonNameAndIssuer** bajo fabricSettings, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="56118-124">To specify the list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="56118-125">Pueden agregarse varios pares de huella digital de emisor y nombre común de certificado en el elemento de matriz de parámetros.</span><span class="sxs-lookup"><span data-stu-id="56118-125">Multiple certificate common name and issuer thumbprint pairs can be added in the parameters array element.</span></span> 

<span data-ttu-id="56118-126">Si el proxy inverso de punto de conexión al que se está conectando presenta un certificado cuya huella digital de emisor y nombre común coincide con cualquiera de los valores especificados aquí, se establece el canal SSL.</span><span class="sxs-lookup"><span data-stu-id="56118-126">If the endpoint reverse proxy is connecting to presents a certificate who's common name and  issuer thumbprint matches any of the values specified here, SSL channel is established.</span></span> <span data-ttu-id="56118-127">Si no se puede realizar la coincidencia de los detalles del certificado, el proxy inverso produce un error en la solicitud del cliente con el código de estado 502 (Puerta de enlace incorrecta).</span><span class="sxs-lookup"><span data-stu-id="56118-127">Upon failure to match the certificate details, reverse proxy fails the client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="56118-128">La línea de estado HTTP también contendrá la frase "Certificado SSL no válido".</span><span class="sxs-lookup"><span data-stu-id="56118-128">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="56118-129">**ServiceCertificateThumbprints**: el proxy inverso comprobará el certificado de los servicios con proxy en función de su huella digital.</span><span class="sxs-lookup"><span data-stu-id="56118-129">**ServiceCertificateThumbprints**: Reverse proxy will verify the proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="56118-130">Puede elegir este camino cuando los servicios estén configurados con certificados autofirmados: especifique el **ApplicationCertificateValidationPolicy** con el valor **ServiceCertificateThumbprints** en la sección de parámetros del elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="56118-130">You can choose to go this route when the services are configured with self signed certificates: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="56118-131">Especifique también las huellas digitales con una entrada **ServiceCertificateThumbprints** en la sección de parámetros del elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="56118-131">Also specify the thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="56118-132">Pueden especificarse varias huellas digitales como una lista separada por comas en el campo de valor, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="56118-132">Multiple thumbprints can be specified as a comma-separated list in the value field, as shown below:</span></span>

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

<span data-ttu-id="56118-133">Si la huella digital del certificado del servidor se muestra en esta entrada de configuración, el proxy inverso realiza correctamente la conexión SSL.</span><span class="sxs-lookup"><span data-stu-id="56118-133">If the thumbprint of the server certificate is listed in this config entry, reverse proxy succeeds the SSL connection.</span></span> <span data-ttu-id="56118-134">En caso contrario, se termina la conexión y se produce un error en la solicitud del cliente con un 502 (Puerta de enlace incorrecta).</span><span class="sxs-lookup"><span data-stu-id="56118-134">Otherwise, it terminates the connection and fails the client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="56118-135">La línea de estado HTTP también contendrá la frase "Certificado SSL no válido".</span><span class="sxs-lookup"><span data-stu-id="56118-135">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="56118-136">Lógica de selección de punto de conexión cuando los servicios exponen tanto puntos de conexión seguros como no seguros</span><span class="sxs-lookup"><span data-stu-id="56118-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="56118-137">Service Fabric admite la configuración de varios puntos de conexión para un servicio.</span><span class="sxs-lookup"><span data-stu-id="56118-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="56118-138">Consulte [Especificación de los recursos en un manifiesto de servicio](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="56118-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="56118-139">El proxy inverso selecciona uno de los puntos de conexión al que reenviar la solicitud en función del parámetro de consulta **ListenerName**.</span><span class="sxs-lookup"><span data-stu-id="56118-139">Reverse proxy selects one of the endpoints to forward the request based on the  **ListenerName** query parameter.</span></span> <span data-ttu-id="56118-140">Si no se especifica, puede elegir cualquier punto de conexión de la lista de puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="56118-140">If this is not specified, it can pick any endpoint from the endpoints list.</span></span> <span data-ttu-id="56118-141">Ahora puede ser un punto de conexión HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="56118-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="56118-142">Puede haber escenarios o requisitos en los que desee que el proxy inverso funcione en un "modo solo seguro"; es decir,</span><span class="sxs-lookup"><span data-stu-id="56118-142">There might be scenarios/requirements where you want the reverse proxy to operate in a "secure only mode", i.e</span></span> <span data-ttu-id="56118-143">no desea que el proxy inverso seguro reenvíe solicitudes a los puntos de conexión no seguros.</span><span class="sxs-lookup"><span data-stu-id="56118-143">you don't want the secure reverse proxy to forward requests to unsecured endpoints.</span></span> <span data-ttu-id="56118-144">Esto puede lograrse mediante la especificación de la entrada de configuración **SecureOnlyMode** con el valor **true** en la sección de parámetros del elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="56118-144">This can be achieved by specifying the **SecureOnlyMode** configuration entry with value **true** in the parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="56118-145">Cuando se trabaja en **SecureOnlyMode**, si el cliente ha especificado un **ListenerName** correspondiente a un punto de conexión HTTP (no protegido), el proxy inverso produce un error en la solicitud con un código de estado HTTP 404 (No encontrado).</span><span class="sxs-lookup"><span data-stu-id="56118-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding to an HTTP(unsecured) endpoint, reverse proxy fails the request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-the-reverse-proxy"></a><span data-ttu-id="56118-146">Configuración de la autenticación de certificados de cliente mediante el proxy inverso</span><span class="sxs-lookup"><span data-stu-id="56118-146">Setting up client certificate authentication through the reverse proxy</span></span>
<span data-ttu-id="56118-147">Se produce la terminación SSL en el proxy inverso y se pierden todos los datos del certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="56118-147">SSL termination happens at the reverse proxy and all the client certificate data is lost.</span></span> <span data-ttu-id="56118-148">Para que los servicios autentiquen el certificado de cliente, establezca el valor **ForwardClientCertificate** en la sección de parámetros del elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="56118-148">For the services to perform client certificate authentication, set the **ForwardClientCertificate** setting in the parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="56118-149">Cuando **ForwardClientCertificate** está establecido en **false**, el proxy inverso no solicitará el certificado de cliente durante el protocolo de enlace SSL con el cliente.</span><span class="sxs-lookup"><span data-stu-id="56118-149">When **ForwardClientCertificate** is set to **false**, reverse proxy will not request for the client certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="56118-150">Este es el comportamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="56118-150">This is the default behavior.</span></span>

2. <span data-ttu-id="56118-151">Cuando **ForwardClientCertificate** está establecido en **true**, el proxy inverso solicita el certificado del cliente durante el protocolo de enlace SSL con el cliente.</span><span class="sxs-lookup"><span data-stu-id="56118-151">When **ForwardClientCertificate** is set to **true**, reverse proxy requests for the client's certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="56118-152">Luego, reenvía los datos del certificado de cliente en un encabezado HTTP personalizado denominado **X-Client-Certificate**.</span><span class="sxs-lookup"><span data-stu-id="56118-152">It will then forward the client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="56118-153">El valor del encabezado es la cadena en formato PEM con codificación base64 del certificado del cliente.</span><span class="sxs-lookup"><span data-stu-id="56118-153">The header value is the base64 encoded PEM format string of the client's certificate.</span></span> <span data-ttu-id="56118-154">El servicio puede completar correctamente la solicitud o no con el código de estado adecuado después de inspeccionar los datos del certificado.</span><span class="sxs-lookup"><span data-stu-id="56118-154">The service can succeed/fail the request with appropriate status code after inspecting the certificate data.</span></span>
<span data-ttu-id="56118-155">Si el cliente no presenta un certificado, el proxy inverso reenvía un encabezado vacío y deja que el servicio gestione el caso.</span><span class="sxs-lookup"><span data-stu-id="56118-155">If the client does not present a certificate, reverse proxy forwards an empty header and let the service handle the case.</span></span>

> <span data-ttu-id="56118-156">El proxy inverso es un simple reenviador.</span><span class="sxs-lookup"><span data-stu-id="56118-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="56118-157">No validará en modo alguno el certificado del cliente.</span><span class="sxs-lookup"><span data-stu-id="56118-157">It will not perform any validation of the client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="56118-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56118-158">Next steps</span></span>
* <span data-ttu-id="56118-159">Consulte [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) (Configuración del proxy inverso para conectarse a servicios seguros) para ver las muestras de plantillas de Azure Resource Manager y para configurar el proxy inverso seguro con diferentes opciones de validación de certificados de servicio.</span><span class="sxs-lookup"><span data-stu-id="56118-159">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="56118-160">Vea un ejemplo de comunicación HTTP entre los servicios de un [proyecto de ejemplo en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="56118-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="56118-161">Llamadas a procedimiento remoto con la comunicación remota de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="56118-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="56118-162">API web que usa OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="56118-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="56118-163">Administración de certificados del clúster</span><span class="sxs-lookup"><span data-stu-id="56118-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
