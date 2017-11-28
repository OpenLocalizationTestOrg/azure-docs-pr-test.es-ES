---
title: "información general sobre el servicio de metadatos de instancia aaaAzure | Documentos de Microsoft"
description: "Información de tooget interfaz rESTful sobre el proceso de la máquina virtual, red y eventos de mantenimiento próximo."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="a54b0-103">Servicio de metadatos de instancia de Azure</span><span class="sxs-lookup"><span data-stu-id="a54b0-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="a54b0-104">Hola servicio de metadatos de instancia de Azure proporciona información sobre instancias de máquina virtual que pueden ser usado toomanage y configurar las máquinas virtuales en ejecución.</span><span class="sxs-lookup"><span data-stu-id="a54b0-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="a54b0-105">Esto incluye información como SKU, configuración de red y eventos de mantenimiento próximos.</span><span class="sxs-lookup"><span data-stu-id="a54b0-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="a54b0-106">Para más información sobre el tipo de información está disponible, vea las [categorías de metadatos](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="a54b0-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="a54b0-107">Servicio de metadatos de instancia de Azure es un extremo de REST accesible tooall las máquinas virtuales IaaS creada a través de hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="a54b0-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="a54b0-108">Hola extremo está disponible en una dirección IP no enrutables conocida (`169.254.169.254`) que puede tener acceso sólo desde dentro de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a54b0-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="a54b0-109">Información importante</span><span class="sxs-lookup"><span data-stu-id="a54b0-109">Important information</span></span>

<span data-ttu-id="a54b0-110">Este servicio está **disponible con carácter general** en regiones de Azure globales.</span><span class="sxs-lookup"><span data-stu-id="a54b0-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="a54b0-111">Azure Cloud se encuentra en versión preliminar pública para Azure Government, Azure en China y Azure Alemania.</span><span class="sxs-lookup"><span data-stu-id="a54b0-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="a54b0-112">Periódicamente recibe actualizaciones tooexpose nueva información acerca de las instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a54b0-112">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="a54b0-113">Esta página refleja Hola actualizada [categorías de datos](#instance-metadata-data-categories) disponibles.</span><span class="sxs-lookup"><span data-stu-id="a54b0-113">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="a54b0-114">Disponibilidad del servicio</span><span class="sxs-lookup"><span data-stu-id="a54b0-114">Service Availability</span></span>
<span data-ttu-id="a54b0-115">servicio de Hello está disponible en todas las regiones de Azure Global disponibles con carácter general.</span><span class="sxs-lookup"><span data-stu-id="a54b0-115">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="a54b0-116">servicio de Hello está en vista previa pública en regiones de hello gubernamentales, China o Alemania.</span><span class="sxs-lookup"><span data-stu-id="a54b0-116">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="a54b0-117">Regiones</span><span class="sxs-lookup"><span data-stu-id="a54b0-117">Regions</span></span>                                        | <span data-ttu-id="a54b0-118">¿Disponibilidad?</span><span class="sxs-lookup"><span data-stu-id="a54b0-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="a54b0-119">Todas las regiones globales de Azure disponibles con carácter general</span><span class="sxs-lookup"><span data-stu-id="a54b0-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="a54b0-120">Disponibilidad general</span><span class="sxs-lookup"><span data-stu-id="a54b0-120">Generally Available</span></span> 
[<span data-ttu-id="a54b0-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="a54b0-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="a54b0-122">En versión preliminar</span><span class="sxs-lookup"><span data-stu-id="a54b0-122">In Preview</span></span> 
[<span data-ttu-id="a54b0-123">Azure en China</span><span class="sxs-lookup"><span data-stu-id="a54b0-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="a54b0-124">En versión preliminar</span><span class="sxs-lookup"><span data-stu-id="a54b0-124">In Preview</span></span>
[<span data-ttu-id="a54b0-125">Azure Alemania</span><span class="sxs-lookup"><span data-stu-id="a54b0-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="a54b0-126">En versión preliminar</span><span class="sxs-lookup"><span data-stu-id="a54b0-126">In Preview</span></span>

<span data-ttu-id="a54b0-127">Esta tabla se actualiza cuando Hola servicio deja de estar disponible en otras nubes de Azure.</span><span class="sxs-lookup"><span data-stu-id="a54b0-127">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="a54b0-128">tootry out Hola servicio de metadatos de instancia, cree una máquina virtual desde [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) o hello [portal de Azure](http://portal.azure.com) Hola por encima de las regiones y seguimiento Hola ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="a54b0-128">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="a54b0-129">Uso</span><span class="sxs-lookup"><span data-stu-id="a54b0-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="a54b0-130">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="a54b0-130">Versioning</span></span>
<span data-ttu-id="a54b0-131">Hola servicio de metadatos de instancia tiene una versión.</span><span class="sxs-lookup"><span data-stu-id="a54b0-131">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="a54b0-132">Versiones son obligatorias y la versión actual de hello es `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="a54b0-132">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="a54b0-133">Versiones anteriores de vista previa de los eventos programados formando Hola api-version {más reciente}.</span><span class="sxs-lookup"><span data-stu-id="a54b0-133">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="a54b0-134">Este formato ya no se admite y dejará de utilizarse en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="a54b0-134">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="a54b0-135">A medida que agreguemos versiones más recientes, todavía se podrá acceder a las versiones anteriores por motivos de compatibilidad si los scripts tienen dependencias en formatos de datos específicos.</span><span class="sxs-lookup"><span data-stu-id="a54b0-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="a54b0-136">Sin embargo, tenga en cuenta que version(2017-03-01) de vista previa actual de hello puede no estar disponible una vez que el servicio Hola está generalmente disponible.</span><span class="sxs-lookup"><span data-stu-id="a54b0-136">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="a54b0-137">Uso de encabezados</span><span class="sxs-lookup"><span data-stu-id="a54b0-137">Using Headers</span></span>
<span data-ttu-id="a54b0-138">Al consultar Hola servicio de metadatos de instancia, debe proporcionar encabezado de hello `Metadata: true` solicitud de hello tooensure no se ha redirigido involuntariamente.</span><span class="sxs-lookup"><span data-stu-id="a54b0-138">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="a54b0-139">Recuperar metadatos</span><span class="sxs-lookup"><span data-stu-id="a54b0-139">Retrieving metadata</span></span>

<span data-ttu-id="a54b0-140">Los metadatos de instancia están disponibles para ejecutar máquinas virtuales creadas o administradas mediante [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="a54b0-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="a54b0-141">Tener acceso a todas las categorías de datos de una instancia de máquina virtual utilizando Hola después de solicitud:</span><span class="sxs-lookup"><span data-stu-id="a54b0-141">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="a54b0-142">Todas las consultas de metadatos de instancia distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a54b0-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="a54b0-143">Salida de datos</span><span class="sxs-lookup"><span data-stu-id="a54b0-143">Data output</span></span>
<span data-ttu-id="a54b0-144">De forma predeterminada, Hola servicio de metadatos de la instancia devuelve datos en formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="a54b0-144">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="a54b0-145">Pero las distintas API pueden devolver los datos en formatos diferentes si se solicita.</span><span class="sxs-lookup"><span data-stu-id="a54b0-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="a54b0-146">Hello tabla siguiente es una referencia de API pueden admitir otros formatos de datos.</span><span class="sxs-lookup"><span data-stu-id="a54b0-146">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="a54b0-147">API</span><span class="sxs-lookup"><span data-stu-id="a54b0-147">API</span></span> | <span data-ttu-id="a54b0-148">Formato predeterminado de datos</span><span class="sxs-lookup"><span data-stu-id="a54b0-148">Default Data Format</span></span> | <span data-ttu-id="a54b0-149">Otros formatos</span><span class="sxs-lookup"><span data-stu-id="a54b0-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="a54b0-150">/instance</span><span class="sxs-lookup"><span data-stu-id="a54b0-150">/instance</span></span> | <span data-ttu-id="a54b0-151">json</span><span class="sxs-lookup"><span data-stu-id="a54b0-151">json</span></span> | <span data-ttu-id="a54b0-152">text</span><span class="sxs-lookup"><span data-stu-id="a54b0-152">text</span></span>
<span data-ttu-id="a54b0-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="a54b0-153">/scheduledevents</span></span> | <span data-ttu-id="a54b0-154">json</span><span class="sxs-lookup"><span data-stu-id="a54b0-154">json</span></span> | <span data-ttu-id="a54b0-155">Ninguna</span><span class="sxs-lookup"><span data-stu-id="a54b0-155">none</span></span>

<span data-ttu-id="a54b0-156">tooaccess un formato de respuesta no predeterminado, especificar formato solicitado Hola como un parámetro de cadena de consulta de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="a54b0-156">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="a54b0-157">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a54b0-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="a54b0-158">Seguridad</span><span class="sxs-lookup"><span data-stu-id="a54b0-158">Security</span></span>
<span data-ttu-id="a54b0-159">extremo de servicio de metadatos de instancia de Hello es accesible únicamente desde dentro de hello ejecutando la instancia de máquina virtual en una dirección IP no es enrutable.</span><span class="sxs-lookup"><span data-stu-id="a54b0-159">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="a54b0-160">Además, cualquier solicitud con un `X-Forwarded-For` encabezado es rechazado por el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a54b0-160">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="a54b0-161">También se requiere solicitudes toocontain una `Metadata: true` tooensure de encabezado que Hola solicitud real directamente era deseada y no forma parte de la redirección involuntaria.</span><span class="sxs-lookup"><span data-stu-id="a54b0-161">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="a54b0-162">Error</span><span class="sxs-lookup"><span data-stu-id="a54b0-162">Error</span></span>
<span data-ttu-id="a54b0-163">Si hay un elemento de datos no encontrado o una solicitud con formato incorrecto, Hola servicio de metadatos de la instancia devuelve errores HTTP estándares.</span><span class="sxs-lookup"><span data-stu-id="a54b0-163">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="a54b0-164">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a54b0-164">For example:</span></span>

<span data-ttu-id="a54b0-165">Código de estado HTTP</span><span class="sxs-lookup"><span data-stu-id="a54b0-165">HTTP Status Code</span></span> | <span data-ttu-id="a54b0-166">Motivo</span><span class="sxs-lookup"><span data-stu-id="a54b0-166">Reason</span></span>
----------------|-------
<span data-ttu-id="a54b0-167">200 OK</span><span class="sxs-lookup"><span data-stu-id="a54b0-167">200 OK</span></span> |
<span data-ttu-id="a54b0-168">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="a54b0-168">400 Bad Request</span></span> | <span data-ttu-id="a54b0-169">Falta el encabezado `Metadata: true`</span><span class="sxs-lookup"><span data-stu-id="a54b0-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="a54b0-170">404 No encontrado</span><span class="sxs-lookup"><span data-stu-id="a54b0-170">404 Not Found</span></span> | <span data-ttu-id="a54b0-171">Existen Hello does't elemento solicitado</span><span class="sxs-lookup"><span data-stu-id="a54b0-171">hello requested element does't exist</span></span> 
<span data-ttu-id="a54b0-172">405 Método no permitido</span><span class="sxs-lookup"><span data-stu-id="a54b0-172">405 Method Not Allowed</span></span> | <span data-ttu-id="a54b0-173">Solo se admiten solicitudes `GET` y `POST`</span><span class="sxs-lookup"><span data-stu-id="a54b0-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="a54b0-174">429 Demasiadas solicitudes</span><span class="sxs-lookup"><span data-stu-id="a54b0-174">429 Too Many Requests</span></span> | <span data-ttu-id="a54b0-175">API de Hello actualmente admite un máximo de 5 consultas por segundo</span><span class="sxs-lookup"><span data-stu-id="a54b0-175">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="a54b0-176">500 Error de servicio</span><span class="sxs-lookup"><span data-stu-id="a54b0-176">500 Service Error</span></span>     | <span data-ttu-id="a54b0-177">Vuelva a intentarlo más tarde</span><span class="sxs-lookup"><span data-stu-id="a54b0-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="a54b0-178">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a54b0-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="a54b0-179">Todas las respuestas de las API son cadenas JSON.</span><span class="sxs-lookup"><span data-stu-id="a54b0-179">All API responses are JSON strings.</span></span> <span data-ttu-id="a54b0-180">Todas las respuestas de ejemplo siguientes se han impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="a54b0-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="a54b0-181">Recuperación de información de red</span><span class="sxs-lookup"><span data-stu-id="a54b0-181">Retrieving network information</span></span>

<span data-ttu-id="a54b0-182">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="a54b0-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="a54b0-183">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="a54b0-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="a54b0-184">respuesta de Hello es una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="a54b0-184">hello response is a JSON string.</span></span> <span data-ttu-id="a54b0-185">Después de respuesta de ejemplo de Hola es impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="a54b0-185">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="a54b0-186">Recuperación de dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="a54b0-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="a54b0-187">Recuperación de todos los metadatos para una instancia</span><span class="sxs-lookup"><span data-stu-id="a54b0-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="a54b0-188">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="a54b0-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="a54b0-189">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="a54b0-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="a54b0-190">respuesta de Hello es una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="a54b0-190">hello response is a JSON string.</span></span> <span data-ttu-id="a54b0-191">Después de respuesta de ejemplo de Hola es impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="a54b0-191">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="a54b0-192">Recuperación de metadatos en una máquina virtual con Windows</span><span class="sxs-lookup"><span data-stu-id="a54b0-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="a54b0-193">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="a54b0-193">**Request**</span></span>

<span data-ttu-id="a54b0-194">Se pueden recuperar los metadatos de instancia de Windows a través de la utilidad de PowerShell de Hola `curl`:</span><span class="sxs-lookup"><span data-stu-id="a54b0-194">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="a54b0-195">O a través de hello `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a54b0-195">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="a54b0-196">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="a54b0-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="a54b0-197">respuesta de Hello es una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="a54b0-197">hello response is a JSON string.</span></span> <span data-ttu-id="a54b0-198">Después de respuesta de ejemplo de Hola es impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="a54b0-198">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="a54b0-199">Categorías de datos de metadatos de instancia</span><span class="sxs-lookup"><span data-stu-id="a54b0-199">Instance metadata data categories</span></span>
<span data-ttu-id="a54b0-200">Hola siguientes categorías de datos está disponible a través de hello servicio de metadatos de instancia:</span><span class="sxs-lookup"><span data-stu-id="a54b0-200">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="a54b0-201">Datos</span><span class="sxs-lookup"><span data-stu-id="a54b0-201">Data</span></span> | <span data-ttu-id="a54b0-202">Descripción</span><span class="sxs-lookup"><span data-stu-id="a54b0-202">Description</span></span>
-----|------------
<span data-ttu-id="a54b0-203">location</span><span class="sxs-lookup"><span data-stu-id="a54b0-203">location</span></span> | <span data-ttu-id="a54b0-204">Hola de región de Azure VM se esté ejecutando</span><span class="sxs-lookup"><span data-stu-id="a54b0-204">Azure Region hello VM is running in</span></span>
<span data-ttu-id="a54b0-205">name</span><span class="sxs-lookup"><span data-stu-id="a54b0-205">name</span></span> | <span data-ttu-id="a54b0-206">Nombre del programa Hola a máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a54b0-206">Name of hello VM</span></span> 
<span data-ttu-id="a54b0-207">offer</span><span class="sxs-lookup"><span data-stu-id="a54b0-207">offer</span></span> | <span data-ttu-id="a54b0-208">Ofrece información para la imagen de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="a54b0-208">Offer information for hello VM image.</span></span> <span data-ttu-id="a54b0-209">Este valor solo está presente para las imágenes que se implementan desde la galería de imágenes de Azure.</span><span class="sxs-lookup"><span data-stu-id="a54b0-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="a54b0-210">publisher</span><span class="sxs-lookup"><span data-stu-id="a54b0-210">publisher</span></span> | <span data-ttu-id="a54b0-211">Publicador de la imagen de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="a54b0-211">Publisher of hello VM image</span></span>
<span data-ttu-id="a54b0-212">sku</span><span class="sxs-lookup"><span data-stu-id="a54b0-212">sku</span></span> | <span data-ttu-id="a54b0-213">SKU específica para la imagen de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="a54b0-213">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="a54b0-214">versión</span><span class="sxs-lookup"><span data-stu-id="a54b0-214">version</span></span> | <span data-ttu-id="a54b0-215">Versión de imagen de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="a54b0-215">Version of hello VM image</span></span> 
<span data-ttu-id="a54b0-216">osType</span><span class="sxs-lookup"><span data-stu-id="a54b0-216">osType</span></span> | <span data-ttu-id="a54b0-217">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="a54b0-217">Linux or Windows</span></span> 
<span data-ttu-id="a54b0-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="a54b0-218">platformUpdateDomain</span></span> |  <span data-ttu-id="a54b0-219">[Dominio de actualización](virtual-machines-windows-manage-availability.md) Hola máquina virtual se está ejecutando en</span><span class="sxs-lookup"><span data-stu-id="a54b0-219">[Update domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="a54b0-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="a54b0-220">platformFaultDomain</span></span> | <span data-ttu-id="a54b0-221">[Dominio de error](virtual-machines-windows-manage-availability.md) Hola máquina virtual se está ejecutando en</span><span class="sxs-lookup"><span data-stu-id="a54b0-221">[Fault domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="a54b0-222">vmId</span><span class="sxs-lookup"><span data-stu-id="a54b0-222">vmId</span></span> | <span data-ttu-id="a54b0-223">[Identificador único](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) para hello VM</span><span class="sxs-lookup"><span data-stu-id="a54b0-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="a54b0-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="a54b0-224">vmSize</span></span> | [<span data-ttu-id="a54b0-225">Tamaño de VM</span><span class="sxs-lookup"><span data-stu-id="a54b0-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="a54b0-226">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="a54b0-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="a54b0-227">Dirección IPv4 local de hello VM</span><span class="sxs-lookup"><span data-stu-id="a54b0-227">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="a54b0-228">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="a54b0-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="a54b0-229">Dirección IPv4 pública de hello VM</span><span class="sxs-lookup"><span data-stu-id="a54b0-229">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="a54b0-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="a54b0-230">subnet/address</span></span> | <span data-ttu-id="a54b0-231">Dirección de subred de VM de hello</span><span class="sxs-lookup"><span data-stu-id="a54b0-231">Subnet address of hello VM</span></span>
<span data-ttu-id="a54b0-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="a54b0-232">subnet/prefix</span></span> | <span data-ttu-id="a54b0-233">Prefijo de la subred, ejemplo, 24</span><span class="sxs-lookup"><span data-stu-id="a54b0-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="a54b0-234">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="a54b0-234">ipv6/ipAddress</span></span> | <span data-ttu-id="a54b0-235">Dirección IPv6 local de hello VM</span><span class="sxs-lookup"><span data-stu-id="a54b0-235">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="a54b0-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="a54b0-236">macAddress</span></span> | <span data-ttu-id="a54b0-237">Dirección de MAC de la VM</span><span class="sxs-lookup"><span data-stu-id="a54b0-237">VM mac address</span></span> 
<span data-ttu-id="a54b0-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="a54b0-238">scheduledevents</span></span> | <span data-ttu-id="a54b0-239">Actualmente en Versión preliminar pública Vea [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="a54b0-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="a54b0-240">Escenarios de ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="a54b0-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="a54b0-241">Seguimiento de una máquina virtual que se ejecuta en Azure</span><span class="sxs-lookup"><span data-stu-id="a54b0-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="a54b0-242">Como proveedor de servicios, puede requerir número de hello tootrack de máquinas virtuales que ejecutan el software o con agentes que necesitan tootrack unicidad del programa Hola a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a54b0-242">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="a54b0-243">toobe tooget capaz de un identificador único para una máquina virtual, use hello `vmId` arrastrándolo desde el servicio de metadatos de la instancia.</span><span class="sxs-lookup"><span data-stu-id="a54b0-243">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="a54b0-244">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="a54b0-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="a54b0-245">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="a54b0-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="a54b0-246">Ubicación de contenedores, dominio de error/actualización basado en particiones de datos</span><span class="sxs-lookup"><span data-stu-id="a54b0-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="a54b0-247">Para ciertos escenarios, la ubicación de las distintas réplicas de datos es de máxima importancia.</span><span class="sxs-lookup"><span data-stu-id="a54b0-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="a54b0-248">Por ejemplo, [selección de ubicación de réplica HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) o la ubicación del contenedor a través de un [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) puede requerir hello tooknow `platformFaultDomain` y `platformUpdateDomain` Hola VM se ejecuta en.</span><span class="sxs-lookup"><span data-stu-id="a54b0-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="a54b0-249">Puede consultar estos datos directamente a través de hello servicio de metadatos de la instancia.</span><span class="sxs-lookup"><span data-stu-id="a54b0-249">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="a54b0-250">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="a54b0-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="a54b0-251">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="a54b0-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="a54b0-252">Obtener más información acerca de hello VM durante el caso de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="a54b0-252">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="a54b0-253">Como proveedor de servicios, puede obtener una llamada de soporte técnico que desee que tooknow obtener más información acerca de hello VM.</span><span class="sxs-lookup"><span data-stu-id="a54b0-253">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="a54b0-254">Pedir Hola cliente tooshare Hola proceso metadatos pueden proporcionar información básica para tooknow profesional de soporte técnico de hello sobre tipo de saludo de la máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="a54b0-254">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="a54b0-255">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="a54b0-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="a54b0-256">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="a54b0-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="a54b0-257">respuesta de Hello es una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="a54b0-257">hello response is a JSON string.</span></span> <span data-ttu-id="a54b0-258">Después de respuesta de ejemplo de Hola es impreso correctamente para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="a54b0-258">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="a54b0-259">Ejemplos de llamar al servicio de metadatos mediante distintos lenguajes dentro de hello VM</span><span class="sxs-lookup"><span data-stu-id="a54b0-259">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="a54b0-260">language</span><span class="sxs-lookup"><span data-stu-id="a54b0-260">Language</span></span> | <span data-ttu-id="a54b0-261">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a54b0-261">Example</span></span> 
---------|----------------
<span data-ttu-id="a54b0-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="a54b0-262">Ruby</span></span>     | <span data-ttu-id="a54b0-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="a54b0-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="a54b0-264">Go Lan</span><span class="sxs-lookup"><span data-stu-id="a54b0-264">Go Lan</span></span>   | <span data-ttu-id="a54b0-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="a54b0-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="a54b0-266">Python</span><span class="sxs-lookup"><span data-stu-id="a54b0-266">python</span></span>   | <span data-ttu-id="a54b0-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="a54b0-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="a54b0-268">C++</span><span class="sxs-lookup"><span data-stu-id="a54b0-268">C++</span></span>      | <span data-ttu-id="a54b0-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="a54b0-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="a54b0-270">C#</span><span class="sxs-lookup"><span data-stu-id="a54b0-270">C#</span></span>       | <span data-ttu-id="a54b0-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="a54b0-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="a54b0-272">Javascript</span><span class="sxs-lookup"><span data-stu-id="a54b0-272">Javascript</span></span> | <span data-ttu-id="a54b0-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="a54b0-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="a54b0-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a54b0-274">Powershell</span></span> | <span data-ttu-id="a54b0-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="a54b0-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="a54b0-276">Bash</span><span class="sxs-lookup"><span data-stu-id="a54b0-276">Bash</span></span>       | <span data-ttu-id="a54b0-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="a54b0-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="a54b0-278">P+F</span><span class="sxs-lookup"><span data-stu-id="a54b0-278">FAQ</span></span>
1. <span data-ttu-id="a54b0-279">Recibo mensajes de error de hello `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="a54b0-279">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="a54b0-280">¿Qué significa?</span><span class="sxs-lookup"><span data-stu-id="a54b0-280">What does this mean?</span></span>
   * <span data-ttu-id="a54b0-281">Hola servicio de metadatos de instancia requiere el encabezado de hello `Metadata: true` toobe transmiten durante una solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="a54b0-281">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="a54b0-282">Pasar este encabezado en llamada REST de hello permite acceso toohello servicio de metadatos de la instancia.</span><span class="sxs-lookup"><span data-stu-id="a54b0-282">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="a54b0-283">¿Por qué no recibo información de proceso de mi máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="a54b0-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="a54b0-284">Hola servicio de metadatos de instancia sólo admite actualmente instancias creadas con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a54b0-284">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="a54b0-285">Hola futuras, podemos agreguemos compatibilidad para las VM del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="a54b0-285">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="a54b0-286">Creé mi máquina virtual mediante Azure Resource Manager hace un tiempo.</span><span class="sxs-lookup"><span data-stu-id="a54b0-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="a54b0-287">¿Por qué no veo la información de metadatos de proceso?</span><span class="sxs-lookup"><span data-stu-id="a54b0-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="a54b0-288">Para las máquinas virtuales creadas después de septiembre de 2016, agregue un [etiqueta](../azure-resource-manager/resource-group-using-tags.md) toostart ver metadatos de proceso.</span><span class="sxs-lookup"><span data-stu-id="a54b0-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="a54b0-289">Para máquinas virtuales anteriores (creadas antes de septiembre de 2016), agregar o quitar extensiones de metadatos o con datos discos toohello VM toorefresh.</span><span class="sxs-lookup"><span data-stu-id="a54b0-289">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="a54b0-290">¿Por qué recibo errores hello `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="a54b0-290">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="a54b0-291">Vuelva a intentar la solicitud en función del sistema de interrupción exponencial.</span><span class="sxs-lookup"><span data-stu-id="a54b0-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="a54b0-292">Si no se soluciona el problema de hello póngase en contacto con el soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="a54b0-292">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="a54b0-293">¿Dónde puedo compartir preguntas o comentarios adicionales?</span><span class="sxs-lookup"><span data-stu-id="a54b0-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="a54b0-294">Envíe los comentarios en http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="a54b0-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="a54b0-295">¿Esto funciona para la instancia del conjunto de escala de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="a54b0-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="a54b0-296">Sí, el servicio de metadatos está disponible para las instancias del conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="a54b0-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="a54b0-297">¿Cómo se puede obtener soporte técnico para servicio de hello?</span><span class="sxs-lookup"><span data-stu-id="a54b0-297">How do I get support for hello service?</span></span>
   * <span data-ttu-id="a54b0-298">tooget soporte para el servicio de hello, crear un problema de compatibilidad en el portal de Azure para hello VM donde no es capaz de tooget metadatos respuesta después de varios reintentos largos</span><span class="sxs-lookup"><span data-stu-id="a54b0-298">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Soporte técnico de metadatos de instancia](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="a54b0-300">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a54b0-300">Next Steps</span></span>

- <span data-ttu-id="a54b0-301">Obtener más información sobre hello [scheduledevents](virtual-machines-scheduled-events.md) API **en Public Preview** proporcionada por hello servicio de metadatos de la instancia.</span><span class="sxs-lookup"><span data-stu-id="a54b0-301">Learn more about hello [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by hello Instance Metadata Service.</span></span>
