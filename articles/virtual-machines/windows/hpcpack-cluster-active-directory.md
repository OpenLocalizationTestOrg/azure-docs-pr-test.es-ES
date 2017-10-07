---
title: "aaaHPC módulo de clúster con Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar toointegrate una 2016 de HPC Pack en Azure con Azure Active Directory"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="1371e-103">Administrar un clúster de HPC Pack en Azure con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1371e-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="1371e-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) admite la integración con [Azure Active Directory](../../active-directory/index.md) (Azure AD) para los administradores que implementación un clúster de HPC Pack en Azure.</span><span class="sxs-lookup"><span data-stu-id="1371e-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="1371e-105">Siga los pasos de hello en este artículo para hello siguiente las tareas de nivel alto:</span><span class="sxs-lookup"><span data-stu-id="1371e-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="1371e-106">Integración manual del clúster de HPC Pack con el inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1371e-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="1371e-107">Administración y programación de trabajos en el clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="1371e-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="1371e-108">Integrar una solución de clúster de HPC Pack con Azure AD sigue los pasos estándar toointegrate otras aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="1371e-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="1371e-109">En este artículo se da por supuesto que está familiarizado con la administración básica de usuarios en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1371e-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="1371e-110">Para obtener más información y contexto, vea hello [documentación de Azure Active Directory](../../active-directory/index.md) y Hola pasos de la sección.</span><span class="sxs-lookup"><span data-stu-id="1371e-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="1371e-111">Ventajas de la integración</span><span class="sxs-lookup"><span data-stu-id="1371e-111">Benefits of integration</span></span>


<span data-ttu-id="1371e-112">Azure Active Directory (Azure AD) es un multiempresa en la nube identidades y directorios servicio de administración que proporciona acceso de inicio de sesión único (SSO) toocloud soluciones.</span><span class="sxs-lookup"><span data-stu-id="1371e-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="1371e-113">Integración de un clúster de HPC Pack con Azure AD puede ayudarle a conseguir Hola siguientes objetivos:</span><span class="sxs-lookup"><span data-stu-id="1371e-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="1371e-114">Quitar el controlador de dominio de Active Directory tradicional de Hola de clúster de HPC Pack Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="1371e-115">Esto puede ayudar a reducir los costes de Hola de mantenimiento de clúster de hello si esto no es necesario para su empresa y el proceso de implementación de acelerar Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="1371e-116">Aprovechar Hola después ventajas señalados por Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1371e-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="1371e-117">Inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="1371e-117">Single sign-on</span></span> 
    *   <span data-ttu-id="1371e-118">Con una identidad de AD local para el clúster de HPC Pack hello en Azure</span><span class="sxs-lookup"><span data-stu-id="1371e-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Entorno de Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="1371e-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1371e-120">Prerequisites</span></span>
* <span data-ttu-id="1371e-121">**Clúster de HPC Pack 2016 implementado en máquinas virtuales de Azure**: Para conocer los pasos, consulte [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md) (Implementación de un clúster de HPC Pack 2016 en Azure).</span><span class="sxs-lookup"><span data-stu-id="1371e-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="1371e-122">Necesita el nombre DNS de hello del nodo principal de Hola y las credenciales de Hola de un administrador de clústeres para completar los pasos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1371e-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1371e-123">La integración con Azure Active Directory no se admite en versiones de HPC Pack antes a HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="1371e-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="1371e-124">**Equipo cliente** -necesita un Windows o Windows Server cliente equipo ejecuta demasiado HPC Pack utilidades de cliente.</span><span class="sxs-lookup"><span data-stu-id="1371e-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="1371e-125">Si solo desea portal web de toouse Hola HPC Pack o trabajos de toosubmit de API de REST, puede usar todos los equipos cliente de su elección.</span><span class="sxs-lookup"><span data-stu-id="1371e-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="1371e-126">**Utilidades de cliente de HPC Pack** -instalar utilidades de cliente de HPC Pack Hola en los equipos de cliente de hello con el paquete de instalación gratuito de hello disponible desde Microsoft Download Center Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="1371e-127">Paso 1: Registrar servidor de clúster HPC de hello con su inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1371e-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="1371e-128">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1371e-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="1371e-129">Haga clic en **Active Directory** en Hola menú izquierdo y, a continuación, haga clic en directorio que desee hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="1371e-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="1371e-130">Debe tener permisos de los recursos tooaccess en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="1371e-131">Haga clic en **Usuarios** y asegúrese de que ya hay cuentas de usuario creadas o configuradas.</span><span class="sxs-lookup"><span data-stu-id="1371e-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="1371e-132">Haga clic en **Aplicaciones** > **Agregar** y luego en **Agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="1371e-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="1371e-133">Escriba Hola después información Hola asistente:</span><span class="sxs-lookup"><span data-stu-id="1371e-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="1371e-134">**Nombre**: HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="1371e-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="1371e-135">**Tipo**: Seleccione **Aplicación web y/o API web**</span><span class="sxs-lookup"><span data-stu-id="1371e-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="1371e-136">**Dirección URL de inicio de sesión**: hello dirección URL base para el ejemplo hello, que de forma predeterminada`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="1371e-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="1371e-137">**URI de id. de aplicación** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="1371e-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="1371e-138">Reemplace `<Directory_name`> con el nombre completo del inquilino de Azure AD, por ejemplo, hello `hpclocal.onmicrosoft.com`y reemplace `<application_name>` con nombre hello elegido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1371e-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="1371e-139">Después de agrega la aplicación hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="1371e-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="1371e-140">Configurar Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="1371e-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="1371e-141">Seleccione **Sí** en **La aplicación es multiempresa**.</span><span class="sxs-lookup"><span data-stu-id="1371e-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="1371e-142">Seleccione **Sí** para **usuario asignación requiere tooaccess aplicación**.</span><span class="sxs-lookup"><span data-stu-id="1371e-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="1371e-143">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1371e-143">Click **Save**.</span></span> <span data-ttu-id="1371e-144">Cuando se complete el almacenamiento, haga clic en **Administrar manifiesto**.</span><span class="sxs-lookup"><span data-stu-id="1371e-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="1371e-145">Esta acción descarga la notación de objetos JavaScript (JSON) del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1371e-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="1371e-146">Editar manifiesto de hello descargado ubicando hello `appRoles` establecimiento y adición de hello después de rol de aplicación:</span><span class="sxs-lookup"><span data-stu-id="1371e-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="1371e-147">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="1371e-147">Save hello file.</span></span> <span data-ttu-id="1371e-148">Haga clic en el portal de hello, **administrar manifiesto** > **cargar manifiesto**.</span><span class="sxs-lookup"><span data-stu-id="1371e-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="1371e-149">A continuación, puede cargar el manifiesto editado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="1371e-150">Haga clic en **Usuarios**, seleccione un usuario y luego haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="1371e-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="1371e-151">Asignar uno de usuario de toohello (HpcUsers o HpcAdminMirror) roles disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="1371e-152">Repita este paso con otros usuarios en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="1371e-153">Para información general sobre de los usuarios de clúster, consulte [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx) (Administrar usuarios de clústeres).</span><span class="sxs-lookup"><span data-stu-id="1371e-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="1371e-154">toomanage los usuarios, recomendamos usar la hoja de vista previa de Azure Active Directory de Hola Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1371e-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="1371e-155">Paso 2: Registrar el cliente de clúster HPC de hello con su inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1371e-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="1371e-156">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1371e-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="1371e-157">Haga clic en **Active Directory** en Hola menú izquierdo y, a continuación, haga clic en directorio que desee hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="1371e-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="1371e-158">Debe tener permisos de los recursos tooaccess en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="1371e-159">Haga clic en **Aplicaciones** > **Agregar** y luego en **Agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="1371e-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="1371e-160">Escriba Hola después información Hola asistente:</span><span class="sxs-lookup"><span data-stu-id="1371e-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="1371e-161">**Nombre**: HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="1371e-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="1371e-162">**Tipo**: Seleccione **Aplicación de cliente nativo**</span><span class="sxs-lookup"><span data-stu-id="1371e-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="1371e-163">**URI de redirección** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="1371e-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="1371e-164">Después de agrega la aplicación hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="1371e-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="1371e-165">Hola copia **Id. de cliente** valor y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="1371e-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="1371e-166">Lo necesitará más adelante cuando configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1371e-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="1371e-167">En **permisos tooother aplicaciones**, haga clic en **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="1371e-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="1371e-168">Buscar y Agregar aplicación de hello HpcPackClusterServer (creado en el paso 1).</span><span class="sxs-lookup"><span data-stu-id="1371e-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="1371e-169">Hola **permisos delegados** lista desplegable, seleccione **HpcClusterServer de acceso**.</span><span class="sxs-lookup"><span data-stu-id="1371e-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="1371e-170">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1371e-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="1371e-171">Paso 3: Configurar el clúster de HPC de Hola</span><span class="sxs-lookup"><span data-stu-id="1371e-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="1371e-172">Conecte el nodo principal de HPC Pack 2016 toohello en Azure.</span><span class="sxs-lookup"><span data-stu-id="1371e-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="1371e-173">Inicie PowerShell HPC.</span><span class="sxs-lookup"><span data-stu-id="1371e-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="1371e-174">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="1371e-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="1371e-175">donde</span><span class="sxs-lookup"><span data-stu-id="1371e-175">where</span></span>

    * <span data-ttu-id="1371e-176">`AADTenant`Especifica el nombre del inquilino de Azure AD de hello, como`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="1371e-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="1371e-177">`AADClientAppId`Especifica el identificador de cliente de hello para la aplicación hello creado en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="1371e-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="1371e-178">Reinicie el servicio de hello HpcSchedulerStateful.</span><span class="sxs-lookup"><span data-stu-id="1371e-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="1371e-179">En un clúster con varios nodos principales, puede ejecutar Hola siguiente comandos de PowerShell de hello nodo principal tooswitch Hola réplica principal de servicio de Hola HpcSchedulerStateful:</span><span class="sxs-lookup"><span data-stu-id="1371e-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="1371e-180">Paso 4: Administrar y enviar trabajos de cliente hello</span><span class="sxs-lookup"><span data-stu-id="1371e-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="1371e-181">Utilidades de cliente de HPC Pack tooinstall hello en el equipo, descargue los archivos de instalación de HPC Pack 2016 (instalación completa) de hello Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="1371e-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="1371e-182">Al comenzar la instalación de hello, elija la opción de instalación de Hola para hello **utilidades de cliente de HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="1371e-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="1371e-183">equipo de cliente de tooprepare hello, instalar certificado de hello usa durante la [el programa de instalación de clúster HPC](hpcpack-2016-cluster.md) en el equipo cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="1371e-184">Usar Windows estándares de certificados administración procedimientos tooinstall Hola certificado público toohello **certificados – usuario actual** > **entidades de certificación raíz de confianza** almacenar.</span><span class="sxs-lookup"><span data-stu-id="1371e-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="1371e-185">Ahora puede ejecutar comandos de HPC Pack Hola o usar Hola GUI del Administrador de trabajos de HPC Pack toosubmit y administrar trabajos del clúster mediante el uso de la cuenta de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1371e-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="1371e-186">Para opciones de envío de trabajos, consulte [clúster de HPC enviar trabajos tooan HPC Pack en Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="1371e-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="1371e-187">Al tratar de clúster de HPC Pack del toohello tooconnect en Azure para hello primera vez, aparece una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="1371e-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="1371e-188">Escriba su toolog de credenciales de Azure AD en.</span><span class="sxs-lookup"><span data-stu-id="1371e-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="1371e-189">símbolo (token) de Hello, a continuación, se almacena en caché.</span><span class="sxs-lookup"><span data-stu-id="1371e-189">hello token is then cached.</span></span> <span data-ttu-id="1371e-190">Clúster de toohello conexiones posterior Hola de uso de Azure almacena en caché símbolo (token), a menos que los cambios de autenticación o hello almacenado en memoria caché se borra.</span><span class="sxs-lookup"><span data-stu-id="1371e-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="1371e-191">Por ejemplo, después de completar los pasos anteriores de hello, puede consultar para trabajos desde un cliente local como sigue:</span><span class="sxs-lookup"><span data-stu-id="1371e-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="1371e-192">Cmdlets útiles para el envío de trabajos con integración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1371e-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="1371e-193">Administrar la caché de tokens local Hola</span><span class="sxs-lookup"><span data-stu-id="1371e-193">Manage hello local token cache</span></span>

<span data-ttu-id="1371e-194">HPC Pack 2016 proporciona dos nuevos cmdlets de PowerShell de HPC en caché de tokens local toomanage Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="1371e-195">Estos cmdlets son útiles para enviar trabajos de una manera no interactiva.</span><span class="sxs-lookup"><span data-stu-id="1371e-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="1371e-196">Vea el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="1371e-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="1371e-197">Establecer las credenciales de hello para el envío de trabajos con cuenta de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1371e-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="1371e-198">En ocasiones, puede que desee toorun trabajo de hello en el usuario del clúster HPC de hello (para un clúster HPC Unidos a un dominio, ejecutar como usuario de un dominio; para un clúster HPC no unido a un dominio, ejecutar como un usuario local en el nodo principal de hello).</span><span class="sxs-lookup"><span data-stu-id="1371e-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="1371e-199">Usar hello siguiendo las credenciales de Hola de tooset de comandos:</span><span class="sxs-lookup"><span data-stu-id="1371e-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="1371e-200">A continuación, enviar trabajo hello como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="1371e-200">Then submit hello job as follows.</span></span> <span data-ttu-id="1371e-201">Hola trabajo o tarea se ejecuta en $localUser en nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="1371e-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="1371e-202">Si `–Credential` no se especifica con `Submit-HpcJob`, Hola trabajo o la tarea se ejecuta bajo un usuario local asignado como Hola cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1371e-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="1371e-203">(clúster de HPC de hello crea un usuario local con hello mismo nombre como tarea de Azure AD cuenta toorun hello hello).</span><span class="sxs-lookup"><span data-stu-id="1371e-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="1371e-204">Establecer datos extendidos para hello cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1371e-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="1371e-205">Esto es útil cuando se ejecuta un trabajo de MPI en nodos de Linux con cuenta de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1371e-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="1371e-206">Establecer datos extendidos para hello propia cuenta de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1371e-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="1371e-207">Establezca los datos extendidos y realice la ejecución como usuario del clúster HPC.</span><span class="sxs-lookup"><span data-stu-id="1371e-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

