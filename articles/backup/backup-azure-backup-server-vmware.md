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
# <a name="back-up-a-vmware-server-tooazure"></a>Copia un tooAzure de servidor de VMware

Este artículo explica cómo tooconfigure servidor de copia de seguridad de Azure toohelp proteger cargas de trabajo de VMware server. En este artículo se da por supuesto que ya tiene instalado Azure Backup Server. Si no tiene servidor de copia de seguridad de Azure instalada, consulte [preparar tooback seguridad cargas de trabajo utilizando el servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md).

Azure Backup Server puede hacer una copia de seguridad de las versiones 6.5, 6.0 y 5.5 de VMware vCenter Server, así como ayudarle a protegerlas.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>Crear un servidor de vCenter toohello de conexión segura

De forma predeterminada Azure Backup Server se comunica con cada instancia de vCenter Server a través de canal HTTPS. tooturn en una comunicación segura hello, se recomienda que instale el certificado de entidad de certificación de VMware (CA) de hello en el servidor de copia de seguridad de Azure. Si no requieren una comunicación segura y preferiría requisito de toodisable Hola HTTPS, consulte [protocolo de comunicación segura de deshabilitar](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol). toocreate una conexión segura entre el servidor de copia de seguridad de Azure y Hola vCenter Server, importe el certificado de confianza de hello en el servidor de copia de seguridad de Azure.

Normalmente, se usa un explorador Hola servidor de copia de seguridad de Azure máquina tooconnect toohello vCenter Server a través de hello vSphere cliente Web. Hello primera vez que use Hola servidor de copia de seguridad de Azure explorador tooconnect toohello vCenter Server, conexión hello no es segura. Hola siguiente imagen muestra la conexión de hello no segura.

![Ejemplo de servidor de tooVMware de conexión no segura](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix este problema y crear una conexión segura, descargar certificados de CA raíz de confianza de Hola.

1. En el Explorador de hello en el servidor de copia de seguridad de Azure, escriba Hola URL toohello vSphere cliente Web. aparece la página de inicio de sesión de cliente Web de vSphere Hola.

    ![Cliente web de vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    En parte inferior de Hola de información de Hola para los administradores y desarrolladores, busque hello **certificados de CA raíz de confianza de descarga** vínculo.

    ![Certificados de CA raíz de confianza de hello toodownload de vínculo](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Si no ve la página de inicio de sesión de cliente Web de vSphere hello, compruebe la configuración del proxy de su explorador.

2. Haga clic en **Download trusted root CA certificates** (Descargar certificados de entidad de certificación raíz de confianza).

    Hola vCenter Server descarga un equipo local de tooyour de archivo. Hello nombre del archivo se denomina **descargar**. Según el navegador, recibirá un mensaje que le pregunta si tooopen o guardar el archivo hello.

    ![descargar el mensaje cuando se descargan los certificados](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Guardar tooa ubicación del archivo de hello en el servidor de copia de seguridad de Azure. Cuando se guarda el archivo hello, agregar la extensión de nombre de archivo .zip de Hola.

    archivo Hello es un archivo .zip que contiene información de hello acerca de los certificados de Hola. Con la extensión .zip de hello, puede usar herramientas de extracción de Hola.

4. Haga clic en **download.zip**y, a continuación, seleccione **extraer todo** contenido de hello tooextract.

    archivo .zip de Hello extrae su carpeta de tooa contenido denominado **certificados**. Dos tipos de archivos aparecen en la carpeta de certificados de Hola. archivo de certificado de raíz de Hello tiene una extensión que comienza con una secuencia numerada como.0 y.1.
    
    archivo CRL de Hello tiene una extensión que comienza con una secuencia como .r0 o .r1. archivo CRL de Hello está asociado con un certificado.

    ![Descargar el archivo extraído localmente ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. Hola **certificados** carpeta, haga clic en archivo de certificado de raíz de hello y, a continuación, haga clic en **cambiar el nombre de**.

    ![Cambiar nombre de certificado raíz ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    Cambiar too.crt de extensión del certificado de raíz de Hola. Cuando se le pregunte si está seguro de que desea la extensión de hello toochange, haga clic en **Sí** o **Aceptar**. En caso contrario, cambiar función prevista del archivo Hola. icono de Hello para el icono de tooan de cambios de archivo de Hola que representa un certificado raíz.

6. Haga clic en certificado de raíz de Hola y en el menú emergente de hello, seleccione **instalar certificado**.

    Hola **Asistente para importar certificados** aparece el cuadro de diálogo.

7. Hola **Asistente para importar certificados** cuadro de diálogo, seleccione **equipo Local** como destino Hola Hola certificado y, a continuación, haga clic en **siguiente** toocontinue.

    ![Opciones de destino de almacenamiento de certificados ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    Si se le pregunta si desea que el equipo de toohello de tooallow cambios, haga clic en **Sí** o **Aceptar**, cambios de hello tooall.

8. En hello **almacén de certificados** página, seleccione **colocar todos los certificados en hello después almacén**y, a continuación, haga clic en **examinar** almacén de certificados de toochoose Hola.

    ![Colocar certificados en una zona de almacenamiento específica](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    Hola **Seleccionar almacén de certificados** aparece el cuadro de diálogo.

    ![Jerarquía de carpetas de almacenamiento de certificado](./media/backup-azure-backup-server-vmware/cert-store.png)

9. Seleccione **entidades de certificación raíz de confianza** como carpeta de destino de Hola para los certificados de hello y, a continuación, haga clic en **Aceptar**.

    ![Carpeta de destino de certificado](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    Hola **entidades de certificación raíz de confianza** carpeta se confirma como almacén de certificados de Hola. Haga clic en **Siguiente**.

    ![Carpeta de almacén de certificados](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. En hello **finalización Hola Asistente para importar certificados** página, compruebe que dicho certificado Hola está en la carpeta que desee hello y, a continuación, haga clic en **finalizar**.

    ![Comprobar el certificado se encuentra en la carpeta apropiada de Hola](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    Aparece un cuadro de diálogo, se confirma la importación de certificados correcta de Hola.

11. Inicie sesión en vCenter toohello tooconfirm de servidor que la conexión es segura.

  Si no es correcta la importación de certificados de hello y no se puede establecer una conexión segura, consulte la documentación de hello VMware vSphere en [obtener certificados de servidor](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).

  Si tiene límites de seguridad dentro de su organización y no desea tooturn en hello protocolo HTTPS, use Hola siguiendo las comunicaciones seguras de procedimiento toodisable Hola.

### <a name="disable-secure-communication-protocol"></a>Deshabilitación del protocolo de comunicación segura

Si su organización no necesita el protocolo HTTPS de hello, utilice Hola siguiendo los pasos toodisable HTTPS. toodisable Hola comportamiento predeterminado, cree una clave del registro que se pasa por alto el comportamiento predeterminado de Hola.

1. Copie y pegue Hola después de texto en un archivo .txt.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Guarde el equipo de servidor de copia de seguridad de Azure de hello archivo tooyour. Nombre de archivo de hello, use DisableSecureAuthentication.reg.

3. Haga doble clic en la entrada del registro de hello archivo tooactivate Hola.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Crear una cuenta de usuario y rol Hola vCenter Server

En el servidor de vCenter hello, un rol es un conjunto predefinido de privilegios. Un administrador del servidor vCenter crea funciones de Hola. permisos de tooassign, Administrador de hello pares cuentas de usuario con un rol. tooestablish Hola usuario necesarios credenciales tooback equipo de servidor de vCenter hello, crear un rol con privilegios específicos y, a continuación, asocie la cuenta de usuario de hello con rol de Hola.

Servidor de copia de seguridad de Azure usa un nombre de usuario y contraseña tooauthenticate con hello vCenter Server. Azure Backup Server utiliza las credenciales como autenticación para todas las operaciones de copia de seguridad.

tooadd un rol de servidor de vCenter y sus privilegios de un administrador de copia de seguridad:

1. Inicie sesión en el servidor de vCenter toohello y, a continuación, en el servidor de vCenter hello **navegador** del panel, haga clic en **administración**.

    ![Opción de administración en el panel Navegador de vCenter Server](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. En **administración** seleccione **Roles**y, a continuación, en hello **Roles** panel haga clic en hello agregar icono de rol (símbolo + hello).

    ![Agregar rol](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    Hola **Create Role** aparece el cuadro de diálogo.

    ![Crear rol](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. Hola **Create Role** cuadro de diálogo hello **nombre de la función** cuadro, escriba *BackupAdminRole*. nombre de la función Hello puede ser el que desee, pero debe ser reconocible para la finalidad del rol de Hola.

4. Seleccione los privilegios de hello para la versión adecuada de Hola de vCenter y, a continuación, haga clic en **Aceptar**. Hello en la tabla siguiente identifica los privilegios de hello necesario para vCenter 6.0 y vCenter 5.5.

  Cuando se selecciona privilegios hello, haga clic en hello icono siguiente toohello primario etiqueta tooexpand Hola primario y vista Hola secundarios privilegios. privilegios de máquina virtual de tooselect hello, necesita toogo varios niveles en hello primarios jerarquía secundarios. No es necesario tooselect todos los privilegios de secundarios dentro de un privilegio primario.

  ![Jerarquía de privilegios primaria-secundaria](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  Tras hacer clic en **Aceptar**, Hola nuevo rol aparecerá en la lista de hello en el panel de funciones de Hola.

|Privilegios para vCenter 6.0| Privilegios para vCenter 5.5|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>Creación de permisos y una cuenta de usuario de vCenter Server

Después de configura el rol de hello con privilegios, cree una cuenta de usuario. cuenta de usuario de Hello tiene un nombre y una contraseña, que proporciona las credenciales de Hola que se usan para la autenticación.

1. una cuenta de usuario en el servidor de vCenter hello toocreate **navegador** del panel, haga clic en **usuarios y grupos**.

    ![Opción Usuarios y grupos](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    Hola **vCenter usuarios y grupos** panel aparece.

    ![Panel Usuarios y grupos de vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. Hola **vCenter usuarios y grupos** panel, seleccione hello **usuarios** ficha y, a continuación, haga clic en hello agregar icono de usuarios (símbolo + hello).

    Hola **nuevo usuario** aparece el cuadro de diálogo.

3. Hola **nuevo usuario** diálogo cuadro, agregue la información del usuario de hello y, a continuación, haga clic en **Aceptar**. En este procedimiento, el nombre de usuario de hello es BackupAdmin.

    ![Cuadro de diálogo Nuevo usuario](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    nueva cuenta de usuario de Hello aparece en la lista de Hola.

4. cuenta de usuario de hello tooassociate con rol de hello, Hola **navegador** del panel, haga clic en **permisos globales**. Hola **permisos globales** panel, seleccione hello **administrar** ficha y, a continuación, haga clic en hello agregar icono (símbolo + hello).

    ![Panel Permisos globales](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    Hola **Root permisos globales - agregar permiso** aparece el cuadro de diálogo.

5. Hola **Global permiso Root - agregar permiso** cuadro de diálogo, haga clic en **agregar** toochoose Hola usuario o grupo.

    ![Elegir un usuario o grupo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    Hola **Seleccionar usuarios o grupos** aparece el cuadro de diálogo.

6. Hola **Seleccionar usuarios o grupos** diálogo cuadro, elija **BackupAdmin** y, a continuación, haga clic en **agregar**.

    En **usuarios**, hello *dominio ombre de usuario* formato se utiliza para la cuenta de usuario de Hola. Si desea que toouse un dominio diferente, elíjalo en hello **dominio** lista.

    ![Agregar usuario BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    Haga clic en **Aceptar** tooadd Hola seleccionado usuarios toohello **agregar permiso** cuadro de diálogo.

7. Ahora que ha identificado usuario hello, asigne el rol de toohello de usuario de Hola. En **rol asignado**, en la lista desplegable de hello, seleccione **BackupAdminRole**y, a continuación, haga clic en **Aceptar**.

    ![Asignar usuario toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  En hello **administrar** ficha hello **permisos globales** panel, nueva cuenta de usuario de Hola y rol Hola asociado aparecen en la lista Hola.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>Establecimiento de las credenciales de vCenter Server en Azure Backup Server

Antes de agregar Hola VMware server tooAzure servidor de copia de seguridad, instalar [actualización 1 para el servidor de copia de seguridad de Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).

1. tooopen servidor de copia de seguridad de Azure, haga doble clic en el icono de hello en el escritorio del servidor de copia de seguridad de Azure de Hola.

    ![Icono de Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Si no se encuentra el icono de hello en el escritorio de hello, abrir el servidor de copia de seguridad de Azure en lista de Hola de las aplicaciones instaladas. nombre de aplicación de servidor de copia de seguridad de Azure Hola se denomina copia de seguridad de Microsoft Azure.

2. En la consola del servidor de copia de seguridad de Azure hello, haga clic en **administración**, haga clic en **servidores de producción**y, a continuación, en la cinta de opciones de herramienta de hello, haga clic en **administrar VMware**.

    ![Consola de Azure Backup Server](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    Hola **administrar credenciales** aparece el cuadro de diálogo.

    ![Cuadro de diálogo Administrar credenciales de Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. Hola **administrar credenciales** cuadro de diálogo, haga clic en **agregar** tooopen hello **Add Credential** cuadro de diálogo.

4. Hola **Add Credential** diálogo cuadro, escriba un nombre y una descripción para la nueva credencial de Hola. A continuación, especifique la contraseña y nombre de usuario de Hola. nombre de Hello, *Contoso Vcenter credencial* se utiliza tooidentify credencial de hello en el procedimiento siguiente Hola. Use Hola mismo nombre de usuario y la contraseña que se usa para Hola servidor vCenter. Si no están en el servidor de vCenter hello y servidor de copia de seguridad de Azure Hola mismo dominio, en **nombre de usuario**, especifique el dominio de Hola.

    ![Cuadro de diálogo Agregar credenciales de Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    Haga clic en **agregar** tooadd Hola tooAzure de credencial nuevo servidor de copia de seguridad. nueva credencial de Hello aparece en la lista de Hola Hola **administrar credenciales** cuadro de diálogo.
    
    ![Cuadro de diálogo Administrar credenciales de Azure Backup Server](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. Hola tooclose **administrar credenciales** diálogo cuadro, haga clic en hello **X** en la esquina superior derecha de Hola.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Agregar Hola vCenter Server tooAzure servidor de copia de seguridad

Asistente para la adición de servidor de producción es tooadd usado Hola vCenter Server tooAzure servidor de copia de seguridad.

tooopen Asistente para adición Server de producción, Hola completa siguiendo el procedimiento:

1. En la consola del servidor de copia de seguridad de Azure hello, haga clic en **administración**, haga clic en **servidores de producción**y, a continuación, haga clic en **agregar**.

    ![Abrir el Asistente para adición del servidor de producción](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    Hola **Asistente para la adición de servidor de producción** aparece el cuadro de diálogo.

    ![Asistente para adición del servidor de producción](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. En hello **tipo Seleccionar servidor de producción** , seleccione **servidores VMware**y, a continuación, haga clic en **siguiente**.

3. En **servidor nombre o la dirección IP**, especifique el nombre de dominio completo (FQDN) de Hola o dirección IP del servidor de VMware Hola. Si administran todos los servidores de ESXi Hola Hola mismo vCenter, puede usar el nombre vCenter Hola.

    ![Especificar el nombre de dominio completo o dirección IP del servidor de VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. En **puerto SSL**, escriba el puerto hello toocommunicate usado con el servidor de VMware de Hola. Usar el puerto 443, que es el puerto predeterminado de hello, a menos que sepa que se requiere un puerto diferente.

5. En **Specify Credential**, seleccione Hola credencial que creó anteriormente.

    ![Especificar credenciales](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. Haga clic en **agregar** lista tooadd Hola VMware server toohello de **agregado servidores de VMware**y, a continuación, haga clic en **siguiente** toomove toohello página siguiente en el Asistente de Hola.

    ![Agregar credencial y el servidor de VMWare](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. Hola **resumen** página, haga clic en **agregar** tooadd Hola especificado VMware server tooAzure servidor de copia de seguridad.

    ![Agregar VMware server tooAzure servidor de copia de seguridad](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  copia de seguridad del servidor de VMware de Hello es una copia de seguridad sin agente y se agrega inmediatamente Hola nuevo servidor. Hola **finalizar** página muestra Hola resultados.

  ![Página Finalizar](./media/backup-azure-backup-server-vmware/summary-screen.png)

  tooadd varias instancias de vCenter Server tooAzure servidor de copia de seguridad, repita Hola anterior de los pasos de esta sección.

Después de agregar Hola vCenter Server tooAzure servidor de copia de seguridad, Hola siguiente paso es toocreate un grupo de protección. grupo de protección de Hello especifica Hola varios detalles de retención a corto o a largo plazo, y es donde se definen y aplicar la directiva de copia de seguridad de Hola. Directiva de copia de seguridad de Hello es la programación de Hola para cuando se producen las copias de seguridad y qué copia de seguridad.


## <a name="configure-a-protection-group"></a>Configuración de un grupo de protección

Si no ha usado System Center Data Protection Manager o servidor de copia de seguridad de Azure antes de, consulte [Plan para las copias de seguridad de disco](https://technet.microsoft.com/library/hh758026.aspx) tooprepare el entorno de hardware. Después de comprobar que tiene el almacenamiento adecuado, utilice máquinas virtuales de VMware de tooadd de Asistente de hello crear nuevo grupo de protección.

1. En la consola del servidor de copia de seguridad de Azure hello, haga clic en **protección**y haga clic en la cinta de opciones de herramienta de hello, **New** Asistente Crear nuevo grupo de protección de tooopen Hola.

    ![Asistente para crear nuevo grupo de protección de hello abierto](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    Hola **crear nuevo grupo de protección** aparece el cuadro de diálogo del asistente.

    ![Cuadro de diálogo del asistente Crear nuevo grupo de protección](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    Haga clic en **siguiente** tooadvance toohello **Seleccionar tipo de grupo de protección** página.

2. En hello **tipo de grupo de protección seleccione** , seleccione **servidores** y, a continuación, haga clic en **siguiente**. Hola **seleccionar miembros del grupo** aparecerá la página.

3. En hello **seleccionar miembros del grupo** página, los miembros disponibles de Hola y miembros de hello seleccionado aparecen. Seleccionar miembros de Hola que desee tooprotect y, a continuación, haga clic en **siguiente**.

    ![Seleccionar a miembros del grupo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    Al seleccionar un miembro, si selecciona una carpeta que contiene otras carpetas o máquinas virtuales, estas también se seleccionarán. inclusión de Hola de carpetas de Hola y máquinas virtuales en la carpeta principal de Hola se denomina protección de nivel de carpeta. tooremove una carpeta o la máquina virtual, Hola desactive casilla de verificación.

    Si una máquina virtual o una carpeta que contiene una máquina virtual, ya está protegido tooAzure, no puede seleccionar esa máquina virtual de nuevo. Es decir, después de una máquina virtual es tooAzure protegido, no se puede proteger de nuevo, lo que impide que los puntos de recuperación duplicados que se crea para una máquina virtual. Si desea toosee qué instancia del servidor de copia de seguridad de Azure ya está protegiendo un miembro, el nombre de Hola de punto toohello miembro toosee del programa Hola a proteger el servidor.

4. En hello **Seleccionar método de protección de datos** página, escriba un nombre para el grupo de protección de Hola. Se seleccionan en línea y la protección a corto plazo (toodisk). Si desea que la protección en línea de toouse (tooAzure), debe utilizar toodisk de protección a corto plazo. Haga clic en **siguiente** duración tooproceed toohello de protección a corto plazo.

    ![Seleccionar método de protección de datos](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. En hello **especificar objetivos a corto plazo** página, para **duración de retención**, especifique Hola número de días que desea que los puntos de recuperación de tooretain que son *almacenado toodisk*. Si desea toochange hello y los días cuando se toman los puntos de recuperación, haga clic en **modificar**. puntos de recuperación a corto plazo de Hello son copias de seguridad completas. No son copias de seguridad incrementales. Cuando esté satisfecho con los objetivos a corto plazo de hello, haga clic en **siguiente**.

    ![Especificar objetivos a corto plazo](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. En hello **Revisar asignación de disco** página, revise y si es necesario, modifique el espacio en disco Hola para hello las máquinas virtuales. Hola recomienda las asignaciones de disco se basan en la duración de retención de Hola que se especifica en hello **especificar objetivos a corto plazo** página, tipo de Hola de carga de trabajo y el tamaño de Hola de hello los datos protegidos (identificados en el paso 3).  

  - **Tamaño de los datos:** tamaño de los datos de Hola Hola grupo de protección.
  - **Espacio en disco:** Hola la cantidad de espacio en disco para el grupo de protección de hello recomendada. Si desea toomodify esta configuración, debe asignar espacio total ligeramente mayor que la cantidad de Hola que calcular que aumenta de tamaño de cada origen de datos.
  - **Colocación de los datos:** si activa la colocación, pueden asignar varios orígenes de datos en la protección de hello tooa única réplica y del volumen de punto de recuperación. La ubicación compartida no es compatible con todas las cargas de trabajo.
  - **Crecimiento automático:** si activa esta opción, si los datos de grupo de hello protegido sobrepasan asignación inicial de hello, System Center Data Protection Manager intenta tamaño del disco hello tooincrease 25 por ciento.
  - **Detalles del bloque de almacenamiento:** muestra el estado de Hola Hola del grupo de almacenamiento, incluido total y el tamaño de disco restante.

    ![Revisar la asignación de disco](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    Cuando esté satisfecho con la asignación de espacio de hello, haga clic en **siguiente**.

7. En hello **Seleccionar método de creación de réplica** página, especifique cómo desea que copia inicial de toogenerate Hola o réplica de datos de hello protegido en el servidor de copia de seguridad de Azure.

    valor predeterminado de Hello es **automáticamente a través de la red de hello** y **ahora**. Si utiliza Hola predeterminado, se recomienda que especifique una hora de poco tráfico. Elija **Más tarde** y especifique un día y una hora.

    Para grandes cantidades de datos o en condiciones de red menos óptimas, considere la posibilidad de replicar datos Hola sin conexión mediante un medio extraíble.

    Una vez que haya elegido sus opciones, haga clic en **Siguiente**.

    ![Elegir método de creación de réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. En hello **opciones de comprobación de coherencia** página, seleccione cómo y cuándo las comprobaciones de coherencia de Hola de tooautomate. Puede ejecutar comprobaciones de coherencia si los datos de réplica no son coherentes o en una programación establecida.

    Si no desea tooconfigure comprobaciones de coherencia automáticas, puede ejecutar una comprobación manual. En área de protección de Hola de consola del servidor de copia de seguridad de Azure hello, haga clic en grupo de protección de hello y, a continuación, seleccione **realizar comprobación de coherencia**.

    Haga clic en **siguiente** toomove toohello siguiente página.

9. En hello **especificar datos de protección en línea** , seleccione uno o varios orígenes de datos que desea tooprotect. Puede seleccionar los miembros de hello individualmente, o haga clic en **seleccionar todo** toochoose todos los miembros. Después de elegir los miembros de hello, haga clic en **siguiente**.

    ![Especificar datos de protección en línea](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. En hello **especificar una programación de copia de seguridad en línea** página, especifique los puntos de recuperación toogenerate Hola de programación de copia de seguridad de disco de Hola. Cuando se genera el punto de recuperación de hello, es toohello transfieren el almacén de servicios de recuperación de Azure. Cuando esté satisfecho con la programación de copia de seguridad en línea hello, haga clic en **siguiente**.

    ![Especificar programación de copia de seguridad en línea](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. En hello **especificar directiva de retención en línea** página, indicar cuánto tiempo quiere que los datos de copia de seguridad de hello tooretain en Azure. Después de define la directiva de hello, haga clic en **siguiente**.

    ![Especificar directiva de retención en línea](./media/backup-azure-backup-server-vmware/retention-policy.png)

    Los datos pueden guardarse en Azure sin límite de tiempo. Al almacenar los datos de punto de recuperación en Azure, hello solo límite es que no puede tener más de 9999 puntos de recuperación por instancia protegido. En este ejemplo, instancia protegido hello es servidor de VMware de Hola.

12. En hello **resumen** página, revise los detalles de Hola para los miembros del grupo de protección y la configuración y, a continuación, haga clic en **crear grupo**.

    ![Resumen de configuración y miembros del grupo de protección](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>Pasos siguientes
Si usa las cargas de trabajo de servidor de copia de seguridad de Azure tooprotect VMware, es posible que interesado en usar el servidor de copia de seguridad de Azure toohelp proteger un [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [granja de SharePoint de Microsoft](./backup-azure-backup-sharepoint-mabs.md), o un [Base de datos de SQL Server](./backup-azure-sql-mabs.md).

Para obtener información sobre problemas de registro de agente de hello, configuración de grupo de protección de Hola o copia de seguridad de los trabajos, consulte [solucionar problemas de servidor de copia de seguridad de Azure](./backup-azure-mabs-troubleshoot.md).
