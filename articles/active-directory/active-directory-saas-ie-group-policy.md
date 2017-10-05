---
title: "Implementación de la extensión del Panel de acceso de Azure para Internet Explorer mediante un objeto de directiva de grupo (GPO) | Microsoft Docs"
description: "Cómo usar la directiva de grupo para implementar el complemento de Internet Explorer para el portal de Mis aplicaciones."
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
ms.openlocfilehash: b402ae326ab34ec71ad9de966e22be00045fee3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-deploy-the-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="c0e97-103">Implementación de la extensión de panel de acceso para Internet Explorer mediante la directiva de grupo</span><span class="sxs-lookup"><span data-stu-id="c0e97-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="c0e97-104">En este tutorial se muestra cómo usar la directiva de grupo para instalar de forma remota la extensión de panel de acceso para Internet Explorer en los equipos de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c0e97-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="c0e97-105">Esta extensión es necesaria para los usuarios de Internet Explorer que deben iniciar sesión en aplicaciones que están configuradas con un [inicio de sesión único basado en contraseña](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="c0e97-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="c0e97-106">Se recomienda que los administradores automaticen la implementación de esta extensión.</span><span class="sxs-lookup"><span data-stu-id="c0e97-106">It is recommended that admins automate the deployment of this extension.</span></span> <span data-ttu-id="c0e97-107">De lo contrario, los usuarios tendrán que descargar e instalar la extensión por sí mismos, lo que puede ocasionar errores y además requiere permisos de administrador.</span><span class="sxs-lookup"><span data-stu-id="c0e97-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span></span> <span data-ttu-id="c0e97-108">En este tutorial, se trata un método para automatizar las implementaciones de software mediante la directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="c0e97-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="c0e97-109">Más información acerca de la directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="c0e97-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="c0e97-110">La extensión de panel de acceso también está disponible para [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) y [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), ninguno de los cuales requieren permisos de administrador para la instalación.</span><span class="sxs-lookup"><span data-stu-id="c0e97-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0e97-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c0e97-111">Prerequisites</span></span>
* <span data-ttu-id="c0e97-112">Configuró [Servicios de dominio de Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)y unió los equipos de los usuarios a su dominio.</span><span class="sxs-lookup"><span data-stu-id="c0e97-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>
* <span data-ttu-id="c0e97-113">Debe tener el permiso "Editar configuración" para editar el objeto de directiva de grupo (GPO).</span><span class="sxs-lookup"><span data-stu-id="c0e97-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="c0e97-114">De forma predeterminada, los miembros de los siguientes grupos de seguridad poseen este permiso: Administradores de dominio, Administradores de organización y Propietarios del creador de directivas de grupo.</span><span class="sxs-lookup"><span data-stu-id="c0e97-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="c0e97-115">Más información.</span><span class="sxs-lookup"><span data-stu-id="c0e97-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-the-distribution-point"></a><span data-ttu-id="c0e97-116">Paso 1: Crear el punto de distribución</span><span class="sxs-lookup"><span data-stu-id="c0e97-116">Step 1: Create the Distribution Point</span></span>
<span data-ttu-id="c0e97-117">En primer lugar, debe colocar el paquete del instalador en una ubicación de red a la que se pueda acceder desde todas las máquinas donde desee instalar la extensión de forma remota.</span><span class="sxs-lookup"><span data-stu-id="c0e97-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span></span> <span data-ttu-id="c0e97-118">Para ello, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c0e97-118">To do this, follow these steps:</span></span>

1. <span data-ttu-id="c0e97-119">Inicie sesión en el servidor como administrador.</span><span class="sxs-lookup"><span data-stu-id="c0e97-119">Log on to the server as an administrator</span></span>
2. <span data-ttu-id="c0e97-120">En la ventana **Administrador del servidor**, vaya a **Servicios de archivos y almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-120">In the **Server Manager** window, go to **Files and Storage Services**.</span></span>
   
    ![Abra Servicios de archivos y almacenamiento.](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="c0e97-122">Vaya a la pestaña **Recursos compartidos** . A continuación, haga clic en **Tareas** > **Nuevo recurso compartido...**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Abra Servicios de archivos y almacenamiento.](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="c0e97-124">Complete el **Asistente para nuevo recurso compartido** y establezca permisos para asegurarse de que se pueda acceder desde los equipos de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c0e97-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="c0e97-125">Más información acerca de los recursos compartidos.</span><span class="sxs-lookup"><span data-stu-id="c0e97-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="c0e97-126">Descargue el paquete de Microsoft Windows Installer (archivo .msi) siguiente: [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="c0e97-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="c0e97-127">Copie el paquete del instalador en la ubicación deseada del recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="c0e97-127">Copy the installer package to a desired location on the share.</span></span>
   
    ![Copie el archivo .msi en el recurso compartido.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="c0e97-129">Compruebe que los equipos cliente tengan acceso al paquete de instalador desde el recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="c0e97-129">Verify that your client machines are able to access the installer package from the share.</span></span> 

## <a name="step-2-create-the-group-policy-object"></a><span data-ttu-id="c0e97-130">Paso 2: Crear el objeto de directiva de grupo</span><span class="sxs-lookup"><span data-stu-id="c0e97-130">Step 2: Create the Group Policy Object</span></span>
1. <span data-ttu-id="c0e97-131">Inicie sesión en el servidor que hospeda la instalación de Servicios de dominio de Active Directory (AD DS).</span><span class="sxs-lookup"><span data-stu-id="c0e97-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="c0e97-132">En el Administrador del servidor, vaya a **Herramientas** > **Administración de directivas de grupo**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span></span>
   
    ![Vaya a Herramientas > Administración de directivas de grupo.](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="c0e97-134">En el panel izquierdo de la ventana **Administración de directivas de grupo** , vea la jerarquía de unidad organizativa (OU) y determine en qué ámbito desea aplicar la directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="c0e97-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span></span> <span data-ttu-id="c0e97-135">Por ejemplo, puede decidir elegir una unidad organizativa pequeña para implementarla en unos cuantos usuarios para probarla o puede seleccionar una de nivel superior para implementarla en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="c0e97-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c0e97-136">Si desea crear o editar sus unidades organizativas (OU), vuelva al Administrador del servidor y vaya a **Herramientas** > **Usuarios y equipos de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="c0e97-137">Cuando haya seleccionado una unidad organizativa, haga clic con el botón derecho en ella y seleccione **Crear un GPO en este dominio y vincularlo aquí...**</span><span class="sxs-lookup"><span data-stu-id="c0e97-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Cree un nuevo GPO.](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="c0e97-139">En el símbolo **Nuevo GPO** , escriba un nombre para el nuevo objeto de directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="c0e97-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span></span>
   
    ![Asigne nombre al nuevo GPO.](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="c0e97-141">Haga clic con el botón derecho en el objeto de directiva de grupo que acaba de crear y seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-141">Right-click the Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Edite el nuevo GPO.](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-the-installation-package"></a><span data-ttu-id="c0e97-143">Paso 3: Asignar el paquete de instalación</span><span class="sxs-lookup"><span data-stu-id="c0e97-143">Step 3: Assign the Installation Package</span></span>
1. <span data-ttu-id="c0e97-144">Determine si desea implementar la extensión según **Configuración del equipo** o **Configuración de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="c0e97-145">Cuando use [Configuración del equipo](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), la extensión se instalará en el equipo sin tener en cuenta qué usuarios inician sesión en él.</span><span class="sxs-lookup"><span data-stu-id="c0e97-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span></span> <span data-ttu-id="c0e97-146">Con [Configuración de usuario](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), la extensión se instalará automáticamente para los usuarios independientemente de en qué equipo inicien sesión.</span><span class="sxs-lookup"><span data-stu-id="c0e97-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="c0e97-147">En el panel izquierdo de la ventana **Editor de administración de directivas de grupo** , vaya a cualquiera de las siguientes rutas de carpeta, en función del tipo de configuración que eligiera:</span><span class="sxs-lookup"><span data-stu-id="c0e97-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="c0e97-148">Haga clic con el botón derecho en **Instalación de software** y después seleccione **Nuevo** > **Paquete...**</span><span class="sxs-lookup"><span data-stu-id="c0e97-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Cree un nuevo paquete de instalación de software.](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="c0e97-150">Vaya a la carpeta compartida que contiene el paquete del instalador del [Paso 1: Crear el punto de distribución](#step-1-create-the-distribution-point), seleccione el archivo .msi y haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c0e97-151">Si el recurso compartido se encuentra en este mismo servidor, compruebe que tiene acceso el archivo .msi a través de la ruta de archivo de red, en lugar de la ruta de archivo local.</span><span class="sxs-lookup"><span data-stu-id="c0e97-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span></span>
   > 
   > 
   
    ![Seleccione el paquete de instalación de la carpeta compartida.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="c0e97-153">En el símbolo **Implementar software**, seleccione **Asignado** para el método de implementación</span><span class="sxs-lookup"><span data-stu-id="c0e97-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="c0e97-154">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-154">Then click **OK**.</span></span>
   
    ![Seleccione Asignado y haga clic en Aceptar.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="c0e97-156">Ahora se implementa la extensión en la unidad organizativa que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="c0e97-156">The extension is now deployed to the OU that you selected.</span></span> [<span data-ttu-id="c0e97-157">Más información acerca de la instalación de software de directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="c0e97-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-the-extension-for-internet-explorer"></a><span data-ttu-id="c0e97-158">Paso 4: Habilitar automáticamente la extensión para Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c0e97-158">Step 4: Auto-Enable the Extension for Internet Explorer</span></span>
<span data-ttu-id="c0e97-159">Además de ejecutar el programa de instalación, todas las extensiones de Internet Explorer deben habilitarse explícitamente para poder usarlas.</span><span class="sxs-lookup"><span data-stu-id="c0e97-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="c0e97-160">Siga estos pasos para habilitar la extensión de panel de acceso mediante la directiva de grupo:</span><span class="sxs-lookup"><span data-stu-id="c0e97-160">Follow the steps below to enable the Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="c0e97-161">En la ventana **Editor de administración de directivas de grupo** , vaya a cualquiera de las siguientes rutas, en función del tipo de configuración que eligiera en [Paso 3: Asignar el paquete de instalación](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="c0e97-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="c0e97-162">Haga clic con el botón derecho en **Lista de complementos** y seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="c0e97-163">![Edite la lista de complementos.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="c0e97-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="c0e97-164">En la ventana **Lista de complementos**, seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-164">In the **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="c0e97-165">Después, en la sección **Opciones**, haga clic en **Mostrar**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-165">Then, under the **Options** section, click **Show...**.</span></span>
   
    ![Haga clic en Habilitar y después en Mostrar.](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="c0e97-167">En la ventana **Mostrar contenido** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c0e97-167">In the **Show Contents** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="c0e97-168">Para la primera columna (el campo **Nombre de valor**), copie y pegue el siguiente identificador de clase:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="c0e97-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="c0e97-169">Para la segunda columna (el campo **Valor**), escriba el siguiente valor: `1`</span><span class="sxs-lookup"><span data-stu-id="c0e97-169">For the second column (the **Value** field), type in the following value: `1`</span></span>
   3. <span data-ttu-id="c0e97-170">Haga clic en **Aceptar** para cerrar la ventana **Mostrar contenido**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-170">Click **OK** to close the **Show Contents** window.</span></span>
      
      ![Rellene los valores como se especificó.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="c0e97-172">Haga clic en **Aceptar** para aplicar los cambios y cerrar la ventana **Lista de complementos**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-172">Click **OK** to apply your changes and close the **Add-on List** window.</span></span>

<span data-ttu-id="c0e97-173">Ahora, la extensión debería estar habilitada para los equipos de la unidad organizativa seleccionada.</span><span class="sxs-lookup"><span data-stu-id="c0e97-173">The extension should now be enabled for the machines in the selected OU.</span></span> [<span data-ttu-id="c0e97-174">Más información acerca de cómo usar la directiva de grupo para habilitar o deshabilitar complementos de Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="c0e97-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="c0e97-175">Paso 5 (opcional): deshabilitar el mensaje "Recordar contraseña"</span><span class="sxs-lookup"><span data-stu-id="c0e97-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="c0e97-176">Cuando los usuarios inician sesión en sitios web mediante la extensión del panel de acceso, es posible que Internet Explorer muestre el siguiente mensaje preguntándole "¿Desea almacenar su contraseña?"</span><span class="sxs-lookup"><span data-stu-id="c0e97-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="c0e97-177">Si desea impedir que los usuarios vean este mensaje, a continuación, siga estos pasos para evitar que Autocompletar recuerde las contraseñas:</span><span class="sxs-lookup"><span data-stu-id="c0e97-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="c0e97-178">En la ventana **Editor de administración de directivas de grupo** , vaya a la ruta de acceso indicada a continuación.</span><span class="sxs-lookup"><span data-stu-id="c0e97-178">In the **Group Policy Management Editor** window, go to the path listed below.</span></span> <span data-ttu-id="c0e97-179">Esta opción de configuración solo está disponible en **Configuración de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="c0e97-180">Busque el valor denominado **Activar la función Autocompletar para nombres de usuario y contraseñas en formularios**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c0e97-181">Es posible que las versiones anteriores de Active Directory muestren esta configuración del modo siguiente: **No permitir que autocompletar guarde las contraseñas**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span></span> <span data-ttu-id="c0e97-182">La configuración de esa opción varía de la descrita en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c0e97-182">The configuration for that setting differs from the setting described in this tutorial.</span></span>
   > 
   > 
   
    ![No olvide buscar esto en Configuración de usuario.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="c0e97-184">Haga clic con el botón derecho en la configuración anterior y seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-184">Right click the above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="c0e97-185">En la ventana **Activar la función Autocompletar para nombres de usuario y contraseñas en formularios**, seleccione **Deshabilitado**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Seleccione Deshabilitar](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="c0e97-187">Haga clic en **Aceptar** para aplicar estos cambios y cerrar la ventana.</span><span class="sxs-lookup"><span data-stu-id="c0e97-187">Click **OK** to apply these changes and close the window.</span></span>

<span data-ttu-id="c0e97-188">Los usuarios ya no podrán almacenar sus credenciales ni usar Autocompletar para tener acceso a las credenciales almacenadas previamente.</span><span class="sxs-lookup"><span data-stu-id="c0e97-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span></span> <span data-ttu-id="c0e97-189">Sin embargo, esta directiva permite a los usuarios seguir usando Autocompletar para otros tipos de campos de formulario, como campos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c0e97-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="c0e97-190">Si se habilita esta directiva después de que los usuarios hayan decidido almacenar algunas credenciales, esta directiva *no* borrará las credenciales que ya se han almacenado.</span><span class="sxs-lookup"><span data-stu-id="c0e97-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-the-deployment"></a><span data-ttu-id="c0e97-191">Paso 6: Prueba de la implementación</span><span class="sxs-lookup"><span data-stu-id="c0e97-191">Step 6: Testing the Deployment</span></span>
<span data-ttu-id="c0e97-192">Siga estos pasos para comprobar si la implementación de la extensión se realizó correctamente:</span><span class="sxs-lookup"><span data-stu-id="c0e97-192">Follow the steps below to verify if the extension deployment was successful:</span></span>

1. <span data-ttu-id="c0e97-193">Si implementó con **Configuración del equipo**, inicie sesión en un equipo cliente que pertenezca a la unidad organizativa que seleccionó en el [Paso 2: Crear el objeto de directiva de grupo](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="c0e97-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="c0e97-194">Si implementó con **Configuración de usuario**, asegúrese de iniciar sesión como un usuario que pertenezca a esa unidad organizativa.</span><span class="sxs-lookup"><span data-stu-id="c0e97-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span></span>
2. <span data-ttu-id="c0e97-195">Es posible que se deba iniciar sesión un par de veces para que los cambios de la directiva de grupo se actualicen totalmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c0e97-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span></span> <span data-ttu-id="c0e97-196">Para forzar la actualización, abra una ventana **Símbolo del sistema** y ejecute el siguiente comando: `gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="c0e97-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="c0e97-197">Deberá reiniciar la máquina para que se lleve a cabo la instalación.</span><span class="sxs-lookup"><span data-stu-id="c0e97-197">You must restart the machine for the installation to take place.</span></span> <span data-ttu-id="c0e97-198">El arranque puede tardar mucho más tiempo del habitual mientras la extensión se instala.</span><span class="sxs-lookup"><span data-stu-id="c0e97-198">Bootup may take significantly more time than usual while the extension installs.</span></span>
4. <span data-ttu-id="c0e97-199">Después de reiniciar, abra **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="c0e97-200">En la esquina superior derecha de la ventana, haga clic en **Herramientas** (el icono de engranaje) y después seleccione **Administrar complementos**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Vaya a Herramientas > Administrar complementos.](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="c0e97-202">En la ventana **Administrar complementos**, compruebe que la **extensión de panel de acceso** se haya instalado y que su **Estado** se haya establecido en **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="c0e97-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span></span>
   
    ![Compruebe que la extensión de panel de acceso esté instalada y habilitada.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="c0e97-204">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="c0e97-204">Related Articles</span></span>
* [<span data-ttu-id="c0e97-205">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0e97-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c0e97-206">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0e97-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c0e97-207">Solución de problemas de la extensión del Panel de acceso para Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c0e97-207">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

