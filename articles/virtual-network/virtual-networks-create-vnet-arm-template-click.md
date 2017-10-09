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
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="49e7e-103">Creación de una red virtual mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="49e7e-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="49e7e-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="49e7e-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="49e7e-105">Microsoft recomienda crear recursos a través del modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="49e7e-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="49e7e-106">Obtenga más información sobre toolearn Hola diferencias entre Hola dos modelos, leer hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="49e7e-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="49e7e-107">Este artículo explica cómo toocreate una red virtual a través de la implementación del Administrador de recursos de hello modelo usando una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49e7e-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="49e7e-108">También puede crear una red virtual mediante el Administrador de recursos con otras herramientas o crear una red virtual a través del modelo de implementación clásica de hello seleccionando una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="49e7e-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="49e7e-109">Portal</span><span class="sxs-lookup"><span data-stu-id="49e7e-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="49e7e-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49e7e-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="49e7e-111">CLI</span><span class="sxs-lookup"><span data-stu-id="49e7e-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="49e7e-112">Plantilla</span><span class="sxs-lookup"><span data-stu-id="49e7e-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="49e7e-113">Portal (clásico)</span><span class="sxs-lookup"><span data-stu-id="49e7e-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="49e7e-114">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="49e7e-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="49e7e-115">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="49e7e-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="49e7e-116">Obtendrá información sobre cómo toodownload y modificar y existente de la plantilla de ARM de GitHub e implementar plantilla Hola de hello CLI de Azure, PowerShell y GitHub.</span><span class="sxs-lookup"><span data-stu-id="49e7e-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="49e7e-117">Si va a implementar simplemente plantilla de ARM de hello directamente desde GitHub, sin realizar ningún cambio, omitir demasiado[implementar una plantilla de github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="49e7e-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="49e7e-118">Descargar y comprender la plantilla de Azure Resource Manager Hola</span><span class="sxs-lookup"><span data-stu-id="49e7e-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="49e7e-119">Puede descargar Hola plantilla existente para crear una red virtual y dos subredes desde GitHub, realice los cambios que podría desee y volver a usarla.</span><span class="sxs-lookup"><span data-stu-id="49e7e-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="49e7e-120">toodo por lo tanto, complete Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="49e7e-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="49e7e-121">Navegue demasiado[página de plantilla de ejemplo de Hola](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="49e7e-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="49e7e-122">Haga clic en **azuredeploy.json** y luego en **RAW**.</span><span class="sxs-lookup"><span data-stu-id="49e7e-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="49e7e-123">Guardar Hola archivo tooa una carpeta local en el equipo.</span><span class="sxs-lookup"><span data-stu-id="49e7e-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="49e7e-124">Si está familiarizado con las plantillas, omitir toostep 7.</span><span class="sxs-lookup"><span data-stu-id="49e7e-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="49e7e-125">Abrir archivo hello que acaba de guardar y ver contenido de hello en **parámetros** en la línea 5.</span><span class="sxs-lookup"><span data-stu-id="49e7e-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="49e7e-126">Los parámetros de plantilla ARM proporcionan un marcador de posición para los valores que se pueden rellenar durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="49e7e-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="49e7e-127">Parámetro</span><span class="sxs-lookup"><span data-stu-id="49e7e-127">Parameter</span></span> | <span data-ttu-id="49e7e-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="49e7e-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="49e7e-129">**ubicación**</span><span class="sxs-lookup"><span data-stu-id="49e7e-129">**location**</span></span> |<span data-ttu-id="49e7e-130">Región de Azure donde se creará Hola red virtual</span><span class="sxs-lookup"><span data-stu-id="49e7e-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="49e7e-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="49e7e-131">**vnetName**</span></span> |<span data-ttu-id="49e7e-132">Nombre de hello red virtual nueva</span><span class="sxs-lookup"><span data-stu-id="49e7e-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="49e7e-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="49e7e-133">**addressPrefix**</span></span> |<span data-ttu-id="49e7e-134">Espacio de direcciones de Hola de red virtual, en formato CIDR</span><span class="sxs-lookup"><span data-stu-id="49e7e-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="49e7e-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="49e7e-135">**subnet1Name**</span></span> |<span data-ttu-id="49e7e-136">Nombre de hello primera red virtual</span><span class="sxs-lookup"><span data-stu-id="49e7e-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="49e7e-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="49e7e-137">**subnet1Prefix**</span></span> |<span data-ttu-id="49e7e-138">Bloque CIDR para la primera subred de Hola</span><span class="sxs-lookup"><span data-stu-id="49e7e-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="49e7e-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="49e7e-139">**subnet2Name**</span></span> |<span data-ttu-id="49e7e-140">Nombre de hello segunda red virtual</span><span class="sxs-lookup"><span data-stu-id="49e7e-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="49e7e-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="49e7e-141">**subnet2Prefix**</span></span> |<span data-ttu-id="49e7e-142">Bloque CIDR para la segunda subred de Hola</span><span class="sxs-lookup"><span data-stu-id="49e7e-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="49e7e-143">Las plantillas del Administrador de recursos de Azure que se mantienen en GitHub pueden cambiar con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="49e7e-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="49e7e-144">Asegúrese de que ha activado plantilla Hola antes de usarlo.</span><span class="sxs-lookup"><span data-stu-id="49e7e-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="49e7e-145">Compruebe el contenido de hello en **recursos** y observe el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="49e7e-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="49e7e-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="49e7e-146">**type**.</span></span> <span data-ttu-id="49e7e-147">Tipo de recurso que se está creando plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="49e7e-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="49e7e-148">En este caso, **Microsoft.Network/virtualNetworks**, que representan una red virtual.</span><span class="sxs-lookup"><span data-stu-id="49e7e-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="49e7e-149">**nombre**.</span><span class="sxs-lookup"><span data-stu-id="49e7e-149">**name**.</span></span> <span data-ttu-id="49e7e-150">Nombre de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="49e7e-150">Name for hello resource.</span></span> <span data-ttu-id="49e7e-151">Uso de Hola de aviso de **[parameters('vnetName')]**, que significa Hola will nombre proporcionado como entrada por usuario de Hola o un archivo de parámetros durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="49e7e-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="49e7e-152">**propiedades**.</span><span class="sxs-lookup"><span data-stu-id="49e7e-152">**properties**.</span></span> <span data-ttu-id="49e7e-153">Lista de propiedades para el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="49e7e-153">List of properties for hello resource.</span></span> <span data-ttu-id="49e7e-154">Esta plantilla utiliza propiedades de espacio y la subred de la dirección de Hola durante la creación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="49e7e-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="49e7e-155">Navegue hacia atrás demasiado[página de plantilla de ejemplo de Hola](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="49e7e-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="49e7e-156">Haga clic en **azuredeploy-paremeters.json** y luego en **RAW**.</span><span class="sxs-lookup"><span data-stu-id="49e7e-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="49e7e-157">Guardar Hola archivo tooa una carpeta local en el equipo.</span><span class="sxs-lookup"><span data-stu-id="49e7e-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="49e7e-158">Abra el archivo hello que acaba de guardar y modificar los valores de hello para los parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="49e7e-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="49e7e-159">Usar hello siguiendo los valores inferiores a toodeploy Hola descrito en hello escenario de red virtual:</span><span class="sxs-lookup"><span data-stu-id="49e7e-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

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

11. <span data-ttu-id="49e7e-160">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="49e7e-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="49e7e-161">Implementar la plantilla de hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="49e7e-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="49e7e-162">Completar Hola sigue pasos toodeploy Hola template que descargan mediante PowerShell:</span><span class="sxs-lookup"><span data-stu-id="49e7e-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="49e7e-163">Instalar y configurar Azure PowerShell siguiendo los pasos de Hola Hola [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.</span><span class="sxs-lookup"><span data-stu-id="49e7e-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="49e7e-164">Ejecute hello después comando toocreate un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="49e7e-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="49e7e-165">comando de Hello crea un grupo de recursos denominado *TestRG* en hello *Central US* región de azure.</span><span class="sxs-lookup"><span data-stu-id="49e7e-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="49e7e-166">Para obtener más información sobre los grupos de recursos, visite [Información general del Administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49e7e-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="49e7e-167">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="49e7e-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="49e7e-168">Ejecute hello siguiente comando toodeploy Hola nueva red virtual con hello de archivos de plantilla y los parámetros que descargó y modificado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="49e7e-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="49e7e-169">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="49e7e-169">Expected output:</span></span>
   
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
4. <span data-ttu-id="49e7e-170">Siguiente ejecución Hola comando Propiedades de hello tooview de hello nueva red virtual:</span><span class="sxs-lookup"><span data-stu-id="49e7e-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="49e7e-171">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="49e7e-171">Expected output:</span></span>

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

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="49e7e-172">Implementar la plantilla de hello mediante haga clic en implementar</span><span class="sxs-lookup"><span data-stu-id="49e7e-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="49e7e-173">Puede volver a usar predefinido repositorio de GitHub tooa cargado de plantillas de Azure Resource Manager, mantenido por Microsoft y de la Comunidad de toohello abrir.</span><span class="sxs-lookup"><span data-stu-id="49e7e-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="49e7e-174">Estas plantillas se pueden implementar sin desviarse para extraerla de GitHub, o descargaron y modificación toofit sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="49e7e-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="49e7e-175">toodeploy una plantilla que crea una red virtual con dos subredes, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="49e7e-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="49e7e-176">Desde un explorador, navegue demasiado[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="49e7e-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="49e7e-177">Desplácese hacia abajo Hola lista de plantillas y haga clic en **101-red virtual dos subredes**.</span><span class="sxs-lookup"><span data-stu-id="49e7e-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="49e7e-178">Comprobar hello **README.md** de archivos, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="49e7e-178">Check hello **README.md** file, as shown below.</span></span>

    ![Archivo README.md en github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="49e7e-180">Haga clic en **implementar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="49e7e-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="49e7e-181">Si es necesario, escriba sus credenciales de inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="49e7e-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="49e7e-182">Hola **parámetros** hoja, escriba los valores de hello que desee toouse toocreate la red virtual nueva y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="49e7e-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="49e7e-183">Hello en la ilustración siguiente se muestra los valores de hello para el escenario de hello:</span><span class="sxs-lookup"><span data-stu-id="49e7e-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![Parámetros de plantilla ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="49e7e-185">Haga clic en **grupo de recursos** y seleccione Hola red virtual a un tooadd de grupo de recursos, o haga clic en **crear nuevo** tooadd Hola red virtual tooa nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="49e7e-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="49e7e-186">Hello en la ilustración siguiente se muestra hello recurso configuración de grupo para un grupo de recursos nuevo llamado **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="49e7e-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![Grupos de recursos](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="49e7e-188">Si es necesario, cambie hello **suscripción** y **ubicación** configuración de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="49e7e-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="49e7e-189">Si no desea toosee Hola red virtual como un icono en hello **panel de inicio**, deshabilitar **tooStartboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="49e7e-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="49e7e-190">Haga clic en **condiciones legales**, lea los términos de Hola y haga clic en **comprar** tooagree.</span><span class="sxs-lookup"><span data-stu-id="49e7e-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="49e7e-191">Haga clic en **crear** toocreate Hola red virtual.</span><span class="sxs-lookup"><span data-stu-id="49e7e-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Enviar icono de implementación al portal de vista previa](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="49e7e-193">Una vez completada la implementación de hello, Hola portal de Azure haga clic en **más servicios**, tipo *redes virtuales* en el cuadro de filtro de Hola que aparece, haga clic en hoja de redes de Virtual de Virtual redes toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="49e7e-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="49e7e-194">En la hoja de hello, haga clic en *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="49e7e-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="49e7e-195">Hola *TestVNet* hoja, haga clic en **subredes** subredes de hello crea toosee, como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="49e7e-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![Crear red virtual en el portal de vista previa](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="49e7e-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49e7e-197">Next steps</span></span>

<span data-ttu-id="49e7e-198">Obtenga información acerca de cómo tooconnect:</span><span class="sxs-lookup"><span data-stu-id="49e7e-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="49e7e-199">Una red virtual de máquina virtual (VM) tooa por leer hello [crear una VM de Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) o [crear una VM Linux](../virtual-machines/linux/quick-create-portal.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="49e7e-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="49e7e-200">En lugar de crear una red virtual y la subred en los pasos de Hola de artículos de hello, puede seleccionar una red virtual existente y la subred tooconnect una máquina virtual a.</span><span class="sxs-lookup"><span data-stu-id="49e7e-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="49e7e-201">Hola redes virtuales de red virtual tooother leyendo hello [conectar redes virtuales](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="49e7e-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="49e7e-202">Hola tooan de red virtual local de la red mediante una red privada virtual (VPN) de sitio a sitio o el circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="49e7e-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="49e7e-203">Obtenga información acerca de cómo leyendo hello [conectar una red de red virtual tooan local mediante una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) y [vincular un circuito de ExpressRoute de red virtual tooan](../expressroute/expressroute-howto-linkvnet-arm.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="49e7e-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
