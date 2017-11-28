---
title: "Azure AD Connect sync: cambiar contraseña de cuenta de hello AD DS | Documentos de Microsoft"
description: "Este documento de tema describe cómo se cambia tooupdate Azure AD Connect después de la contraseña de Hola de cuenta de hello AD DS."
services: active-directory
keywords: "cuenta de AD DS, cuenta de Active Directory, contraseña"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="beb6d-104">Cambiar la contraseña de la cuenta de hello AD DS</span><span class="sxs-lookup"><span data-stu-id="beb6d-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="beb6d-105">cuenta de Hello AD DS refiere la cuenta de usuario de toohello utilizada toocommunicate de Azure AD Connect con local de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="beb6d-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="beb6d-106">Si cambia la contraseña Hola de hello cuenta AD DS, debe actualizar servicio de sincronización de Connect de Azure AD con hello nueva contraseña.</span><span class="sxs-lookup"><span data-stu-id="beb6d-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="beb6d-107">En caso contrario, Hola que sincronización ya no se puede sincronizar correctamente con hello Active Directory local y se producirán Hola siguientes errores:</span><span class="sxs-lookup"><span data-stu-id="beb6d-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="beb6d-108">Hola operación Synchronization Service Manager, cualquier importación o exportación con local se produce un error de AD con **credenciales de inicio no** error.</span><span class="sxs-lookup"><span data-stu-id="beb6d-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="beb6d-109">En el Visor de eventos de Windows, el registro de eventos de aplicación Hola contiene un error con **6000 de Id. de evento** y mensaje **'agente de administración de Hola "contoso.com" error toorun porque las credenciales de hello no eran válidas'** .</span><span class="sxs-lookup"><span data-stu-id="beb6d-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="beb6d-110">¿Cómo tooupdate Hola servicio de sincronización con la nueva contraseña de cuenta de AD DS</span><span class="sxs-lookup"><span data-stu-id="beb6d-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="beb6d-111">Hola de tooupdate servicio de sincronización con la nueva contraseña de hello:</span><span class="sxs-lookup"><span data-stu-id="beb6d-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="beb6d-112">Iniciar Hola Synchronization Service Manager (servicio de sincronización de inicio →).</span><span class="sxs-lookup"><span data-stu-id="beb6d-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="beb6d-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="beb6d-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="beb6d-114">Vaya toohello **conectores** ficha.</span><span class="sxs-lookup"><span data-stu-id="beb6d-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="beb6d-115">Seleccione hello **conector AD** correspondiente cuenta de toohello AD DS para la que se ha cambiado su contraseña.</span><span class="sxs-lookup"><span data-stu-id="beb6d-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="beb6d-116">En **Acciones**, seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="beb6d-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="beb6d-117">En el cuadro de diálogo emergente de hello, seleccione **conectar tooActive Directory bosque**:</span><span class="sxs-lookup"><span data-stu-id="beb6d-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="beb6d-118">Escriba Hola nueva contraseña de cuenta de AD DS Hola Hola **contraseña** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="beb6d-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="beb6d-119">Haga clic en **Aceptar** toosave Hola nueva contraseña y el cuadro de diálogo emergente de hello cerrar.</span><span class="sxs-lookup"><span data-stu-id="beb6d-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="beb6d-120">Reinicio Hola servicio Azure AD Connect sincronización en el Administrador de Control de servicios de Windows.</span><span class="sxs-lookup"><span data-stu-id="beb6d-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="beb6d-121">Se trata de tooensure que cualquier contraseña antigua de toohello de referencia se quita de la caché de memoria de Hola.</span><span class="sxs-lookup"><span data-stu-id="beb6d-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="beb6d-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="beb6d-122">Next steps</span></span>
<span data-ttu-id="beb6d-123">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="beb6d-123">**Overview topics**</span></span>

* [<span data-ttu-id="beb6d-124">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="beb6d-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="beb6d-125">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="beb6d-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
