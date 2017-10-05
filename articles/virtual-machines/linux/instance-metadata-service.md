---
title: "Servicio de metadatos de instancia de Azure para máquinas virtuales Linux | Microsoft Docs"
description: "Interfaz RESTful para obtener información sobre proceso, red y próximos eventos de mantenimiento de la máquina virtual Linux."
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a61acbe0532ece3a6a26ceb366c12c69db4c304c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a><span data-ttu-id="fbd0b-103">Servicio de metadatos de instancia de Azure para máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="fbd0b-103">Azure Instance Metadata service for Linux VMs</span></span>


<span data-ttu-id="fbd0b-104">El servicio de metadatos de instancia de Azure proporciona información sobre instancias de máquina virtual en ejecución que pueden usarse para administrar y configurar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="fbd0b-105">Esto incluye información como SKU, configuración de red y eventos de mantenimiento próximos.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="fbd0b-106">Para más información sobre el tipo de información está disponible, vea las [categorías de metadatos](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="fbd0b-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="fbd0b-107">El servicio de metadatos de instancia de Azure es un punto de conexión REST al que pueden tener acceso todas las máquinas virtuales IaaS creadas a través de [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="fbd0b-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="fbd0b-108">El punto de conexión está disponible en una dirección IP no enrutable conocida (`169.254.169.254`) a la que solo se puede tener acceso desde dentro de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbd0b-109">Este servicio está **disponible con carácter general** en regiones de Azure globales.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="fbd0b-110">Azure Cloud se encuentra en versión preliminar pública para Azure Government, Azure en China y Azure Alemania.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="fbd0b-111">Recibe actualizaciones periódicas para exponer información nueva sobre instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-111">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="fbd0b-112">En esta página se reflejan las [categorías de datos](#instance-metadata-data-categories) actualizadas disponibles.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-112">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="fbd0b-113">Disponibilidad del servicio</span><span class="sxs-lookup"><span data-stu-id="fbd0b-113">Service availability</span></span>
<span data-ttu-id="fbd0b-114">El servicio está disponible con carácter general en regiones de Azure globales.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-114">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="fbd0b-115">El servicio se encuentra en versión preliminar pública en las regiones Government, China y Alemania.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-115">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="fbd0b-116">Regiones</span><span class="sxs-lookup"><span data-stu-id="fbd0b-116">Regions</span></span>                                        | <span data-ttu-id="fbd0b-117">¿Disponibilidad?</span><span class="sxs-lookup"><span data-stu-id="fbd0b-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="fbd0b-118">Todas las regiones globales de Azure disponibles con carácter general</span><span class="sxs-lookup"><span data-stu-id="fbd0b-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="fbd0b-119">Disponibilidad general</span><span class="sxs-lookup"><span data-stu-id="fbd0b-119">Generally Available</span></span> 
[<span data-ttu-id="fbd0b-120">Azure Government</span><span class="sxs-lookup"><span data-stu-id="fbd0b-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="fbd0b-121">En versión preliminar</span><span class="sxs-lookup"><span data-stu-id="fbd0b-121">In Preview</span></span> 
[<span data-ttu-id="fbd0b-122">Azure en China</span><span class="sxs-lookup"><span data-stu-id="fbd0b-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="fbd0b-123">En versión preliminar</span><span class="sxs-lookup"><span data-stu-id="fbd0b-123">In Preview</span></span>
[<span data-ttu-id="fbd0b-124">Azure Alemania</span><span class="sxs-lookup"><span data-stu-id="fbd0b-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="fbd0b-125">En versión preliminar</span><span class="sxs-lookup"><span data-stu-id="fbd0b-125">In Preview</span></span>

<span data-ttu-id="fbd0b-126">Esta tabla se actualiza cuando el servicio está disponible en otras nubes de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-126">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="fbd0b-127">Para probar el servicio de metadatos de instancia, cree una máquina virtual desde [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) o [Azure Portal](http://portal.azure.com) en las regiones anteriores, y siga los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-127">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="fbd0b-128">Uso</span><span class="sxs-lookup"><span data-stu-id="fbd0b-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="fbd0b-129">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="fbd0b-129">Versioning</span></span>
<span data-ttu-id="fbd0b-130">El servicio de metadatos de instancia tiene versiones.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-130">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="fbd0b-131">Las versiones son obligatorias y la versión actual es la `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-131">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="fbd0b-132">Las versiones preliminares de eventos programados compatibles {más reciente} como la versión de api.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-132">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="fbd0b-133">Este formato ya no es compatible y dejará de utilizarse en el futuro.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-133">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="fbd0b-134">A medida que agreguemos versiones más recientes, todavía se podrá acceder a las versiones anteriores por motivos de compatibilidad si los scripts tienen dependencias en formatos de datos específicos.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="fbd0b-135">Pero tenga en cuenta que es posible que la versión preliminar actual (2017-03-01) no esté disponible una vez que el servicio esté disponible con carácter general.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-135">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="fbd0b-136">Uso de encabezados</span><span class="sxs-lookup"><span data-stu-id="fbd0b-136">Using headers</span></span>
<span data-ttu-id="fbd0b-137">Al consultar el servicio de metadatos de instancia, debe proporcionar el encabezado `Metadata: true` para asegurarse de que la solicitud no se ha redirigido de manera involuntaria.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-137">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="fbd0b-138">Recuperar metadatos</span><span class="sxs-lookup"><span data-stu-id="fbd0b-138">Retrieving metadata</span></span>

<span data-ttu-id="fbd0b-139">Los metadatos de instancia están disponibles para ejecutar máquinas virtuales creadas o administradas mediante [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="fbd0b-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="fbd0b-140">Para tener acceso a todas las categorías de datos de una instancia de máquina virtual, use la solicitud siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbd0b-140">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="fbd0b-141">Todas las consultas de metadatos de instancia distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="fbd0b-142">Salida de datos</span><span class="sxs-lookup"><span data-stu-id="fbd0b-142">Data output</span></span>
<span data-ttu-id="fbd0b-143">De forma predeterminada, el servicio de metadatos de instancia devuelve datos en formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="fbd0b-143">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="fbd0b-144">Pero las distintas API pueden devolver los datos en formatos diferentes si se solicita.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="fbd0b-145">En la tabla siguiente se muestra una referencia de otros formatos de datos que las API pueden admitir.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-145">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="fbd0b-146">API</span><span class="sxs-lookup"><span data-stu-id="fbd0b-146">API</span></span> | <span data-ttu-id="fbd0b-147">Formato predeterminado de datos</span><span class="sxs-lookup"><span data-stu-id="fbd0b-147">Default Data Format</span></span> | <span data-ttu-id="fbd0b-148">Otros formatos</span><span class="sxs-lookup"><span data-stu-id="fbd0b-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="fbd0b-149">/instance</span><span class="sxs-lookup"><span data-stu-id="fbd0b-149">/instance</span></span> | <span data-ttu-id="fbd0b-150">json</span><span class="sxs-lookup"><span data-stu-id="fbd0b-150">json</span></span> | <span data-ttu-id="fbd0b-151">text</span><span class="sxs-lookup"><span data-stu-id="fbd0b-151">text</span></span>
<span data-ttu-id="fbd0b-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="fbd0b-152">/scheduledevents</span></span> | <span data-ttu-id="fbd0b-153">json</span><span class="sxs-lookup"><span data-stu-id="fbd0b-153">json</span></span> | <span data-ttu-id="fbd0b-154">Ninguna</span><span class="sxs-lookup"><span data-stu-id="fbd0b-154">none</span></span>

<span data-ttu-id="fbd0b-155">Para obtener acceso a un formato de respuesta que no sea el predeterminado, especifique el formato solicitado como un parámetro de cadena de consulta en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-155">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="fbd0b-156">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fbd0b-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="fbd0b-157">Seguridad</span><span class="sxs-lookup"><span data-stu-id="fbd0b-157">Security</span></span>
<span data-ttu-id="fbd0b-158">El punto de conexión del servicio de metadatos de instancia solo es accesible desde la instancia de máquina virtual en ejecución en una dirección IP no enrutable.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-158">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="fbd0b-159">Además, el servicio rechaza cualquier solicitud que tenga un encabezado `X-Forwarded-For`.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-159">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="fbd0b-160">También es necesario que las solicitudes incluyan un encabezado `Metadata: true` para garantizar que la solicitud actual esté dirigida directamente y no como parte de un redireccionamiento accidental.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-160">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="fbd0b-161">Error</span><span class="sxs-lookup"><span data-stu-id="fbd0b-161">Error</span></span>
<span data-ttu-id="fbd0b-162">Si no se encuentra un elemento de datos o hay una solicitud con formato incorrecto, el servicio de metadatos de instancia devuelve errores HTTP estándar.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-162">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="fbd0b-163">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fbd0b-163">For example:</span></span>

<span data-ttu-id="fbd0b-164">Código de estado HTTP</span><span class="sxs-lookup"><span data-stu-id="fbd0b-164">HTTP Status Code</span></span> | <span data-ttu-id="fbd0b-165">Motivo</span><span class="sxs-lookup"><span data-stu-id="fbd0b-165">Reason</span></span>
----------------|-------
<span data-ttu-id="fbd0b-166">200 OK</span><span class="sxs-lookup"><span data-stu-id="fbd0b-166">200 OK</span></span> |
<span data-ttu-id="fbd0b-167">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="fbd0b-167">400 Bad Request</span></span> | <span data-ttu-id="fbd0b-168">Falta el encabezado `Metadata: true`</span><span class="sxs-lookup"><span data-stu-id="fbd0b-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="fbd0b-169">404 No encontrado</span><span class="sxs-lookup"><span data-stu-id="fbd0b-169">404 Not Found</span></span> | <span data-ttu-id="fbd0b-170">El elemento solicitado no existe</span><span class="sxs-lookup"><span data-stu-id="fbd0b-170">The requested element does't exist</span></span> 
<span data-ttu-id="fbd0b-171">405 Método no permitido</span><span class="sxs-lookup"><span data-stu-id="fbd0b-171">405 Method Not Allowed</span></span> | <span data-ttu-id="fbd0b-172">Solo se admiten solicitudes `GET` y `POST`</span><span class="sxs-lookup"><span data-stu-id="fbd0b-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="fbd0b-173">429 Demasiadas solicitudes</span><span class="sxs-lookup"><span data-stu-id="fbd0b-173">429 Too Many Requests</span></span> | <span data-ttu-id="fbd0b-174">La API es compatible actualmente con un máximo de cinco consultas por segundo</span><span class="sxs-lookup"><span data-stu-id="fbd0b-174">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="fbd0b-175">500 Error de servicio</span><span class="sxs-lookup"><span data-stu-id="fbd0b-175">500 Service Error</span></span>     | <span data-ttu-id="fbd0b-176">Vuelva a intentarlo más tarde</span><span class="sxs-lookup"><span data-stu-id="fbd0b-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="fbd0b-177">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="fbd0b-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="fbd0b-178">Todas las respuestas de las API son cadenas JSON.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-178">All API responses are JSON strings.</span></span> <span data-ttu-id="fbd0b-179">Todas las respuestas de ejemplo siguientes se han impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="fbd0b-180">Recuperación de información de red</span><span class="sxs-lookup"><span data-stu-id="fbd0b-180">Retrieving network information</span></span>

<span data-ttu-id="fbd0b-181">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="fbd0b-182">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="fbd0b-183">La respuesta es una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-183">The response is a JSON string.</span></span> <span data-ttu-id="fbd0b-184">La respuesta de ejemplo siguiente se ha impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-184">The following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="fbd0b-185">Recuperación de dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="fbd0b-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="fbd0b-186">Recuperación de todos los metadatos para una instancia</span><span class="sxs-lookup"><span data-stu-id="fbd0b-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="fbd0b-187">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="fbd0b-188">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="fbd0b-189">La respuesta es una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-189">The response is a JSON string.</span></span> <span data-ttu-id="fbd0b-190">La respuesta de ejemplo siguiente se ha impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-190">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="fbd0b-191">Recuperación de metadatos en una máquina virtual con Windows</span><span class="sxs-lookup"><span data-stu-id="fbd0b-191">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="fbd0b-192">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-192">**Request**</span></span>

<span data-ttu-id="fbd0b-193">Los metadatos de instancia se pueden recuperar en Windows a través de la utilidad `curl` de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fbd0b-193">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="fbd0b-194">O bien a través del cmdlet `Invoke-RestMethod`:</span><span class="sxs-lookup"><span data-stu-id="fbd0b-194">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="fbd0b-195">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="fbd0b-196">La respuesta es una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-196">The response is a JSON string.</span></span> <span data-ttu-id="fbd0b-197">La respuesta de ejemplo siguiente se ha impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-197">The following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="fbd0b-198">Categorías de datos de metadatos de instancia</span><span class="sxs-lookup"><span data-stu-id="fbd0b-198">Instance metadata data categories</span></span>
<span data-ttu-id="fbd0b-199">Las categorías de datos siguientes están disponibles a través del servicio de metadatos de instancia:</span><span class="sxs-lookup"><span data-stu-id="fbd0b-199">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="fbd0b-200">Datos</span><span class="sxs-lookup"><span data-stu-id="fbd0b-200">Data</span></span> | <span data-ttu-id="fbd0b-201">Descripción</span><span class="sxs-lookup"><span data-stu-id="fbd0b-201">Description</span></span>
-----|------------
<span data-ttu-id="fbd0b-202">location</span><span class="sxs-lookup"><span data-stu-id="fbd0b-202">location</span></span> | <span data-ttu-id="fbd0b-203">La región de Azure donde se ejecuta la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbd0b-203">Azure Region the VM is running in</span></span>
<span data-ttu-id="fbd0b-204">name</span><span class="sxs-lookup"><span data-stu-id="fbd0b-204">name</span></span> | <span data-ttu-id="fbd0b-205">Nombre de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbd0b-205">Name of the VM</span></span> 
<span data-ttu-id="fbd0b-206">offer</span><span class="sxs-lookup"><span data-stu-id="fbd0b-206">offer</span></span> | <span data-ttu-id="fbd0b-207">Ofrece información para la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-207">Offer information for the VM image.</span></span> <span data-ttu-id="fbd0b-208">Este valor solo está presente para las imágenes que se implementan desde la galería de imágenes de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="fbd0b-209">publisher</span><span class="sxs-lookup"><span data-stu-id="fbd0b-209">publisher</span></span> | <span data-ttu-id="fbd0b-210">Publicador de la imagen de VM</span><span class="sxs-lookup"><span data-stu-id="fbd0b-210">Publisher of the VM image</span></span>
<span data-ttu-id="fbd0b-211">sku</span><span class="sxs-lookup"><span data-stu-id="fbd0b-211">sku</span></span> | <span data-ttu-id="fbd0b-212">SKU específica de la imagen de VM</span><span class="sxs-lookup"><span data-stu-id="fbd0b-212">Specific SKU for the VM image</span></span>  
<span data-ttu-id="fbd0b-213">versión</span><span class="sxs-lookup"><span data-stu-id="fbd0b-213">version</span></span> | <span data-ttu-id="fbd0b-214">Versión de la imagen de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbd0b-214">Version of the VM image</span></span> 
<span data-ttu-id="fbd0b-215">osType</span><span class="sxs-lookup"><span data-stu-id="fbd0b-215">osType</span></span> | <span data-ttu-id="fbd0b-216">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="fbd0b-216">Linux or Windows</span></span> 
<span data-ttu-id="fbd0b-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="fbd0b-217">platformUpdateDomain</span></span> |  <span data-ttu-id="fbd0b-218">El [dominio de actualización](manage-availability.md) en que se ejecuta la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-218">[Update domain](manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="fbd0b-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="fbd0b-219">platformFaultDomain</span></span> | <span data-ttu-id="fbd0b-220">El [dominio de error](manage-availability.md) en que se ejecuta la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-220">[Fault domain](manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="fbd0b-221">vmId</span><span class="sxs-lookup"><span data-stu-id="fbd0b-221">vmId</span></span> | <span data-ttu-id="fbd0b-222">[Identificador único](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="fbd0b-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="fbd0b-223">vmSize</span></span> | [<span data-ttu-id="fbd0b-224">Tamaño de VM</span><span class="sxs-lookup"><span data-stu-id="fbd0b-224">VM size</span></span>](sizes.md)
<span data-ttu-id="fbd0b-225">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="fbd0b-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="fbd0b-226">Dirección IPv4 local de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbd0b-226">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="fbd0b-227">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="fbd0b-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="fbd0b-228">Dirección IPv4 pública de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbd0b-228">Public IPv4 address of the VM</span></span>
<span data-ttu-id="fbd0b-229">subnet/address</span><span class="sxs-lookup"><span data-stu-id="fbd0b-229">subnet/address</span></span> | <span data-ttu-id="fbd0b-230">Dirección de subred de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbd0b-230">Subnet address of the VM</span></span>
<span data-ttu-id="fbd0b-231">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="fbd0b-231">subnet/prefix</span></span> | <span data-ttu-id="fbd0b-232">Prefijo de la subred, ejemplo, 24</span><span class="sxs-lookup"><span data-stu-id="fbd0b-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="fbd0b-233">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="fbd0b-233">ipv6/ipAddress</span></span> | <span data-ttu-id="fbd0b-234">Dirección IPv6 local de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbd0b-234">Local IPv6 address of the VM</span></span>
<span data-ttu-id="fbd0b-235">macAddress</span><span class="sxs-lookup"><span data-stu-id="fbd0b-235">macAddress</span></span> | <span data-ttu-id="fbd0b-236">Dirección de MAC de la VM</span><span class="sxs-lookup"><span data-stu-id="fbd0b-236">VM mac address</span></span> 
<span data-ttu-id="fbd0b-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="fbd0b-237">scheduledevents</span></span> | <span data-ttu-id="fbd0b-238">Actualmente en Versión preliminar pública Vea [scheduledevents](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="fbd0b-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="fbd0b-239">Escenarios de ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="fbd0b-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="fbd0b-240">Seguimiento de una máquina virtual que se ejecuta en Azure</span><span class="sxs-lookup"><span data-stu-id="fbd0b-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="fbd0b-241">Como proveedor de servicios, es posible que necesite hacer seguimiento de la cantidad de máquinas virtuales que ejecutan su software o que tenga agentes que deban hacer seguimiento de la unicidad de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-241">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="fbd0b-242">Para poder obtener un identificador único para una máquina virtual, use el campo `vmId` del servicio de metadatos de instancia.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-242">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="fbd0b-243">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="fbd0b-244">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="fbd0b-245">Ubicación de los contenedores y el dominio de error/actualización basado en particiones de datos</span><span class="sxs-lookup"><span data-stu-id="fbd0b-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="fbd0b-246">Para ciertos escenarios, la ubicación de las distintas réplicas de datos es de máxima importancia.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="fbd0b-247">Por ejemplo, para [la ubicación de réplicas de HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) o la ubicación de contenedores a través de un [orquestador](https://kubernetes.io/docs/user-guide/node-selection/) se debe saber en qué `platformFaultDomain` y `platformUpdateDomain` se ejecuta la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="fbd0b-248">Puede consultar directamente estos datos a través del servicio de metadatos de instancia.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-248">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="fbd0b-249">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="fbd0b-250">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="fbd0b-251">Obtención de más información sobre la VM durante el caso de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="fbd0b-251">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="fbd0b-252">Como proveedor de servicios, es posible que reciba una llamada de soporte técnico en la que le gustaría tener más información sobre la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-252">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="fbd0b-253">Pedirle al cliente que comparta los metadatos del equipo puede proporcionar información básica para que el profesional de soporte técnico conozca la variante de máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-253">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="fbd0b-254">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="fbd0b-255">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="fbd0b-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="fbd0b-256">La respuesta es una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-256">The response is a JSON string.</span></span> <span data-ttu-id="fbd0b-257">La respuesta de ejemplo siguiente se ha impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-257">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="fbd0b-258">Ejemplos de llamadas al servicio de metadatos mediante lenguajes diferentes dentro de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbd0b-258">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="fbd0b-259">Idioma</span><span class="sxs-lookup"><span data-stu-id="fbd0b-259">Language</span></span> | <span data-ttu-id="fbd0b-260">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="fbd0b-260">Example</span></span> 
---------|----------------
<span data-ttu-id="fbd0b-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="fbd0b-261">Ruby</span></span>     | <span data-ttu-id="fbd0b-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="fbd0b-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="fbd0b-263">Go Lan</span><span class="sxs-lookup"><span data-stu-id="fbd0b-263">Go Lan</span></span>   | <span data-ttu-id="fbd0b-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="fbd0b-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="fbd0b-265">Python</span><span class="sxs-lookup"><span data-stu-id="fbd0b-265">python</span></span>   | <span data-ttu-id="fbd0b-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="fbd0b-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="fbd0b-267">C++</span><span class="sxs-lookup"><span data-stu-id="fbd0b-267">C++</span></span>      | <span data-ttu-id="fbd0b-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="fbd0b-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="fbd0b-269">C#</span><span class="sxs-lookup"><span data-stu-id="fbd0b-269">C#</span></span>       | <span data-ttu-id="fbd0b-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="fbd0b-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="fbd0b-271">Javascript</span><span class="sxs-lookup"><span data-stu-id="fbd0b-271">Javascript</span></span> | <span data-ttu-id="fbd0b-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="fbd0b-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="fbd0b-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbd0b-273">Powershell</span></span> | <span data-ttu-id="fbd0b-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="fbd0b-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="fbd0b-275">Bash</span><span class="sxs-lookup"><span data-stu-id="fbd0b-275">Bash</span></span>       | <span data-ttu-id="fbd0b-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="fbd0b-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="fbd0b-277">P+F</span><span class="sxs-lookup"><span data-stu-id="fbd0b-277">FAQ</span></span>
1. <span data-ttu-id="fbd0b-278">Obtengo el error `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-278">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="fbd0b-279">¿Qué significa?</span><span class="sxs-lookup"><span data-stu-id="fbd0b-279">What does this mean?</span></span>
   * <span data-ttu-id="fbd0b-280">El servicio de metadatos de instancia requiere que el encabezado `Metadata: true` se transmita en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-280">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="fbd0b-281">Transmitir este encabezado en la llamada de REST permite tener acceso al servicio de metadatos de instancia.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-281">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="fbd0b-282">¿Por qué no recibo información de proceso de mi máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="fbd0b-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="fbd0b-283">Actualmente el servicio de metadatos de instancia solo admite instancias creadas con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-283">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="fbd0b-284">En el futuro, es posible que se agregue compatibilidad para máquinas virtuales de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-284">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="fbd0b-285">Creé mi máquina virtual mediante Azure Resource Manager hace un tiempo.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="fbd0b-286">¿Por qué no veo la información de metadatos de proceso?</span><span class="sxs-lookup"><span data-stu-id="fbd0b-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="fbd0b-287">En el caso de las máquinas virtuales que se crearon después de septiembre de 2016, agregue una [etiqueta](../../azure-resource-manager/resource-group-using-tags.md) para empezar a ver los metadatos de proceso.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="fbd0b-288">En el caso de máquinas virtuales anteriores (creadas antes de septiembre de 2016), agregue o quite extensiones o discos de datos a la máquina virtual para actualizar los metadatos.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-288">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="fbd0b-289">¿Por qué recibo el error `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="fbd0b-289">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="fbd0b-290">Vuelva a intentar la solicitud en función del sistema de interrupción exponencial.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="fbd0b-291">Si el problema persiste, póngase en contacto con el servicio de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-291">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="fbd0b-292">¿Dónde puedo compartir preguntas o comentarios adicionales?</span><span class="sxs-lookup"><span data-stu-id="fbd0b-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="fbd0b-293">Envíe los comentarios en http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="fbd0b-294">¿Esto funciona para la instancia del conjunto de escala de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="fbd0b-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="fbd0b-295">Sí, el servicio de metadatos está disponible para las instancias del conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="fbd0b-296">¿Cómo puedo obtener soporte técnico para el servicio?</span><span class="sxs-lookup"><span data-stu-id="fbd0b-296">How do I get support for the service?</span></span>
   * <span data-ttu-id="fbd0b-297">Para obtener soporte técnico para el servicio, cree un problema de compatibilidad en Azure Portal para la máquina virtual en la que no es posible obtener respuesta de metadatos después de reintentos prolongados</span><span class="sxs-lookup"><span data-stu-id="fbd0b-297">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![Soporte técnico de metadatos de instancia](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="fbd0b-299">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fbd0b-299">Next steps</span></span>

- <span data-ttu-id="fbd0b-300">Más información sobre la API [Scheduled Events](scheduled-events.md) **en versión preliminar pública** proporcionada por el servicio de metadatos de instancia.</span><span class="sxs-lookup"><span data-stu-id="fbd0b-300">Learn more about the [Scheduled Events](scheduled-events.md) API **in public preview** provided by the Instance Metadata service.</span></span>
