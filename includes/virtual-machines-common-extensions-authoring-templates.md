## <a name="overview-of-azure-resource-manager-templates"></a>Información general de las plantillas del Administrador de recursos de Azure
Plantillas de administrador de recursos de Azure le permiten toodeclaratively especificar infraestructura de IaaS de Azure de hello en el idioma de Json mediante la definición de dependencias de hello entre los recursos. Para obtener una descripción detallada de las plantillas de administrador de recursos de Azure, consulte toohello artículo siguiente:

[Información general del grupo de recursos](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Fragmento de plantilla de ejemplo para extensiones de VM.
Implementar extensiones de máquina virtual como parte de una plantilla de Azure Resource Manager requiere que toodeclaratively especificar configuración de la extensión de hello en plantilla Hola.
Aquí es el formato de Hola para especificar la configuración de la extensión de Hola.

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

Como puede ver de hello anterior, plantilla de extensión de hello consta de dos partes principales:

1. Nombre de extensión, editor y versión.
2. Configuración de la extensión.

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Identificación de publicador hello, tipo y typeHandlerVersion en cualquier extensión de
Extensiones de VM de Azure son publicadas por Microsoft y de confianza 3rd publicadores de entidad y cada extensión se identifica mediante su typeHandlerVersion hello, tipo y publicador. Pueden determinarse de la manera siguiente:  

