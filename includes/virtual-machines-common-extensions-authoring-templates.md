## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="ff9af-101">Información general de las plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="ff9af-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="ff9af-102">Plantillas de administrador de recursos de Azure le permiten toodeclaratively especificar infraestructura de IaaS de Azure de hello en el idioma de Json mediante la definición de dependencias de hello entre los recursos.</span><span class="sxs-lookup"><span data-stu-id="ff9af-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="ff9af-103">Para obtener una descripción detallada de las plantillas de administrador de recursos de Azure, consulte toohello artículo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ff9af-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="ff9af-104">Información general del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ff9af-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="ff9af-105">Fragmento de plantilla de ejemplo para extensiones de VM.</span><span class="sxs-lookup"><span data-stu-id="ff9af-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="ff9af-106">Implementar extensiones de máquina virtual como parte de una plantilla de Azure Resource Manager requiere que toodeclaratively especificar configuración de la extensión de hello en plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="ff9af-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="ff9af-107">Aquí es el formato de Hola para especificar la configuración de la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff9af-107">Here is hello format for specifying hello extension configuration.</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

<span data-ttu-id="ff9af-108">Como puede ver de hello anterior, plantilla de extensión de hello consta de dos partes principales:</span><span class="sxs-lookup"><span data-stu-id="ff9af-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="ff9af-109">Nombre de extensión, editor y versión.</span><span class="sxs-lookup"><span data-stu-id="ff9af-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="ff9af-110">Configuración de la extensión.</span><span class="sxs-lookup"><span data-stu-id="ff9af-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="ff9af-111">Identificación de publicador hello, tipo y typeHandlerVersion en cualquier extensión de</span><span class="sxs-lookup"><span data-stu-id="ff9af-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="ff9af-112">Extensiones de VM de Azure son publicadas por Microsoft y de confianza 3rd publicadores de entidad y cada extensión se identifica mediante su typeHandlerVersion hello, tipo y publicador.</span><span class="sxs-lookup"><span data-stu-id="ff9af-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="ff9af-113">Pueden determinarse de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="ff9af-113">These can be determined as following:</span></span>  

