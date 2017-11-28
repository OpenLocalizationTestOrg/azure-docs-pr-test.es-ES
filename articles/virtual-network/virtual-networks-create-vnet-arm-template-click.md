---
title: "Creación de una red virtual mediante una plantilla de Azure Resource Manager | Microsoft Docs"
description: Aprenda a crear una red virtual mediante una plantilla de Azure Resource Manager.
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
ms.openlocfilehash: 81602766848a91331c8d811ea1c8ec3ffae44b96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="1d724-103">Creación de una red virtual mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d724-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="1d724-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="1d724-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="1d724-105">Microsoft recomienda crear recursos mediante el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d724-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="1d724-106">Para más información acerca de las diferencias entre los dos modelos, lea el artículo [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Descripción de los modelos de implementación de Azure).</span><span class="sxs-lookup"><span data-stu-id="1d724-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="1d724-107">En este artículo se describe cómo crear una red virtual con el modelo de implementación de Resource Manager mediante una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d724-107">This article explains how to create a VNet through the Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="1d724-108">También puede crear una red virtual mediante Resource Manager con otras herramientas o crear una red virtual a través del modelo de implementación clásica seleccionando una opción diferente en la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="1d724-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="1d724-109">Portal</span><span class="sxs-lookup"><span data-stu-id="1d724-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="1d724-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d724-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="1d724-111">CLI</span><span class="sxs-lookup"><span data-stu-id="1d724-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="1d724-112">Plantilla</span><span class="sxs-lookup"><span data-stu-id="1d724-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="1d724-113">Portal (clásico)</span><span class="sxs-lookup"><span data-stu-id="1d724-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="1d724-114">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="1d724-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="1d724-115">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="1d724-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="1d724-116">Aprenderá a descargar y modificar una plantilla de ARM existente desde GitHub, así como a implementar la plantilla de GitHub, PowerShell y la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d724-116">You will learn how to download and modify and existing ARM template from GitHub, and deploy the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="1d724-117">Si simplemente va a implementar la plantilla de ARM directamente desde GitHub, sin realizar ningún cambio, vaya a [implementar una plantilla desde github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="1d724-117">If you are simply deploying the ARM template directly from GitHub, without any changes, skip to [deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="1d724-118">Descarga e información sobre la plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="1d724-118">Download and understand the Azure Resource Manager template</span></span>
<span data-ttu-id="1d724-119">Puede descargar la plantilla existente para crear una red virtual y dos subredes desde GitHub, realizar los cambios que desee y volver a utilizarla.</span><span class="sxs-lookup"><span data-stu-id="1d724-119">You can download the existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="1d724-120">Para hacerlo, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1d724-120">To do so, complete the following steps:</span></span>

1. <span data-ttu-id="1d724-121">Navegue a [la página de la plantilla de ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="1d724-121">Navigate to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="1d724-122">Haga clic en **azuredeploy.json** y luego en **RAW**.</span><span class="sxs-lookup"><span data-stu-id="1d724-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="1d724-123">Guarde el archivo en un una carpeta local en su equipo.</span><span class="sxs-lookup"><span data-stu-id="1d724-123">Save the file to a a local folder on your computer.</span></span>
4. <span data-ttu-id="1d724-124">Si está familiarizado con las plantillas, salte al paso 7.</span><span class="sxs-lookup"><span data-stu-id="1d724-124">If you are familiar with templates, skip to step 7.</span></span>
5. <span data-ttu-id="1d724-125">Abra el archivo que acaba de guardar y vea el contenido de la línea 5 en **parameters** .</span><span class="sxs-lookup"><span data-stu-id="1d724-125">Open the file you just saved and look at the contents under **parameters** in line 5.</span></span> <span data-ttu-id="1d724-126">Los parámetros de plantilla ARM proporcionan un marcador de posición para los valores que se pueden rellenar durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="1d724-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="1d724-127">Parámetro</span><span class="sxs-lookup"><span data-stu-id="1d724-127">Parameter</span></span> | <span data-ttu-id="1d724-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="1d724-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="1d724-129">**ubicación**</span><span class="sxs-lookup"><span data-stu-id="1d724-129">**location**</span></span> |<span data-ttu-id="1d724-130">Región de Azure donde se creará la red virtual</span><span class="sxs-lookup"><span data-stu-id="1d724-130">Azure region where the VNet will be created</span></span> |
   | <span data-ttu-id="1d724-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="1d724-131">**vnetName**</span></span> |<span data-ttu-id="1d724-132">Nombre de la red virtual nueva</span><span class="sxs-lookup"><span data-stu-id="1d724-132">Name for the new VNet</span></span> |
   | <span data-ttu-id="1d724-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="1d724-133">**addressPrefix**</span></span> |<span data-ttu-id="1d724-134">Espacio de direcciones de la red virtual, en formato CIDR</span><span class="sxs-lookup"><span data-stu-id="1d724-134">Address space for the VNet, in CIDR format</span></span> |
   | <span data-ttu-id="1d724-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="1d724-135">**subnet1Name**</span></span> |<span data-ttu-id="1d724-136">Nombre de la primera red virtual</span><span class="sxs-lookup"><span data-stu-id="1d724-136">Name for the first VNet</span></span> |
   | <span data-ttu-id="1d724-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="1d724-137">**subnet1Prefix**</span></span> |<span data-ttu-id="1d724-138">Bloque CIDR de la primera subred</span><span class="sxs-lookup"><span data-stu-id="1d724-138">CIDR block for the first subnet</span></span> |
   | <span data-ttu-id="1d724-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="1d724-139">**subnet2Name**</span></span> |<span data-ttu-id="1d724-140">Nombre de la segunda red virtual</span><span class="sxs-lookup"><span data-stu-id="1d724-140">Name for the second VNet</span></span> |
   | <span data-ttu-id="1d724-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="1d724-141">**subnet2Prefix**</span></span> |<span data-ttu-id="1d724-142">Bloque CIDR de la segunda subred</span><span class="sxs-lookup"><span data-stu-id="1d724-142">CIDR block for the second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="1d724-143">Las plantillas del Administrador de recursos de Azure que se mantienen en GitHub pueden cambiar con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="1d724-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="1d724-144">Asegúrese de comprobar la plantilla antes de usarla.</span><span class="sxs-lookup"><span data-stu-id="1d724-144">Make sure you check the template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="1d724-145">Compruebe el contenido en **resources** y observe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1d724-145">Check the content under **resources** and notice the following:</span></span>
   
   * <span data-ttu-id="1d724-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="1d724-146">**type**.</span></span> <span data-ttu-id="1d724-147">Tipo de recurso que creó la plantilla.</span><span class="sxs-lookup"><span data-stu-id="1d724-147">Type of resource being created by the template.</span></span> <span data-ttu-id="1d724-148">En este caso, **Microsoft.Network/virtualNetworks**, que representan una red virtual.</span><span class="sxs-lookup"><span data-stu-id="1d724-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="1d724-149">**nombre**.</span><span class="sxs-lookup"><span data-stu-id="1d724-149">**name**.</span></span> <span data-ttu-id="1d724-150">Nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="1d724-150">Name for the resource.</span></span> <span data-ttu-id="1d724-151">Observe el uso de **[parameters('vnetName')]**, lo que significa que será el usuario quien proporcione el nombre como entrada o como archivo de parámetros durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="1d724-151">Notice the use of **[parameters('vnetName')]**, which means the name will provided as input by the user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="1d724-152">**propiedades**.</span><span class="sxs-lookup"><span data-stu-id="1d724-152">**properties**.</span></span> <span data-ttu-id="1d724-153">Lista de propiedades para el recurso.</span><span class="sxs-lookup"><span data-stu-id="1d724-153">List of properties for the resource.</span></span> <span data-ttu-id="1d724-154">Esta plantilla usa las propiedades de espacio de direcciones y subred durante la creación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="1d724-154">This template uses the address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="1d724-155">Vuelva a [la página de la plantilla de ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="1d724-155">Navigate back to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="1d724-156">Haga clic en **azuredeploy-paremeters.json** y luego en **RAW**.</span><span class="sxs-lookup"><span data-stu-id="1d724-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="1d724-157">Guarde el archivo en un una carpeta local en su equipo.</span><span class="sxs-lookup"><span data-stu-id="1d724-157">Save the file to a a local folder on your computer.</span></span>
10. <span data-ttu-id="1d724-158">Abra el archivo que acaba de guardar y edite los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="1d724-158">Open the file you just saved and edit the values for the parameters.</span></span> <span data-ttu-id="1d724-159">Utilice los siguientes valores para implementar la red virtual que se describe en este escenario:</span><span class="sxs-lookup"><span data-stu-id="1d724-159">Use the following values below to deploy the VNet described in the scenario:</span></span>

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

11. <span data-ttu-id="1d724-160">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="1d724-160">Save the file.</span></span>


## <a name="deploy-the-template-using-powershell"></a><span data-ttu-id="1d724-161">Implementación de la plantilla mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d724-161">Deploy the template using PowerShell</span></span>

<span data-ttu-id="1d724-162">Complete los siguientes pasos para implementar la plantilla que descargó con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1d724-162">Complete the following steps to deploy the template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="1d724-163">Instale y configure Azure PowerShell completando los pasos del artículo [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1d724-163">Install and configure Azure PowerShell by completing the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="1d724-164">Ejecute el comando siguiente para crear un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="1d724-164">Run the following command to create a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="1d724-165">El comando crea un grupo de recursos denominado *TestRG* en la región *Centro de EE. UU.* de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d724-165">The command creates a resource group named *TestRG* in the *Central US* azure region.</span></span> <span data-ttu-id="1d724-166">Para más información acerca de los grupos de recursos, visite [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d724-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="1d724-167">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="1d724-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="1d724-168">Ejecute el siguiente comando para implementar la nueva red virtual mediante la plantilla y los archivos de parámetros que descargó y modificó antes:</span><span class="sxs-lookup"><span data-stu-id="1d724-168">Run the following command to deploy the new VNet using the template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="1d724-169">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="1d724-169">Expected output:</span></span>
   
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
4. <span data-ttu-id="1d724-170">Ejecute el siguiente comando para ver las propiedades de la nueva red virtual:</span><span class="sxs-lookup"><span data-stu-id="1d724-170">Run the following command to view the properties of the new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="1d724-171">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="1d724-171">Expected output:</span></span>

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

## <a name="deploy-the-template-using-click-to-deploy"></a><span data-ttu-id="1d724-172">Implementación de la plantilla por medio de un solo clic para implementar</span><span class="sxs-lookup"><span data-stu-id="1d724-172">Deploy the template using click-to-deploy</span></span>

<span data-ttu-id="1d724-173">Puede reutilizar plantillas de Azure Resource Manager predefinidas que se han cargado en un repositorio GitHub que mantiene Microsoft y está abierto a la comunidad.</span><span class="sxs-lookup"><span data-stu-id="1d724-173">You can reuse pre-defined Azure Resource Manager templates uploaded to a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="1d724-174">Estas plantillas pueden implementarse directamente desde GitHub o pueden descargarse y modificarse para ajustarlas a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="1d724-174">These templates can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> <span data-ttu-id="1d724-175">Para implementar una plantilla que crea una red virtual con dos subredes, complete los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1d724-175">To deploy a template that creates a VNet with two subnets, complete the following steps:</span></span>

1. <span data-ttu-id="1d724-176">Desde un explorador, vaya a [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="1d724-176">From a browser, navigate to [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="1d724-177">Desplácese hacia abajo por la lista de plantillas y haga clic en **101-vnet-two-subnets**.</span><span class="sxs-lookup"><span data-stu-id="1d724-177">Scroll down the list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="1d724-178">Compruebe el archivo **README.md** , como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="1d724-178">Check the **README.md** file, as shown below.</span></span>

    ![Archivo README.md en github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="1d724-180">Haga clic en **Implementar en Azure**.</span><span class="sxs-lookup"><span data-stu-id="1d724-180">Click **Deploy to Azure**.</span></span> <span data-ttu-id="1d724-181">Si es necesario, escriba sus credenciales de inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d724-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="1d724-182">En la hoja **Parámetros**, escriba los valores que desee utilizar para crear la red virtual nueva y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1d724-182">In the **Parameters** blade, enter the values you want to use to create your new VNet, and then click **OK**.</span></span> <span data-ttu-id="1d724-183">En la siguiente ilustración se muestran los valores para el escenario:</span><span class="sxs-lookup"><span data-stu-id="1d724-183">The following figure shows the values for the scenario:</span></span>
   
    ![Parámetros de plantilla ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="1d724-185">Haga clic en **Grupo de recursos** y seleccione un grupo de recursos al que va a agregar la red virtual, o haga clic en **Crear nuevo** para agregar la red virtual a un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1d724-185">Click **Resource group** and select a resource group to add the VNet to, or click **Create new** to add the VNet to a new resource group.</span></span> <span data-ttu-id="1d724-186">En la siguiente ilustración se muestra la configuración de grupo de recursos de uno nuevo denominado **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="1d724-186">The following figure shows the resource group settings for a new resource group called **TestRG**:</span></span>

    ![Grupos de recursos](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="1d724-188">Si es necesario, cambie la configuración de la **Suscripción** y la **Ubicación** de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="1d724-188">If necessary, change the **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="1d724-189">Si no desea ver la red virtual como un icono en el **Panel de inicio**, deshabilite **Anclar a panel de inicio**.</span><span class="sxs-lookup"><span data-stu-id="1d724-189">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span></span>
8. <span data-ttu-id="1d724-190">Haga clic en **Términos legales**, lea los términos y haga clic en **Comprar** para aceptar.</span><span class="sxs-lookup"><span data-stu-id="1d724-190">Click **Legal terms**, read the terms, and click **Buy** to agree.</span></span> 
9. <span data-ttu-id="1d724-191">Haga clic en **Crear** para crear la red virtual.</span><span class="sxs-lookup"><span data-stu-id="1d724-191">Click **Create** to create the VNet.</span></span>
   
    ![Enviar icono de implementación al portal de vista previa](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="1d724-193">Una vez finalizada la implementación, en Azure Portal, haga clic en **Más servicios**, escriba *redes virtuales* en el cuadro de filtro que aparece y haga clic en Redes virtuales para ver la hoja Redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="1d724-193">Once the deployment is complete, in the Azure portal click **More services**, type *virtual networks* in the filter box that appears, then click Virtual networks to see the Virtual networks blade.</span></span> <span data-ttu-id="1d724-194">En la hoja, haga clic en *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="1d724-194">In the blade, click *TestVNet*.</span></span> <span data-ttu-id="1d724-195">En la hoja *TestVNet*, haga clic en **Subredes** para ver las subredes creadas, como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="1d724-195">In the *TestVNet* blade, click **Subnets** to see the created subnets, as shown in the following picture:</span></span>
    
     ![Crear red virtual en el portal de vista previa](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="1d724-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d724-197">Next steps</span></span>

<span data-ttu-id="1d724-198">Aprenda a conectar:</span><span class="sxs-lookup"><span data-stu-id="1d724-198">Learn how to connect:</span></span>

- <span data-ttu-id="1d724-199">Una máquina virtual (VM) a una red virtual, para lo cual debería leer los artículos [Creación de una máquina virtual Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) o [Creación de una máquina virtual Linux](../virtual-machines/linux/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1d724-199">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="1d724-200">En lugar de crear una red virtual y la subred en los pasos de los artículos, puede seleccionar una red virtual y una subred a la que conectar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1d724-200">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="1d724-201">La red virtual a otras redes virtuales. Para ello, lea el artículo [Conexión de redes virtuales](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1d724-201">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="1d724-202">La red virtual a una red local mediante una red privada virtual (VPN) de sitio a sitio o un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1d724-202">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="1d724-203">Aprenda cómo hacerlo mediante los artículos [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) (Conexión de una red virtual a una red local mediante una VPN de sitio a sitio) y [Vinculación de una red virtual a un circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1d724-203">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
