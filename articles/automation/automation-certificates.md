---
title: "aaaCertificate activos de automatización de Azure | Documentos de Microsoft"
description: "Certificados se pueden almacenar de forma segura en automatización de Azure para que se pueden obtener acceso por runbooks o tooauthenticate de configuraciones de DSC en Azure y recursos de otros fabricantes.  En este artículo se explica los detalles de Hola de certificados y cómo toowork con ellos en la creación gráfica y textual."
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
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="2f301-104">Activos de certificados en Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="2f301-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="2f301-105">Certificados pueden ser almacenados de forma segura en automatización de Azure para que se pueden obtener acceso por runbooks o configuraciones de DSC mediante hello **AzureRmAutomationRmCertificate Get** actividad para los recursos de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2f301-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="2f301-106">Esto le permite toocreate runbooks y las configuraciones de DSC que usan certificados para la autenticación o agrega recursos tooAzure o de terceros.</span><span class="sxs-lookup"><span data-stu-id="2f301-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="2f301-107">Los recursos protegidos en Automatización de Azure incluyen credenciales, certificados, conexiones y variables cifradas.</span><span class="sxs-lookup"><span data-stu-id="2f301-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="2f301-108">Estos activos se cifran y almacenan en hello automatización de Azure mediante una clave única que se genera para cada cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="2f301-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="2f301-109">Esta clave se cifra mediante un certificado maestro y se almacena en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f301-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="2f301-110">Antes de almacenar un recurso seguro, clave de hello para la cuenta de automatización de Hola se descifra mediante certificado maestro hello y, a continuación, utilice activos de hello tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="2f301-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="2f301-111">Cmdlets de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f301-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="2f301-112">cmdlets de Hello en hello en la tabla siguiente son toocreate usado y administrar recursos de certificado de automatización con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f301-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="2f301-113">Se incluyen como parte del programa Hola a [módulo Azure PowerShell](../powershell-install-configure.md) que está disponible para su uso en runbooks de automatización y las configuraciones de DSC.</span><span class="sxs-lookup"><span data-stu-id="2f301-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="2f301-114">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="2f301-114">Cmdlets</span></span>|<span data-ttu-id="2f301-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f301-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="2f301-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="2f301-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="2f301-117">Recupera información sobre una toouse de certificado en un runbook o la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="2f301-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="2f301-118">Solo puede recuperar el propio certificado Hola de actividad de Get-AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="2f301-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="2f301-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="2f301-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="2f301-120">Crea un certificado nuevo en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="2f301-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="2f301-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="2f301-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="2f301-122">Quita un certificado a Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f301-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="2f301-123">Crea un certificado nuevo en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="2f301-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="2f301-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="2f301-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="2f301-125">Establece las propiedades de Hola de un certificado existente, incluidas la carga de archivo de certificado de hello y establecer la contraseña para un .pfx Hola.</span><span class="sxs-lookup"><span data-stu-id="2f301-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="2f301-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="2f301-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="2f301-127">Cargas de un servicio de certificados para hello especifican servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="2f301-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="2f301-128">Creación de un certificado nuevo</span><span class="sxs-lookup"><span data-stu-id="2f301-128">Creating a new certificate</span></span>

<span data-ttu-id="2f301-129">Cuando se crea un nuevo certificado, cargue un archivo .cer o .pfx tooAzure automatización.</span><span class="sxs-lookup"><span data-stu-id="2f301-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="2f301-130">Si marca certificado hello como exportable, puede transferir fuera del almacén de certificados de automatización de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="2f301-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="2f301-131">Si no es exportable, a continuación, solo se puede utilizar para firmar dentro de runbook de Hola o configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="2f301-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="2f301-132">toocreate un nuevo certificado con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2f301-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="2f301-133">En su cuenta de automatización, haga clic en hello **activos** icono tooopen hello **activos** hoja.</span><span class="sxs-lookup"><span data-stu-id="2f301-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="2f301-134">Haga clic en hello **certificados** icono tooopen hello **certificados** hoja.</span><span class="sxs-lookup"><span data-stu-id="2f301-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="2f301-135">Haga clic en **agregar un certificado** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f301-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="2f301-136">Escriba un nombre para el certificado de Hola Hola **nombre** cuadro.</span><span class="sxs-lookup"><span data-stu-id="2f301-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="2f301-137">Haga clic en **seleccionar un archivo** en **cargar un archivo de certificado** toobrowse para un archivo .cer o .pfx.</span><span class="sxs-lookup"><span data-stu-id="2f301-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="2f301-138">Si selecciona un archivo .pfx, especifique una contraseña y si debe permitirse toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="2f301-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="2f301-139">Haga clic en **crear** toosave Hola nuevo certificado activo.</span><span class="sxs-lookup"><span data-stu-id="2f301-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="2f301-140">toocreate un nuevo certificado con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f301-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="2f301-141">Hello ejemplo siguiente se muestra cómo toocreate una automatización nueva de certificados y marcarla exportable.</span><span class="sxs-lookup"><span data-stu-id="2f301-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="2f301-142">Esta acción importa un archivo pfx ya existente.</span><span class="sxs-lookup"><span data-stu-id="2f301-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="2f301-143">Uso de un certificado</span><span class="sxs-lookup"><span data-stu-id="2f301-143">Using a certificate</span></span>

<span data-ttu-id="2f301-144">Debe usar hello **Get-AutomationCertificate** toouse actividad un certificado.</span><span class="sxs-lookup"><span data-stu-id="2f301-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="2f301-145">No se puede usar hello [AzureRmAutomationCertificate Get](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet debido a que devuelve información sobre el activo de certificado de hello, pero no Hola propio certificado.</span><span class="sxs-lookup"><span data-stu-id="2f301-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="2f301-146">Ejemplo de runbook de texto</span><span class="sxs-lookup"><span data-stu-id="2f301-146">Textual runbook sample</span></span>

<span data-ttu-id="2f301-147">Hola siguiendo el ejemplo de código muestra cómo el servicio en un runbook de la nube de tooadd un tooa de certificado.</span><span class="sxs-lookup"><span data-stu-id="2f301-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="2f301-148">En este ejemplo, contraseña de Hola se recupera de una variable de automatización cifrada.</span><span class="sxs-lookup"><span data-stu-id="2f301-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="2f301-149">Ejemplo de runbook gráfico</span><span class="sxs-lookup"><span data-stu-id="2f301-149">Graphical runbook sample</span></span>

<span data-ttu-id="2f301-150">Agrega un **Get-AutomationCertificate** tooa un runbook gráfico con el botón secundario en hello en el certificado Hola biblioteca panel del editor gráfico de Hola y seleccionando **agregar toocanvas**.</span><span class="sxs-lookup"><span data-stu-id="2f301-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![Agregar certificado toohello lienzo](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="2f301-152">Hello siguiente imagen muestra un ejemplo del uso de un certificado en un runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="2f301-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="2f301-153">Se trata de hello mismo ejemplo expuesto anteriormente para agregar un servicio de nube de tooa de certificado desde un runbook textual.</span><span class="sxs-lookup"><span data-stu-id="2f301-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="2f301-154">Creación gráfica de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2f301-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="2f301-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f301-155">Next steps</span></span>

- <span data-ttu-id="2f301-156">toolearn más sobre cómo trabajar con un flujo lógico Hola de vínculos toocontrol de actividades del runbook está diseñado tooperform, consulte [vínculos de edición gráfica](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="2f301-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
