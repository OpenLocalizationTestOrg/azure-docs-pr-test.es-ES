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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="f2d0e-103">Actualizar la configuración de DNS para hello red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="f2d0e-103">Update DNS settings for hello Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="f2d0e-104">Tarea 4: Actualizar valores de DNS para hello red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="f2d0e-104">Task 4: Update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="f2d0e-105">Hola anterior tareas de configuración, ha habilitado correctamente Azure Servicios de dominio de Active Directory para su directorio.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="f2d0e-106">Hola siguiente tarea es tooensure que los equipos de red virtual de hello pueden conectarse y usar estos servicios.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="f2d0e-107">En este artículo, se actualiza la configuración de servidor DNS de Hola para sus red virtual toopoint toohello dos direcciones IP en servicios de dominio de Active Directory de Azure está disponible en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="f2d0e-108">Después de habilitar Azure Servicios de dominio de Active Directory para el directorio de hello, tenga en cuenta las direcciones IP Hola para Azure Active Directory Domain Services que se muestran en hello **configurar** pestaña del directorio.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-108">After you've enabled Azure Active Directory Domain Services for hello directory, note hello IP addresses for Azure Active Directory Domain Services that are displayed on hello **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="f2d0e-109">configuración de servidor de tooupdate Hola DNS para la red virtual de hello en el que ha habilitado Azure Active Directory Domain Services, completa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f2d0e-109">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="f2d0e-110">Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f2d0e-110">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f2d0e-111">En el panel izquierdo de hello, seleccione **redes**.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-111">In hello left pane, select **Networks**.</span></span>  
    <span data-ttu-id="f2d0e-112">Hola **redes** abre la ventana.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-112">hello **Networks** window opens.</span></span>

    ![Ventana Redes virtuales](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="f2d0e-114">En hello **redes virtuales** ficha, en el que ha habilitado Servicios de dominio de Active Directory de Azure tooview sus propiedades de red virtual seleccione Hola.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-114">On hello **Virtual Networks** tab, select hello virtual network in which you enabled Azure Active Directory Domain Services tooview its properties.</span></span>
4. <span data-ttu-id="f2d0e-115">Haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-115">Click hello **Configure** tab.</span></span>

    ![Ventana Redes virtuales](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="f2d0e-117">Hola **servidores DNS** sección, escriba dos direcciones IP de Hola que se mostraron en hello **los servicios de dominio** sección en hello **configurar** pestaña del directorio.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-117">In hello **DNS servers** section, enter both of hello IP addresses that were displayed in hello **Domain Services** section on hello **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="f2d0e-118">Haga clic en configuración del servidor DNS toosave Hola para esta red virtual, en panel de tareas de hello en parte inferior de Hola de ventana hello, **guardar**.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-118">toosave hello DNS server settings for this virtual network, in hello task pane at hello bottom of hello window, click **Save**.</span></span>

   ![Actualizar la configuración de servidor DNS de hello para la red virtual de Hola](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="f2d0e-120">Máquinas virtuales de red de hello solo obtiene la configuración de DNS nueva de hello después del reinicio.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="f2d0e-121">Si necesita configuración DNS de tooget Hola actualiza inmediatamente, desencadenar un reinicio del portal de hello, PowerShell u Hola CLI.</span><span class="sxs-lookup"><span data-stu-id="f2d0e-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f2d0e-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2d0e-122">Next steps</span></span>
<span data-ttu-id="f2d0e-123">Tarea 5: [habilitar la sincronización de contraseña tooAzure los servicios de dominio de Active Directory](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="f2d0e-123">Task 5: [Enable password synchronization tooAzure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
