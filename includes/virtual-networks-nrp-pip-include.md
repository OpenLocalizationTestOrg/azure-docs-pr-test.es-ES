## <a name="public-ip-address"></a>Dirección IP pública
Un recurso de dirección IP pública le proporciona una dirección IP de Internet reservada o dinámica. Aunque puede crear una dirección IP pública como un objeto independiente, necesita tooassociate se tooanother objeto tooactually usar dirección Hola. Puede asociar un equilibrador de carga de tooa de dirección IP público, puerta de enlace de aplicaciones o una NIC tooprovide Internet acceder a toothose los recursos.  

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **publicIPAllocationMethod** |Define si la dirección IP de hello es *estático* o *dinámica*. |estática, dinámica |
| **idleTimeoutInMinutes** |Define Hola inactivo tiempo de espera, con un valor predeterminado de 4 minutos. Si no se recibe ningún paquete más de una sesión específica dentro de este tiempo, la sesión Hola terminó. |cualquier valor entre 4 y 30 |
| **ipAddress** |Dirección IP asignada tooobject. Se trata de una propiedad de solo lectura. |104.42.233.77 |

### <a name="dns-settings"></a>Configuración de DNS
Las direcciones IP públicas tienen un objeto secundario denominado **dnsSettings** que contiene Hola propiedades siguientes:

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **domainNameLabel** |Nombre de host usado para la resolución de nombres. |www, ftp, vm1 |
| **fqdn** |Nombre completo para la dirección IP pública Hola. |www.westus.cloudapp.azure.com |
| **reverseFqdn** |Nombre de dominio completo que resuelve la dirección IP de toohello y está registrado en DNS como un registro PTR. |www.contoso.com. |

Dirección IP pública de ejemplo en formato JSON:

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a>Recursos adicionales
* Obtener más información sobre [direcciones IP públicas](../articles/virtual-network/virtual-networks-reserved-public-ip.md).
* Obtenga más información sobre las [direcciones IP públicas de nivel de instancia](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).
* Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) para la dirección IP pública direcciones.

