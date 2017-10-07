---
title: un servicio en la nube con herramientas de Azure de hello aaaPublishing | Documentos de Microsoft
description: "Obtenga información acerca de cómo toopublish Azure cloud proyectos de servicio mediante Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/14/2017
ms.author: kraigb
ms.openlocfilehash: 31ede8308146de2bb128b768f23f64eb85bc7548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publishing-a-cloud-service-using-hello-azure-tools"></a>Publicar un servicio de nube mediante hello Azure Tools
Mediante el uso de hello Azure Tools para Microsoft Visual Studio, puede publicar su aplicación de Azure directamente desde Visual Studio. Visual Studio admite integrado publicar tooeither Hola almacenamiento provisional u Hola entorno de producción de un servicio de nube.

Para poder publicar una aplicación de Azure, debe tener una suscripción de Azure. También debe configurar un toobe nube almacenamiento y servicio de cuenta utilizado por la aplicación. Puede configurar estos en hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!IMPORTANT]
> Al publicar, puede seleccionar el entorno de implementación de hello para el servicio de nube. También debe seleccionar una cuenta de almacenamiento que sea el paquete de aplicación Hola toostore usado para la implementación. Después de la implementación, paquete de aplicación Hola se quita de la cuenta de almacenamiento de Hola.
> 
> 

Cuando se desarrolla y prueba una aplicación de Azure, puede usar Web Deploy toopublish cambios incrementalmente para sus roles web. Después de publicar el entorno de implementación de aplicación tooa, Web Deploy le permite implementar cambios directamente toohello está ejecutando máquina virtual rol web de Hola. No tiene toopackage y publicar la aplicación de Azure completa cada vez que desee tooupdate su tootest de rol web los cambios de Hola. Con este enfoque puede tener los cambios del rol web disponibles en la nube de Hola para realizar pruebas, sin toohave de espera, el entorno de implementación de aplicación tooa publicado.

Usar hello siguiendo los procedimientos toopublish su aplicación de Azure y tooupdate un rol web mediante Web Deploy:

* Publicar o empaquetar una aplicación de Azure desde Visual Studio
* Actualizar un rol web como parte de hello ciclo de desarrollo y prueba

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>Publicar o empaquetar una aplicación de Azure desde Visual Studio
Al publicar su aplicación de Azure, puede elegir entre Hola siguientes tareas:

* Crear un paquete de servicio: puede usar esta toopublish de archivo de configuración de servicio hello y paquete de su entorno de implementación de aplicación tooa de hello [Portal clásico de Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
* Publicar su proyecto de Azure desde Visual Studio: toopublish directamente tooAzure, use la aplicación Hola a Asistente para publicación. Para obtener información, consulte [Asistente Publicar aplicación de Azure](vs-azure-tools-publish-azure-application-wizard.md)

### <a name="toocreate-a-service-package-from-visual-studio"></a>toocreate un paquete de servicio desde Visual Studio
1. Cuando esté listo toopublish la aplicación, abra el Explorador de soluciones, menú contextual abierto Hola Hola proyecto de Azure que contiene sus roles, y elija Publicar.
2. toocreate un paquete de servicios, siga estos pasos:  
   
   1. En el menú contextual Hola Hola Azure proyecto de equipo y elija **paquete**.
   2. Hola **empaquetar aplicación de Azure** cuadro de diálogo, elija la configuración del servicio de hello para el que desea toocreate un paquete y, a continuación, elija Configuración de compilación de Hola.
   3. tooturn (opcional) en el escritorio remoto para servicio de nube Hola después de publicarlo, seleccione hello **habilitar Escritorio remoto para todos los Roles** casilla de verificación y, a continuación, seleccione **configuración** tooconfigure escritorio remoto. Si desea que toodebug su servicio en la nube después de publicarlo, activar la depuración remota mediante la selección **habilitar depurador remoto para todos los Roles**.
      
      Para más información, consulte [Usar Escritorio remoto con los roles de Azure](vs-azure-tools-remote-desktop-roles.md).
   4. Hola toocreate del paquete, elija hello **paquete** vínculo.
      
      Explorador de archivos muestra la ubicación de archivo de Hola de hello recién creado el paquete. Puede copiar esta ubicación para que pueda usarlo de hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).
   5. toopublish este entorno de implementación de paquete tooa, debe usar esta ubicación como Hola ubicación del paquete al crear un servicio de nube e implementar este entorno de tooan de paquete con hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).
3. Elija el proceso de implementación de hello toocancel (opcional), en directo de Hola de artículo de línea de hello en el registro de actividad de hello, **Cancelar y quitar**. Esto detiene el proceso de implementación de Hola y elimina el entorno de implementación de Hola de Azure.
   
   > [!NOTE]
   > tooremove este entorno de implementación después de ha sido implementado, debe usar hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).
   > 
   > 
4. (Opcional) Una vez se hayan iniciado las instancias de rol, Visual Studio muestra automáticamente el entorno de implementación de Hola Hola **servicios en la nube** nodo en el Explorador de servidores. Desde aquí, puede ver estado de Hola Hola individuales de instancias de rol. Vea [recursos de administración de Azure con el Explorador de nube](vs-azure-tools-resources-managing-with-cloud-explorer.md).hello siguiente ilustración muestra las instancias de rol Hola mientras están todavía en estado Initializing hello:
   
    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-hello-development-and-testing-cycle"></a>Actualizar un rol Web como parte del desarrollo de Hola y ciclo de pruebas
Si la infraestructura de back-end de la aplicación es estable, pero las funciones hello web necesitan actualizaciones más frecuentes, puede usar Web Deploy tooupdate solo un rol web en el proyecto. Esto es útil cuando no desee toorebuild y volver a implementar roles de trabajo de back-end de hello, o si tiene varios roles web y desea tooupdate solo uno de los roles de web Hola.

### <a name="requirements"></a>Requisitos
Estos es Hola requisitos toouse Web Deploy tooupdate su rol web:

* **Solo con fines de desarrollo y pruebas:** Hola se realizan cambios directamente toohello máquina donde se ejecuta el rol web de Hola. Si esta máquina virtual tiene toobe reciclando, cambios de Hola se pierden porque Hola del paquete original que publicó máquina de virtual hello toorecreate usado para el rol de Hola. Debe volver a publicar los cambios más recientes de aplicación tooget hello para el rol web de Hola.
* **Solo se pueden actualizar los roles web** : los roles de trabajo no se pueden actualizar. Además, no se puede actualizar hello RoleEntryPoint en web role.cs.
* **Solo puede admitir una instancia de un rol web** : no puede tener varias instancias de ningún rol web en su entorno de implementación. Sin embargo, se admiten varios roles web cada uno con solo una instancia.
* **Debe habilitar las conexiones a escritorio remotas:** esto es necesario para que Web Deploy pueda utilizar Hola usuario y contraseña tooconnect toohello máquina virtual toodeploy Hola cambios toohello servidor que ejecuta Internet Information Services (IIS). Además, tendrá que tooconnect toohello máquina virtual tooadd un tooIIS de certificados de confianza en esta máquina virtual. (Esto garantiza que la conexión remota de Hola de IIS que utiliza Web Deploy es segura).

Hello siguiente procedimiento se supone que está usando hello **publicar aplicación de Azure** asistente.

### <a name="tooenable-web-deploy-when-you-publish-your-application"></a>tooEnable implementar cuando se publique la aplicación Web
1. Hola tooenable **habilitar Web Deploy** para todas las web casilla de verificación de roles, primero debe configurar conexiones a Escritorio remoto. Seleccione **habilitar Escritorio remoto** para todas las funciones y, a continuación, especifique las credenciales de Hola que serán usado tooconnect remotamente en hello **configuración de escritorio remoto** cuadro que aparece. Consulte [Usar Escritorio remoto con los roles de Azure](vs-azure-tools-remote-desktop-roles.md) para obtener más información.
2. tooenable Web Deploy para todos Hola roles web en su aplicación, seleccione **habilitar Web Deploy para todos los roles web**.
   
    Se muestra un triángulo de advertencia amarillo. Web Deploy usa de forma predeterminada un certificado autofirmado no de confianza, que no se recomienda para cargar datos confidenciales. Si necesita toosecure este proceso para datos confidenciales, puede agregar un toobe de certificado SSL usado para las conexiones Web Deploy. Este certificado debe toobe un certificado de confianza. Para obtener información acerca de cómo toodo esto, consulte la sección de hello **tooMake implementar Secure Web** más adelante en este tema.
3. Elija **siguiente** tooshow hello **resumen** pantalla y, a continuación, elija **publicar** servicio en la nube toodeploy Hola.
   
    se publica el servicio en la nube Hola. máquina virtual de Hola que se crea tiene conexiones remotas habilitadas para IIS para que Web Deploy pueda tooupdate usado sus roles web sin volver a publicarlos.
   
   > [!NOTE]
   > Si tiene más de una instancia configurada para un rol web, aparece un mensaje de advertencia que indica que cada rol web será la instancia de tooone limitado sólo en paquete de Hola que ha creado toopublish su aplicación. Seleccione **Aceptar** toocontinue. Como se mencionó en la sección de requisitos de hello, puede tener más de un rol web, pero solo una instancia de cada rol.
   > 
   > 

### <a name="tooupdate-your-web-role-by-using-web-deploy"></a>tooUpdate su rol Web utilizando Web Deploy
1. toouse Web Deploy, asegúrese de proyecto de toohello de cambios de código para cualquiera de sus roles web en Visual Studio que desee toopublish y, a continuación, haga clic en este nodo de proyecto en la solución y elija demasiado**publicar**. Hola **Publicar Web** aparece el cuadro de diálogo.
2. (Opcional) Si ha agregado una confianza toouse de certificado SSL para las conexiones remotas para IIS, puede desactivar hello **certificado sin confianza permitir** casilla de verificación. Para obtener información sobre cómo tooadd una toomake certificado Web Deploy proteger, vea la sección hello **tooMake Web implementar segura** más adelante en este tema.
3. toouse Web Deploy, Hola publicar mecanismo necesita el nombre de usuario de Hola y la contraseña que configuró para la conexión a Escritorio remoto cuando publicó por primera vez el paquete de saludo.
   
   1. En **nombre de usuario**, escriba el nombre de usuario de Hola.
   2. En **contraseña**, escriba la contraseña de Hola.
   3. (Opcional) Elija si desea toosave esta contraseña en este perfil, **Guardar contraseña**.
4. rol de toopublish Hola cambios tooyour web, elija **publicar**.
   
    Muestra la línea de estado de Hello **publicar iniciado**. Cuando haya finalizado la publicación de hello, **publicar se realizó correctamente** aparece. cambios de Hello ahora han sido rol web de toohello implementado en la máquina virtual. Ahora puede iniciar la aplicación de Azure en hello entorno Azure tootest los cambios.

### <a name="toomake-web-deploy-secure"></a>tooMake implementar Secure Web
1. Web Deploy usa de forma predeterminada un certificado autofirmado no de confianza, que no se recomienda para cargar datos confidenciales. Si necesita toosecure este proceso para datos confidenciales, puede agregar un toobe de certificado SSL usado para las conexiones Web Deploy. Este certificado debe toobe un certificado de confianza, que se obtiene de una entidad de certificación (CA).
   
    toomake Web Deploy seguro para cada máquina virtual para cada uno de sus roles web, debe cargar el certificado de confianza de Hola que desee toouse por WebDeploy toohello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885). Esto asegura que ese certificado Hola se agrega la máquina virtual de toohello que se crea para el rol web de hello al publicar la aplicación.
2. tooadd una confianza toouse de tooIIS de certificado SSL para las conexiones remotas, siga estos pasos:
   
   1. máquina virtual de tooconnect toohello que se ejecuta el rol web de hello, instancia de select Hola de rol web de hello en **nube explorador** o **Explorador de servidores**y, a continuación, elija hello **conectar usando Escritorio remoto** comando. Para obtener pasos detallados acerca de cómo tooconnect toohello virtual machine, vea [usar Escritorio remoto con Roles de Azure](vs-azure-tools-remote-desktop-roles.md).
      
      El explorador le solicitará que toodownload una. Archivo RDP.
   2. tooadd un certificado SSL, servicio de administración de hello abierto en el Administrador de IIS. En el Administrador de IIS, habilite SSL por abrir hello **enlaces** vínculo Hola **acción** panel. Hola **Agregar enlace de sitio** aparece el cuadro de diálogo. Elija **agregar**y, a continuación, elija HTTPS en hello **tipo** lista desplegable. Hola **certificado SSL** lista, elija el certificado SSL de Hola que obtuvo firmado por una entidad de certificación y que cargó toohello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885). Para obtener más información, consulte [configurar opciones de conexión para el servicio de administración de hello](http://go.microsoft.com/fwlink/?LinkId=215824).
      
      > [!NOTE]
      > Si agrega un certificado SSL de confianza, triángulo de advertencia amarillo Hola ya no aparece en hello **Asistente para publicación**.
      > 
      > 

## <a name="include-files-in-hello-service-package"></a>Incluir archivos en hello paquete de servicio
Puede que tenga tooinclude determinados archivos en el paquete de servicio para que estén disponibles en la máquina virtual de Hola que se crea para un rol. Por ejemplo, conviene tooadd .exe o un archivo .msi que se usa un paquete de servicio de tooyour de script de inicio. O bien, podría necesitar tooadd un ensamblado que necesita un proyecto de rol web, rol o de trabajo. archivos de tooinclude deben ser agregan toohello solución para la aplicación de Azure.

### <a name="tooinclude-files-in-hello-service-package"></a>tooinclude archivos en el paquete del servicio de Hola
1. tooadd un paquete de servicio de tooa ensamblado, utilice Hola pasos:
   
   1. En **el Explorador de soluciones** nodo Hola Abrir proyecto de Hola que le falta el ensamblado hello al que hace referencia.
   2. proyecto de toohello ensamblado tooadd hello, menú contextual abierto Hola Hola **referencias** carpeta y, a continuación, elija **Agregar referencia**. aparece el cuadro de diálogo de agregar referencia de Hola.
   3. Elija Hola referencia que desee tooadd y, a continuación, elija hello **Aceptar** botón.
      
      referencia de Hola se agrega la lista toohello en hello **referencias** carpeta.
   4. Abra el menú contextual de hello para el ensamblado hello que agregó y elija **propiedades**. Hola **propiedades** aparecerá la ventana.
      
      tooinclude este ensamblado en el servicio de hello del paquete, en hello **lista Copy Local** elegir **True**.
2. En **el Explorador de soluciones** nodo Hola Abrir proyecto de Hola que le falta el ensamblado hello al que hace referencia.
3. proyecto de toohello ensamblado tooadd hello, menú contextual abierto Hola Hola **referencias** carpeta y, a continuación, elija **Agregar referencia**. Hola **Agregar referencia** aparece el cuadro de diálogo.
4. Elija Hola referencia que desee tooadd y, a continuación, elija hello **Aceptar** botón.
   
    referencia de Hola se agrega la lista toohello en hello **referencias** carpeta.
5. Abra el menú contextual de hello para el ensamblado hello que agregó y elija **propiedades**. aparece la ventana de propiedades de Hola.
6. tooinclude este ensamblado en el servicio de hello del paquete, en hello **Copy Local** elija **True**.
7. archivos de tooinclude en el paquete del servicio de Hola que se han agregado tooyour proyecto de rol web, abra el acceso directo de hello para el archivo hello y, a continuación, elija **propiedades**. De hello **propiedades** ventana, elija **contenido** de hello **acción de compilación** cuadro de lista.
8. archivos de tooinclude en el paquete del servicio de Hola que se han agregado tooyour proyecto de rol de trabajo, abra el acceso directo de hello para el archivo hello y, a continuación, elija **propiedades**. De hello **propiedades** ventana, elija **copiar si es posterior** de hello **toooutput directorio** cuadro de lista.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la publicación tooAzure desde Visual Studio, vea [Asistente para publicar aplicaciones de Azure](vs-azure-tools-publish-azure-application-wizard.md).

