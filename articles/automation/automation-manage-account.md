---
title: "aaaManage cuenta de automatización de Azure | Documentos de Microsoft"
description: "Este artículo describe cómo toomanage Hola configuración de la cuenta de automatización, como la renovación de certificados, eliminación y una configuración incorrecta."
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
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="3dcdc-103">Administración de la cuenta de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="3dcdc-103">Manage Azure Automation account</span></span>
<span data-ttu-id="3dcdc-104">En algún momento antes de que expire su cuenta de automatización, necesitará toorenew Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="3dcdc-105">Si cree que Hola cuenta de ejecución está en peligro, puede eliminar y volver a crearla.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="3dcdc-106">Esta sección se describe cómo tooperform estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="3dcdc-107">Renovación de certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="3dcdc-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="3dcdc-108">certificado autofirmado de Hola que creó para la cuenta de ejecución de Hola expira un año a partir de la fecha de Hola de creación.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="3dcdc-109">Se puede renovar en cualquier momento antes de que expire.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="3dcdc-110">Cuando renovarlo, certificado válido de hello actual es retenido tooensure que los runbooks que se ponen en cola hasta o activamente ejecutándose y que autenticarse con hello cuenta de ejecución, no se afecta negativamente.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="3dcdc-111">certificado de Hello sigue siendo válido hasta la fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="3dcdc-112">Si ha configurado su toouse de cuenta automatización ejecutar como un certificado emitido por la entidad de certificación de empresa y use esta opción, certificado de empresa de Hola se reemplazará por un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="3dcdc-113">Hola toorenew certificados, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="3dcdc-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="3dcdc-114">Hola portal de Azure, abrir cuenta de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="3dcdc-115">En hello **cuenta de automatización** hoja en hello **cuenta propiedades** panel, en **configuración de la cuenta**, seleccione **cuentas de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Panel de propiedades de la cuenta de Automation](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="3dcdc-117">En hello **cuentas de ejecución** hoja de propiedades, seleccione cualquier Hola ejecutar como cuenta u Hola clásico cuenta de ejecución que desea toorenew Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="3dcdc-118">En hello **propiedades** hoja para hello seleccionado cuenta, haga clic en **renovar certificado**.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Renovación del certificado para una cuenta de ejecución](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="3dcdc-120">Mientras se que se va a renovar el certificado de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="3dcdc-121">Eliminación de una cuenta de ejecución o de ejecución clásica</span><span class="sxs-lookup"><span data-stu-id="3dcdc-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="3dcdc-122">Esta sección se describe cómo toodelete y volver a crear una cuenta de ejecución o identificación clásico.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="3dcdc-123">Al realizar esta acción, se conserva Hola cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="3dcdc-124">Después de eliminar una cuenta de ejecución o identificación clásico, puede volver a crearla en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="3dcdc-125">Hola portal de Azure, abrir cuenta de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="3dcdc-126">En hello **cuenta de automatización** hoja, en el panel de propiedades de cuenta hello, seleccione **cuentas de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="3dcdc-127">En hello **cuentas de ejecución** hoja de propiedades, seleccione cualquier Hola ejecutar como cuenta de ejecución de o clásico como la cuenta que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="3dcdc-128">A continuación, en hello **propiedades** hoja para hello seleccionado cuenta, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Eliminación de una cuenta de ejecución](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="3dcdc-130">Mientras se está eliminando la cuenta de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="3dcdc-131">Después de que se ha eliminado la cuenta de hello, se puede volver a crear en hello **cuentas de ejecución** opción de creación de la hoja de propiedades seleccionando hello **ejecutar como cuenta de Azure**.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Volver a crear Hola automatización de la cuenta de ejecución](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="3dcdc-133">Error de configuración</span><span class="sxs-lookup"><span data-stu-id="3dcdc-133">Misconfiguration</span></span>
<span data-ttu-id="3dcdc-134">Algunos elementos de configuración necesarios para toofunction de cuenta de identificación o identificación clásico Hola correctamente podrían se han eliminado o creó incorrectamente durante la instalación inicial.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="3dcdc-135">Hola elementos incluyen:</span><span class="sxs-lookup"><span data-stu-id="3dcdc-135">hello items include:</span></span>

* <span data-ttu-id="3dcdc-136">Recurso de certificado</span><span class="sxs-lookup"><span data-stu-id="3dcdc-136">Certificate asset</span></span>
* <span data-ttu-id="3dcdc-137">Recurso de conexión</span><span class="sxs-lookup"><span data-stu-id="3dcdc-137">Connection asset</span></span>
* <span data-ttu-id="3dcdc-138">Se ha quitado la cuenta de ejecución de rol de colaborador de Hola</span><span class="sxs-lookup"><span data-stu-id="3dcdc-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="3dcdc-139">Entidad de servicio o aplicación en Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dcdc-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="3dcdc-140">Hola anterior y otras instancias de una configuración incorrecta, Hola cuenta de automatización detecta Hola cambia y muestra un estado de *incompleta* en hello **cuentas de ejecución** hoja de propiedades para hello cuenta.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Estado de configuración incompleta de la cuenta de ejecución](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="3dcdc-142">Cuando se selecciona la cuenta de identificación de hello, Hola cuenta **propiedades** panel muestra hello mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3dcdc-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Mensaje de advertencia de configuración incompleta de la cuenta de ejecución](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="3dcdc-144">.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-144">.</span></span>

<span data-ttu-id="3dcdc-145">Rápidamente puede resolver estos problemas de la cuenta ejecutar como eliminar y volver a crear la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="3dcdc-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dcdc-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3dcdc-146">Next steps</span></span>
* <span data-ttu-id="3dcdc-147">Para obtener más información acerca de las entidades de servicio, consulte demasiado[objetos de entidad de servicio y aplicación](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="3dcdc-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="3dcdc-148">Para obtener más información sobre el Control de acceso basado en roles en automatización de Azure, consulte demasiado[control de acceso basado en roles en automatización de Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="3dcdc-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="3dcdc-149">Para obtener más información sobre los certificados y servicios de Azure, consulte demasiado[Introducción a los certificados para servicios en la nube](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="3dcdc-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
