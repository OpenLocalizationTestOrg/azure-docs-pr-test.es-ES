## <a name="application-gateway"></a><span data-ttu-id="439d4-101">Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="439d4-101">Application Gateway</span></span>
<span data-ttu-id="439d4-102">La puerta de enlace de aplicaciones ofrece una solución de equilibrio de carga HTTP administrada de Azure basada en el equilibrio de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="439d4-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="439d4-103">Equilibrio de carga de aplicación permite el uso de Hola de reglas de enrutamiento para el tráfico de red basado en HTTP.</span><span class="sxs-lookup"><span data-stu-id="439d4-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="439d4-104">Propiedad</span><span class="sxs-lookup"><span data-stu-id="439d4-104">Property</span></span> | <span data-ttu-id="439d4-105">Descripción</span><span class="sxs-lookup"><span data-stu-id="439d4-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="439d4-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="439d4-106">**backendAddressPools**</span></span> |<span data-ttu-id="439d4-107">lista de Hola de direcciones IP de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="439d4-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="439d4-108">direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP o IP privada</span><span class="sxs-lookup"><span data-stu-id="439d4-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="439d4-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="439d4-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="439d4-110">Cada grupo tiene una configuración como el puerto, el protocolo y la afinidad basada en las cookies.</span><span class="sxs-lookup"><span data-stu-id="439d4-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="439d4-111">Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola</span><span class="sxs-lookup"><span data-stu-id="439d4-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="439d4-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="439d4-112">**frontendPorts**</span></span> |<span data-ttu-id="439d4-113">Este puerto es el puerto público Hola abierto en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="439d4-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="439d4-114">Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="439d4-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="439d4-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="439d4-115">**httpListeners**</span></span> |<span data-ttu-id="439d4-116">Agente de escucha tiene un puerto de front-end, un protocolo (Http o Https, estos distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL)</span><span class="sxs-lookup"><span data-stu-id="439d4-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="439d4-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="439d4-117">**requestRoutingRules**</span></span> |<span data-ttu-id="439d4-118">regla de Hello enlaza el grupo de servidores de back-end de agente de escucha y Hola Hola y define qué tráfico de hello del grupo de servidor back-end debe ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="439d4-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="439d4-119">Trabaja actualmente como round robin</span><span class="sxs-lookup"><span data-stu-id="439d4-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="439d4-120">Ejemplo de una plantilla de Json de una puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="439d4-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[variables('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[variables('subnetName')]",
                "properties": {
                  "addressPrefix": "[parameters('subnetPrefix')]"
                }
              }
            ]
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="439d4-121">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="439d4-121">Additional resources</span></span>
<span data-ttu-id="439d4-122">Lea [ API de REST de la puerta de enlace de aplicaciones](https://msdn.microsoft.com/library/azure/mt299388.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="439d4-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

