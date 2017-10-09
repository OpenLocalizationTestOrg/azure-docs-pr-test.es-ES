## <a name="azure-dns"></a>DNS de Azure
DNS de Azure es un servicio de hospedaje para los dominios DNS, que permite resolver nombres mediante la infraestructura de Microsoft Azure.

| Propiedad | Descripción | Valor de ejemplo |
| --- | --- | --- |
| **DNSzones** |Registros DNS toohost de información de zona de dominio de un dominio en particular |/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com" |

### <a name="dns-record-sets"></a>Conjuntos de registros de DNS
Las zonas DNS tienen un objeto secundario, llamado conjunto de registros. Los conjuntos de registros son una recopilación de los registros del host por tipo en una zona DNS. Los tipos de registro son A, AAAA, CNAME, MX, NS, SOA, SRV y TXT.

| Propiedad | Descripción | Valor de ejemplo |
| --- | --- | --- |
| Encontrará |Tipo de registro de IPv4 |/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www |
| AAAA |Tipo de registro de IPv6 |/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord |
| CNAME |tipo de registro de nombre canónico <sup>1</sup> |/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www |
| MX |tipo de registro de correo |/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail |
| NS |tipo de registro de servidor DNS |/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/ |
| SOA |tipo de registro de Inicio de autoridad (SOA) <sup>2</sup> |/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA |
| SRV |tipo de registro de servicio |/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV |

<sup>1</sup> solo se permite un valor por conjunto de registros.

<sup>2</sup> solo se permite un tipo de registro por SOA por zona DNS. 

Ejemplo de una zona DNS en formato JSON:

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

## <a name="additional-resources"></a>Recursos adicionales
Hola de lectura [documentación de API de REST para las zonas DNS ](https://msdn.microsoft.com/library/azure/mt130626.aspx) para obtener más información.

Hola de lectura [documentación de API de REST para conjuntos de registros de DNS](https://msdn.microsoft.com/library/azure/mt130627.aspx) para obtener más información.

