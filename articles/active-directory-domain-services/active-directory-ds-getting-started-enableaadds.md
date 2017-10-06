---
title: "Azure Active Directory Domain Services: habilitación de Azure Active Directory Domain Services | Microsoft Docs"
description: "Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="b6380-103">Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="b6380-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="b6380-104">Tarea 3: Habilitación de Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="b6380-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="b6380-105">En esta tarea, habilitar Azure Active Directory Domain Services (Azure AD DS) para su directorio haciendo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b6380-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="b6380-106">Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b6380-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b6380-107">En el panel izquierdo de hello, seleccione hello **Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="b6380-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="b6380-108">Seleccione el inquilino de Azure Active Directory (Azure AD) de hello (directorio) que se desea tooenable Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="b6380-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="b6380-110">En hello **directorio de vista previa** página, haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="b6380-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![Pestaña Configurar del directorio](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="b6380-112">En **los servicios de dominio**, cambiar hello **habilitar los servicios de dominio para este directorio** opción demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="b6380-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="b6380-113">Opciones de configuración de servicios de dominio de Active Directory de Azure adicionales aparecen en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6380-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Habilitación de los Servicios de dominio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="b6380-115">Cuando se habilita Azure Servicios de dominio de Active Directory para el inquilino, Azure AD genera y almacena Hola Kerberos y NTLM hashes de credenciales que son necesarios para autenticar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b6380-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="b6380-116">Especificar hello **nombre de dominio DNS de servicios de dominio**.</span><span class="sxs-lookup"><span data-stu-id="b6380-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="b6380-117">nombre de dominio predeterminado de Hello del directorio de hello (con un **. onmicrosoft.com** sufijo) está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b6380-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="b6380-118">Hello lista contiene todos los dominios que se han configurado para su directorio Azure AD, las incluidas comprobado y no comprobados dominios que se configuran en hello **dominios** ficha.</span><span class="sxs-lookup"><span data-stu-id="b6380-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="b6380-119">También puede escribir un nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="b6380-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="b6380-120">En este ejemplo, es el nombre de dominio personalizado de hello *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="b6380-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="b6380-121">prefijo de Hola de su nombre de dominio especificado (por ejemplo, *contoso100* en hello *contoso100.com* nombre de dominio) debe contener 15 caracteres o menos.</span><span class="sxs-lookup"><span data-stu-id="b6380-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="b6380-122">No se puede crear un dominio de Azure Active Directory Domain Services con un prefijo que contenga más de 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b6380-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="b6380-123">Asegúrese de que ha elegido para hello administrado dominio todavía no existe en la red virtual de hello ese nombre de dominio DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6380-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="b6380-124">En concreto, compruebe si toosee:</span><span class="sxs-lookup"><span data-stu-id="b6380-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="b6380-125">Ya tiene un dominio con hello mismo nombre de dominio DNS de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6380-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="b6380-126">Hello red virtual que ha seleccionado no tiene una conexión VPN con la red local y tiene un dominio con hello mismo nombre de dominio DNS de la red local.</span><span class="sxs-lookup"><span data-stu-id="b6380-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="b6380-127">Tiene un servicio en la nube con ese nombre de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6380-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="b6380-128">Seleccione una red virtual en el que desea toobe de servicios de dominio de Active Directory de Azure disponible.</span><span class="sxs-lookup"><span data-stu-id="b6380-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="b6380-129">Seleccione la red virtual de Hola y subred dedicada que creó en hello **toothis de red virtual de servicios de dominio de conectar** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="b6380-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="b6380-130">También tenga en cuenta los siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="b6380-130">Also consider hello following:</span></span>

   * <span data-ttu-id="b6380-131">Asegurarse de esa red virtual de Hola que ha especificado pertenece tooan región de Azure es compatible con servicios de dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6380-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="b6380-132">tooascertain Hola regiones de Azure en servicios de dominio de Active Directory de Azure está disponible, consulte [servicios de Azure por región](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="b6380-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="b6380-133">Redes virtuales que pertenecen región tooa donde no se admite servicios de dominio de Active Directory de Azure no aparecen en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6380-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="b6380-134">Utilice una subred dedicada dentro de la red virtual de Hola para servicios de dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6380-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="b6380-135">Hacer *no* seleccione Hola subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="b6380-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="b6380-136">Consulte las [consideraciones sobre redes](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="b6380-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="b6380-137">De forma similar, las redes virtuales que se crearon mediante el Administrador de recursos de Azure no aparecen en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6380-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="b6380-138">Esto es porque las redes virtuales basadas en Resource Manager no son compatibles de momento con Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="b6380-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="b6380-139">Haga clic en tooenable Azure Active Directory Domain Services, en panel de tareas de hello en parte inferior de Hola de página de hello, **guardar**.</span><span class="sxs-lookup"><span data-stu-id="b6380-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="b6380-140">Mientras los servicios de dominio de Active Directory de Azure está habilitado para el directorio, página de hello muestra un estado de *pendiente*.</span><span class="sxs-lookup"><span data-stu-id="b6380-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Habilitación de la ventana Servicios de dominio](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="b6380-142">Azure Active Directory Domain Services proporciona una alta disponibilidad para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="b6380-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="b6380-143">Después de habilitar servicios de dominio de Active Directory de Azure, direcciones IP de hello en qué dominio de servicios están disponibles en la red virtual de hello son muestran uno a la vez.</span><span class="sxs-lookup"><span data-stu-id="b6380-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="b6380-144">dirección IP de la segunda Hola se muestra en primer lugar, poco después de hello como pronto servicio Hola permite una alta disponibilidad para el dominio.</span><span class="sxs-lookup"><span data-stu-id="b6380-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="b6380-145">Cuando se configura la alta disponibilidad y activo para su dominio, debería ver dos direcciones IP en hello **los servicios de dominio** sección de hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="b6380-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="b6380-146">Después de aproximadamente 20 minutos de too30, primera dirección IP hello en qué dominio de servicios están disponibles en la red virtual en hello **dirección IP** campo hello **configurar** página.</span><span class="sxs-lookup"><span data-stu-id="b6380-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![Ventana de Domain Services que muestra la primera dirección IP aprovisionada](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="b6380-148">Cuando esté en funcionamiento para el dominio de alta disponibilidad, se muestran dos direcciones IP en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6380-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="b6380-149">El dominio administrado está disponible en la red virtual seleccionada en estas dos direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="b6380-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="b6380-150">Tenga en cuenta dos direcciones IP Hola para que pueda actualizar configuración de DNS de hello para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="b6380-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="b6380-151">Si lo hace, permite que las máquinas virtuales en dominio de toohello de tooconnect de red virtual de Hola para operaciones como la unión a un dominio.</span><span class="sxs-lookup"><span data-stu-id="b6380-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![Ventana de Domain Services que muestra ambas direcciones IP aprovisionadas](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="b6380-153">Según el tamaño de hello del inquilino de Azure AD (por ejemplo, el número de Hola de usuarios o grupos), el dominio de sincronización tooyour administrado tarda algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="b6380-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="b6380-154">Este proceso de sincronización se produce en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6380-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="b6380-155">Para inquilinos grandes con decenas de miles de objetos, puede tardar un día o dos para todos los usuarios, las pertenencias a grupos y toobe credenciales sincronizado.</span><span class="sxs-lookup"><span data-stu-id="b6380-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="b6380-156">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="b6380-156">Next step</span></span>
[<span data-ttu-id="b6380-157">Tarea 4: actualizar la configuración de DNS de Hola de hello red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="b6380-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
