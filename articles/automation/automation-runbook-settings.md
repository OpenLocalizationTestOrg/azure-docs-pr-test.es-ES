---
title: "configuración de aaaRunbook | Documentos de Microsoft"
description: "Describe los valores de configuración de Hola para un runbook en automatización de Azure y cómo toochange con ambos Hola Portal de administración de Azure y Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="4713e-103">Configuración de runbook</span><span class="sxs-lookup"><span data-stu-id="4713e-103">Runbook settings</span></span>
<span data-ttu-id="4713e-104">Cada runbook de automatización de Azure tiene varias opciones de configuración para facilitar su toobe identificado y toochange su comportamiento de registro.</span><span class="sxs-lookup"><span data-stu-id="4713e-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="4713e-105">Cada uno de estos valores se describe a continuación los procedimientos sobre cómo toomodify ellos.</span><span class="sxs-lookup"><span data-stu-id="4713e-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="4713e-106">Settings</span><span class="sxs-lookup"><span data-stu-id="4713e-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="4713e-107">Nombre y descripción</span><span class="sxs-lookup"><span data-stu-id="4713e-107">Name and description</span></span>
<span data-ttu-id="4713e-108">No se puede cambiar nombre de Hola de un runbook una vez creada.</span><span class="sxs-lookup"><span data-stu-id="4713e-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="4713e-109">Hola descripción es opcional y puede ser too512 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4713e-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="4713e-110">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="4713e-110">Tags</span></span>
<span data-ttu-id="4713e-111">Las etiquetas permiten que tooassign diferentes palabras y frases toohelp identifican un runbook.</span><span class="sxs-lookup"><span data-stu-id="4713e-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="4713e-112">Por ejemplo, cuando se envía un runbook toohello [Galería de PowerShell](https://www.powershellgallery.com/), especifique tooidentify etiquetas determinado qué categorías de Hola runbook debe aparecer en.</span><span class="sxs-lookup"><span data-stu-id="4713e-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="4713e-113">Puede especificar varias etiquetas para un runbook separándolas por comas.</span><span class="sxs-lookup"><span data-stu-id="4713e-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="4713e-114">Registro</span><span class="sxs-lookup"><span data-stu-id="4713e-114">Logging</span></span>
<span data-ttu-id="4713e-115">De forma predeterminada, los registros detallado y de progreso no se escriben toojob historial.</span><span class="sxs-lookup"><span data-stu-id="4713e-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="4713e-116">Puede cambiar valores de hello para un runbook determinado toolog estos registros.</span><span class="sxs-lookup"><span data-stu-id="4713e-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="4713e-117">Para obtener más información sobre estos registros, consulte [Salida y mensajes de los runbooks](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="4713e-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="4713e-118">Cambio de la configuración del runbook</span><span class="sxs-lookup"><span data-stu-id="4713e-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="4713e-119">Cambiar la configuración de runbook con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4713e-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="4713e-120">Puede cambiar la configuración de un runbook en hello portal de Azure de hello **configuración** hoja Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="4713e-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="4713e-121">Hola portal de Azure, seleccione **automatización** y, a continuación, haga clic en nombre de Hola de una cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="4713e-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="4713e-122">Seleccione hello **Runbooks** ficha.</span><span class="sxs-lookup"><span data-stu-id="4713e-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="4713e-123">Haga clic en nombre de Hola de un runbook y son toohello dirigido hoja de configuración de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="4713e-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="4713e-124">Desde aquí puede especificar o modificar etiquetas, Hola descripción del runbook, configurar el registro y la configuración de seguimiento y tener acceso a solucionar problemas de compatibilidad con herramientas toohelp.</span><span class="sxs-lookup"><span data-stu-id="4713e-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="4713e-125">Cambio de la configuración del runbook mediante Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4713e-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="4713e-126">Puede usar hello [AzureRmAutomationRunbook conjunto](https://msdn.microsoft.com/library/mt603786.aspx) configuración de cmdlet toochange Hola de un runbook.</span><span class="sxs-lookup"><span data-stu-id="4713e-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="4713e-127">Si desea toospecify varias etiquetas, se puede proporcionar una matriz o una sola cadena con el parámetro de etiquetas de toohello de valores delimitada por comas.</span><span class="sxs-lookup"><span data-stu-id="4713e-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="4713e-128">Puede obtener etiquetas actuales de hello con hello [AzureRmAutomationRunbook Get](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="4713e-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="4713e-129">Hola después de comandos de ejemplo muestra cómo tooset Hola propiedades de un runbook.</span><span class="sxs-lookup"><span data-stu-id="4713e-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="4713e-130">Este ejemplo agrega tres etiquetas toohello existente etiquetas y especifica que se deben registrar registros detallados.</span><span class="sxs-lookup"><span data-stu-id="4713e-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="4713e-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4713e-131">Next steps</span></span>
* <span data-ttu-id="4713e-132">toolearn toocreate y recuperar mensajes de error y de salida de runbooks, vea [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="4713e-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="4713e-133">toounderstand cómo ver un runbook que ya se haya desarrollado por hello Comunidad otro origen o toocreate su propio runbook tooadd [crear o importar un Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="4713e-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

