---
title: "Extensión del Panel de acceso de Azure para Internet Explorer utilizando un GPO aaaDeploy | Documentos de Microsoft"
description: "¿Cómo toouse grupo complemento de Internet Explorer de directiva toodeploy Hola para portal mis aplicaciones de Hola."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>¿Cómo tooDeploy Hola extensión del Panel de acceso para Internet Explorer utilizando la directiva de grupo
Este tutorial muestra cómo tooremotely de directiva de grupo de toouse instalar extensión de Panel de acceso de Hola para Internet Explorer en equipos de los usuarios. Esta extensión es necesaria para los usuarios de Internet Explorer que necesitan toosign en aplicaciones que se configuran mediante [basada en contraseña de inicio de sesión único](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

Se recomienda que administradores automatizan la implementación de Hola de esta extensión. En caso contrario, los usuarios tienen toodownload e instalan extensión de Hola por sí mismos, que es toouser propensas a errores y necesita permisos de administrador. En este tutorial, se trata un método para automatizar las implementaciones de software mediante la directiva de grupo. [Más información acerca de la directiva de grupo.](https://technet.microsoft.com/windowsserver/bb310732.aspx)

Hola extensión del Panel de acceso también está disponible para [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) y [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), ninguno de los cuales requieren tooinstall de permisos de administrador.

## <a name="prerequisites"></a>Requisitos previos
* Ha configurado [los servicios de dominio de Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), y se han unido a dominio de tooyour de máquinas de los usuarios.
* Debe tener Hola "Editar configuración de" permiso tooedit Hola objeto de directiva de grupo (GPO). De forma predeterminada, los miembros del programa Hola a los grupos de seguridad siguientes tienen este permiso: los administradores de dominio, los administradores de organización y propietarios del creador de directivas de grupo. [Más información.](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>Paso 1: Crear el punto de distribución de Hola
En primer lugar, debe colocar el paquete del instalador de hello en una ubicación de red que puede tener acceso a las máquinas de Hola que desee tooremotely instalar extensión de hello en. toodo, siga estos pasos:

1. Inicie sesión en el servidor de toohello como administrador
2. Hola **el administrador del servidor** ventana, vaya demasiado**servicios de almacenamiento y los archivos**.
   
    ![Abra Servicios de archivos y almacenamiento.](./media/active-directory-saas-ie-group-policy/files-services.png)
3. Vaya toohello **recursos compartidos** ficha. A continuación, haga clic en **Tareas** > **Nuevo recurso compartido...**.
   
    ![Abra Servicios de archivos y almacenamiento.](./media/active-directory-saas-ie-group-policy/shares.png)
4. Hola completa **nuevo Asistente de recurso compartido** y tooensure de conjunto de permisos que puede obtenerse a partir de máquinas de los usuarios. [Más información acerca de los recursos compartidos.](https://technet.microsoft.com/library/cc753175.aspx)
5. Descargar Hola después el paquete de Microsoft Windows Installer (archivo .msi): [Extension.msi del Panel de acceso](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. Copie la ubicación de tooa deseado del paquete de instalador de hello en el recurso compartido de Hola.
   
    ![Hola .msi archivo toohello recurso compartido.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. Compruebe que los equipos cliente tengan paquete del instalador de hello tooaccess capaz de recurso compartido de Hola. 

## <a name="step-2-create-hello-group-policy-object"></a>Paso 2: Crear Hola objeto de directiva de grupo
1. Inicie sesión en toohello servidor que hospeda la instalación de servicios de dominio de Active Directory (AD DS).
2. En el administrador del servidor de hello, vaya demasiado**herramientas** > **Group Policy Management**.
   
    ![Vaya tooTools > Administración de directivas de grupo](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. En panel izquierdo de Hola de hello **Group Policy Management** ventana, ver la jerarquía de unidad organizativa (OU) y determinar en qué ámbito que desea que la directiva de grupo de hello tooapply. Por ejemplo, puede decidir toopick un pequeño tooa toodeploy de unidad organizativa determinados usuarios para la prueba, o puede elegir una nivel superior OU toodeploy tooyour toda organización.
   
   > [!NOTE]
   > Si prefiere como toocreate o editar sus unidades organizativas (OU), cambiar toohello espera el administrador del servidor y vaya demasiado**herramientas** > **equipos y usuarios de Active Directory**.
   > 
   > 
4. Cuando haya seleccionado una unidad organizativa, haga clic con el botón derecho en ella y seleccione **Crear un GPO en este dominio y vincularlo aquí...**
   
    ![Cree un nuevo GPO.](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. Hola **nuevo GPO** símbolo del sistema, escriba un nombre para Hola nuevo objeto de directiva de grupo.
   
    ![Nombre hello nuevo GPO](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. Hola contextual objeto de directiva de grupo que ha creado y seleccione **editar**.
   
    ![Editar Hola nuevo GPO](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>Paso 3: Asignar Hola paquete de instalación
1. Determinar si desea que la extensión de hello toodeploy basada en **configuración del equipo** o **configuración de usuario**. Cuando se usa [configuración del equipo](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), extensión de Hola se instala en el equipo Hola sin tener en cuenta que los usuarios inician sesión tooit. Con [configuración de usuario](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), los usuarios tienen la extensión de hello instalado para ellos independientemente de los equipos en el que inicien sesión.
2. En panel izquierdo de Hola de hello **Editor de administración de directivas de grupo** ventana, vaya tooeither de hello siguiendo las rutas de acceso de carpeta, dependiendo del tipo de configuración elegido:
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. Haga clic con el botón derecho en **Instalación de software** y después seleccione **Nuevo** > **Paquete...**
   
    ![Cree un nuevo paquete de instalación de software.](./media/active-directory-saas-ie-group-policy/new-package.png)
4. Vaya toohello carpeta compartida que contiene el paquete del instalador Hola de [paso 1: crear el punto de distribución de hello](#step-1-create-the-distribution-point), seleccione el archivo .msi de hello y haga clic en **abiertos**.
   
   > [!IMPORTANT]
   > Si se encuentra el recurso compartido de hello en este mismo servidor, compruebe que está accediendo a través de la ruta de acceso de archivos de red de hello, en lugar de la ruta de acceso de archivo local de Hola Hola .msi.
   > 
   > 
   
    ![Seleccione el paquete de instalación de Hola desde la carpeta compartida de Hola.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. Hola **implementar Software** símbolo del sistema, seleccione **asignado** para el método de implementación. y, a continuación, haga clic en **Aceptar**.
   
    ![Seleccione Asignado y haga clic en Aceptar.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

extensión de Hello ahora está implementado toohello unidad organizativa que ha seleccionado. [Más información acerca de la instalación de software de directiva de grupo.](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>Paso 4: Hola de Auto-Enable extensión de Internet Explorer
Además instalador de hello toorunning, todas las extensiones de Internet Explorer debe habilitarse explícitamente antes de poder utilizarlo. Siga los pasos a continuación tooenable Hola Hola extensión del Panel de acceso mediante la directiva de grupo:

1. Hola **Editor de administración de directivas de grupo** ventana, vaya tooeither de hello siguiendo las rutas de acceso, dependiendo del tipo de configuración que eligió en el [paso 3: asignar Hola paquete de instalación](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. Haga clic con el botón derecho en **Lista de complementos** y seleccione **Editar**.
    ![Edite la lista de complementos.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. Hola **lista de complementos** ventana, seleccione **habilitado**. A continuación, en hello **opciones** sección, haga clic en **mostrar... **.
   
    ![Haga clic en Habilitar y después en Mostrar.](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. Hola **mostrar contenido** ventana, realizar Hola pasos:
   
   1. Para la primera columna de hello (hello **nombre del valor** campo), copie y pegue Hola siguiente Id. de clase:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Para la segunda columna de hello (hello **valor** campo), escriba Hola siguiente valor:`1`
   3. Haga clic en **Aceptar** tooclose hello **mostrar contenido** ventana.
      
      ![Rellene los valores de hello especificados anteriormente.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. Haga clic en **Aceptar** tooapply los cambios y cerrar hello **lista de complementos** ventana.

Hello extensión ahora debe estar habilitada para las máquinas de Hola Hola seleccionado OU. [Más información sobre el uso de tooenable de directiva de grupo o deshabilitar los complementos de Internet Explorer.](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>Paso 5 (opcional): deshabilitar el mensaje "Recordar contraseña"
Cuando los usuarios de inicio de sesión toowebsites con hello extensión del Panel de acceso, Internet Explorer puede mostrar los siguientes hello, símbolo del sistema que se pregunta "¿desea toostore su contraseña?"

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

Si desea que los usuarios vean este mensaje tooprevent, a continuación, siga estos pasos hello tooprevent Autocompletar respecto a contraseñas teniendo en cuenta:

1. Hola **Editor de administración de directivas de grupo** (ventana), ruta de acceso de toohello vaya enumerados a continuación. Esta opción de configuración solo está disponible en **Configuración de usuario**.
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. Buscar con el nombre de configuración de hello **activar la característica Autocompletar de Hola para nombres de usuario y contraseñas en formularios**.
   
   > [!NOTE]
   > Las versiones anteriores de Active Directory pueden enumerar esta configuración con nombre hello **no se admiten contraseñas de Autocompletar toosave**. configuración de Hola para dicha configuración difiere de hello configuración descrita en este tutorial.
   > 
   > 
   
    ![Recuerde toolook para esto en configuración de usuario.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. Haga clic en hello por encima de la configuración y seleccione **editar**.
4. En la ventana de hello titulada **activar la característica Autocompletar de Hola para nombres de usuario y contraseñas en formularios**, seleccione **deshabilitado**.
   
    ![Seleccione Deshabilitar](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. Haga clic en **Aceptar** tooapply estos cambios y la ventana hello cerrar.

Los usuarios ya no se pueda toostore capaz de sus credenciales o usar credenciales de Autocompletar tooaccess almacenado previamente. Sin embargo, esta directiva permite a los usuarios toocontinue toouse Autocompletar para otros tipos de campos de formulario, como campos de búsqueda.

> [!WARNING]
> Si esta directiva está habilitada después de que los usuarios eligió toostore algunas credenciales, realizará esta directiva *no* Borrar credenciales de Hola que ya han sido almacenadas.
> 
> 

## <a name="step-6-testing-hello-deployment"></a>Paso 6: Probar Hola implementación
Siga los pasos de hello debajo tooverify si la implementación de extensión de hello finalizó correctamente:

1. Si ha implementado utilizando **configuración del equipo**, inicio de sesión en un equipo cliente que pertenece toohello OU que seleccionó en [paso 2: crear objetos de directiva de grupo de hello](#step-2-create-the-group-policy-object). Si ha implementado utilizando **configuración de usuario**, realizar toosign seguro en como un usuario que pertenece toothat OU.
2. Puede tardar un par de inicio de sesión inicios Hola la directiva de grupo cambian toofully actualización a esta máquina. actualización de tooforce hello, abra un **símbolo** ventana y ejecución Hola siguiente comando:`gpupdate /force`
3. Debe reiniciar la máquina de hello para el contexto de tootake de instalación de Hola. Arranque puede tardar mucho más tiempo en el que instala habitual al extensión Hola.
4. Después de reiniciar, abra **Internet Explorer**. En la esquina superior derecha de Hola de ventana hello, haga clic en **herramientas** (icono de engranaje hello) y, a continuación, seleccione **administrar complementos**.
   
    ![Vaya tooTools > Administrar complementos](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. Hola **administrar complementos** ventana, compruebe que hello **extensión del Panel de acceso** se ha instalado y que su **estado** se estableció demasiado**habilitado**.
   
    ![Compruebe que Hola extensión del Panel de acceso está instalado y habilitado.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Solución de problemas de hello extensión del Panel de acceso de Internet Explorer](active-directory-saas-ie-troubleshooting.md)

