---
title: aaaCreate una red virtual | Plantilla de administrador de recursos de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate a virtual de red usando una plantilla de Azure Resource Manager."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Creación de una red virtual mediante una plantilla de Azure Resource Manager

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico. Microsoft recomienda crear recursos a través del modelo de implementación del Administrador de recursos de Hola. Obtenga más información sobre toolearn Hola diferencias entre Hola dos modelos, leer hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md) artículo.
 
Este artículo explica cómo toocreate una red virtual a través de la implementación del Administrador de recursos de hello modelo usando una plantilla de Azure Resource Manager. También puede crear una red virtual mediante el Administrador de recursos con otras herramientas o crear una red virtual a través del modelo de implementación clásica de hello seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
- [Portal](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [CLI](virtual-networks-create-vnet-arm-cli.md)
- [Plantilla](virtual-networks-create-vnet-arm-template-click.md)
- [Portal (clásico)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (clásico)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [CLI (clásico)](virtual-networks-create-vnet-classic-cli.md)

Obtendrá información sobre cómo toodownload y modificar y existente de la plantilla de ARM de GitHub e implementar plantilla Hola de hello CLI de Azure, PowerShell y GitHub.

Si va a implementar simplemente plantilla de ARM de hello directamente desde GitHub, sin realizar ningún cambio, omitir demasiado[implementar una plantilla de github](#deploy-the-arm-template-by-using-click-to-deploy).

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Descargar y comprender la plantilla de Azure Resource Manager Hola
Puede descargar Hola plantilla existente para crear una red virtual y dos subredes desde GitHub, realice los cambios que podría desee y volver a usarla. toodo por lo tanto, complete Hola pasos:

1. Navegue demasiado[página de plantilla de ejemplo de Hola](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
2. Haga clic en **azuredeploy.json** y luego en **RAW**.
3. Guardar Hola archivo tooa una carpeta local en el equipo.
4. Si está familiarizado con las plantillas, omitir toostep 7.
5. Abrir archivo hello que acaba de guardar y ver contenido de hello en **parámetros** en la línea 5. Los parámetros de plantilla ARM proporcionan un marcador de posición para los valores que se pueden rellenar durante la implementación.
   
   | Parámetro | Descripción |
   | --- | --- |
   | **ubicación** |Región de Azure donde se creará Hola red virtual |
   | **vnetName** |Nombre de hello red virtual nueva |
   | **addressPrefix** |Espacio de direcciones de Hola de red virtual, en formato CIDR |
   | **subnet1Name** |Nombre de hello primera red virtual |
   | **subnet1Prefix** |Bloque CIDR para la primera subred de Hola |
   | **subnet2Name** |Nombre de hello segunda red virtual |
   | **subnet2Prefix** |Bloque CIDR para la segunda subred de Hola |
   
   > [!IMPORTANT]
   > Las plantillas del Administrador de recursos de Azure que se mantienen en GitHub pueden cambiar con el tiempo. Asegúrese de que ha activado plantilla Hola antes de usarlo.
   > 
   > 
6. Compruebe el contenido de hello en **recursos** y observe el siguiente hello:
   
   * **type**. Tipo de recurso que se está creando plantilla Hola. En este caso, **Microsoft.Network/virtualNetworks**, que representan una red virtual.
   * **nombre**. Nombre de recurso de Hola. Uso de Hola de aviso de **[parameters('vnetName')]**, que significa Hola will nombre proporcionado como entrada por usuario de Hola o un archivo de parámetros durante la implementación.
   * **propiedades**. Lista de propiedades para el recurso de Hola. Esta plantilla utiliza propiedades de espacio y la subred de la dirección de Hola durante la creación de la red virtual.
7. Navegue hacia atrás demasiado[página de plantilla de ejemplo de Hola](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
8. Haga clic en **azuredeploy-paremeters.json** y luego en **RAW**.
9. Guardar Hola archivo tooa una carpeta local en el equipo.
10. Abra el archivo hello que acaba de guardar y modificar los valores de hello para los parámetros de Hola. Usar hello siguiendo los valores inferiores a toodeploy Hola descrito en hello escenario de red virtual:

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. Guarde el archivo hello.


## <a name="deploy-hello-template-using-powershell"></a>Implementar la plantilla de hello mediante PowerShell

Completar Hola sigue pasos toodeploy Hola template que descargan mediante PowerShell:

1. Instalar y configurar Azure PowerShell siguiendo los pasos de Hola Hola [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.
2. Ejecute hello después comando toocreate un nuevo grupo de recursos:

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    comando de Hello crea un grupo de recursos denominado *TestRG* en hello *Central US* región de azure. Para obtener más información sobre los grupos de recursos, visite [Información general del Administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md).

    Resultado esperado:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. Ejecute hello siguiente comando toodeploy Hola nueva red virtual con hello de archivos de plantilla y los parámetros que descargó y modificado anteriormente:

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    Resultado esperado:
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. Siguiente ejecución Hola comando Propiedades de hello tooview de hello nueva red virtual:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    Resultado esperado:

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a>Implementar la plantilla de hello mediante haga clic en implementar

Puede volver a usar predefinido repositorio de GitHub tooa cargado de plantillas de Azure Resource Manager, mantenido por Microsoft y de la Comunidad de toohello abrir. Estas plantillas se pueden implementar sin desviarse para extraerla de GitHub, o descargaron y modificación toofit sus necesidades. toodeploy una plantilla que crea una red virtual con dos subredes, Hola completa pasos:

1. Desde un explorador, navegue demasiado[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
2. Desplácese hacia abajo Hola lista de plantillas y haga clic en **101-red virtual dos subredes**. Comprobar hello **README.md** de archivos, tal y como se muestra a continuación.

    ![Archivo README.md en github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. Haga clic en **implementar tooAzure**. Si es necesario, escriba sus credenciales de inicio de sesión de Azure. 
4. Hola **parámetros** hoja, escriba los valores de hello que desee toouse toocreate la red virtual nueva y, a continuación, haga clic en **Aceptar**. Hello en la ilustración siguiente se muestra los valores de hello para el escenario de hello:
   
    ![Parámetros de plantilla ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. Haga clic en **grupo de recursos** y seleccione Hola red virtual a un tooadd de grupo de recursos, o haga clic en **crear nuevo** tooadd Hola red virtual tooa nuevo grupo de recursos. Hello en la ilustración siguiente se muestra hello recurso configuración de grupo para un grupo de recursos nuevo llamado **TestRG**:

    ![Grupos de recursos](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. Si es necesario, cambie hello **suscripción** y **ubicación** configuración de la red virtual.
7. Si no desea toosee Hola red virtual como un icono en hello **panel de inicio**, deshabilitar **tooStartboard Pin**.
8. Haga clic en **condiciones legales**, lea los términos de Hola y haga clic en **comprar** tooagree. 
9. Haga clic en **crear** toocreate Hola red virtual.
   
    ![Enviar icono de implementación al portal de vista previa](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Una vez completada la implementación de hello, Hola portal de Azure haga clic en **más servicios**, tipo *redes virtuales* en el cuadro de filtro de Hola que aparece, haga clic en hoja de redes de Virtual de Virtual redes toosee Hola. En la hoja de hello, haga clic en *TestVNet*. Hola *TestVNet* hoja, haga clic en **subredes** subredes de hello crea toosee, como se muestra en hello después de imagen:
    
     ![Crear red virtual en el portal de vista previa](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooconnect:

- Una red virtual de máquina virtual (VM) tooa por leer hello [crear una VM de Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) o [crear una VM Linux](../virtual-machines/linux/quick-create-portal.md) artículos. En lugar de crear una red virtual y la subred en los pasos de Hola de artículos de hello, puede seleccionar una red virtual existente y la subred tooconnect una máquina virtual a.
- Hola redes virtuales de red virtual tooother leyendo hello [conectar redes virtuales](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artículo.
- Hola tooan de red virtual local de la red mediante una red privada virtual (VPN) de sitio a sitio o el circuito de ExpressRoute. Obtenga información acerca de cómo leyendo hello [conectar una red de red virtual tooan local mediante una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) y [vincular un circuito de ExpressRoute de red virtual tooan](../expressroute/expressroute-howto-linkvnet-arm.md) artículos.
