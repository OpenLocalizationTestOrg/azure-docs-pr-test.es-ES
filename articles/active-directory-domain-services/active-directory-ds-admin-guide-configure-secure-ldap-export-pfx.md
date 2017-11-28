---
title: "Configuración de LDAP seguro (LDAPS) en Azure AD Domain Services | Microsoft Docs"
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
ms.openlocfilehash: 5d46f376d46b8bbf3f93de57a7d4e31abdbcdb2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="82ce8-103">Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="82ce8-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="82ce8-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="82ce8-104">Before you begin</span></span>
<span data-ttu-id="82ce8-105">Asegúrese de haber completado la [Tarea 1: Obtención de un certificado para LDAP seguro](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="82ce8-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="82ce8-106">Tarea 2: Exportación del certificado LDAP seguro a un archivo .PFX</span><span class="sxs-lookup"><span data-stu-id="82ce8-106">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="82ce8-107">Antes de iniciar esta tarea, asegúrese de haber obtenido el certificado de LDAP seguro de una entidad de certificación pública, o bien haber creado un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="82ce8-107">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="82ce8-108">Realice los pasos siguientes para exportar el certificado LDAPS a un archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="82ce8-108">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="82ce8-109">Pulse el botón **Inicio** y escriba **E**. En el cuadro de diálogo **Ejecutar**, escriba **mmc** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Inicio de la consola MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="82ce8-111">En el aviso **Control de cuentas de usuario**, haga clic en **Sí** para iniciar MMC (Microsoft Management Console) como administrador.</span><span class="sxs-lookup"><span data-stu-id="82ce8-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="82ce8-112">En el menú **Archivo**, haga clic en **Agregar o quitar complemento**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Adición del complemento a la consola MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="82ce8-114">En el cuadro de diálogo **Agregar o quitar complemento**, seleccione el complemento **Certificados** y haga clic en el botón **Agregar >**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![Adición del complemento Certificados a la consola MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="82ce8-116">En el Asistente para el **complemento Certificados**, seleccione **Cuenta de equipo** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Adición del complemento Certificados a la cuenta de equipo](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="82ce8-118">En la página **Seleccionar equipo**, seleccione **Equipo local**: (el equipo en el que se está ejecutando esta consola) y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![Adición del complemento Certificados: seleccionar equipo](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="82ce8-120">En el cuadro de diálogo **Agregar o quitar complementos**, haga clic en **Aceptar** para agregar el complemento de certificados a MMC.</span><span class="sxs-lookup"><span data-stu-id="82ce8-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![Adición del complemento Certificados a la consola MMC: listo](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="82ce8-122">En la ventana de MMC, haga clic para expandir **Raíz de consola**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="82ce8-123">Debería ver el complemento Certificados cargado.</span><span class="sxs-lookup"><span data-stu-id="82ce8-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="82ce8-124">Haga clic en **Certificados (equipo local)** para expandirlo.</span><span class="sxs-lookup"><span data-stu-id="82ce8-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="82ce8-125">Haga clic para expandir el nodo **Personal** y después el nodo **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![Abrir el almacén de certificados personal](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="82ce8-127">Debería ver el certificado autofirmado que se creó.</span><span class="sxs-lookup"><span data-stu-id="82ce8-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="82ce8-128">Puede examinar las propiedades del certificado para asegurarse de que la huella digital coincide con lo que notificó en las ventanas de PowerShell cuando creó el certificado.</span><span class="sxs-lookup"><span data-stu-id="82ce8-128">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="82ce8-129">Seleccione el certificado autofirmado y **haga clic con el botón derecho**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="82ce8-130">En el menú contextual, seleccione **Todas las tareas** y **Exportar**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Exportación de certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="82ce8-132">En **Asistente para exportar certificados**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![Asistente para exportación de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="82ce8-134">En la página **Exportar la clave privada**, seleccione **Exportar la clave privada** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="82ce8-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![Exportación de certificados: clave privada](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="82ce8-136">DEBE exportar la clave privada junto con el certificado.</span><span class="sxs-lookup"><span data-stu-id="82ce8-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="82ce8-137">Se producirá un error al habilitar LDAP seguro para el dominio administrado si proporciona un archivo PFX que no contiene la clave privada del certificado.</span><span class="sxs-lookup"><span data-stu-id="82ce8-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="82ce8-138">En la página **Formato de archivo de exportación**, seleccione **Intercambio de información personal: PKCS #12 (.PFX)** como formato de archivo para el certificado exportado.</span><span class="sxs-lookup"><span data-stu-id="82ce8-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![Exportación de certificados: formato de archivos](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="82ce8-140">Solo se admite el formato de archivo .PFX.</span><span class="sxs-lookup"><span data-stu-id="82ce8-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="82ce8-141">No exporte el certificado al formato de archivo .CER.</span><span class="sxs-lookup"><span data-stu-id="82ce8-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="82ce8-142">En la página **Seguridad**, seleccione la opción **Contraseña** y escriba una contraseña para proteger el archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="82ce8-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="82ce8-143">Recuerde esta contraseña, ya que se necesitará en la siguiente tarea.</span><span class="sxs-lookup"><span data-stu-id="82ce8-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="82ce8-144">Haga clic en **Siguiente** para continuar.</span><span class="sxs-lookup"><span data-stu-id="82ce8-144">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="82ce8-145">Contraseña para la exportación de certificados</span><span class="sxs-lookup"><span data-stu-id="82ce8-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="82ce8-146">Anote esta contraseña.</span><span class="sxs-lookup"><span data-stu-id="82ce8-146">Make a note of this password.</span></span> <span data-ttu-id="82ce8-147">La necesitará al habilitar LDAP seguro para este dominio administrado en la [Tarea 3: Habilitación de LDAP seguro para el dominio administrado](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="82ce8-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="82ce8-148">En la página **Archivo que se va a exportar** , especifique el nombre de archivo y la ubicación donde desea exportar el certificado.</span><span class="sxs-lookup"><span data-stu-id="82ce8-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![Ruta para la exportación de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="82ce8-150">En la página siguiente, haga clic en **Finalizar** para exportar el certificado a un archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="82ce8-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="82ce8-151">Debería ver el cuadro de diálogo de confirmación cuando se haya exportado el certificado.</span><span class="sxs-lookup"><span data-stu-id="82ce8-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![Exportación de certificados: listo](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="82ce8-153">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="82ce8-153">Next step</span></span>
[<span data-ttu-id="82ce8-154">Tarea 3: Habilitación de LDAP seguro para el dominio administrado</span><span class="sxs-lookup"><span data-stu-id="82ce8-154">Task 3 - enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
