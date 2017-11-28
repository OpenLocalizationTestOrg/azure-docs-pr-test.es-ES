---
title: toouse de red virtual de Azure de hello aaaValidate con Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomake seguro de que la red virtual de Azure está lista toouse con Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="0a558-103">Validar hello toouse de red virtual de Azure con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0a558-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0a558-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="0a558-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0a558-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0a558-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0a558-106">Antes de usar una red virtual de Azure con Azure RemoteApp, conviene toovalidate Hola red virtual.</span><span class="sxs-lookup"><span data-stu-id="0a558-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="0a558-107">Esto ayuda a evitar problemas con la conectividad.</span><span class="sxs-lookup"><span data-stu-id="0a558-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="0a558-108">toovalidate su red virtual de Azure, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="0a558-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="0a558-109">Crear una máquina virtual dentro de la subred Hola de hello red virtual de Azure que desee toouse con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0a558-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="0a558-110">Conectar toothat VM mediante el uso de hello **conectar** opción en el portal de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a558-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="0a558-111">Unir toohello de máquina virtual de hello mismo dominio que desea que toouse con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0a558-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="0a558-112">Si va a crear una colección híbrida que se conecta la red local de tooyour, unirse al dominio local de tooyour de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a558-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="0a558-113">Si esto se realiza correctamente, Hola red virtual de Azure es toouse listo con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0a558-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="0a558-114">Para obtener más información acerca de flujo de trabajo de recopilación de hello híbrida to-end, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="0a558-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="0a558-115">¿Cómo tooplan la red virtual de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0a558-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="0a558-116">Creación de una colección híbrida</span><span class="sxs-lookup"><span data-stu-id="0a558-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="0a558-117">Implementar Azure RemoteApp colección tooyour red Virtual de Azure (con compatibilidad para ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="0a558-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

