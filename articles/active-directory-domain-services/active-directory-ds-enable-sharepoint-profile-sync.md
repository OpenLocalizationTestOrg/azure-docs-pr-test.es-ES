---
title: 'Azure Active Directory Domain Services: Habilitar la compatibilidad con el servicio de perfil de usuario de SharePoint | Microsoft Docs'
description: "Configurar la sincronización de perfil de servicios de dominio de Active Directory de Azure dominios administrados toosupport de SharePoint Server"
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
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="381bf-103">Configurar una sincronización de perfil de dominio administrados toosupport para SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="381bf-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="381bf-104">SharePoint Server incluye un servicio de perfiles de usuario que se usa para la sincronización de perfiles de usuario.</span><span class="sxs-lookup"><span data-stu-id="381bf-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="381bf-105">tooset seguridad Hola servicio de perfiles de usuario, los permisos adecuados necesitan toobe concedido en un dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="381bf-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="381bf-106">Para más información, vea [Concesión de permisos de Active Directory Domain Services para la sincronización de perfiles en SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="381bf-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="381bf-107">Este artículo explica cómo puede configurar el servicio de sincronización de perfil de usuario de SharePoint Server de servicios de dominio de AD de Azure dominios administrados toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="381bf-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="381bf-108">grupo de Hello 'Cuentas de servicio de controlador de dominio de AAD'</span><span class="sxs-lookup"><span data-stu-id="381bf-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="381bf-109">Un grupo de seguridad denominado '**cuentas de servicio de controlador de dominio de AAD**' está disponible en la unidad organizativa de hello 'Usuarios' en el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="381bf-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="381bf-110">Puede ver este grupo en hello **equipos y usuarios de Active Directory** complemento MMC en el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="381bf-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Grupo de seguridad Cuentas de servicio de controlador de dominio de AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="381bf-112">Los miembros de este grupo de seguridad son delegado Hola siguientes privilegios:</span><span class="sxs-lookup"><span data-stu-id="381bf-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="381bf-113">privilegio de 'Replicar los cambios en el directorio' Hello en raíz de hello DSE de hello administrados dominio.</span><span class="sxs-lookup"><span data-stu-id="381bf-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="381bf-114">Hola privilegio 'Replicar los cambios en el directorio' en el contexto de nomenclatura de configuración de hello (cn = contenedor de configuración) del programa Hola a administrar el dominio.</span><span class="sxs-lookup"><span data-stu-id="381bf-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="381bf-115">Este grupo de seguridad también es miembro del grupo integrado hello **acceso de compatible con versiones anteriores de Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="381bf-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Grupo de seguridad Cuentas de servicio de controlador de dominio de AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="381bf-117">Habilitar la sincronización del perfil de usuario de SharePoint Server toosupport de dominio administrado</span><span class="sxs-lookup"><span data-stu-id="381bf-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="381bf-118">Puede agregar la cuenta de servicio de hello usada para toohello de sincronización de perfil de usuario de SharePoint **cuentas de servicio de controlador de dominio de AAD** grupo.</span><span class="sxs-lookup"><span data-stu-id="381bf-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="381bf-119">Como resultado, cuenta de sincronización de hello Obtiene el directorio de los privilegios adecuados tooreplicate cambios toohello.</span><span class="sxs-lookup"><span data-stu-id="381bf-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="381bf-120">Este paso de configuración permite toowork de sincronización de perfil de usuario de SharePoint Server correctamente.</span><span class="sxs-lookup"><span data-stu-id="381bf-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![Cuentas de servicio de controlador de dominio de AAD - Agregar miembros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Cuentas de servicio de controlador de dominio de AAD - Agregar miembros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="381bf-123">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="381bf-123">Related Content</span></span>
* [<span data-ttu-id="381bf-124">Referencia técnica - Concesión de permisos de Active Directory Domain Services para la sincronización de perfiles en SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="381bf-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
