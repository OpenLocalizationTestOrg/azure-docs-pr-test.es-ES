---
title: "¿aaaHow hace Azure RemoteApp Guardar configuración y los datos de usuario? | Microsoft Docs"
description: "Obtenga información acerca de cómo guarda los datos de usuario mediante el disco de perfil de usuario de hello Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>¿Cómo guarda Azure RemoteApp la configuración y datos de usuario?
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Azure RemoteApp guarda la identidad y las personalizaciones de los usuarios en dispositivos y sesiones. Estos datos de los usuarios se almacenan en un disco para cada colección y cada usuario, conocido como disco de perfil de usuario (UDP). disco de Hola sigue usuario hello y se asegura de usuario de hello tiene una experiencia coherente, independientemente de donde inician sesión en.

Discos de perfil de usuario son completamente transparentes toohello usuario: los usuarios guardar la carpeta de documentos tootheir documentos (en lo que parece toobe una unidad local) y cambiar su configuración de la aplicación como de costumbre. Hola al mismo tiempo, personales de todos los valores se conservan cuando se conecte tooAzure RemoteApp desde cualquier dispositivo. Todos los datos de usuario de hello ve la cantidad de datos en hello mismo lugar.

Cada UPD tiene 50 GB de almacenamiento persistente y contiene datos de usuarios y configuraciones de aplicaciones. 

Siga leyendo para obtener información específica sobre los datos del perfil de usuario.

> [!NOTE]
> ¿Necesita toodisable Hola UPD? Puede hacerlo ahora: compruebe la entrada de blog de Pavithra, [Deshabilitar discos de perfil de usuario (UPD) en Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), para más información.
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a>¿Cómo un administrador puede obtener los datos de toohello?
Si necesita datos de hello tooaccess para uno de los usuarios (para la recuperación ante desastres o si el usuario de hello deja la empresa de hello), póngase en contacto con soporte técnico de Azure y proporcionar información de suscripción de hello para la recopilación de Hola y de identidad de usuario de Hola. equipo de Azure RemoteApp Hola proporcionará un disco duro virtual toohello de dirección URL. Descargue ese VHD y recupere los documentos o archivos que necesite. Tenga en cuenta que Hola VHD es 50GB, por lo que tardará un toodownload de bits.

## <a name="is-hello-data-backed-up"></a>¿Se copian datos de hello?
Sí, se guarda una copia de seguridad de datos de usuario de Hola por ubicación geográfica. Hello datos es de solo lectura y se puede al que obtuvo acceso Hola igual manera que serían datos normales de hello (póngase en contacto con Azure RemoteApp tooget lo), si el centro de datos principal de hello está inactivo. datos Hello están la ubicación de copia de seguridad de copiado toohello en tiempo real y no se conserva copias de las distintas versiones. Por lo tanto, en datos dañados, no se será capaz de toorestore se tooa anteriormente denominada versión válida pero si Hola data center primario no está activo, será capaz de tooget datos de usuario de Hola a otra ubicación.

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a>¿Cómo los usuarios ven Hola UPD en hello servidor?
Cada usuario tendrá su propio directorio en servidor hello que asigna tootheir UPD: c:\Users\username.

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a>¿Qué es Hola mejor manera toouse Outlook y UPD?
Azure RemoteApp guarda el estado de Outlook de hello (buzones, PST) entre sesiones. tooenable, necesitamos Hola a toobe PST almacenado en los datos de perfil de usuario de hello (c:\users\<nombre de usuario >). Se trata de ubicación predeterminada de Hola para los datos de hello, por lo que siempre y cuando no cambiar la ubicación de hello, se conservarán los datos de hello entre sesiones.

También se recomienda usar el modo "en caché" en Outlook y usar el modo "servidor/online" para buscar.

Consulte [este artículo](remoteapp-outlook.md) para más información sobre el uso de Outlook y Azure RemoteApp.

## <a name="what-about-redirection"></a>Información acerca del redireccionamiento
Puede configurar RemoteApp de Azure toolet a los usuarios tener acceso a los dispositivos locales mediante la configuración de [redirección](remoteapp-redirection.md). Los dispositivos locales, a continuación, será capaz de tooaccess datos Hola Hola UPD.

## <a name="can-i-use-my-upd-as-a-network-share"></a>¿Puedo usar mi UPD como un recurso compartido de red?
No. Los UPD no pueden utilizarse como un recurso compartido de red. Un UPD es usuario de toohello disponible solo cuando el usuario de hello activamente conectado tooAzure RemoteApp.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Si se elimina un usuario de una colección, ¿se elimina su UPD?
No, cuando se elimina un usuario, no se elimina automáticamente Hola UPD: en su lugar, se almacenan datos de Hola hasta que elimine la colección de Hola. 90 días después de Eliminar colección de hello, eliminamos todas las UPD. 

Si necesita toodelete una UPD de una colección, póngase en contacto con Azure RemoteApp: podemos eliminar UPD de nuestra parte.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>¿Puedo acceder a los UPD de mis usuarios (de los usuarios actuales o eliminados)?
Sí, si ponerse en contacto con [Azure RemoteApp](mailto:remoteappforum@microsoft.com), podemos configurar también con una dirección URL tooaccess datos Hola. Tendrá sobre toodownload de 10 horas todos los datos o archivos de hello UPD antes de que expire el acceso de Hola.

## <a name="are-upds-available-offline"></a>¿Están los UPD disponibles sin conexión?
En estos momentos no proporcionamos tooUPDs de acceso sin conexión, más allá de la ventana acceso hello 10 hora que se ha descrito anteriormente. Esto significa que no tenemos un tooprovide de manera que con tener acceso para lo suficientemente largo tareas toocomplete más complejo, como ejecutar software antivirus en UPD Hola o tener acceso a datos para una auditoría.

## <a name="do-registry-key-settings-persist"></a>¿La configuración de la clave del Registro se conserva?
Sí, algo escrito tooHKEY_Current_User forma parte de hello UPD.

## <a name="can-i-disable-upds-for-a-collection"></a>¿Puedo deshabilitar los UPD para una colección?
Sí, puede pedir Azure RemoteApp toodisable UPD una suscripción, pero no puede hacer que usted mismo. Esto significa que se deshabilitará UPD para todas las colecciones de suscripción de Hola.

Puede ser conveniente UPD toodisable en cualquiera de hello siguientes situaciones: 

* Debe completar el acceso y el control de los datos de usuario (para fines de auditoría y revisión como instituciones financieras).
* Tiene 3rd terceros usuario generar perfiles de soluciones de administración de local y quiere toocontinue su uso en la implementación de Azure RemoteApp Unidos a un dominio. Esto requeriría Hola perfil agente toobe cargado en la imagen de hello gold. 
* No es necesario ningún almacenamiento de datos local o que tengan todos los datos en hello en la nube o archivo compartido y quiere que el almacenamiento de toocontrol de los datos localmente mediante Azure RemoteApp.

Vea [Deshabilitar discos de perfil de usuario (UPD) en Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) para obtener más información.

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a>¿Se puede impedir que los usuarios guardar la unidad del sistema de toohello de datos?
Sí, pero deberá tooset que la de plantilla de hello de la imagen antes de crear la colección de Hola. Usar hello después de la unidad del sistema de pasos tooblock acceso toohello:

1. Ejecutar **gpedit.msc** en la imagen de la plantilla de Hola.
2. Navegue demasiado**configuración de usuario > plantillas administrativas > componentes de Windows > explorador**.
3. Seleccione Hola siguientes opciones:
   * **Ocultar estas unidades especificadas en Mi PC**
   * **Impedir el acceso toodrives desde Mi PC**

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a>¿Se pueden propagar los UPD? Deseo tooput algunos datos en hello UPD que está disponible Hola Hola usuario inicia sesión.
Sí, cuando se crea la imagen de la plantilla de hello, puede agregar información toohello perfil de manera predeterminada. Esa información se agrega entonces toohello UPD.

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a>¿Puedo cambiar tamaño de Hola de hello UPD según la cantidad de datos deseada toostore?
No, todos los UPD tienen 50 GB de almacenamiento. Si desea que toostore diferentes cantidades de datos, intente Hola siguiente:

1. Deshabilitar UPD para la recopilación de Hola.
2. Configurar un recurso compartido de archivos para los usuarios tooaccess.
3. Carga Hola archivo compartido mediante un script de inicio. Consulte a continuación para obtener detalles sobre los scripts de inicio en Azure RemoteApp.
4. Dirigir los usuarios toosave todos los recursos compartidos de archivos de toohello de datos.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>¿Cómo se ejecuta un script de inicio en Azure RemoteApp?
Si desea que toorun un script de inicio, comience creando una tarea programada en la imagen de la plantilla de Hola va toouse para la recopilación de Hola. (Haga esto *antes* de ejecutar sysprep). 

![Crear una tarea del sistema](./media/remoteapp-upd/upd1.png)

![Crear una tarea del sistema que se ejecute cuando un usuario inicia sesión](./media/remoteapp-upd/upd2.png)

En hello **General** ficha, ser seguro hello toochange **cuenta de usuario** con la seguridad demasiado "BUILTIN\Users".

![Cambiar el grupo de tooa de cuenta de usuario de Hola](./media/remoteapp-upd/upd4.png)

tarea programada de Hello iniciará el script de inicio, mediante las credenciales de usuario de Hola. Programar Hola tarea toorun cada una vez que un usuario inicia sesión.

![Conjunto Hola desencadenador de tarea hello como "En el inicio de sesión"](./media/remoteapp-upd/upd3.png)

También puede usar [Scripts de inicio basados en directivas de grupo](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a>¿Qué le parece y se coloca un script de inicio en hello menú Inicio? ¿Funcionaría?
¿En otras palabras, puedo crear un archivo .bat que se ejecuta un script de configuración de la ventana y guardar toohello c:\ProgramData\Microsoft\Windows\Start Inicio\Programas\Inicio carpeta y, a continuación, tener ese script que se ejecuta cada vez que un usuario inicia una sesión de RemoteApp?

No, que no es compatible con Azure RemoteApp, que utiliza RDSH, que también no admite scripts de inicio en el menú de inicio de Hola.

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a>¿Puedo usar scripts de inicio de sesión de mstsc.exe (programa de escritorio remoto de hello) tooconfigure?
No, no es compatible con Azure RemoteApp.

## <a name="can-i-store-data-on-hello-vm-locally"></a>¿Se puede almacenar datos en hello VM localmente?
NO, se perderán los datos almacenados en cualquier lugar en hello VM distinto en hello UPD. Hay un usuario de Hola de probabilidad alta no obtendrá Hola Hola VM mismo próxima vez que inicien sesión en Azure RemoteApp. No mantenemos persistencia de VM de usuario, por lo que el usuario de hello no iniciará sesión en Hola misma máquina virtual y se perderán datos Hola. Además, cuando se actualiza la colección de Hola, hello que las máquinas virtuales existentes se reemplazan por un nuevo conjunto de máquinas virtuales - que significa que todos los datos almacenados en hello propia máquina virtual se pierde. recomendación de Hello es toostore datos Hola UPD, almacenamiento compartido como los archivos de Azure, un servidor de archivos dentro de una red virtual, o en la nube de hello mediante un sistema de almacenamiento en la nube como DropBox.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>¿Cómo se puede montar un recurso compartido de Archivos de Azure en una máquina virtual usando PowerShell?
Puede usar Hola unidad Hola de Net-PSDrive cmdlet toomount, como se indica a continuación:

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


También puede guardar las credenciales mediante la ejecución Hola siguiente:

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Que permite omitir Hola - parámetro de credenciales en el cmdlet New-PSDrive Hola.

