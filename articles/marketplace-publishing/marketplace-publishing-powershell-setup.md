---
title: "aaaSet seguridad PowerShell toocreate una máquina virtual para hello Marketplace | Documentos de Microsoft"
description: "Instrucciones para configurar Azure PowerShell y lo usa como un proceso opcional de flujo de toocreate toodeploy de imágenes de máquina virtual y venden en, hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="868d5-103">Configurar Azure PowerShell toocreate una oferta de hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="868d5-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="868d5-104">Para obtener información detallada acerca de cómo tooset PowerShell de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="868d5-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="868d5-105">Un enfoque sencillo es toouse Hola certificado (método), que descarga e importa un certificado necesario para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="868d5-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="868d5-106">Hola tooobtain necesita certificados, usar hello **Get-AzurePublishSettingsFile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="868d5-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="868d5-107">Guarde el archivo hello cuando se le pida.</span><span class="sxs-lookup"><span data-stu-id="868d5-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="868d5-108">certificado de hello tooimport en una sesión de PowerShell, use hello **importación-AzurePublishSettingsFile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="868d5-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="868d5-109">tooconfigure y almacén Hola comunes Microsoft Azure suscripción de sesión de PowerShell de hello, utilice hello **Set-AzureSubscription** y **Select-AzureSubscription** cmdlets:</span><span class="sxs-lookup"><span data-stu-id="868d5-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="868d5-110">primer comando de Hello asocia una cuenta de almacenamiento predeterminada con suscripción de hello (necesario para algunas operaciones de aprovisionamiento de VM).</span><span class="sxs-lookup"><span data-stu-id="868d5-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="868d5-111">en segundo lugar, Hola hace suscripción Hola Hola uno actual (reconocido por otros cmdlets).</span><span class="sxs-lookup"><span data-stu-id="868d5-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="868d5-112">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="868d5-112">See also</span></span>
* [<span data-ttu-id="868d5-113">Introducción: cómo toopublish una toohello de oferta de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="868d5-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="868d5-114">Crear una imagen de máquina virtual para hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="868d5-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

