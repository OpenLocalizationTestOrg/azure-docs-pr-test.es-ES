---
title: "aaaRun cualquier aplicación de Windows en cualquier dispositivo con Azure RemoteApp | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooshare cualquier aplicación de Windows con los usuarios mediante el uso de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 961d40ca-9673-4977-aa54-d6b22fc61ce1
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 750f3b881e0cb671ff6e8f3e851bccdf2262d156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-any-windows-app-on-any-device-with-azure-remoteapp"></a>Ejecución de cualquier aplicación de Windows en cualquier dispositivo con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Puede ejecutar una aplicación de Windows en cualquier lugar, en cualquier dispositivo, ahora mismo, en serio: simplemente usando Azure RemoteApp. Si es una aplicación personalizada creada hace 10 años, o una aplicación de Office, los usuarios ya no tienen toobe vinculada tooa sistema operativo específico (por ejemplo, Windows XP) para las aplicaciones algunos.

Con Azure RemoteApp, los usuarios también pueden usar su propios Android o get y dispositivos de Apple Hola misma experiencia que se pusieron en Windows (o en dispositivos Windows Phone). Esto se logra al hospedar la aplicación de Windows en una colección de máquinas virtuales de Windows en Azure. Los usuarios pueden tener acceso desde cualquier lugar con una conexión a Internet. 

Siga leyendo para obtener un ejemplo de exactamente cómo toodo esto.

En este artículo, vamos tooshare acceso a todos los usuarios. Sin embargo, puede usar CUALQUIER aplicación. Como puede instalar la aplicación en un equipo Windows Server 2012 R2, puede compartir mediante estos pasos Hola. Puede revisar hello [requisitos de la aplicación](remoteapp-appreqs.md) toomake seguro de que funcionará la aplicación.

Por favor, tenga en cuenta que puesto que el acceso es una base de datos y que deseamos que toobe de base de datos útiles, se llevarán a cabo algunos pasos adicionales toolet a los usuarios tener acceso a recurso compartido de datos de Access de Hola. Si la aplicación no es una base de datos, o si no necesita la toobe de los usuarios pueden tooaccess un recurso compartido de archivos, puede omitir los pasos de este tutorial

> [!NOTE]
> <a name="note"></a>Necesita una cuenta de Azure toocomplete este tutorial:
> 
> * También puede [abrir una cuenta de Azure de forma gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F): obtenga créditos puede usar tootry los servicios de Azure de pago e incluso después de que se utilizan hasta puede mantener la cuenta de hello y libre de usar servicios de Azure, como sitios Web. Nunca se cargará su tarjeta de crédito a menos que cambiar la configuración y pida toobe cobrado explícitamente.
> * Puede [activar las ventajas de suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)- Su suscripción a MSDN le proporciona crédito todos los meses que puede usar con servicios de Azure de pago.
> 
> 

## <a name="create-a-collection-in-remoteapp"></a>Creación de una colección de RemoteApp
Empiece por crear una colección. colección de Hello actúa como un contenedor para sus aplicaciones y los usuarios. Cada colección se basa en una imagen; puede crear las suyas propias o utilizar una proporcionada con la suscripción. Para este tutorial, usamos la imagen de evaluación de hello Office 2013 - contiene aplicación hello que deseamos tooshare.

1. Hola portal de Azure, desplácese hacia abajo en el árbol de navegación izquierdo de hello hasta que vea RemoteApp. Abra esa página.
2. Haga clic en **Crear una colección de RemoteApp**.
3. Haga clic en **Creación rápida** y escriba un nombre para la colección.
4. Seleccione la región Hola desea toouse toocreate la colección. Para la mejor experiencia de hello, seleccione la región de Hola que esté más cercano geográficamente ubicación toohello donde los usuarios tendrán acceso a aplicación hello. Por ejemplo, en este tutorial, los usuarios de Hola se ubicará en Redmond, Washington. región de Azure más cercano de Hello es **West US**.
5. Seleccione el plan de facturación de hello que desea toouse. plan de facturación básica Hello coloca 16 usuarios en una máquina virtual grande de Azure, mientras el plan de facturación estándar hello tiene 10 usuarios en una máquina virtual de Azure grande. Como ejemplo general, plan básico de hello funciona muy bien para flujo de trabajo de tipo de entrada de datos. Para las aplicaciones de productividad, como Office, sería aconsejable plan estándar Hola.
6. Por último, seleccione la imagen de Office 2013 Professional Hola. Esta imagen contiene aplicaciones de Office 2013. Le recordamos que esta imagen solo es buena para colecciones de prueba y pruebas de concepto. Esta imagen no se puede usar en una colección de producción.
7. Ahora, haga clic en **Crear una colección de RemoteApp**.

![Creación de una colección en la nube en RemoteApp](./media/remoteapp-anyapp/ra-anyappcreatecollection.png)

Este modo inicia la creación de la colección, pero puede tardar hasta hora tooan.

Ahora que está listo tooadd los usuarios.

## <a name="share-hello-app-with-users"></a>Aplicación de hello de recurso compartido con usuarios
Una vez que la colección se ha creado correctamente, es hora toopublish acceso toousers y agregar usuarios de Hola que deben tener acceso a tooit.

Si ha navegado fuera de nodo de Azure RemoteApp Hola mientras se creaba la colección de hello, empiece por dirigiéndose realizar copia de tooit de hello página principal de Azure.

1. Haga clic en crear tooaccess anteriores opciones adicionales de colección de Hola y configurar la recopilación de Hola.
   ![Una nueva colección en la nube de RemoteApp](./media/remoteapp-anyapp/ra-anyappcollection.png)
2. En hello **publicación** , haga clic en **publicar** final Hola de pantalla de bienvenida y, a continuación, haga clic en **programas del menú Inicio publicar**.
   ![Publicación de un programa de RemoteApp](./media/remoteapp-anyapp/ra-anyapppublish.png)
3. Seleccionar aplicaciones Hola desea toopublish de lista de Hola. Para los fines de este tutorial, elegimos Access. Haga clic en **Completo**. Espere a que la publicación de hello aplicaciones toofinish.
   ![Publicación de Access en RemoteApp](./media/remoteapp-anyapp/ra-anyapppublishaccess.png)
4. Una vez que la aplicación hello ha terminado de publicar, diríjase toohello **acceso de usuario** ficha tooadd todos los usuarios de Hola que necesitan acceder a las aplicaciones de tooyour. Escriba los nombres de usuario (dirección de correo electrónico) de los usuarios y, a continuación, haga clic en **Guardar**.

![Agregar usuarios tooRemoteApp](./media/remoteapp-anyapp/ra-anyappaddusers.png)

1. Ahora, es hora tootell los usuarios acerca de estas nuevas aplicaciones y cómo tooaccess ellos. toodo, enviar a los usuarios un correo electrónico que se dirijan toohello de dirección URL de descarga del cliente de escritorio remoto.
   ![URL de descarga de cliente Hello de RemoteApp](./media/remoteapp-anyapp/ra-anyappurl.png)

## <a name="configure-access-tooaccess"></a>Configurar acceso tooAccess
Algunas aplicaciones necesitan configuración adicional después de implementarlas a través de RemoteApp. En concreto, para tener acceso, estamos toocreate continuo compartir un archivo en Azure que puede tener acceso cualquier usuario. (Si no desea toodo, puede crear un [colección híbrida](remoteapp-create-hybrid-deployment.md) [en lugar de la colección en la nube] que permite a los usuarios tener acceso a archivos y la información de la red local.) A continuación, se necesitará tootell nuestro toomap a los usuarios una unidad local en su sistema de archivos de Azure toohello de equipo.

Hola primera parte como Hola, administrador hace. Luego, tenemos algunos pasos que deben seguir los usuarios.

1. Empiece por la interfaz de línea de comandos (cmd.exe) de publicación Hola. Hola **publicación** ficha, seleccione **cmd**y, a continuación, haga clic en **publicar > programa de publicación con la ruta de acceso**.
2. Escriba el nombre de Hola de aplicación hello y ruta de acceso de Hola. Para nuestro propósito, utilice "Explorador de archivos" como nombre de Hola y "% SYSTEMDRIVE%\windows\explorer.exe" como ruta de acceso de Hola.
   ![Publicar el archivo de hello cmd.exe.](./media/remoteapp-anyapp/ra-publishcmd.png)
3. Ahora tiene un Azure toocreate [cuenta de almacenamiento](../storage/common/storage-create-storage-account.md). Hemos llamado al nuestro "accessstorage", así que elija un nombre que sea significativo tooyou. (toomisquote Highlander, puede haber solo un "accessstorage.") ![Cuenta de almacenamiento de Azure nuestra](./media/remoteapp-anyapp/ra-anyappazurestorage.png)
4. Ahora vuelva tooyour panel para que puedas (ubicación de punto de conexión) del almacenamiento de tooyour de ruta de acceso de Hola. La volverá a usar en un momento, así que asegúrese de copiarla en alguna parte.
   ![ruta de acceso de cuenta de almacenamiento de Hola](./media/remoteapp-anyapp/ra-anyappstoragelocation.png)
5. A continuación, una vez creada la cuenta de almacenamiento de hello, necesita clave de acceso principal de Hola. Haga clic en **administrar claves de acceso**y, a continuación, clave de acceso principal de copia Hola.
6. Ahora, establecer contexto de Hola de cuenta de almacenamiento de Hola y crear un nuevo recurso compartido de archivos para el acceso. Ejecute hello siguientes cmdlets en una ventana de Windows PowerShell con privilegios elevados:
   
        $ctx=New-AzureStorageContext <account name> <account key>
        $s = New-AzureStorageShare <share name> -Context $ctx
   
    Por lo que para nuestra cuota, éstos son cmdlets Hola ejecutamos:
   
        $ctx=New-AzureStorageContext accessstorage <key>
        $s = New-AzureStorageShare <share name> -Context $ctx

Ahora, lo turno del usuario de hello del. En primer lugar, pida a los usuarios que instalen un [cliente RemoteApp](remoteapp-clients.md). A continuación, los usuarios de hello necesitan toomap compartir una unidad de su archivos de Azure toothat de cuenta que ha creado y agregan sus archivos de acceso. Así es como deben hacerlo:

1. En el cliente de RemoteApp de hello, Hola de acceso a las aplicaciones publicadas. Inicie el programa de cmd.exe Hola.
2. Ejecute hello después comando toomap una unidad desde el recurso compartido de archivos de equipo toohello:
   
        net use z: \\<accountname>.file.core.windows.net\<share name> /u:<user name> <account key>
   
    Si establece hello **/ persistent** parámetro tooyes, hello unidad asignada se conservará en las sesiones.
3. Ahora, inicie la aplicación de explorador de archivos de hello de RemoteApp. Copie los archivos de acceso que desee toouse en el recurso compartido de archivos de hello aplicación compartido toohello.
   ![Colocación de los archivos de Access en un recurso compartido de Azure](./media/remoteapp-anyapp/ra-anyappuseraccess.png)
4. Por último, abra Access y, a continuación, abra la base de datos de Hola que acaba de compartir. Debería ver los datos en Access cuando se ejecuta desde la nube de Hola.
   ![Una base de datos de acceso real ejecutando desde la nube de Hola](./media/remoteapp-anyapp/ra-anyapprunningaccess.png)

Ahora puede utilizar Access en cualquiera de sus dispositivos, solo asegúrese de instalar un cliente de RemoteApp.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido a crear una colección, intente crear una [colección que usa Office 365](remoteapp-tutorial-o365anywhere.md). O bien, puede crear una [colección híbrida ](remoteapp-create-hybrid-deployment.md)que pueda tener acceso a la red local.

<!--Image references-->

