---
title: aaaConfigure seguro (LDAPS) de LDAP en servicios de dominio de AD de Azure | Documentos de Microsoft
description: "Configuración de LDAP seguro (LDAPS) para un dominio administrado con Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="83928-103">Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="83928-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="83928-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="83928-104">Before you begin</span></span>
<span data-ttu-id="83928-105">Asegúrese de haber completado la [Tarea 1: Obtención de un certificado para LDAP seguro](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="83928-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="83928-106">Tarea 2: exportar hello tooa de certificado LDAP seguro. Archivo PFX</span><span class="sxs-lookup"><span data-stu-id="83928-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="83928-107">Antes de iniciar esta tarea, asegúrese de que ha obtenido el certificado LDAP seguro de Hola de una entidad de certificación pública o que ha creado un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="83928-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="83928-108">Realizar pasos de hello, tooexport Hola LDAPS certificados tooa. Archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="83928-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="83928-109">Hola presione **iniciar** botón y escriba **R**. Hola **ejecutar** cuadro de diálogo, escriba **mmc** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="83928-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Iniciar la consola de MMC de Hola](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="83928-111">En hello **User Account Control** símbolo del sistema, haga clic en **Sí** toolaunch MMC (Microsoft Management Console) como administrador.</span><span class="sxs-lookup"><span data-stu-id="83928-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="83928-112">De hello **archivo** menú, haga clic en **agregar o quitar complemento...** .</span><span class="sxs-lookup"><span data-stu-id="83928-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Agregar la consola de complemento tooMMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="83928-114">Hola **agregar o quitar complementos** cuadro de diálogo, seleccione hello **certificados** complemento y haga clic en hello **Agregar >** botón.</span><span class="sxs-lookup"><span data-stu-id="83928-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![Agregar la consola de complemento tooMMC de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="83928-116">Hola **complemento certificados** asistente, seleccione **cuenta de equipo** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="83928-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Adición del complemento Certificados a la cuenta de equipo](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="83928-118">En hello **Seleccionar equipo** , seleccione **equipo Local: (equipo de Hola que se está ejecutando esta consola)** y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="83928-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![Adición del complemento Certificados: seleccionar equipo](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="83928-120">Hola **agregar o quitar complementos** cuadro de diálogo, haga clic en **Aceptar** tooadd tooMMC de complemento de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="83928-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![Agregar certificados complemento tooMMC - terminado](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="83928-122">En la ventana MMC de hello, haga clic en tooexpand **raíz de consola**.</span><span class="sxs-lookup"><span data-stu-id="83928-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="83928-123">Debería ver Hola complemento certificados cargado.</span><span class="sxs-lookup"><span data-stu-id="83928-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="83928-124">Haga clic en **certificados (equipo Local)** tooexpand.</span><span class="sxs-lookup"><span data-stu-id="83928-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="83928-125">Haga clic en hello tooexpand **Personal** nodo, seguido por hello **certificados** nodo.</span><span class="sxs-lookup"><span data-stu-id="83928-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![Abrir el almacén de certificados personal](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="83928-127">Debería ver el certificado autofirmado Hola que hemos creado.</span><span class="sxs-lookup"><span data-stu-id="83928-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="83928-128">Puede examinar propiedades Hola de hello certificado tooensure Hola huella digital coincidencias que notificar en windows PowerShell de hello al crear el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="83928-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="83928-129">Seleccione Hola certificado autofirmado y **haga**.</span><span class="sxs-lookup"><span data-stu-id="83928-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="83928-130">En el menú contextual de hello, seleccione **todas las tareas** y seleccione **exportar...** .</span><span class="sxs-lookup"><span data-stu-id="83928-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Exportación de certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="83928-132">Hola **Asistente para exportar certificados**, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="83928-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![Asistente para exportación de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="83928-134">En hello **exportar la clave privada** página, seleccione **Sí, exportar la clave privada de hello**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="83928-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![Exportación de certificados: clave privada](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="83928-136">DEBE exportar la clave privada de hello junto con el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="83928-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="83928-137">Si proporcionas PFX que no contiene la clave privada de hello certificado de Hola, habilitación de LDAP seguro para el dominio administrado produce un error.</span><span class="sxs-lookup"><span data-stu-id="83928-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="83928-138">En hello **Exportar formato de archivo** página, seleccione **intercambio de información Personal: PKCS #12 (. PFX)** como formato de archivo de Hola para hello certificado exportado.</span><span class="sxs-lookup"><span data-stu-id="83928-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![Exportación de certificados: formato de archivos](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="83928-140">Solo Hola. Se admite el formato de archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="83928-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="83928-141">No exporte Hola certificado toohello. Formato de archivo CER.</span><span class="sxs-lookup"><span data-stu-id="83928-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="83928-142">En hello **seguridad** página, seleccione hello **contraseña** opción y escriba un hello tooprotect de contraseña. Archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="83928-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="83928-143">Recuerde esta contraseña porque lo necesitará en la siguiente tarea de Hola.</span><span class="sxs-lookup"><span data-stu-id="83928-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="83928-144">Haga clic en **siguiente** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="83928-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="83928-145">Contraseña para la exportación de certificados</span><span class="sxs-lookup"><span data-stu-id="83928-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="83928-146">Anote esta contraseña.</span><span class="sxs-lookup"><span data-stu-id="83928-146">Make a note of this password.</span></span> <span data-ttu-id="83928-147">Se necesita al habilitar LDAP seguro para este dominio administrado en [tarea 3: habilitar LDAP seguro para el dominio administrado Hola](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="83928-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="83928-148">En hello **tooExport archivo** página, especifique el nombre de archivo de Hola y la ubicación que desee que el certificado de hello tooexport.</span><span class="sxs-lookup"><span data-stu-id="83928-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![Ruta para la exportación de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="83928-150">En hello después de la página, haga clic en **finalizar** archivo PFX de tooexport Hola certificado tooa.</span><span class="sxs-lookup"><span data-stu-id="83928-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="83928-151">Debería ver el cuadro de diálogo de confirmación cuando se ha exportado el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="83928-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![Exportación de certificados: listo](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="83928-153">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="83928-153">Next step</span></span>
[<span data-ttu-id="83928-154">Tarea 3: habilitar LDAP seguro para el dominio administrado Hola</span><span class="sxs-lookup"><span data-stu-id="83928-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
