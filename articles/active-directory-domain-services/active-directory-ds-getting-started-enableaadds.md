---
title: "Azure Active Directory Domain Services: habilitación de Azure Active Directory Domain Services | Microsoft Docs"
description: "Habilitación de Azure Active Directory Domain Services mediante el Portal de Azure clásico"
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
ms.openlocfilehash: ed72325ca9db99405c6173eb882a92f80cd77f47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="d92dc-103">Habilitación de Azure Active Directory Domain Services mediante el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="d92dc-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="d92dc-104">Tarea 3: Habilitación de Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="d92dc-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="d92dc-105">En esta tarea, habilitará Azure Active Directory Domain Services (Azure AD DS) para su directorio mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d92dc-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing the following steps:</span></span>

1. <span data-ttu-id="d92dc-106">Vaya al [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d92dc-106">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d92dc-107">En el panel izquierdo, seleccione el botón **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d92dc-107">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="d92dc-108">Seleccione el inquilino (directorio) de Azure Active Directory para el que quiere habilitar Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="d92dc-108">Select the Azure Active Directory (Azure AD) tenant (directory) for which you want to enable Azure AD DS.</span></span>

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="d92dc-110">En la página de **directorio de vista previa**, haga clic en la pestaña **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="d92dc-110">On the **preview directory** page, click the **Configure** tab.</span></span>

    ![Pestaña Configurar del directorio](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="d92dc-112">En **servicios de dominio**, cambie la opción **Habilitar Servicios de dominio para este directorio** a **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d92dc-112">Under **domain services**, change the **Enable domain services for this directory** option to **Yes**.</span></span>  
    <span data-ttu-id="d92dc-113">Aparecerán en la página opciones de configuración adicionales de Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d92dc-113">Additional Azure Active Directory Domain Services configuration options appear on the page.</span></span>

    ![Habilitación de los Servicios de dominio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="d92dc-115">Al habilitar Azure Active Directory Domain Services para el inquilino, Azure AD genera y almacena los valores de hash de credenciales de Kerberos y NTLM que son necesarios para autenticar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d92dc-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores the Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="d92dc-116">Especifique el **Nombre de dominio DNS de Servicios de dominio**.</span><span class="sxs-lookup"><span data-stu-id="d92dc-116">Specify the **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="d92dc-117">De forma predeterminada, se selecciona el nombre de dominio predeterminado del directorio (con el sufijo **.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="d92dc-117">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="d92dc-118">La lista contiene todos los dominios que se han configurado para el directorio de Azure AD, incluidos también los dominios comprobados y sin comprobar que configura en la pestaña **Dominios**.</span><span class="sxs-lookup"><span data-stu-id="d92dc-118">The list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on the **Domains** tab.</span></span>

   * <span data-ttu-id="d92dc-119">También puede escribir un nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="d92dc-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="d92dc-120">En este ejemplo, el nombre de dominio personalizado es *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="d92dc-120">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="d92dc-121">El prefijo del nombre de dominio especificado (por ejemplo, *contoso100* en el nombre de dominio *contoso100.com*) debe contener 15 caracteres o menos.</span><span class="sxs-lookup"><span data-stu-id="d92dc-121">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="d92dc-122">No se puede crear un dominio de Azure Active Directory Domain Services con un prefijo que contenga más de 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d92dc-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="d92dc-123">Asegúrese de que el nombre de dominio DNS que ha elegido para el dominio administrado no existe ya en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="d92dc-123">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="d92dc-124">En concreto, compruebe si:</span><span class="sxs-lookup"><span data-stu-id="d92dc-124">Specifically, check to see whether:</span></span>

   * <span data-ttu-id="d92dc-125">Ya tiene un dominio con el mismo nombre de dominio DNS en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="d92dc-125">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="d92dc-126">Si la red virtual que ha seleccionado tiene una conexión VPN con la red local y tiene un dominio con el mismo nombre de dominio DNS en la red local.</span><span class="sxs-lookup"><span data-stu-id="d92dc-126">The virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="d92dc-127">Si ya dispone de un servicio en la nube con ese nombre en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="d92dc-127">You have an existing cloud service with that name on the virtual network.</span></span>
8. <span data-ttu-id="d92dc-128">Seleccione una red virtual en la que desee que Azure Active Directory Domain Services esté disponible.</span><span class="sxs-lookup"><span data-stu-id="d92dc-128">Select a virtual network on which you want Azure Active Directory Domain Services to be available.</span></span> <span data-ttu-id="d92dc-129">Seleccione la red virtual y la subred dedicada que ha creado en la lista desplegable **Conectar Servicios de dominio a esta red virtual**.</span><span class="sxs-lookup"><span data-stu-id="d92dc-129">Select the virtual network and dedicated subnet you created in the **Connect domain services to this virtual network** drop-down list.</span></span> <span data-ttu-id="d92dc-130">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d92dc-130">Also consider the following:</span></span>

   * <span data-ttu-id="d92dc-131">Asegúrese de que la red virtual que ha especificado pertenece a una región de Azure compatible con Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d92dc-131">Ensure that the virtual network that you have specified belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d92dc-132">Consulte la página [Servicios de Azure por región](https://azure.microsoft.com/regions/#services/) para saber en qué regiones de Azure está disponible Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d92dc-132">To ascertain the Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="d92dc-133">Las redes virtuales que pertenecen a una región donde no se admite Azure Active Directory Domain Services no aparecerán en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="d92dc-133">Virtual networks that belong to a region where Azure Active Directory Domain Services is not supported do not show up in the drop-down list.</span></span>

   * <span data-ttu-id="d92dc-134">Utilice una subred dedicada en la red virtual para Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d92dc-134">Use a dedicated subnet within the virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d92dc-135">*No* seleccione la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="d92dc-135">Do *not* select the gateway subnet.</span></span> <span data-ttu-id="d92dc-136">Consulte las [consideraciones sobre redes](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="d92dc-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="d92dc-137">De igual forma, las redes virtuales que se crearon mediante Azure Resource Manager no aparecerán en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="d92dc-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in the drop-down list.</span></span> <span data-ttu-id="d92dc-138">Esto es porque las redes virtuales basadas en Resource Manager no son compatibles de momento con Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d92dc-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="d92dc-139">Para habilitar Azure Active Directory Domain Services, haga clic en **Guardar** en el panel de tareas de la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="d92dc-139">To enable Azure Active Directory Domain Services, in the task pane at the bottom of the page, click **Save**.</span></span>
    * <span data-ttu-id="d92dc-140">Durante el proceso de habilitación de Azure Active Directory Domain Services para el directorio, la página muestra un estado de *Pendiente*.</span><span class="sxs-lookup"><span data-stu-id="d92dc-140">While Azure Active Directory Domain Services is being enabled for your directory, the page displays a status of *Pending*.</span></span>

        ![Habilitación de la ventana Servicios de dominio](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="d92dc-142">Azure Active Directory Domain Services proporciona una alta disponibilidad para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="d92dc-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="d92dc-143">Después de habilitar Azure Active Directory Domain Services, las direcciones IP en las que están disponibles los servicios de dominio en la red virtual se muestran de una en una.</span><span class="sxs-lookup"><span data-stu-id="d92dc-143">After you enable Azure Active Directory Domain Services, the IP addresses at which domain services are available on the virtual network are displayed one at a time.</span></span> <span data-ttu-id="d92dc-144">La segunda dirección IP se muestra poco después de la primera, en cuanto el servicio habilita la alta disponibilidad para el dominio.</span><span class="sxs-lookup"><span data-stu-id="d92dc-144">The second IP address is displayed shortly after the first, as soon the service enables high availability for your domain.</span></span> <span data-ttu-id="d92dc-145">Cuando se configura la alta disponibilidad y está activa para su dominio, debe ver dos direcciones IP en la sección **Servicios de dominio**de la pestaña **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="d92dc-145">When high availability is configured and active for your domain, you should see two IP addresses in the **domain services** section of the **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="d92dc-146">Al cabo de unos 20 o 30 minutos, verá la primera dirección IP en la que Domain Services está disponible en la red virtual, en el campo **Dirección IP** de la página **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="d92dc-146">After about 20 to 30 minutes, the first IP address at which domain services are available on your virtual network in the **IP address** field on the **Configure** page.</span></span>

        ![Ventana de Domain Services que muestra la primera dirección IP aprovisionada](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="d92dc-148">Cuando la alta disponibilidad está operativa para el dominio, aparecen dos direcciones IP en la página.</span><span class="sxs-lookup"><span data-stu-id="d92dc-148">When high availability is operational for your domain, two IP addresses are displayed on the page.</span></span> <span data-ttu-id="d92dc-149">El dominio administrado está disponible en la red virtual seleccionada en estas dos direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="d92dc-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="d92dc-150">Anote las dos direcciones IP para que pueda actualizar la configuración de DNS de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="d92dc-150">Note the two IP addresses so that you can update the DNS settings for your virtual network.</span></span> <span data-ttu-id="d92dc-151">Con ello permite a las máquinas virtuales de la red virtual conectarse al dominio de cara para realizar operaciones como unirse a un dominio.</span><span class="sxs-lookup"><span data-stu-id="d92dc-151">Doing so enables virtual machines on the virtual network to connect to the domain for operations such as domain join.</span></span>

    ![Ventana de Domain Services que muestra ambas direcciones IP aprovisionadas](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="d92dc-153">En función del tamaño del inquilino de Azure AD (número de usuarios, grupos, etc.), la sincronización con el dominio administrado llevará tiempo.</span><span class="sxs-lookup"><span data-stu-id="d92dc-153">Depending on the size of your Azure AD tenant (for example, the number of users or groups), synchronization to your managed domain takes a while.</span></span> <span data-ttu-id="d92dc-154">Este proceso de sincronización se produce en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="d92dc-154">This synchronization process happens in the background.</span></span> <span data-ttu-id="d92dc-155">En el caso de inquilinos grandes con decenas de miles de objetos, se puede tardar uno o dos días en sincronizar todos los usuarios, pertenencias a grupos y credenciales.</span><span class="sxs-lookup"><span data-stu-id="d92dc-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials to be synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="d92dc-156">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="d92dc-156">Next step</span></span>
[<span data-ttu-id="d92dc-157">Tarea 4: Actualización de la configuración DNS en Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="d92dc-157">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
