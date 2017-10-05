---
title: "Azure Active Directory Domain Services: actualización de la configuración DNS para Azure Virtual Network | Microsoft Docs"
description: "Introducción a Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: c704ee189072ce8ed196d1ef0a23edd528a10025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="bc0f1-103">Habilitación de Azure Active Directory Domain Services (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="bc0f1-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="bc0f1-104">Tarea 4: Actualización de la configuración DNS para la red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="bc0f1-104">Task 4: update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="bc0f1-105">En las tareas de configuración anteriores, ha habilitado correctamente Azure Active Directory Domain Services para el directorio.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="bc0f1-106">La tarea siguiente consiste en asegurarse de que los equipos dentro de la red virtual pueden conectarse y consumir estos servicios.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="bc0f1-107">En este artículo, se actualiza la configuración del servidor DNS de la red virtual para que apunte a las direcciones IP en las que Azure Active Directory Domain Services está disponible en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

<span data-ttu-id="bc0f1-108">Para actualizar la configuración del servidor DNS en la red virtual en la que ha habilitado Azure Active Directory Domain Services, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="bc0f1-108">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="bc0f1-109">En la pestaña **Información general** se muestra un conjunto de **pasos de configuración obligatorios** que se deben realizar después de que el dominio administrado está completamente aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-109">The **Overview** tab lists a set of **Required configuration steps** to be performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="bc0f1-110">El primer paso de configuración es **Actualizar la configuración de servidores DNS de su red virtual**.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-110">The first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services: pestaña Información general después del aprovisionamiento completo](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="bc0f1-112">Cuando el dominio está completamente aprovisionado, se muestran dos direcciones IP en este icono.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="bc0f1-113">Cada una de estas direcciones IP representa un controlador de dominio en el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="bc0f1-114">Para copiar la primera dirección IP en el Portapapeles, haga clic en el botón Copiar que aparece junto a ella.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-114">To copy the first IP address to clipboard, click the copy button next to it.</span></span> <span data-ttu-id="bc0f1-115">A continuación, haga clic en el botón **Configurar servidores DNS**.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-115">Then click the **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="bc0f1-116">Pegue la primera dirección IP en el cuadro de texto **Agregar servidor DNS** de la hoja **Servidores DNS**.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-116">Paste the first IP address into the **Add DNS server** textbox in the **DNS servers** blade.</span></span> <span data-ttu-id="bc0f1-117">Desplácese horizontalmente a la izquierda para copiar la segunda dirección IP y péguela en el cuadro de texto **Agregar servidor DNS**.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-117">Scroll horizontally to the left to copy the second IP address and paste it into the **Add DNS server** textbox.</span></span>

    ![Domain Services: actualización de DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="bc0f1-119">Cuando haya terminado de actualizar los servidores DNS de la red virtual, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-119">Click **Save** when you are done to update the DNS servers for the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="bc0f1-120">Las máquinas virtuales de la red solo obtendrán la nueva configuración DNS después de reiniciarse.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="bc0f1-121">Si necesita tener la configuración de DNS actualizada inmediatamente, desencadene un reinicio mediante el portal, PowerShell o la CLI.</span><span class="sxs-lookup"><span data-stu-id="bc0f1-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="bc0f1-122">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="bc0f1-122">Next step</span></span>
[<span data-ttu-id="bc0f1-123">Tarea 5: Habilitación de la sincronización de contraseñas con Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="bc0f1-123">Task 5: enable password synchronization to Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
