---
title: 'Azure Active Directory Domain Services: Habilitar la compatibilidad con el servicio de perfil de usuario de SharePoint | Microsoft Docs'
description: "Configuración de dominios administrados de Azure Active Directory Domain Services para admitir la sincronización de perfiles para SharePoint Server"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: c3c923b5c9cd652f0c5b0ec98c1cda740f180122
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="47e81-103">Configuración de un dominio administrado para admitir la sincronización de perfiles para SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="47e81-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="47e81-104">SharePoint Server incluye un servicio de perfiles de usuario que se usa para la sincronización de perfiles de usuario.</span><span class="sxs-lookup"><span data-stu-id="47e81-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="47e81-105">Para configurar el servicio de perfiles de usuario, es necesario conceder los permisos apropiados en un dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="47e81-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="47e81-106">Para más información, vea [Concesión de permisos de Active Directory Domain Services para la sincronización de perfiles en SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="47e81-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="47e81-107">En este artículo se explica cómo configurar dominios administrados de Azure AD Domain Services para implementar el servicio de sincronización de perfiles de usuario de SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="47e81-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="47e81-108">El grupo “Cuentas de servicio de controlador de dominio de AAD”</span><span class="sxs-lookup"><span data-stu-id="47e81-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="47e81-109">Un grupo de seguridad denominado “**Cuentas de servicio de controlador de dominio de AAD**” está disponible en la unidad organizativa “Usuarios” en el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="47e81-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="47e81-110">Puede ver este grupo en el complemento MMC **Usuarios y equipos de Active Directory**  del dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="47e81-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Grupo de seguridad Cuentas de servicio de controlador de dominio de AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="47e81-112">A los miembros de este grupo de seguridad se les delegan los privilegios siguientes:</span><span class="sxs-lookup"><span data-stu-id="47e81-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="47e81-113">El privilegio “Replicación de cambios de directorio” en el atributo DSE raíz del dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="47e81-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="47e81-114">El privilegio “Replicación de cambios de directorio” en el contexto de nomenclatura de configuración (cn = contenedor de configuración) del dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="47e81-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="47e81-115">Este grupo de seguridad también es un miembro del grupo integrado **Acceso de compatible con versiones anteriores de Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="47e81-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Grupo de seguridad Cuentas de servicio de controlador de dominio de AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="47e81-117">Permitir que el dominio administrado admita la sincronización de perfiles de usuario de SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="47e81-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="47e81-118">Puede agregar la cuenta de servicio usada para la sincronización de perfiles de usuario de SharePoint para el grupo **Cuentas de servicio de controlador de dominio de AAD**.</span><span class="sxs-lookup"><span data-stu-id="47e81-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="47e81-119">Como resultado, la cuenta de sincronización obtiene los privilegios adecuados para replicar los cambios en el directorio.</span><span class="sxs-lookup"><span data-stu-id="47e81-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="47e81-120">Este paso de configuración permite que la sincronización de perfiles de usuario de SharePoint Server funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="47e81-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![Cuentas de servicio de controlador de dominio de AAD - Agregar miembros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Cuentas de servicio de controlador de dominio de AAD - Agregar miembros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="47e81-123">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="47e81-123">Related Content</span></span>
* [<span data-ttu-id="47e81-124">Referencia técnica - Concesión de permisos de Active Directory Domain Services para la sincronización de perfiles en SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="47e81-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
