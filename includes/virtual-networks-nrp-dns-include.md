## <a name="azure-dns"></a><span data-ttu-id="b4094-101">DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="b4094-101">Azure DNS</span></span>
<span data-ttu-id="b4094-102">DNS de Azure es un servicio de hospedaje para los dominios DNS, que permite resolver nombres mediante la infraestructura de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b4094-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="b4094-103">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b4094-103">Property</span></span> | <span data-ttu-id="b4094-104">Descripción</span><span class="sxs-lookup"><span data-stu-id="b4094-104">Description</span></span> | <span data-ttu-id="b4094-105">Valor de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b4094-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4094-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="b4094-106">**DNSzones**</span></span> |<span data-ttu-id="b4094-107">Registros DNS toohost de información de zona de dominio de un dominio en particular</span><span class="sxs-lookup"><span data-stu-id="b4094-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="b4094-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span><span class="sxs-lookup"><span data-stu-id="b4094-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="b4094-109">Conjuntos de registros de DNS</span><span class="sxs-lookup"><span data-stu-id="b4094-109">DNS record sets</span></span>
<span data-ttu-id="b4094-110">Las zonas DNS tienen un objeto secundario, llamado conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="b4094-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="b4094-111">Los conjuntos de registros son una recopilación de los registros del host por tipo en una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b4094-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="b4094-112">Los tipos de registro son A, AAAA, CNAME, MX, NS, SOA, SRV y TXT.</span><span class="sxs-lookup"><span data-stu-id="b4094-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="b4094-113">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b4094-113">Property</span></span> | <span data-ttu-id="b4094-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="b4094-114">Description</span></span> | <span data-ttu-id="b4094-115">Valor de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b4094-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4094-116">Encontrará</span><span class="sxs-lookup"><span data-stu-id="b4094-116">A</span></span> |<span data-ttu-id="b4094-117">Tipo de registro de IPv4</span><span class="sxs-lookup"><span data-stu-id="b4094-117">IPv4 record type</span></span> |<span data-ttu-id="b4094-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="b4094-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="b4094-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="b4094-119">AAAA</span></span> |<span data-ttu-id="b4094-120">Tipo de registro de IPv6</span><span class="sxs-lookup"><span data-stu-id="b4094-120">IPv6 record type</span></span> |<span data-ttu-id="b4094-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="b4094-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="b4094-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="b4094-122">CNAME</span></span> |<span data-ttu-id="b4094-123">tipo de registro de nombre canónico <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b4094-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="b4094-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="b4094-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="b4094-125">MX</span><span class="sxs-lookup"><span data-stu-id="b4094-125">MX</span></span> |<span data-ttu-id="b4094-126">tipo de registro de correo</span><span class="sxs-lookup"><span data-stu-id="b4094-126">mail record type</span></span> |<span data-ttu-id="b4094-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="b4094-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="b4094-128">NS</span><span class="sxs-lookup"><span data-stu-id="b4094-128">NS</span></span> |<span data-ttu-id="b4094-129">tipo de registro de servidor DNS</span><span class="sxs-lookup"><span data-stu-id="b4094-129">name server record type</span></span> |<span data-ttu-id="b4094-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="b4094-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="b4094-131">SOA</span><span class="sxs-lookup"><span data-stu-id="b4094-131">SOA</span></span> |<span data-ttu-id="b4094-132">tipo de registro de Inicio de autoridad (SOA) <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="b4094-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="b4094-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="b4094-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="b4094-134">SRV</span><span class="sxs-lookup"><span data-stu-id="b4094-134">SRV</span></span> |<span data-ttu-id="b4094-135">tipo de registro de servicio</span><span class="sxs-lookup"><span data-stu-id="b4094-135">service record type</span></span> |<span data-ttu-id="b4094-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="b4094-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="b4094-137"><sup>1</sup> solo se permite un valor por conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="b4094-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="b4094-138"><sup>2</sup> solo se permite un tipo de registro por SOA por zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b4094-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="b4094-139">Ejemplo de una zona DNS en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="b4094-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="b4094-140">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b4094-140">Additional resources</span></span>
<span data-ttu-id="b4094-141">Hola de lectura [documentación de API de REST para las zonas DNS ](https://msdn.microsoft.com/library/azure/mt130626.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b4094-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="b4094-142">Hola de lectura [documentación de API de REST para conjuntos de registros de DNS](https://msdn.microsoft.com/library/azure/mt130627.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b4094-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

