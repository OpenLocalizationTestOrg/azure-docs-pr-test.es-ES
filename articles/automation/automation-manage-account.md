---
title: "Administración de una cuenta de Azure Automation | Microsoft Docs"
description: "En este artículo se describe cómo administrar la configuración de la cuenta de Automation: renovación, eliminación o configuración incorrecta de certificados."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 41efdbcacede74bac038342688362ff480cadc7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="813b1-103">Administración de la cuenta de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="813b1-103">Manage Azure Automation account</span></span>
<span data-ttu-id="813b1-104">En algún momento antes de que expire su cuenta de Automation, deberá renovar el certificado.</span><span class="sxs-lookup"><span data-stu-id="813b1-104">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="813b1-105">Si cree que se ha puesto en peligro la cuenta de ejecución, puede eliminarla y volver a crearla.</span><span class="sxs-lookup"><span data-stu-id="813b1-105">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="813b1-106">En esta sección se describe cómo realizar estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="813b1-106">This section discusses how to perform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="813b1-107">Renovación de certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="813b1-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="813b1-108">El certificado autofirmado que creó para la cuenta de ejecución expira un año a partir de la fecha de creación.</span><span class="sxs-lookup"><span data-stu-id="813b1-108">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="813b1-109">Se puede renovar en cualquier momento antes de que expire.</span><span class="sxs-lookup"><span data-stu-id="813b1-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="813b1-110">Cuando se renueva, el certificado válido actual se conserva para tener la seguridad de que los runbooks que están en cola o que se están ejecutando activamente y que se autentican con la cuenta de ejecución, no resultan afectados negativamente.</span><span class="sxs-lookup"><span data-stu-id="813b1-110">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="813b1-111">El certificado es válido hasta la fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="813b1-111">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="813b1-112">Si ha configurado la cuenta de ejecución de Automation para que use un certificado emitido por una entidad de certificación de empresa y usa esta opción, ese certificado se reemplazará por un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="813b1-112">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="813b1-113">Para renovar el certificado, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="813b1-113">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="813b1-114">Abra la cuenta de Automation en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="813b1-114">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="813b1-115">En la hoja **Cuenta de Automation**, en el panel **Account properties** (Propiedades de la cuenta), en **Account Settings** (Configuración de la cuenta), seleccione **Run As Accounts** (Cuentas de ejecución).</span><span class="sxs-lookup"><span data-stu-id="813b1-115">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Panel de propiedades de la cuenta de Automation](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="813b1-117">En la hoja de propiedades **Run As Accounts** (Cuentas de ejecución), seleccione la cuenta de ejecución o la cuenta de ejecución clásica para la que quiere renovar el certificado.</span><span class="sxs-lookup"><span data-stu-id="813b1-117">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="813b1-118">En la hoja **Propiedades** de la cuenta seleccionada, haga clic en **Renovar certificado**.</span><span class="sxs-lookup"><span data-stu-id="813b1-118">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Renovación del certificado para una cuenta de ejecución](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="813b1-120">Mientras se está renovando el certificado, puede seguir el progreso desde el menú, en **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="813b1-120">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="813b1-121">Eliminación de una cuenta de ejecución o de ejecución clásica</span><span class="sxs-lookup"><span data-stu-id="813b1-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="813b1-122">En esta sección se describe cómo eliminar y volver a crear una cuenta de ejecución o de ejecución clásica.</span><span class="sxs-lookup"><span data-stu-id="813b1-122">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="813b1-123">Al realizar esta acción, la cuenta de Automation se conserva.</span><span class="sxs-lookup"><span data-stu-id="813b1-123">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="813b1-124">Después de eliminar una cuenta de ejecución o de ejecución clásica, puede volver a crearla en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="813b1-124">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="813b1-125">Abra la cuenta de Automation en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="813b1-125">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="813b1-126">En la hoja **Cuenta de Automation**, en el panel de propiedades de la cuenta, seleccione **Run As Accounts** (Cuentas de ejecución).</span><span class="sxs-lookup"><span data-stu-id="813b1-126">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="813b1-127">En la hoja de propiedades **Run As Accounts** (Cuentas de ejecución), seleccione la cuenta de ejecución o la cuenta de ejecución clásica que quiere eliminar.</span><span class="sxs-lookup"><span data-stu-id="813b1-127">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="813b1-128">A continuación, en la hoja **Propiedades** de la cuenta seleccionada, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="813b1-128">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Eliminación de una cuenta de ejecución](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="813b1-130">Mientras se está eliminando la cuenta, puede seguir el progreso desde el menú, en **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="813b1-130">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="813b1-131">Después de eliminar la cuenta, puede volver a crearla en la hoja de propiedades **Run As Accounts** (Cuentas de ejecución) mediante la selección de la opción de creación **Cuenta de ejecución de Azure**.</span><span class="sxs-lookup"><span data-stu-id="813b1-131">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Nueva creación de la cuenta de ejecución de Automation](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="813b1-133">Error de configuración</span><span class="sxs-lookup"><span data-stu-id="813b1-133">Misconfiguration</span></span>
<span data-ttu-id="813b1-134">Puede que alguno de los elementos de configuración necesarios para que la cuenta de ejecución o la cuenta de ejecución clásica funcionen correctamente se haya eliminado o no se haya creado correctamente durante la configuración inicial.</span><span class="sxs-lookup"><span data-stu-id="813b1-134">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="813b1-135">Estos elementos son:</span><span class="sxs-lookup"><span data-stu-id="813b1-135">The items include:</span></span>

* <span data-ttu-id="813b1-136">Recurso de certificado</span><span class="sxs-lookup"><span data-stu-id="813b1-136">Certificate asset</span></span>
* <span data-ttu-id="813b1-137">Recurso de conexión</span><span class="sxs-lookup"><span data-stu-id="813b1-137">Connection asset</span></span>
* <span data-ttu-id="813b1-138">La cuenta de ejecución se ha quitado del rol de colaborador</span><span class="sxs-lookup"><span data-stu-id="813b1-138">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="813b1-139">Entidad de servicio o aplicación en Azure AD</span><span class="sxs-lookup"><span data-stu-id="813b1-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="813b1-140">En los casos anteriores y otros casos de errores de configuración, la cuenta de Automation detecta los cambios y muestra el estado *Incomplete* (Incompleto) en la hoja de propiedades **Run As Accounts** (Cuentas de ejecución) de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="813b1-140">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Estado de configuración incompleta de la cuenta de ejecución](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="813b1-142">Al seleccionar la cuenta de ejecución, el panel **Propiedades** muestra el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="813b1-142">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Mensaje de advertencia de configuración incompleta de la cuenta de ejecución](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="813b1-144">.</span><span class="sxs-lookup"><span data-stu-id="813b1-144">.</span></span>

<span data-ttu-id="813b1-145">Rápidamente puede resolver estos problemas de la cuenta de ejecución con solo eliminarla cuenta y volver a crearla.</span><span class="sxs-lookup"><span data-stu-id="813b1-145">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="813b1-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="813b1-146">Next steps</span></span>
* <span data-ttu-id="813b1-147">Para más información acerca de las entidades de servicio, consulte [Objetos Application y objetos ServicePrincipal](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="813b1-147">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="813b1-148">Para más información acerca del control de acceso basado en rol de Automatización de Azure, consulte [Control de acceso basado en rol en Automatización de Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="813b1-148">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="813b1-149">Para más información acerca de los certificados y de los servicios de Azure, consulte [Introducción a los certificados para los servicios en la nube de Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="813b1-149">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>