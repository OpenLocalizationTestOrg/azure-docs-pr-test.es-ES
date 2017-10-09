---
title: aaaSet seguridad StorSimple Virtual Array como servidor de archivos | Documentos de Microsoft
description: "Este tercer tutorial de implementación de StorSimple Virtual Array indica tooset un dispositivo virtual como servidor de archivos."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89cade37980f342695c0adee42c4ade0e1d53d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a>Implementación de una matriz virtual de StorSimple: configurar un servidor de archivos mediante Azure Portal
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a>Introducción
Este artículo describe cómo registrar el servidor de archivos de StorSimple, configuración de dispositivo de hello completa, tooperform la instalación inicial y crear y conectarse a recursos compartidos de tooSMB. Se trata de hello último artículo de serie de Hola de tutoriales de implementación necesario toocompletely implementar la matriz virtual como un servidor de archivos o un servidor de iSCSI.

proceso de instalación y configuración de Hello puede tardar unos 10 toocomplete minutos. información de Hello en este artículo aplica solamente la implementación toohello de hello StorSimple Virtual Array. Para la implementación de Hola de dispositivos de la serie StorSimple 8000, vaya a: [implementar el dispositivo de la serie StorSimple 8000 ejecuta Update 2](storsimple-deployment-walkthrough-u2.md).

## <a name="setup-prerequisites"></a>Requisitos previos de instalación
Antes de instalar y configurar StorSimple Virtual Array, asegúrese de que:

* Se han aprovisionado una matriz virtual y tooit conectado como Hola detallada en [aprovisionar una matriz Virtual de StorSimple en Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) o [aprovisionar una matriz Virtual de StorSimple en VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
* Tiene la clave de registro del servicio de hello del servicio de administrador de dispositivos de StorSimple de Hola que creaste toomanage StorSimple Virtual matrices. Para obtener más información, consulte [paso 2: clave de registro del servicio de Get hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) para StorSimple Virtual Array.
* Si se trata de hello segunda o posteriores matriz virtual que va a registrar con un servicio de administrador de dispositivos de StorSimple existente, debe tener la clave de cifrado de datos del servicio de Hola. Esta clave se generó al primer dispositivo de Hola se registró correctamente con este servicio. Si se pierde esta clave, consulte [clave de cifrado de datos del servicio de Get hello](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) para la matriz Virtual de StorSimple.

## <a name="step-by-step-setup"></a>Configuración paso a paso
Usar hello seguimiento tooset instrucciones paso a paso una y configure la matriz Virtual de StorSimple.

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Paso 1: Completar web local de hello el programa de instalación de la interfaz de usuario y registrar el dispositivo
#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete Hola el programa de instalación y registrar un dispositivo Hola
1. Abra una ventana del explorador y conéctese toohello interfaz de usuario de web local. Escriba:
   
   `https://<ip-address of network interface>`
   
   Use la dirección URL de conexión de hello anotada en el paso anterior de Hola. Verá un error que indica que hay un problema con el certificado de seguridad del sitio Web de Hola. Haga clic en **continuar página Web toothis**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. Interfaz de usuario de la matriz virtual como web de inicio de sesión toohello **StorSimpleAdmin**. Escriba la contraseña del Administrador de dispositivos de Hola que cambió en el paso 3: matriz virtual de inicio hello en [aprovisionar una matriz Virtual de StorSimple en Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) o en [aprovisionar una matriz Virtual de StorSimple en VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. Se toman toohello **inicio** página. Esta página describe Hola varias opciones de configuración necesarias tooconfigure y registrar Hola matriz virtual con el servicio de administrador de dispositivos de StorSimple Hola. Hola **configuración de red**, **configuración de proxy Web**, y **configuración de tiempo** son opcionales. Hola solo requiere configuración **configuración de dispositivo** y **configuración de nube**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. Hola **configuración de red** página en **interfaces de red**, DATA 0 se configurarán automáticamente para usted. Cada interfaz de red establece automáticamente la dirección IP predeterminada tooget (DHCP). Por lo tanto, se asignan automáticamente una dirección IP, una subred y una puerta de enlace (tanto para IPv4 como para IPv6).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   Si agrega más de una interfaz de red durante el aprovisionamiento de hello de dispositivo de hello, se pueden configurar aquí. Tenga en cuenta que puede configurar la interfaz de red como IPv4 únicamente o como IPv4 e IPv6. No se admiten las configuraciones de solo IPv6.
5. Servidores DNS son necesarios, ya que se utilizan cuando el dispositivo intenta toocommunicate con los proveedores de servicios de almacenamiento de nube o tooresolve el dispositivo por su nombre cuando se configura como un servidor de archivos. Hola **configuración de red** página en hello **servidores DNS**:
   
   1. Se configuran automáticamente un servidor DNS principal y uno secundario. Si elige tooconfigure direcciones IP estáticas, puede especificar servidores DNS. Para lograr la alta disponibilidad, se recomienda que configure un servidor DNS principal y uno secundario.
   2. Haga clic en **aplicar** tooapply y validar la configuración de red de Hola.
6. Hola **configuración de dispositivo** página:
   
   1. Asignar un único **nombre** tooyour dispositivo. Este nombre puede tener de 1 a 15 caracteres y puede contener letras, números y guiones.
   2. Haga clic en hello **servidor de archivos** icono ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png) para hello **tipo** de dispositivo que está creando. Un servidor de archivos le permitirá toocreate compartir carpetas.
   3. Puesto que el dispositivo es un servidor de archivos, necesitará los dominios de tooa toojoin Hola dispositivo. Escriba un valor en **nombre de dominio**.
   4. Haga clic en **Apply**.
7. Aparece un cuadro de diálogo. Escriba sus credenciales de dominio en formato de hello especificado. Haga clic en el icono de verificación de Hola. se comprueban las credenciales de dominio de Hola. Verá un mensaje de error si Hola credenciales son incorrectas.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. Haga clic en **Apply**. Esto aplicará y validar la configuración de dispositivo de Hola.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > Asegúrese de que la matriz virtual está en su propia unidad organizativa (OU) de Active Directory y ningún objeto de directiva de grupo (GPO) está tooit aplicado o heredado. Directiva de grupo puede instalar aplicaciones como el software antivirus en hello StorSimple Virtual Array. Instalar otro software no se admite y podría provocar daños en toodata. 
   > 
   > 
9. Configure el servidor proxy web (de manera opcional). Aunque la configuración del proxy web es opcional, tenga en cuenta que, si usa un proxy web, solo puede configurarlo aquí.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   Hola **proxy Web** página:
   
   1. Fuente de alimentación hello **dirección URL del proxy Web** en este formato: *http://&lt;dirección IP de host o FQDN&gt;: número de puerto*. Tenga en cuenta que no se admiten direcciones URL HTTPS.
   2. Especifique **Autenticación** como **Básica** o **Ninguna**.
   3. Si utiliza la autenticación, también necesitará tooprovide una **nombre de usuario** y **contraseña**.
   4. Haga clic en **Apply**. Esto se valide y aplicar la configuración de proxy web de hello configurado.
10. (Opcional) configurar las opciones de tiempo de hello para el dispositivo, como la zona horaria y Hola servidores NTP principal y secundarios. Se requieren servidores NTP, ya que el dispositivo debe sincronizar la hora para que pueda autenticarse con los proveedores de servicios en la nube.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    Hola **configuración de tiempo** página:
    
    1. En la lista desplegable de hello, seleccione hello **zona horaria** basadas en ubicación geográfica de hello en qué Hola se va a implementar el dispositivo. zona de horaria predeterminada de Hello para el dispositivo es PST. El dispositivo usará esta zona horaria para todas las operaciones programadas.
    2. Especifique un **servidor NTP principal** para el dispositivo o acepte el valor predeterminado de Hola de time.windows.com. Asegúrese de que su red permite toopass de tráfico NTP desde su toohello de centro de datos Internet.
    3. Opcionalmente, especifique un **servidor NTP secundario** para el dispositivo.
    4. Haga clic en **Apply**. Esto se valide y aplicar la configuración de tiempo de hello configurado.
11. Configurar opciones de nube de hello para el dispositivo. En este paso, se complete la configuración del dispositivo local de hello y, a continuación, registrar dispositivo Hola con el servicio de administrador de dispositivos de StorSimple.
    
    1. Escriba hello **clave de registro del servicio** que obtuvo [paso 2: clave de registro del servicio de Get hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) para StorSimple Virtual Array.
    2. Si éste es el primer dispositivo de registro con este servicio, le presentará hello **clave de cifrado de datos de servicio**. Copie esta clave y guárdela en un lugar seguro, Esta clave es necesaria con hello servicio Registro tooregister clave dispositivos adicionales con hello servicio Administrador de dispositivos de StorSimple. 
       
       Si esto no es dispositivo primera Hola que va a registrar con este servicio, necesitará la clave de cifrado de datos del servicio de tooprovide Hola. Para obtener más información, consulte hello tooget [clave de cifrado de datos de servicio](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) en local de interfaz de usuario web.
    3. Haga clic en **Registrar**. Esto reiniciará el dispositivo de Hola. Puede que tenga toowait de 2 a 3 minutos antes de que se ha registrado correctamente el dispositivo de Hola. Una vez reiniciado el dispositivo de hello, se le llevará toohello inicio de sesión en la página.
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. Devolver toohello portal de Azure. Vaya demasiado**todos los recursos**, busque el servicio Administrador de dispositivos de StorSimple.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. Hola filtradas lista, seleccione el servicio de administrador de dispositivos de StorSimple y, a continuación, navegue demasiado**Administración > dispositivos**. Hola **dispositivos** hoja, compruebe ese dispositivo Hola se ha conectado correctamente el servicio de toohello y tiene el estado de hello **listo tooset seguridad**.
    
    ![Configurar un servidor de archivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-hello-device-as-file-server"></a>Paso 2: Configurar dispositivo hello como servidor de archivos
Realizar Hola siguiendo los pasos de hello [portal de Azure](https://portal.azure.com/) toocomplete Hola requiere el programa de instalación de dispositivos.

#### <a name="tooconfigure-hello-device-as-file-server"></a>dispositivo de hello tooconfigure como servidor de archivos
1. Servicio de administrador de dispositivos de StorSimple tooyour go y, a continuación, vaya demasiado **Administración > dispositivos**. Hola **dispositivos** hoja, un dispositivo de hello select que acaba de crear. Este dispositivo se mostrará como **listo tooset seguridad**.
   
   ![Configurar un servidor de archivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. Haga clic en el dispositivo de Hola y verá un mensaje de pancarta que indica que el dispositivo hello es toosetup listo.
   
    ![Configurar un servidor de archivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. Haga clic en **configurar** en la barra de comandos de Hola. Esto abrirá hello **configurar** hoja. Hola **configurar** hoja, Hola siguientes:
   
    1. nombre de servidor de archivos de Hola se rellena automáticamente.
    
    2. Asegúrese de que el cifrado de almacenamiento en nube Hola se establece demasiado**habilitado**. Esto, se cifrarán todos los datos de Hola se envían toohello en la nube. 
    
    3. Se utiliza una clave AES de 256 bits con clave definidas por el usuario de hello para el cifrado. Especifique una clave de 32 caracteres y, a continuación, vuelva a escribir tooconfirm clave Hola se. Clave de Hola de registro en una aplicación de administración de claves para futuras referencias.
    
    4. Haga clic en **establecer configuración obligatoria** credenciales de la cuenta de almacenamiento de toospecify toobe utilizado con el dispositivo. Haga clic en **Agregar nuevo** si no hay ninguna credencial de la cuenta de almacenamiento configurada. **Asegúrese de que cuenta de almacenamiento de Hola que use admite blobs en bloques. No se admiten blobs en páginas.** Más información sobre [blobs en bloques y blobs en páginas](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).
   
    ![Configurar un servidor de archivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. Hola **agregar credenciales de la cuenta de almacenamiento** hoja, Hola siguientes: 

    1. Elija la suscripción actual cuando haya cuenta de almacenamiento de Hola Hola misma suscripción que el servicio de Hola. Especifique otro es almacenamiento Hola cuenta está fuera de la suscripción al servicio Hola. 
    
    2. En la lista desplegable de hello, elija una cuenta de almacenamiento existente. 
    
    3. ubicación de Hola se rellenarán automáticamente en función de hello especificado cuenta de almacenamiento. 
    
    4. Habilitar SSL tooensure un canal de comunicación de red segura entre dispositivos de Hola y de nube de Hola.
    
    5. Haga clic en **agregar** tooadd credencial de cuenta de este almacenamiento. 
   
        ![Configurar un servidor de archivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. Una vez que se crea correctamente la credencial de cuenta de almacenamiento de hello, Hola **configurar** hoja se actualizará hello toodisplay especificó las credenciales de cuenta de almacenamiento. Haga clic en **Configurar**.
   
   ![Configurar un servidor de archivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   Verá que se crea un servidor de archivos. Una vez que el servidor de archivos de Hola se crea correctamente, se le notificará.
   
   ![Configurar un servidor de archivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   estado del dispositivo Hello también cambiará demasiado**Online**.
   
   ![Configurar un servidor de archivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   Puede continuar tooadd un recurso compartido.

## <a name="step-3-add-a-share"></a>Paso 3: Agregar un recurso compartido
Realizar Hola siguiendo los pasos de hello [portal de Azure](https://portal.azure.com/) toocreate un recurso compartido.

#### <a name="toocreate-a-share"></a>toocreate un recurso compartido
1. Seleccionar dispositivo de servidor de archivo Hola que configuró en hello anterior paso y haga clic en **...**  (o secundario). En el menú contextual de hello, seleccione **recurso compartido de agregar**. Como alternativa, puede hacer clic en **+ Agregar recurso compartido** en la barra de comandos de dispositivo de Hola.
   
   ![Agregar un recurso compartido](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. Especifique Hola después de la configuración del recurso compartido:

    1. Un nombre exclusivo para el recurso compartido. nombre de Hello debe ser una cadena que contiene 3 too127 caracteres.
    
    2. Opcional **descripción** para el recurso compartido de Hola. Descripción de Hello le ayudará a identificar los propietarios del recurso compartido de Hola.
    
    3. A **tipo** para el recurso compartido de Hola. Hola tipo puede ser **"en capas"** o **anclado localmente**, con la que se va a en capas Hola de forma predeterminada. Para las cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione un recurso compartido **Anclado localmente** . Para todos los demás datos, seleccione un recurso compartido **En capas** .
    Un recurso compartido de anclados localmente se realiza un aprovisionamiento grueso y asegura que los datos principal de hello en el recurso compartido de Hola permanece dispositivo toohello local y no volcarse toohello en la nube. Un recurso compartido en capas en hello con aprovisionamiento fino otra parte. Cuando se crea un recurso compartido en capas, 10% de espacio de Hola se aprovisionó en nivel local hello y 90% del espacio de Hola se aprovisiona en nube Hola. Por ejemplo, si ha aprovisionado un volumen de 1 TB, 100 GB residiría en el espacio local hello y 900 GB se utilizaría en nube Hola Hola cuando capas de datos. A su vez, esto implica que si se ejecuta fuera de todo el espacio local en hello en dispositivo hello, no se puede aprovisionar un recurso compartido en capas.
   
    4. Hola **establezca predeterminados todos los permisos** , a continuación, asignar Hola permisos toohello, usuario o grupo de Hola que tenga acceso a este recurso compartido. Especifique Hola nombre de usuario de Hola o grupo de usuarios de hello en  *john@contoso.com*  formato. Se recomienda usar un tooaccess de privilegios de administrador de usuario grupo (en lugar de un solo usuario) tooallow estos recursos compartidos. Después de haber asignado permisos de hello aquí, a continuación, puede usar estos permisos toomodify del explorador de archivos.
   
    5. Haga clic en **agregar** recurso compartido de hello toocreate. 
    
        ![Agregar un recurso compartido](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        Se le notifica que la creación de recursos compartidos de hello está en curso.
   
        ![Agregar un recurso compartido](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    Una vez creado el recurso compartido de hello con hello especificada configuración, hello **recursos compartidos** hoja actualizará el nuevo recurso compartido de hello tooreflect. De forma predeterminada, supervisión y copia de seguridad están habilitadas para el recurso compartido de Hola.
   
    ![Agregar un recurso compartido](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-toohello-share"></a>Paso 4: Conectar el recurso compartido de toohello
Ahora deberá tooconnect tooone o más recursos compartidos que creó en el paso anterior de Hola. Realice estos pasos en su tooyour de host conectado de Windows Server StorSimple Virtual Array.

#### <a name="tooconnect-toohello-share"></a>recurso compartido de toohello tooconnect
1. Presione ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) + r. En la ventana de la ejecución de hello, especifique hello *&#92; &#92;&lt; nombre del servidor de archivos&gt;*  como ruta de acceso de hello, reemplazando *el nombre del servidor de archivos* con dispositivo Hola nombre que se tooyour asignado servidor de archivos. Haga clic en **Aceptar**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. Se abre el Explorador de archivos. Ahora debe ser capaz de toosee recursos compartidos de Hola que crean como carpetas. Seleccione y haga doble clic en un contenido de hello tooview de recurso compartido (carpeta).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. Ahora puede agregar recursos compartidos de archivos toothese y realice una copia de seguridad.

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo toouse Hola IU web local demasiado[administrar la matriz Virtual de StorSimple](storsimple-ova-web-ui-admin.md).

