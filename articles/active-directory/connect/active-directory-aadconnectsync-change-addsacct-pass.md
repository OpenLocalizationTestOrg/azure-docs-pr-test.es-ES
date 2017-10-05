---
title: "Azure AD Connect Sync: cambio de la contraseña de la cuenta de AD DS | Microsoft Docs"
description: "En este tema se describe cómo actualizar Azure AD Connect después de cambiar la contraseña de la cuenta de AD DS."
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
ms.openlocfilehash: 14e16a238e60ecfeeb3cbf88c3922a79349dcc75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="2c77a-104">Cambio de la contraseña de la cuenta de AD DS</span><span class="sxs-lookup"><span data-stu-id="2c77a-104">Changing the AD DS account password</span></span>
<span data-ttu-id="2c77a-105">La cuenta de AD DS se refiere a la cuenta de usuario que usa Azure AD Connect para comunicarse con la instancia local de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2c77a-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span></span> <span data-ttu-id="2c77a-106">Si cambia la contraseña de la cuenta de AD DS, debe actualizar Azure AD Connect Synchronization Service con la nueva contraseña.</span><span class="sxs-lookup"><span data-stu-id="2c77a-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span></span> <span data-ttu-id="2c77a-107">En caso contrario, el servicio ya no puede sincronizar correctamente con la instancia local de Active Directory y se producirán los errores siguientes:</span><span class="sxs-lookup"><span data-stu-id="2c77a-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span></span>

* <span data-ttu-id="2c77a-108">En Synchronization Service Manager, cualquier operación de importación o exportación con un directorio de AD local genera un error **no-start-credentials**.</span><span class="sxs-lookup"><span data-stu-id="2c77a-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="2c77a-109">En el Visor de eventos de Windows, el registro de eventos de aplicación contiene un error con el **identificador de evento 6000** y mensaje **'El agente de administración "contoso.com" no se pudo ejecutar porque las credenciales no eran válidas'**.</span><span class="sxs-lookup"><span data-stu-id="2c77a-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span></span>


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="2c77a-110">Cómo actualizar Synchronization Service con la nueva contraseña de la cuenta de AD DS</span><span class="sxs-lookup"><span data-stu-id="2c77a-110">How to update the Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="2c77a-111">Para actualizar Synchronization Service con la nueva contraseña:</span><span class="sxs-lookup"><span data-stu-id="2c77a-111">To update the Synchronization Service with the new password:</span></span>

1. <span data-ttu-id="2c77a-112">Inicie el Synchronization Service Manager (INICIO → Synchronization Service).</span><span class="sxs-lookup"><span data-stu-id="2c77a-112">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="2c77a-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="2c77a-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="2c77a-114">Vaya a la pestaña **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="2c77a-114">Go to the **Connectors** tab.</span></span>

3. <span data-ttu-id="2c77a-115">Seleccione el **Conector AD** correspondiente a la cuenta de AD DS cuya contraseña se ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="2c77a-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="2c77a-116">En **Acciones**, seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2c77a-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="2c77a-117">En el cuadro de diálogo emergente, seleccione **Connect to Active Directory Forest** (Conectar con el bosque de Active Directory):</span><span class="sxs-lookup"><span data-stu-id="2c77a-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>

6. <span data-ttu-id="2c77a-118">Escriba la nueva contraseña de la cuenta de AD DS en el cuadro de texto **Password** (Contraseña).</span><span class="sxs-lookup"><span data-stu-id="2c77a-118">Enter the new password of the AD DS account in the **Password** textbox.</span></span>

7. <span data-ttu-id="2c77a-119">Haga clic en **OK** (Aceptar) para guardar la nueva contraseña y cerrar el cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="2c77a-119">Click **OK** to save the new password and close the pop-up dialog.</span></span>

8. <span data-ttu-id="2c77a-120">Reinicie Azure AD Connect Synchronization Service en el Administrador de Control de servicios de Windows.</span><span class="sxs-lookup"><span data-stu-id="2c77a-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="2c77a-121">Esto sirve para asegurarse de que cualquier referencia a la contraseña antigua se quita de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="2c77a-121">This is to ensure that any reference to the old password is removed from the memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c77a-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2c77a-122">Next steps</span></span>
<span data-ttu-id="2c77a-123">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="2c77a-123">**Overview topics**</span></span>

* [<span data-ttu-id="2c77a-124">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="2c77a-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="2c77a-125">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c77a-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
