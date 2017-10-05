---
title: Recursos de certificados en Azure Automation | Microsoft Docs
description: "Los certificados se pueden almacenar de manera segura en Automatización de Azure, de manera tal que los runbooks o configuraciones de DSC pueden tener acceso a ellos para realizar la autenticación respecto de Azure y recursos de terceros.  Este artículo explica los detalles de los certificados y cómo trabajar con ellos en la creación de textos y de gráficos."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: fd1737a420c132dace9307436bfea98a9bde94a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="19c9d-104">Activos de certificados en Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="19c9d-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="19c9d-105">Los certificados se pueden almacenar de manera segura en Azure Automation de manera que los runbooks o las configuraciones de DSC pueden tener acceso a ellos mediante el uso de la actividad **Get-AzureRmAutomationRmCertificate** para recursos de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="19c9d-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="19c9d-106">Esto le permite crear runbooks y configuraciones de DSC que usan certificados para autenticación o agregarlos a Azure o a recursos de terceros.</span><span class="sxs-lookup"><span data-stu-id="19c9d-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="19c9d-107">Los recursos protegidos en Automatización de Azure incluyen credenciales, certificados, conexiones y variables cifradas.</span><span class="sxs-lookup"><span data-stu-id="19c9d-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="19c9d-108">Estos recursos se cifran y se almacenan en Automatización de Azure con una clave única que se genera para cada cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="19c9d-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="19c9d-109">Esta clave se cifra mediante un certificado maestro y se almacena en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="19c9d-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="19c9d-110">Antes de almacenar un recurso seguro, la clave de la cuenta de automatización se descifra con el certificado maestro y, a continuación, se utiliza para cifrar el recurso.</span><span class="sxs-lookup"><span data-stu-id="19c9d-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="19c9d-111">Cmdlets de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="19c9d-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="19c9d-112">Los cmdlets de la tabla siguiente se usan para crear y administrar variables de Automatización con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19c9d-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="19c9d-113">Se incluyen como parte del [módulo Azure PowerShell](../powershell-install-configure.md) que está disponible para su uso en las configuraciones de DSC y los runbooks de Automatización.</span><span class="sxs-lookup"><span data-stu-id="19c9d-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="19c9d-114">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="19c9d-114">Cmdlets</span></span>|<span data-ttu-id="19c9d-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="19c9d-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="19c9d-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="19c9d-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="19c9d-117">Recupera información sobre un certificado para utilizarlo en un runbook o en la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="19c9d-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="19c9d-118">Solo puede recuperar el certificado mismo desde la actividad Get-AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="19c9d-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="19c9d-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="19c9d-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="19c9d-120">Crea un certificado nuevo en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="19c9d-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="19c9d-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="19c9d-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="19c9d-122">Quita un certificado a Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="19c9d-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="19c9d-123">Crea un certificado nuevo en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="19c9d-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="19c9d-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="19c9d-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="19c9d-125">Establece las propiedades de un certificado existente, incluyendo la carga del archivo de certificado y el establecimiento de la contraseña de un .pfx.</span><span class="sxs-lookup"><span data-stu-id="19c9d-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="19c9d-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="19c9d-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="19c9d-127">Carga un certificado de servicio para el servicio en la nube especificado.</span><span class="sxs-lookup"><span data-stu-id="19c9d-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="19c9d-128">Creación de un certificado nuevo</span><span class="sxs-lookup"><span data-stu-id="19c9d-128">Creating a new certificate</span></span>

<span data-ttu-id="19c9d-129">Cuando crea un certificado nuevo, debe cargar un archivo .cer o .pfx a Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="19c9d-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="19c9d-130">Si marca el certificado como exportable, podrá transferirlo fuera del almacén de certificados de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="19c9d-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="19c9d-131">Si no es exportable, solo se puede usar para firmar dentro del runbook o la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="19c9d-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="19c9d-132">Para crear un certificado nuevo con el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="19c9d-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="19c9d-133">En la cuenta de Automation, haga clic en el icono **Activos** para abrir la hoja **Activos**.</span><span class="sxs-lookup"><span data-stu-id="19c9d-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="19c9d-134">Haga clic en el icono **Certificados** para abrir la hoja **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="19c9d-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="19c9d-135">Haga clic en **Agregar un certificado** en la parte superior del cuadro.</span><span class="sxs-lookup"><span data-stu-id="19c9d-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="19c9d-136">Escriba un nombre para el certificado en el cuadro **Nombre** .</span><span class="sxs-lookup"><span data-stu-id="19c9d-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="19c9d-137">Haga clic en **Seleccionar un archivo** en **Cargar un archivo de certificado** para buscar un archivo .cer o .pfx.</span><span class="sxs-lookup"><span data-stu-id="19c9d-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="19c9d-138">Si selecciona un archivo .pfx, especifique una contraseña y si se permitir o no su exportación.</span><span class="sxs-lookup"><span data-stu-id="19c9d-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="19c9d-139">Haga clic en **Crear** para guardar el recurso de certificado nuevo.</span><span class="sxs-lookup"><span data-stu-id="19c9d-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="19c9d-140">Para crear un certificado nuevo con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="19c9d-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="19c9d-141">En el ejemplo siguiente se muestra cómo crear un nuevo certificado de Automation y marcarlo como exportable.</span><span class="sxs-lookup"><span data-stu-id="19c9d-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="19c9d-142">Esta acción importa un archivo pfx ya existente.</span><span class="sxs-lookup"><span data-stu-id="19c9d-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="19c9d-143">Uso de un certificado</span><span class="sxs-lookup"><span data-stu-id="19c9d-143">Using a certificate</span></span>

<span data-ttu-id="19c9d-144">Debe utilizar la actividad **Get-AutomationCertificate** para usar un certificado.</span><span class="sxs-lookup"><span data-stu-id="19c9d-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="19c9d-145">No puede usar el cmdlet [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx), debido a que devuelve información sobre el activo de certificado, pero no el certificado mismo.</span><span class="sxs-lookup"><span data-stu-id="19c9d-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="19c9d-146">Ejemplo de runbook de texto</span><span class="sxs-lookup"><span data-stu-id="19c9d-146">Textual runbook sample</span></span>

<span data-ttu-id="19c9d-147">El código de ejemplo siguiente muestra cómo agregar un certificado a un servicio en la nube en un runbook.</span><span class="sxs-lookup"><span data-stu-id="19c9d-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="19c9d-148">En este ejemplo, la contraseña se recupera a partir de una variable de automatización cifrada.</span><span class="sxs-lookup"><span data-stu-id="19c9d-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="19c9d-149">Ejemplo de runbook gráfico</span><span class="sxs-lookup"><span data-stu-id="19c9d-149">Graphical runbook sample</span></span>

<span data-ttu-id="19c9d-150">Para agregar **Get-AutomationCertificate** a un runbook gráfico, haga clic con el botón derecho en el certificado en el panel Biblioteca del editor gráfico y, después, seleccione **Agregar al lienzo**.</span><span class="sxs-lookup"><span data-stu-id="19c9d-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![Adición del certificado al lienzo](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="19c9d-152">La imagen siguiente muestra un ejemplo de cómo usar un certificado en un runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="19c9d-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="19c9d-153">Este es el mismo ejemplo anteriormente mostrado para agregar un certificado a un servicio en la nube desde un runbook textual.</span><span class="sxs-lookup"><span data-stu-id="19c9d-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="19c9d-154">Creación gráfica de ejemplo</span><span class="sxs-lookup"><span data-stu-id="19c9d-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="19c9d-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19c9d-155">Next steps</span></span>

- <span data-ttu-id="19c9d-156">Para obtener más información sobre cómo trabajar con vínculos para controlar el flujo lógico de las actividades que su runbook está diseñado para efectuar, consulte el tema sobre los [vínculos en la creación gráfica](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="19c9d-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
