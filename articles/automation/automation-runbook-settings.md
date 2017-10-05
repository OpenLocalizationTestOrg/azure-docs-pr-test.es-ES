---
title: "Configuración de runbooks | Microsoft Docs"
description: "Describe las opciones de configuración para un runbook en Automatización de Azure y cómo cambiarlas mediante el Portal de administración de Azure y Windows PowerShell."
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
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="045cf-103">Configuración de runbook</span><span class="sxs-lookup"><span data-stu-id="045cf-103">Runbook settings</span></span>
<span data-ttu-id="045cf-104">Cada runbook en Automatización de Azure tiene varias opciones de configuración para ayudarle a identificar y cambiar su comportamiento de registro.</span><span class="sxs-lookup"><span data-stu-id="045cf-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="045cf-105">A continuación se describen todas estas opciones, seguido de procedimientos acerca de cómo modificarlas.</span><span class="sxs-lookup"><span data-stu-id="045cf-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="045cf-106">Settings</span><span class="sxs-lookup"><span data-stu-id="045cf-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="045cf-107">Nombre y descripción</span><span class="sxs-lookup"><span data-stu-id="045cf-107">Name and description</span></span>
<span data-ttu-id="045cf-108">No se puede cambiar el nombre de un runbook después de su creación.</span><span class="sxs-lookup"><span data-stu-id="045cf-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="045cf-109">La descripción es opcional y puede tener hasta 512 caracteres.</span><span class="sxs-lookup"><span data-stu-id="045cf-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="045cf-110">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="045cf-110">Tags</span></span>
<span data-ttu-id="045cf-111">Las etiquetas permiten asignar diferentes palabras y frases para ayudar a identificar un runbook.</span><span class="sxs-lookup"><span data-stu-id="045cf-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="045cf-112">Por ejemplo, cuando se envía un runbook a la [Galería de PowerShell](https://www.powershellgallery.com/), se especifican etiquetas determinadas para identificar qué categorías deben aparecer en el runbook.</span><span class="sxs-lookup"><span data-stu-id="045cf-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="045cf-113">Puede especificar varias etiquetas para un runbook separándolas por comas.</span><span class="sxs-lookup"><span data-stu-id="045cf-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="045cf-114">Registro</span><span class="sxs-lookup"><span data-stu-id="045cf-114">Logging</span></span>
<span data-ttu-id="045cf-115">De forma predeterminada, los registros detallados y de progreso no se escriben en el historial de trabajos.</span><span class="sxs-lookup"><span data-stu-id="045cf-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="045cf-116">Puede cambiar la configuración de un runbook determinado para estas entradas de registro.</span><span class="sxs-lookup"><span data-stu-id="045cf-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="045cf-117">Para obtener más información sobre estos registros, consulte [Salida y mensajes de los runbooks](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="045cf-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="045cf-118">Cambio de la configuración del runbook</span><span class="sxs-lookup"><span data-stu-id="045cf-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="045cf-119">Cambio de la configuración del runbook mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="045cf-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="045cf-120">Puede cambiar la configuración de un runbook en Azure Portal en la hoja **Configuración** del runbook.</span><span class="sxs-lookup"><span data-stu-id="045cf-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="045cf-121">En el Portal de Azure, seleccione **Automatización** y, a continuación, haga clic en el nombre de una cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="045cf-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="045cf-122">Seleccione la pestaña **Runbooks** .</span><span class="sxs-lookup"><span data-stu-id="045cf-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="045cf-123">Haga clic en el nombre de un runbook y se le redirigirá a la hoja de configuración del runbook.</span><span class="sxs-lookup"><span data-stu-id="045cf-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="045cf-124">Aquí podrá especificar o modificar etiquetas, la descripción del runbook, configurar opciones de seguimiento y registro, y acceder herramientas de soporte técnico para ayudarlo a solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="045cf-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="045cf-125">Cambio de la configuración del runbook mediante Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="045cf-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="045cf-126">Puede utilizar el cmdlet [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) para cambiar la configuración de un runbook.</span><span class="sxs-lookup"><span data-stu-id="045cf-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="045cf-127">Si desea especificar varias etiquetas, se puede proporcionar una matriz o una sola cadena con valores delimitados por comas al parámetro Tags.</span><span class="sxs-lookup"><span data-stu-id="045cf-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="045cf-128">Puede obtener las etiquetas actuales con el [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="045cf-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="045cf-129">Los siguientes comandos de ejemplo muestran cómo establecer las propiedades de un runbook.</span><span class="sxs-lookup"><span data-stu-id="045cf-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="045cf-130">Este ejemplo agrega tres etiquetas a las etiquetas existentes y especifica que se deben registrar registros detallados.</span><span class="sxs-lookup"><span data-stu-id="045cf-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="045cf-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="045cf-131">Next steps</span></span>
* <span data-ttu-id="045cf-132">Para aprender a crear y recuperar los mensajes de salida y de error de los runbooks, consulte [Salida y mensajes de los runbooks](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="045cf-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="045cf-133">Para saber cómo agregar un runbook que ya haya desarrollado la Comunidad u otro medio, o para crear sus propios runbooks, consulte [Creación o importación de un runbook](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="045cf-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

