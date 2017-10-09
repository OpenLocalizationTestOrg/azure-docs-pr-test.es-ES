---
title: "aaaInstall Visual Studio y conéctese tooAzure pila | Documentos de Microsoft"
description: "Obtenga información acerca de los pasos de hello necesarios tooinstall Visual Studio y conéctese tooAzure pila"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: aa63f9eaf5cd72a0b2f31256c2df99fb41ca11fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-connect-tooazure-stack"></a><span data-ttu-id="7de13-103">Instalar Visual Studio y conéctese tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="7de13-103">Install Visual Studio and connect tooAzure Stack</span></span>

<span data-ttu-id="7de13-104">Usar Visual Studio tooauthor e implementar Azure Resource Manager [plantillas](azure-stack-arm-templates.md) en pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7de13-104">Use Visual Studio tooauthor and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) in Azure Stack.</span></span> <span data-ttu-id="7de13-105">Puede utilizar pasos de hello descritos en este tooinstall artículo Visual Studio o desde [Kit de desarrollo de Azure pila](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está conectado a través de [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="7de13-105">You can use hello steps described in this article tooinstall Visual Studio either from [Azure Stack Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are connected through [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span> <span data-ttu-id="7de13-106">Estos pasos crean una nueva instalación de Visual Studio 2015 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="7de13-106">These steps perform a new installation of Visual Studio 2015 Community Edition.</span></span> <span data-ttu-id="7de13-107">Obtenga más información sobre la [coexistencia](https://msdn.microsoft.com/library/ms246609.aspx) de otras versiones de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7de13-107">Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) between other Visual Studio versions.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="7de13-108">Instalación de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7de13-108">Install Visual Studio</span></span>
1. <span data-ttu-id="7de13-109">Descargue y ejecute hello [instalador de plataforma Web](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="7de13-109">Download and run hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>             
2. <span data-ttu-id="7de13-110">Busque **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, haga clic en **Agregar** e **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="7de13-110">Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, click **Add**, and **Install**.</span></span>

    ![Captura de pantalla de los pasos de la instalación de WebPI](./media/azure-stack-install-visual-studio/image1.png) 

3. <span data-ttu-id="7de13-112">Desinstalar hello **Microsoft Azure PowerShell** que se instala como parte del programa Hola a Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="7de13-112">Uninstall hello **Microsoft Azure PowerShell** that is installed as part of hello Azure SDK.</span></span>

    ![Captura de pantalla de la interfaz de agregar o quitar programas para Azure PowerShell](./media/azure-stack-install-visual-studio/image2.png) 

4. <span data-ttu-id="7de13-114">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Instalación de PowerShell para Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="7de13-114">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md)</span></span>

5. <span data-ttu-id="7de13-115">Reinicie el sistema de operativo de hello al finalizar la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7de13-115">Restart hello operating system after hello installation completes.</span></span>

## <a name="connect-tooazure-stack"></a><span data-ttu-id="7de13-116">Conectar tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="7de13-116">Connect tooAzure Stack</span></span>

1. <span data-ttu-id="7de13-117">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7de13-117">Launch Visual Studio.</span></span>

2. <span data-ttu-id="7de13-118">De hello **vista** menú, seleccione **nube explorador**.</span><span class="sxs-lookup"><span data-stu-id="7de13-118">From hello **View** menu, select **Cloud Explorer**.</span></span>

3. <span data-ttu-id="7de13-119">En el nuevo panel de hello, seleccione **Agregar cuenta** e inicie sesión con sus credenciales de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7de13-119">In hello new pane, select **Add Account** and sign in with your Azure Active Directory credentials.</span></span>  
    <span data-ttu-id="7de13-120">![Captura de pantalla del explorador de la nube una vez iniciado la sesión y conectado tooAzure pila](./media/azure-stack-install-visual-studio/image6.png)</span><span class="sxs-lookup"><span data-stu-id="7de13-120">![Screenshot of Cloud Explorer once logged in and connected tooAzure Stack](./media/azure-stack-install-visual-studio/image6.png)</span></span>

<span data-ttu-id="7de13-121">Una vez iniciada la sesión, puede [implementar plantillas](azure-stack-deploy-template-visual-studio.md) o examinar los tipos de recursos disponibles y grupos de recursos toocreate sus propias plantillas.</span><span class="sxs-lookup"><span data-stu-id="7de13-121">Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups toocreate your own templates.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7de13-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7de13-122">Next Steps</span></span>

 - [<span data-ttu-id="7de13-123">Desarrollo de plantillas para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7de13-123">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
