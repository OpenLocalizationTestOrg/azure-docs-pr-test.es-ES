---
title: aaaBack servidores de VMware con el servidor de copia de seguridad de Azure | Documentos de Microsoft
description: "Usar servidor de copia de seguridad de Azure tooback un VMware vCenter/ESXi servidores tooAzure o el disco. En este artículo se proporciona instrucciones detalladas para realizar copias de seguridad (o proteger) las cargas de trabajo de VMware."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="e074f-104">Copia un tooAzure de servidor de VMware</span><span class="sxs-lookup"><span data-stu-id="e074f-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="e074f-105">Este artículo explica cómo tooconfigure servidor de copia de seguridad de Azure toohelp proteger cargas de trabajo de VMware server.</span><span class="sxs-lookup"><span data-stu-id="e074f-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="e074f-106">En este artículo se da por supuesto que ya tiene instalado Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="e074f-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="e074f-107">Si no tiene servidor de copia de seguridad de Azure instalada, consulte [preparar tooback seguridad cargas de trabajo utilizando el servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e074f-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="e074f-108">Azure Backup Server puede hacer una copia de seguridad de las versiones 6.5, 6.0 y 5.5 de VMware vCenter Server, así como ayudarle a protegerlas.</span><span class="sxs-lookup"><span data-stu-id="e074f-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="e074f-109">Crear un servidor de vCenter toohello de conexión segura</span><span class="sxs-lookup"><span data-stu-id="e074f-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="e074f-110">De forma predeterminada Azure Backup Server se comunica con cada instancia de vCenter Server a través de canal HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e074f-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="e074f-111">tooturn en una comunicación segura hello, se recomienda que instale el certificado de entidad de certificación de VMware (CA) de hello en el servidor de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="e074f-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="e074f-112">Si no requieren una comunicación segura y preferiría requisito de toodisable Hola HTTPS, consulte [protocolo de comunicación segura de deshabilitar](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="e074f-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="e074f-113">toocreate una conexión segura entre el servidor de copia de seguridad de Azure y Hola vCenter Server, importe el certificado de confianza de hello en el servidor de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="e074f-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="e074f-114">Normalmente, se usa un explorador Hola servidor de copia de seguridad de Azure máquina tooconnect toohello vCenter Server a través de hello vSphere cliente Web.</span><span class="sxs-lookup"><span data-stu-id="e074f-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="e074f-115">Hello primera vez que use Hola servidor de copia de seguridad de Azure explorador tooconnect toohello vCenter Server, conexión hello no es segura.</span><span class="sxs-lookup"><span data-stu-id="e074f-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="e074f-116">Hola siguiente imagen muestra la conexión de hello no segura.</span><span class="sxs-lookup"><span data-stu-id="e074f-116">hello following image shows hello unsecured connection.</span></span>

![Ejemplo de servidor de tooVMware de conexión no segura](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="e074f-118">toofix este problema y crear una conexión segura, descargar certificados de CA raíz de confianza de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="e074f-119">En el Explorador de hello en el servidor de copia de seguridad de Azure, escriba Hola URL toohello vSphere cliente Web.</span><span class="sxs-lookup"><span data-stu-id="e074f-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="e074f-120">aparece la página de inicio de sesión de cliente Web de vSphere Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-120">hello vSphere Web Client login page appears.</span></span>

    ![Cliente web de vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="e074f-122">En parte inferior de Hola de información de Hola para los administradores y desarrolladores, busque hello **certificados de CA raíz de confianza de descarga** vínculo.</span><span class="sxs-lookup"><span data-stu-id="e074f-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![Certificados de CA raíz de confianza de hello toodownload de vínculo](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="e074f-124">Si no ve la página de inicio de sesión de cliente Web de vSphere hello, compruebe la configuración del proxy de su explorador.</span><span class="sxs-lookup"><span data-stu-id="e074f-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="e074f-125">Haga clic en **Download trusted root CA certificates** (Descargar certificados de entidad de certificación raíz de confianza).</span><span class="sxs-lookup"><span data-stu-id="e074f-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="e074f-126">Hola vCenter Server descarga un equipo local de tooyour de archivo.</span><span class="sxs-lookup"><span data-stu-id="e074f-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="e074f-127">Hello nombre del archivo se denomina **descargar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-127">hello file's name is named **download**.</span></span> <span data-ttu-id="e074f-128">Según el navegador, recibirá un mensaje que le pregunta si tooopen o guardar el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="e074f-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![descargar el mensaje cuando se descargan los certificados](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="e074f-130">Guardar tooa ubicación del archivo de hello en el servidor de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="e074f-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="e074f-131">Cuando se guarda el archivo hello, agregar la extensión de nombre de archivo .zip de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="e074f-132">archivo Hello es un archivo .zip que contiene información de hello acerca de los certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="e074f-133">Con la extensión .zip de hello, puede usar herramientas de extracción de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="e074f-134">Haga clic en **download.zip**y, a continuación, seleccione **extraer todo** contenido de hello tooextract.</span><span class="sxs-lookup"><span data-stu-id="e074f-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="e074f-135">archivo .zip de Hello extrae su carpeta de tooa contenido denominado **certificados**.</span><span class="sxs-lookup"><span data-stu-id="e074f-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="e074f-136">Dos tipos de archivos aparecen en la carpeta de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="e074f-137">archivo de certificado de raíz de Hello tiene una extensión que comienza con una secuencia numerada como.0 y.1.</span><span class="sxs-lookup"><span data-stu-id="e074f-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="e074f-138">archivo CRL de Hello tiene una extensión que comienza con una secuencia como .r0 o .r1.</span><span class="sxs-lookup"><span data-stu-id="e074f-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="e074f-139">archivo CRL de Hello está asociado con un certificado.</span><span class="sxs-lookup"><span data-stu-id="e074f-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="e074f-140">Descargar el archivo extraído localmente</span><span class="sxs-lookup"><span data-stu-id="e074f-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="e074f-141">Hola **certificados** carpeta, haga clic en archivo de certificado de raíz de hello y, a continuación, haga clic en **cambiar el nombre de**.</span><span class="sxs-lookup"><span data-stu-id="e074f-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="e074f-142">Cambiar nombre de certificado raíz</span><span class="sxs-lookup"><span data-stu-id="e074f-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="e074f-143">Cambiar too.crt de extensión del certificado de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="e074f-144">Cuando se le pregunte si está seguro de que desea la extensión de hello toochange, haga clic en **Sí** o **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="e074f-145">En caso contrario, cambiar función prevista del archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="e074f-146">icono de Hello para el icono de tooan de cambios de archivo de Hola que representa un certificado raíz.</span><span class="sxs-lookup"><span data-stu-id="e074f-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="e074f-147">Haga clic en certificado de raíz de Hola y en el menú emergente de hello, seleccione **instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="e074f-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="e074f-148">Hola **Asistente para importar certificados** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="e074f-149">Hola **Asistente para importar certificados** cuadro de diálogo, seleccione **equipo Local** como destino Hola Hola certificado y, a continuación, haga clic en **siguiente** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="e074f-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="e074f-150">Opciones de destino de almacenamiento de certificados</span><span class="sxs-lookup"><span data-stu-id="e074f-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="e074f-151">Si se le pregunta si desea que el equipo de toohello de tooallow cambios, haga clic en **Sí** o **Aceptar**, cambios de hello tooall.</span><span class="sxs-lookup"><span data-stu-id="e074f-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="e074f-152">En hello **almacén de certificados** página, seleccione **colocar todos los certificados en hello después almacén**y, a continuación, haga clic en **examinar** almacén de certificados de toochoose Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![Colocar certificados en una zona de almacenamiento específica](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="e074f-154">Hola **Seleccionar almacén de certificados** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![Jerarquía de carpetas de almacenamiento de certificado](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="e074f-156">Seleccione **entidades de certificación raíz de confianza** como carpeta de destino de Hola para los certificados de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![Carpeta de destino de certificado](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="e074f-158">Hola **entidades de certificación raíz de confianza** carpeta se confirma como almacén de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="e074f-159">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-159">Click **Next**.</span></span>

    ![Carpeta de almacén de certificados](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="e074f-161">En hello **finalización Hola Asistente para importar certificados** página, compruebe que dicho certificado Hola está en la carpeta que desee hello y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![Comprobar el certificado se encuentra en la carpeta apropiada de Hola](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="e074f-163">Aparece un cuadro de diálogo, se confirma la importación de certificados correcta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="e074f-164">Inicie sesión en vCenter toohello tooconfirm de servidor que la conexión es segura.</span><span class="sxs-lookup"><span data-stu-id="e074f-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="e074f-165">Si no es correcta la importación de certificados de hello y no se puede establecer una conexión segura, consulte la documentación de hello VMware vSphere en [obtener certificados de servidor](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="e074f-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="e074f-166">Si tiene límites de seguridad dentro de su organización y no desea tooturn en hello protocolo HTTPS, use Hola siguiendo las comunicaciones seguras de procedimiento toodisable Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="e074f-167">Deshabilitación del protocolo de comunicación segura</span><span class="sxs-lookup"><span data-stu-id="e074f-167">Disable secure communication protocol</span></span>

<span data-ttu-id="e074f-168">Si su organización no necesita el protocolo HTTPS de hello, utilice Hola siguiendo los pasos toodisable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e074f-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="e074f-169">toodisable Hola comportamiento predeterminado, cree una clave del registro que se pasa por alto el comportamiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="e074f-170">Copie y pegue Hola después de texto en un archivo .txt.</span><span class="sxs-lookup"><span data-stu-id="e074f-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="e074f-171">Guarde el equipo de servidor de copia de seguridad de Azure de hello archivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="e074f-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="e074f-172">Nombre de archivo de hello, use DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="e074f-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="e074f-173">Haga doble clic en la entrada del registro de hello archivo tooactivate Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="e074f-174">Crear una cuenta de usuario y rol Hola vCenter Server</span><span class="sxs-lookup"><span data-stu-id="e074f-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="e074f-175">En el servidor de vCenter hello, un rol es un conjunto predefinido de privilegios.</span><span class="sxs-lookup"><span data-stu-id="e074f-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="e074f-176">Un administrador del servidor vCenter crea funciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="e074f-177">permisos de tooassign, Administrador de hello pares cuentas de usuario con un rol.</span><span class="sxs-lookup"><span data-stu-id="e074f-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="e074f-178">tooestablish Hola usuario necesarios credenciales tooback equipo de servidor de vCenter hello, crear un rol con privilegios específicos y, a continuación, asocie la cuenta de usuario de hello con rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="e074f-179">Servidor de copia de seguridad de Azure usa un nombre de usuario y contraseña tooauthenticate con hello vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="e074f-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="e074f-180">Azure Backup Server utiliza las credenciales como autenticación para todas las operaciones de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e074f-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="e074f-181">tooadd un rol de servidor de vCenter y sus privilegios de un administrador de copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="e074f-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="e074f-182">Inicie sesión en el servidor de vCenter toohello y, a continuación, en el servidor de vCenter hello **navegador** del panel, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="e074f-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Opción de administración en el panel Navegador de vCenter Server](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="e074f-184">En **administración** seleccione **Roles**y, a continuación, en hello **Roles** panel haga clic en hello agregar icono de rol (símbolo + hello).</span><span class="sxs-lookup"><span data-stu-id="e074f-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![Agregar rol](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="e074f-186">Hola **Create Role** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-186">hello **Create Role** dialog box appears.</span></span>

    ![Crear rol](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="e074f-188">Hola **Create Role** cuadro de diálogo hello **nombre de la función** cuadro, escriba *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="e074f-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="e074f-189">nombre de la función Hello puede ser el que desee, pero debe ser reconocible para la finalidad del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="e074f-190">Seleccione los privilegios de hello para la versión adecuada de Hola de vCenter y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="e074f-191">Hello en la tabla siguiente identifica los privilegios de hello necesario para vCenter 6.0 y vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="e074f-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="e074f-192">Cuando se selecciona privilegios hello, haga clic en hello icono siguiente toohello primario etiqueta tooexpand Hola primario y vista Hola secundarios privilegios.</span><span class="sxs-lookup"><span data-stu-id="e074f-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="e074f-193">privilegios de máquina virtual de tooselect hello, necesita toogo varios niveles en hello primarios jerarquía secundarios.</span><span class="sxs-lookup"><span data-stu-id="e074f-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="e074f-194">No es necesario tooselect todos los privilegios de secundarios dentro de un privilegio primario.</span><span class="sxs-lookup"><span data-stu-id="e074f-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![Jerarquía de privilegios primaria-secundaria](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="e074f-196">Tras hacer clic en **Aceptar**, Hola nuevo rol aparecerá en la lista de hello en el panel de funciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="e074f-197">Privilegios para vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="e074f-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="e074f-198">Privilegios para vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="e074f-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="e074f-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="e074f-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="e074f-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="e074f-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="e074f-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="e074f-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="e074f-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="e074f-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="e074f-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="e074f-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="e074f-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="e074f-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="e074f-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="e074f-205">Network.Assign</span></span> |
|<span data-ttu-id="e074f-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="e074f-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="e074f-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="e074f-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="e074f-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="e074f-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="e074f-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="e074f-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="e074f-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="e074f-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="e074f-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="e074f-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="e074f-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="e074f-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="e074f-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="e074f-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="e074f-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="e074f-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="e074f-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="e074f-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="e074f-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="e074f-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="e074f-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="e074f-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="e074f-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="e074f-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="e074f-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="e074f-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="e074f-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="e074f-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="e074f-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="e074f-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="e074f-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="e074f-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="e074f-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="e074f-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="e074f-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="e074f-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="e074f-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="e074f-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="e074f-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="e074f-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="e074f-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="e074f-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="e074f-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="e074f-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="e074f-229">Creación de permisos y una cuenta de usuario de vCenter Server</span><span class="sxs-lookup"><span data-stu-id="e074f-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="e074f-230">Después de configura el rol de hello con privilegios, cree una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="e074f-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="e074f-231">cuenta de usuario de Hello tiene un nombre y una contraseña, que proporciona las credenciales de Hola que se usan para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="e074f-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="e074f-232">una cuenta de usuario en el servidor de vCenter hello toocreate **navegador** del panel, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e074f-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Opción Usuarios y grupos](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="e074f-234">Hola **vCenter usuarios y grupos** panel aparece.</span><span class="sxs-lookup"><span data-stu-id="e074f-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![Panel Usuarios y grupos de vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="e074f-236">Hola **vCenter usuarios y grupos** panel, seleccione hello **usuarios** ficha y, a continuación, haga clic en hello agregar icono de usuarios (símbolo + hello).</span><span class="sxs-lookup"><span data-stu-id="e074f-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="e074f-237">Hola **nuevo usuario** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="e074f-238">Hola **nuevo usuario** diálogo cuadro, agregue la información del usuario de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="e074f-239">En este procedimiento, el nombre de usuario de hello es BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="e074f-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![Cuadro de diálogo Nuevo usuario](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="e074f-241">nueva cuenta de usuario de Hello aparece en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="e074f-242">cuenta de usuario de hello tooassociate con rol de hello, Hola **navegador** del panel, haga clic en **permisos globales**.</span><span class="sxs-lookup"><span data-stu-id="e074f-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="e074f-243">Hola **permisos globales** panel, seleccione hello **administrar** ficha y, a continuación, haga clic en hello agregar icono (símbolo + hello).</span><span class="sxs-lookup"><span data-stu-id="e074f-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![Panel Permisos globales](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="e074f-245">Hola **Root permisos globales - agregar permiso** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="e074f-246">Hola **Global permiso Root - agregar permiso** cuadro de diálogo, haga clic en **agregar** toochoose Hola usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="e074f-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![Elegir un usuario o grupo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="e074f-248">Hola **Seleccionar usuarios o grupos** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="e074f-249">Hola **Seleccionar usuarios o grupos** diálogo cuadro, elija **BackupAdmin** y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="e074f-250">En **usuarios**, hello *dominio ombre de usuario* formato se utiliza para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="e074f-251">Si desea que toouse un dominio diferente, elíjalo en hello **dominio** lista.</span><span class="sxs-lookup"><span data-stu-id="e074f-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![Agregar usuario BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="e074f-253">Haga clic en **Aceptar** tooadd Hola seleccionado usuarios toohello **agregar permiso** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="e074f-254">Ahora que ha identificado usuario hello, asigne el rol de toohello de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="e074f-255">En **rol asignado**, en la lista desplegable de hello, seleccione **BackupAdminRole**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Asignar usuario toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="e074f-257">En hello **administrar** ficha hello **permisos globales** panel, nueva cuenta de usuario de Hola y rol Hola asociado aparecen en la lista Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="e074f-258">Establecimiento de las credenciales de vCenter Server en Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="e074f-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="e074f-259">Antes de agregar Hola VMware server tooAzure servidor de copia de seguridad, instalar [actualización 1 para el servidor de copia de seguridad de Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="e074f-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="e074f-260">tooopen servidor de copia de seguridad de Azure, haga doble clic en el icono de hello en el escritorio del servidor de copia de seguridad de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Icono de Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="e074f-262">Si no se encuentra el icono de hello en el escritorio de hello, abrir el servidor de copia de seguridad de Azure en lista de Hola de las aplicaciones instaladas.</span><span class="sxs-lookup"><span data-stu-id="e074f-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="e074f-263">nombre de aplicación de servidor de copia de seguridad de Azure Hola se denomina copia de seguridad de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e074f-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="e074f-264">En la consola del servidor de copia de seguridad de Azure hello, haga clic en **administración**, haga clic en **servidores de producción**y, a continuación, en la cinta de opciones de herramienta de hello, haga clic en **administrar VMware**.</span><span class="sxs-lookup"><span data-stu-id="e074f-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Consola de Azure Backup Server](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="e074f-266">Hola **administrar credenciales** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Cuadro de diálogo Administrar credenciales de Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="e074f-268">Hola **administrar credenciales** cuadro de diálogo, haga clic en **agregar** tooopen hello **Add Credential** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="e074f-269">Hola **Add Credential** diálogo cuadro, escriba un nombre y una descripción para la nueva credencial de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="e074f-270">A continuación, especifique la contraseña y nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-270">Then specify hello username and password.</span></span> <span data-ttu-id="e074f-271">nombre de Hello, *Contoso Vcenter credencial* se utiliza tooidentify credencial de hello en el procedimiento siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="e074f-272">Use Hola mismo nombre de usuario y la contraseña que se usa para Hola servidor vCenter.</span><span class="sxs-lookup"><span data-stu-id="e074f-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="e074f-273">Si no están en el servidor de vCenter hello y servidor de copia de seguridad de Azure Hola mismo dominio, en **nombre de usuario**, especifique el dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Cuadro de diálogo Agregar credenciales de Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="e074f-275">Haga clic en **agregar** tooadd Hola tooAzure de credencial nuevo servidor de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e074f-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="e074f-276">nueva credencial de Hello aparece en la lista de Hola Hola **administrar credenciales** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Cuadro de diálogo Administrar credenciales de Azure Backup Server](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="e074f-278">Hola tooclose **administrar credenciales** diálogo cuadro, haga clic en hello **X** en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="e074f-279">Agregar Hola vCenter Server tooAzure servidor de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="e074f-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="e074f-280">Asistente para la adición de servidor de producción es tooadd usado Hola vCenter Server tooAzure servidor de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e074f-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="e074f-281">tooopen Asistente para adición Server de producción, Hola completa siguiendo el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="e074f-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="e074f-282">En la consola del servidor de copia de seguridad de Azure hello, haga clic en **administración**, haga clic en **servidores de producción**y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Abrir el Asistente para adición del servidor de producción](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="e074f-284">Hola **Asistente para la adición de servidor de producción** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e074f-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Asistente para adición del servidor de producción](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="e074f-286">En hello **tipo Seleccionar servidor de producción** , seleccione **servidores VMware**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="e074f-287">En **servidor nombre o la dirección IP**, especifique el nombre de dominio completo (FQDN) de Hola o dirección IP del servidor de VMware Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="e074f-288">Si administran todos los servidores de ESXi Hola Hola mismo vCenter, puede usar el nombre vCenter Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![Especificar el nombre de dominio completo o dirección IP del servidor de VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="e074f-290">En **puerto SSL**, escriba el puerto hello toocommunicate usado con el servidor de VMware de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="e074f-291">Usar el puerto 443, que es el puerto predeterminado de hello, a menos que sepa que se requiere un puerto diferente.</span><span class="sxs-lookup"><span data-stu-id="e074f-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="e074f-292">En **Specify Credential**, seleccione Hola credencial que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e074f-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![Especificar credenciales](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="e074f-294">Haga clic en **agregar** lista tooadd Hola VMware server toohello de **agregado servidores de VMware**y, a continuación, haga clic en **siguiente** toomove toohello página siguiente en el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![Agregar credencial y el servidor de VMWare](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="e074f-296">Hola **resumen** página, haga clic en **agregar** tooadd Hola especificado VMware server tooAzure servidor de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e074f-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![Agregar VMware server tooAzure servidor de copia de seguridad](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="e074f-298">copia de seguridad del servidor de VMware de Hello es una copia de seguridad sin agente y se agrega inmediatamente Hola nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="e074f-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="e074f-299">Hola **finalizar** página muestra Hola resultados.</span><span class="sxs-lookup"><span data-stu-id="e074f-299">hello **Finish** page shows you hello results.</span></span>

  ![Página Finalizar](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="e074f-301">tooadd varias instancias de vCenter Server tooAzure servidor de copia de seguridad, repita Hola anterior de los pasos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="e074f-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="e074f-302">Después de agregar Hola vCenter Server tooAzure servidor de copia de seguridad, Hola siguiente paso es toocreate un grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="e074f-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="e074f-303">grupo de protección de Hello especifica Hola varios detalles de retención a corto o a largo plazo, y es donde se definen y aplicar la directiva de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="e074f-304">Directiva de copia de seguridad de Hello es la programación de Hola para cuando se producen las copias de seguridad y qué copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e074f-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="e074f-305">Configuración de un grupo de protección</span><span class="sxs-lookup"><span data-stu-id="e074f-305">Configure a protection group</span></span>

<span data-ttu-id="e074f-306">Si no ha usado System Center Data Protection Manager o servidor de copia de seguridad de Azure antes de, consulte [Plan para las copias de seguridad de disco](https://technet.microsoft.com/library/hh758026.aspx) tooprepare el entorno de hardware.</span><span class="sxs-lookup"><span data-stu-id="e074f-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="e074f-307">Después de comprobar que tiene el almacenamiento adecuado, utilice máquinas virtuales de VMware de tooadd de Asistente de hello crear nuevo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="e074f-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="e074f-308">En la consola del servidor de copia de seguridad de Azure hello, haga clic en **protección**y haga clic en la cinta de opciones de herramienta de hello, **New** Asistente Crear nuevo grupo de protección de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![Asistente para crear nuevo grupo de protección de hello abierto](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="e074f-310">Hola **crear nuevo grupo de protección** aparece el cuadro de diálogo del asistente.</span><span class="sxs-lookup"><span data-stu-id="e074f-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Cuadro de diálogo del asistente Crear nuevo grupo de protección](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="e074f-312">Haga clic en **siguiente** tooadvance toohello **Seleccionar tipo de grupo de protección** página.</span><span class="sxs-lookup"><span data-stu-id="e074f-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="e074f-313">En hello **tipo de grupo de protección seleccione** , seleccione **servidores** y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="e074f-314">Hola **seleccionar miembros del grupo** aparecerá la página.</span><span class="sxs-lookup"><span data-stu-id="e074f-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="e074f-315">En hello **seleccionar miembros del grupo** página, los miembros disponibles de Hola y miembros de hello seleccionado aparecen.</span><span class="sxs-lookup"><span data-stu-id="e074f-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="e074f-316">Seleccionar miembros de Hola que desee tooprotect y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![Seleccionar a miembros del grupo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="e074f-318">Al seleccionar un miembro, si selecciona una carpeta que contiene otras carpetas o máquinas virtuales, estas también se seleccionarán.</span><span class="sxs-lookup"><span data-stu-id="e074f-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="e074f-319">inclusión de Hola de carpetas de Hola y máquinas virtuales en la carpeta principal de Hola se denomina protección de nivel de carpeta.</span><span class="sxs-lookup"><span data-stu-id="e074f-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="e074f-320">tooremove una carpeta o la máquina virtual, Hola desactive casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="e074f-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="e074f-321">Si una máquina virtual o una carpeta que contiene una máquina virtual, ya está protegido tooAzure, no puede seleccionar esa máquina virtual de nuevo.</span><span class="sxs-lookup"><span data-stu-id="e074f-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="e074f-322">Es decir, después de una máquina virtual es tooAzure protegido, no se puede proteger de nuevo, lo que impide que los puntos de recuperación duplicados que se crea para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e074f-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="e074f-323">Si desea toosee qué instancia del servidor de copia de seguridad de Azure ya está protegiendo un miembro, el nombre de Hola de punto toohello miembro toosee del programa Hola a proteger el servidor.</span><span class="sxs-lookup"><span data-stu-id="e074f-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="e074f-324">En hello **Seleccionar método de protección de datos** página, escriba un nombre para el grupo de protección de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="e074f-325">Se seleccionan en línea y la protección a corto plazo (toodisk).</span><span class="sxs-lookup"><span data-stu-id="e074f-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="e074f-326">Si desea que la protección en línea de toouse (tooAzure), debe utilizar toodisk de protección a corto plazo.</span><span class="sxs-lookup"><span data-stu-id="e074f-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="e074f-327">Haga clic en **siguiente** duración tooproceed toohello de protección a corto plazo.</span><span class="sxs-lookup"><span data-stu-id="e074f-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![Seleccionar método de protección de datos](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="e074f-329">En hello **especificar objetivos a corto plazo** página, para **duración de retención**, especifique Hola número de días que desea que los puntos de recuperación de tooretain que son *almacenado toodisk*.</span><span class="sxs-lookup"><span data-stu-id="e074f-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="e074f-330">Si desea toochange hello y los días cuando se toman los puntos de recuperación, haga clic en **modificar**.</span><span class="sxs-lookup"><span data-stu-id="e074f-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="e074f-331">puntos de recuperación a corto plazo de Hello son copias de seguridad completas.</span><span class="sxs-lookup"><span data-stu-id="e074f-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="e074f-332">No son copias de seguridad incrementales.</span><span class="sxs-lookup"><span data-stu-id="e074f-332">They are not incremental backups.</span></span> <span data-ttu-id="e074f-333">Cuando esté satisfecho con los objetivos a corto plazo de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![Especificar objetivos a corto plazo](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="e074f-335">En hello **Revisar asignación de disco** página, revise y si es necesario, modifique el espacio en disco Hola para hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e074f-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="e074f-336">Hola recomienda las asignaciones de disco se basan en la duración de retención de Hola que se especifica en hello **especificar objetivos a corto plazo** página, tipo de Hola de carga de trabajo y el tamaño de Hola de hello los datos protegidos (identificados en el paso 3).</span><span class="sxs-lookup"><span data-stu-id="e074f-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="e074f-337">**Tamaño de los datos:** tamaño de los datos de Hola Hola grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="e074f-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="e074f-338">**Espacio en disco:** Hola la cantidad de espacio en disco para el grupo de protección de hello recomendada.</span><span class="sxs-lookup"><span data-stu-id="e074f-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="e074f-339">Si desea toomodify esta configuración, debe asignar espacio total ligeramente mayor que la cantidad de Hola que calcular que aumenta de tamaño de cada origen de datos.</span><span class="sxs-lookup"><span data-stu-id="e074f-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="e074f-340">**Colocación de los datos:** si activa la colocación, pueden asignar varios orígenes de datos en la protección de hello tooa única réplica y del volumen de punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="e074f-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="e074f-341">La ubicación compartida no es compatible con todas las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e074f-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="e074f-342">**Crecimiento automático:** si activa esta opción, si los datos de grupo de hello protegido sobrepasan asignación inicial de hello, System Center Data Protection Manager intenta tamaño del disco hello tooincrease 25 por ciento.</span><span class="sxs-lookup"><span data-stu-id="e074f-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="e074f-343">**Detalles del bloque de almacenamiento:** muestra el estado de Hola Hola del grupo de almacenamiento, incluido total y el tamaño de disco restante.</span><span class="sxs-lookup"><span data-stu-id="e074f-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![Revisar la asignación de disco](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="e074f-345">Cuando esté satisfecho con la asignación de espacio de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="e074f-346">En hello **Seleccionar método de creación de réplica** página, especifique cómo desea que copia inicial de toogenerate Hola o réplica de datos de hello protegido en el servidor de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="e074f-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="e074f-347">valor predeterminado de Hello es **automáticamente a través de la red de hello** y **ahora**.</span><span class="sxs-lookup"><span data-stu-id="e074f-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="e074f-348">Si utiliza Hola predeterminado, se recomienda que especifique una hora de poco tráfico.</span><span class="sxs-lookup"><span data-stu-id="e074f-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="e074f-349">Elija **Más tarde** y especifique un día y una hora.</span><span class="sxs-lookup"><span data-stu-id="e074f-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="e074f-350">Para grandes cantidades de datos o en condiciones de red menos óptimas, considere la posibilidad de replicar datos Hola sin conexión mediante un medio extraíble.</span><span class="sxs-lookup"><span data-stu-id="e074f-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="e074f-351">Una vez que haya elegido sus opciones, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-351">After you have made your choices, click **Next**.</span></span>

    ![Elegir método de creación de réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="e074f-353">En hello **opciones de comprobación de coherencia** página, seleccione cómo y cuándo las comprobaciones de coherencia de Hola de tooautomate.</span><span class="sxs-lookup"><span data-stu-id="e074f-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="e074f-354">Puede ejecutar comprobaciones de coherencia si los datos de réplica no son coherentes o en una programación establecida.</span><span class="sxs-lookup"><span data-stu-id="e074f-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="e074f-355">Si no desea tooconfigure comprobaciones de coherencia automáticas, puede ejecutar una comprobación manual.</span><span class="sxs-lookup"><span data-stu-id="e074f-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="e074f-356">En área de protección de Hola de consola del servidor de copia de seguridad de Azure hello, haga clic en grupo de protección de hello y, a continuación, seleccione **realizar comprobación de coherencia**.</span><span class="sxs-lookup"><span data-stu-id="e074f-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="e074f-357">Haga clic en **siguiente** toomove toohello siguiente página.</span><span class="sxs-lookup"><span data-stu-id="e074f-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="e074f-358">En hello **especificar datos de protección en línea** , seleccione uno o varios orígenes de datos que desea tooprotect.</span><span class="sxs-lookup"><span data-stu-id="e074f-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="e074f-359">Puede seleccionar los miembros de hello individualmente, o haga clic en **seleccionar todo** toochoose todos los miembros.</span><span class="sxs-lookup"><span data-stu-id="e074f-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="e074f-360">Después de elegir los miembros de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-360">After you choose hello members, click **Next**.</span></span>

    ![Especificar datos de protección en línea](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="e074f-362">En hello **especificar una programación de copia de seguridad en línea** página, especifique los puntos de recuperación toogenerate Hola de programación de copia de seguridad de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="e074f-363">Cuando se genera el punto de recuperación de hello, es toohello transfieren el almacén de servicios de recuperación de Azure.</span><span class="sxs-lookup"><span data-stu-id="e074f-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="e074f-364">Cuando esté satisfecho con la programación de copia de seguridad en línea hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![Especificar programación de copia de seguridad en línea](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="e074f-366">En hello **especificar directiva de retención en línea** página, indicar cuánto tiempo quiere que los datos de copia de seguridad de hello tooretain en Azure.</span><span class="sxs-lookup"><span data-stu-id="e074f-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="e074f-367">Después de define la directiva de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e074f-367">After hello policy is defined, click **Next**.</span></span>

    ![Especificar directiva de retención en línea](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="e074f-369">Los datos pueden guardarse en Azure sin límite de tiempo.</span><span class="sxs-lookup"><span data-stu-id="e074f-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="e074f-370">Al almacenar los datos de punto de recuperación en Azure, hello solo límite es que no puede tener más de 9999 puntos de recuperación por instancia protegido.</span><span class="sxs-lookup"><span data-stu-id="e074f-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="e074f-371">En este ejemplo, instancia protegido hello es servidor de VMware de Hola.</span><span class="sxs-lookup"><span data-stu-id="e074f-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="e074f-372">En hello **resumen** página, revise los detalles de Hola para los miembros del grupo de protección y la configuración y, a continuación, haga clic en **crear grupo**.</span><span class="sxs-lookup"><span data-stu-id="e074f-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Resumen de configuración y miembros del grupo de protección](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="e074f-374">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e074f-374">Next steps</span></span>
<span data-ttu-id="e074f-375">Si usa las cargas de trabajo de servidor de copia de seguridad de Azure tooprotect VMware, es posible que interesado en usar el servidor de copia de seguridad de Azure toohelp proteger un [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [granja de SharePoint de Microsoft](./backup-azure-backup-sharepoint-mabs.md), o un [Base de datos de SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="e074f-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="e074f-376">Para obtener información sobre problemas de registro de agente de hello, configuración de grupo de protección de Hola o copia de seguridad de los trabajos, consulte [solucionar problemas de servidor de copia de seguridad de Azure](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="e074f-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
