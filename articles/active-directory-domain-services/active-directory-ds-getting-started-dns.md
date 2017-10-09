---
title: "Azure Active Directory Domain Services: Actualizar configuración de DNS para hello red virtual de Azure | Documentos de Microsoft"
description: "Introducción a los Servicios de dominio de Azure Active Directory"
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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="2865d-103">Habilitación de Azure Active Directory Domain Services (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="2865d-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="2865d-104">Tarea 4: actualizar la configuración de DNS para hello red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="2865d-104">Task 4: update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="2865d-105">Hola anterior tareas de configuración, ha habilitado correctamente Azure Servicios de dominio de Active Directory para su directorio.</span><span class="sxs-lookup"><span data-stu-id="2865d-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="2865d-106">Hola siguiente tarea es tooensure que los equipos de red virtual de hello pueden conectarse y usar estos servicios.</span><span class="sxs-lookup"><span data-stu-id="2865d-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="2865d-107">En este artículo, se actualiza la configuración de servidor DNS de Hola para sus red virtual toopoint toohello dos direcciones IP en servicios de dominio de Active Directory de Azure está disponible en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2865d-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

<span data-ttu-id="2865d-108">configuración de servidor de tooupdate Hola DNS para la red virtual de hello en el que ha habilitado Azure Active Directory Domain Services, completa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2865d-108">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="2865d-109">Hola **Introducción** ficha enumera un conjunto de **requiere pasos de configuración** toobe realiza después de que el dominio administrado está aprovisionado por completo.</span><span class="sxs-lookup"><span data-stu-id="2865d-109">hello **Overview** tab lists a set of **Required configuration steps** toobe performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="2865d-110">es el primer paso de configuración Hello **configuración del servidor DNS de la actualización de la red virtual**.</span><span class="sxs-lookup"><span data-stu-id="2865d-110">hello first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services: pestaña Información general después del aprovisionamiento completo](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="2865d-112">Cuando el dominio está completamente aprovisionado, se muestran dos direcciones IP en este icono.</span><span class="sxs-lookup"><span data-stu-id="2865d-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="2865d-113">Cada una de estas direcciones IP representa un controlador de dominio en el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="2865d-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="2865d-114">toocopy Hola primera dirección IP tooclipboard de direcciones, haga clic en botón de copia hello tooit siguiente.</span><span class="sxs-lookup"><span data-stu-id="2865d-114">toocopy hello first IP address tooclipboard, click hello copy button next tooit.</span></span> <span data-ttu-id="2865d-115">A continuación, haga clic en hello **servidores DNS configurar** botón.</span><span class="sxs-lookup"><span data-stu-id="2865d-115">Then click hello **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="2865d-116">Pegue la dirección IP de la primera hello en hello **servidor DNS agregar** cuadro de texto en hello **servidores DNS** hoja.</span><span class="sxs-lookup"><span data-stu-id="2865d-116">Paste hello first IP address into hello **Add DNS server** textbox in hello **DNS servers** blade.</span></span> <span data-ttu-id="2865d-117">Desplazarse horizontalmente toohello dejado la segunda dirección IP de toocopy hello y pegarlos en hello **servidor DNS agregar** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="2865d-117">Scroll horizontally toohello left toocopy hello second IP address and paste it into hello **Add DNS server** textbox.</span></span>

    ![Domain Services: actualización de DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="2865d-119">Haga clic en **guardar** cuando haya terminado los servidores DNS de tooupdate hello para la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2865d-119">Click **Save** when you are done tooupdate hello DNS servers for hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="2865d-120">Máquinas virtuales de red de hello solo obtiene la configuración de DNS nueva de hello después del reinicio.</span><span class="sxs-lookup"><span data-stu-id="2865d-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="2865d-121">Si necesita configuración DNS de tooget Hola actualiza inmediatamente, desencadenar un reinicio del portal de hello, PowerShell u Hola CLI.</span><span class="sxs-lookup"><span data-stu-id="2865d-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="2865d-122">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="2865d-122">Next step</span></span>
[<span data-ttu-id="2865d-123">Tarea 5: habilitar la sincronización de contraseña tooAzure los servicios de dominio de Active Directory</span><span class="sxs-lookup"><span data-stu-id="2865d-123">Task 5: enable password synchronization tooAzure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
