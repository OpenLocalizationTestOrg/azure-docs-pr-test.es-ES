## <a name="load-balancer"></a><span data-ttu-id="cb6bd-101">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="cb6bd-101">Load Balancer</span></span>
<span data-ttu-id="cb6bd-102">Un equilibrador de carga se usa cuando se desea tooscale sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cb6bd-102">A load balancer is used when you want tooscale your applications.</span></span> <span data-ttu-id="cb6bd-103">Entre los escenarios de implementación habituales se encuentran las aplicaciones que se ejecutan en varias instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cb6bd-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="cb6bd-104">instancias de máquina virtual de Hola se representado mediante un equilibrador de carga que le ayuda a toohello de tráfico de red toodistribute varias instancias.</span><span class="sxs-lookup"><span data-stu-id="cb6bd-104">hello VM instances are fronted by a load balancer that helps toodistribute network traffic toohello various instances.</span></span> 

![NIC en una sola máquina virtual](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="cb6bd-106">Propiedad</span><span class="sxs-lookup"><span data-stu-id="cb6bd-106">Property</span></span> | <span data-ttu-id="cb6bd-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="cb6bd-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb6bd-108">*frontendIPConfigurations*</span><span class="sxs-lookup"><span data-stu-id="cb6bd-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="cb6bd-109">un Equilibrador de carga puede incluir una o varias direcciones IP de front-end, también conocidas como IP virtuales (VIP).</span><span class="sxs-lookup"><span data-stu-id="cb6bd-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="cb6bd-110">Estas direcciones IP servir como entrada para el tráfico de Hola y pueden ser IP pública o privada</span><span class="sxs-lookup"><span data-stu-id="cb6bd-110">These IP addresses serve as ingress for hello traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="cb6bd-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="cb6bd-111">*backendAddressPools*</span></span> |<span data-ttu-id="cb6bd-112">se trata de direcciones IP asociadas a Hola se distribuirá VM NICs toowhich carga</span><span class="sxs-lookup"><span data-stu-id="cb6bd-112">these are IP addresses associated with hello VM NICs toowhich load will be distributed</span></span> |
| <span data-ttu-id="cb6bd-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="cb6bd-113">*loadBalancingRules*</span></span> |<span data-ttu-id="cb6bd-114">una propiedad de regla asigna una dirección IP determinada front-end y puerto conjunto tooa de combinación de direcciones IP de back-end y combinación de puerto.</span><span class="sxs-lookup"><span data-stu-id="cb6bd-114">a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="cb6bd-115">Con una única definición de un recurso de equilibrador de carga, puede definir varias reglas de equilibrio de carga, donde cada regla refleja una combinación de dirección IP de front-end y puerto y de dirección IP de back-end y puerto asociada con las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cb6bd-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="cb6bd-116">regla de Hello es un puerto en máquinas virtuales toomany de grupo de front-end de hello en el grupo de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="cb6bd-116">hello rule is one port in hello front end pool toomany virtual machines in hello back end pool</span></span> |
| <span data-ttu-id="cb6bd-117">*Sondeos*</span><span class="sxs-lookup"><span data-stu-id="cb6bd-117">*Probes*</span></span> |<span data-ttu-id="cb6bd-118">los sondeos permiten tookeep realizar un seguimiento del estado de Hola de instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cb6bd-118">probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="cb6bd-119">Si se produce un error en un sondeo de estado, instancia de máquina virtual de hello le llevará automáticamente fuera de la rotación</span><span class="sxs-lookup"><span data-stu-id="cb6bd-119">If a health probe fails, hello virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="cb6bd-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="cb6bd-120">*inboundNatRules*</span></span> |<span data-ttu-id="cb6bd-121">Las reglas NAT definir Hola entrada tráfico que fluye a través de IP de front-end de Hola y distribuyen instancia de máquina virtual específica de toohello back-end IP tooa.</span><span class="sxs-lookup"><span data-stu-id="cb6bd-121">NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP tooa specific virtual machine instance.</span></span> <span data-ttu-id="cb6bd-122">Regla NAT es un puerto en la máquina virtual tooone de grupo de front-end de hello en el grupo de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="cb6bd-122">NAT rule is one port in hello front end pool tooone virtual machine in hello back end pool</span></span> |

<span data-ttu-id="cb6bd-123">Ejemplo de plantilla de equilibrador de carga en formato Json:</span><span class="sxs-lookup"><span data-stu-id="cb6bd-123">Example of load balancer template in Json format:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location toodeploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
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
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a><span data-ttu-id="cb6bd-124">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cb6bd-124">Additional resources</span></span>
<span data-ttu-id="cb6bd-125">Lea el artículo [API de REST del Equilibrador de carga](https://msdn.microsoft.com/library/azure/mt163651.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="cb6bd-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

