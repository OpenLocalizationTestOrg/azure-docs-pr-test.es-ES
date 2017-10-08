---
title: aaaCreate una entidad de servicio para la pila de Azure | Documentos de Microsoft
description: "Describe cómo toocreate una nueva entidad de servicio que puede usarse con control de acceso basado en roles de hello en Azure Resource Manager toomanage acceso tooresources."
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: f090ceed941abe9255bc35ec966bc43df3bb2955
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provide-applications-access-tooazure-stack"></a><span data-ttu-id="ff238-103">Proporcionar acceso de las aplicaciones tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="ff238-103">Provide applications access tooAzure Stack</span></span>
<span data-ttu-id="ff238-104">Cuando una aplicación necesita acceso toodeploy o configurar los recursos a través del Administrador de recursos de Azure en la pila de Azure, se crea un servicio principal, que es una credencial para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff238-104">When an application needs access toodeploy or configure resources through Azure Resource Manager in Azure Stack, you create a service principal, which is a credential for your application.</span></span>  <span data-ttu-id="ff238-105">A continuación, puede delegar la entidad de servicio Hola permisos necesarios toothat solo.</span><span class="sxs-lookup"><span data-stu-id="ff238-105">You can then delegate only hello necessary permissions toothat service principal.</span></span>  

<span data-ttu-id="ff238-106">Por ejemplo, puede tener una herramienta de administración de configuración que utiliza Azure tooinventory de administrador de recursos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff238-106">As an example, you may have a configuration management tool that uses Azure Resource Manager tooinventory Azure resources.</span></span>  <span data-ttu-id="ff238-107">En este escenario, puede crear a una entidad de servicio, conceder a lector Hola entidad de servicio de rol toothat y limitar Hola configuración herramienta solo tooread acceso a la administración.</span><span class="sxs-lookup"><span data-stu-id="ff238-107">In this scenario, you can create a service principal, grant hello reader role toothat service principal, and limit hello configuration management tool tooread-only access.</span></span> 

<span data-ttu-id="ff238-108">Entidades de servicio son preferibles toorunning Hola aplicación bajo sus propias credenciales porque:</span><span class="sxs-lookup"><span data-stu-id="ff238-108">Service principals are preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="ff238-109">Puede asignar la entidad de servicio de toohello de permisos que son diferentes de sus propios permisos de cuenta.</span><span class="sxs-lookup"><span data-stu-id="ff238-109">You can assign permissions toohello service principal that are different than your own account permissions.</span></span> <span data-ttu-id="ff238-110">Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo.</span><span class="sxs-lookup"><span data-stu-id="ff238-110">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="ff238-111">No tiene credenciales de la aplicación de toochange Hola si cambian sus responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="ff238-111">You do not have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="ff238-112">Puede usar una autenticación de certificado tooautomate al ejecutar un script de instalación desatendida.</span><span class="sxs-lookup"><span data-stu-id="ff238-112">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="ff238-113">Introducción</span><span class="sxs-lookup"><span data-stu-id="ff238-113">Getting started</span></span>

<span data-ttu-id="ff238-114">Dependiendo de cómo ha implementado Azure Stack, primero debe crear una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="ff238-114">Depending on how you have deployed Azure Stack, you start by creating a service principal.</span></span>  <span data-ttu-id="ff238-115">Este documento le guía a través del proceso de creación de una entidad de servicio para [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) y [Servicios de federación de Active Directory (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="ff238-115">This document guides you through creating a service principal for both [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) and [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>  <span data-ttu-id="ff238-116">Una vez que haya creado Hola entidad de servicio, un conjunto de pasos comunes tooboth AD FS y Azure Active Directory se usan demasiado[delegar permisos](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello rol.</span><span class="sxs-lookup"><span data-stu-id="ff238-116">Once you've created hello service principal, a set of steps common tooboth AD FS and Azure Active Directory are used too[delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello role.</span></span>     

## <a name="create-service-principal-for-azure-ad"></a><span data-ttu-id="ff238-117">Crear una entidad de servicio para Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff238-117">Create service principal for Azure AD</span></span>

<span data-ttu-id="ff238-118">Si ha implementado la pila de Azure con Azure AD como almacén de identidades de hello, puede crear a entidades de servicio igual que hacen de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff238-118">If you've deployed Azure Stack using Azure AD as hello identity store, you can create service principals just like you do for Azure.</span></span>  <span data-ttu-id="ff238-119">Esta sección muestra cómo los pasos a través del portal de hello tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="ff238-119">This section shows you how tooperform hello steps through hello portal.</span></span>  <span data-ttu-id="ff238-120">Compruebe que dispone de hello [requiere permisos de Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) antes de comenzar.</span><span class="sxs-lookup"><span data-stu-id="ff238-120">Check that you have hello [required Azure AD permissions](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before beginning.</span></span>

### <a name="create-service-principal"></a><span data-ttu-id="ff238-121">Creación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="ff238-121">Create service principal</span></span>
<span data-ttu-id="ff238-122">En esta sección, creará una aplicación (entidad de servicio) en Azure AD que representará su aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff238-122">In this section, you create an application (service principal) in Azure AD that will represent your application.</span></span>

1. <span data-ttu-id="ff238-123">Inicie sesión en tooyour cuenta de Azure a través de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff238-123">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ff238-124">Seleccione **Azure Active Directory** > **Registros de aplicaciones** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ff238-124">Select **Azure Active Directory** > **App registrations** > **Add**</span></span>   
3. <span data-ttu-id="ff238-125">Proporcione un nombre y la dirección URL para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ff238-125">Provide a name and URL for hello application.</span></span> <span data-ttu-id="ff238-126">Seleccione **aplicación Web / API** o **nativo** para el tipo de saludo de aplicación desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="ff238-126">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="ff238-127">Después de establecer valores de hello, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="ff238-127">After setting hello values, select **Create**.</span></span>

<span data-ttu-id="ff238-128">Creó una entidad de servicio para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff238-128">You have created a service principal for your application.</span></span>

### <a name="get-credentials"></a><span data-ttu-id="ff238-129">Obtener credenciales</span><span class="sxs-lookup"><span data-stu-id="ff238-129">Get credentials</span></span>
<span data-ttu-id="ff238-130">Al iniciar sesión mediante programación, use el identificador de hello para la aplicación y una clave de autenticación.</span><span class="sxs-lookup"><span data-stu-id="ff238-130">When programmatically logging in, you use hello ID for your application and an authentication key.</span></span> <span data-ttu-id="ff238-131">tooget los valores, Hola uso pasos:</span><span class="sxs-lookup"><span data-stu-id="ff238-131">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="ff238-132">En **App registrations** (Registros de aplicaciones), en Active Directory, seleccione su aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff238-132">From **App registrations** in Active Directory, select your application.</span></span>

2. <span data-ttu-id="ff238-133">Hola copia **Id. de aplicación** y almacenarlo en el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff238-133">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="ff238-134">Hola aplicaciones Hola [aplicaciones de ejemplo](#sample-applications) sección hacen referencia a valor toothis como identificador de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff238-134">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![ID. DE CLIENTE](./media/azure-stack-create-service-principal/image12.png)
3. <span data-ttu-id="ff238-136">toogenerate una clave de autenticación, seleccione **claves**.</span><span class="sxs-lookup"><span data-stu-id="ff238-136">toogenerate an authentication key, select **Keys**.</span></span>

4. <span data-ttu-id="ff238-137">Proporcione una descripción de clave de hello y una duración para la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff238-137">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="ff238-138">Cuando haya terminado, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ff238-138">When done, select **Save**.</span></span>

<span data-ttu-id="ff238-139">Después de guardar la clave de hello, se muestra el valor de Hola de clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff238-139">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="ff238-140">Copie este valor porque no es capaz de tooretrieve clave de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="ff238-140">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="ff238-141">Proporcionar valor de clave de hello con toosign de Id. de aplicación Hola como aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ff238-141">You provide hello key value with hello application ID toosign as hello application.</span></span> <span data-ttu-id="ff238-142">Almacene el valor de clave de Hola donde la aplicación pueda recuperarlos.</span><span class="sxs-lookup"><span data-stu-id="ff238-142">Store hello key value where your application can retrieve it.</span></span>

![clave guardada](./media/azure-stack-create-service-principal/image15.png)


<span data-ttu-id="ff238-144">Una vez completado, continuar demasiado[asignar un rol de la aplicación](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span><span class="sxs-lookup"><span data-stu-id="ff238-144">Once complete, proceed too[assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span></span>

## <a name="create-service-principal-for-ad-fs"></a><span data-ttu-id="ff238-145">Crear una entidad de servicio para AD FS</span><span class="sxs-lookup"><span data-stu-id="ff238-145">Create service principal for AD FS</span></span>
<span data-ttu-id="ff238-146">Si ha implementado la pila de Azure con AD FS, puede usar PowerShell toocreate una entidad de servicio, asignar un rol para el acceso e inicio de sesión desde PowerShell utilizando dicha identidad.</span><span class="sxs-lookup"><span data-stu-id="ff238-146">If you have deployed Azure Stack with AD FS, you can use PowerShell toocreate a service principal, assign a role for access, and sign in from PowerShell using that identity.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="ff238-147">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ff238-147">Before you begin</span></span>

[<span data-ttu-id="ff238-148">Descargar Hola herramientas requiere toowork con el equipo local tooyour de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff238-148">Download hello tools required toowork with Azure Stack tooyour local computer.</span></span>](azure-stack-powershell-download.md)

### <a name="import-hello-identity-powershell-module"></a><span data-ttu-id="ff238-149">Módulo de PowerShell de identidad de Hola de importación</span><span class="sxs-lookup"><span data-stu-id="ff238-149">Import hello Identity PowerShell module</span></span>
<span data-ttu-id="ff238-150">Después de descargar herramientas de hello, desplazarse por las carpetas de toohello descargado e importe el módulo de PowerShell de identidad de hello utilizando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ff238-150">After you download hello tools, navigate toohello downloaded folder and import hello Identity PowerShell module by using hello following command:</span></span>

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

<span data-ttu-id="ff238-151">Al importar el módulo de hello, recibirá un error que dice "AzureStack.Connect.psm1 no está firmado digitalmente.</span><span class="sxs-lookup"><span data-stu-id="ff238-151">When you import hello module, you may receive an error that says “AzureStack.Connect.psm1 is not digitally signed.</span></span> <span data-ttu-id="ff238-152">script de Hola no se ejecutará en el sistema de Hola".</span><span class="sxs-lookup"><span data-stu-id="ff238-152">hello script will not execute on hello system”.</span></span> <span data-ttu-id="ff238-153">tooresolve este problema, puede establecer tooallow de directiva de ejecución ejecutar script de Hola con hello siguiente comando en una sesión de PowerShell con privilegios elevados:</span><span class="sxs-lookup"><span data-stu-id="ff238-153">tooresolve this issue, you can set execution policy tooallow running hello script with hello following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-hello-service-principal"></a><span data-ttu-id="ff238-154">Crear Hola entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="ff238-154">Create hello service principal</span></span>
<span data-ttu-id="ff238-155">Puede crear una entidad de servicio mediante la ejecución Hola siguiente comando, que realiza seguro hello tooupdate *DisplayName* parámetro:</span><span class="sxs-lookup"><span data-stu-id="ff238-155">You can create a Service Principal by executing hello following command, making sure tooupdate hello *DisplayName* parameter:</span></span>
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a><span data-ttu-id="ff238-156">Asignar un rol</span><span class="sxs-lookup"><span data-stu-id="ff238-156">Assign a role</span></span>
<span data-ttu-id="ff238-157">Una vez Hola se crea la entidad de servicio, debe [asignar rol tooa](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span><span class="sxs-lookup"><span data-stu-id="ff238-157">Once hello Service Principal is created, you must [assign it tooa role](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span></span>

### <a name="sign-in-through-powershell"></a><span data-ttu-id="ff238-158">Iniciar sesión a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff238-158">Sign in through PowerShell</span></span>
<span data-ttu-id="ff238-159">Una vez que haya asignado un rol, puede iniciar sesión en tooAzure pila con entidad de servicio de Hola Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ff238-159">Once you've assigned a role, you can sign in tooAzure Stack using hello service principal with hello following command:</span></span>

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-tooservice-principal"></a><span data-ttu-id="ff238-160">Asignar la entidad de seguridad de rol tooservice</span><span class="sxs-lookup"><span data-stu-id="ff238-160">Assign role tooservice principal</span></span>
<span data-ttu-id="ff238-161">tooaccess recursos de la suscripción, debe asignar el rol de tooa de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="ff238-161">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="ff238-162">Decidir qué rol representa permisos adecuados de hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ff238-162">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="ff238-163">toolearn sobre los roles disponibles de hello, consulte [RBAC: integrada en Roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="ff238-163">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="ff238-164">Puede establecer el ámbito de hello en nivel de Hola de suscripción de hello, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="ff238-164">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="ff238-165">Los permisos son heredados toolower niveles de ámbito.</span><span class="sxs-lookup"><span data-stu-id="ff238-165">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="ff238-166">Por ejemplo, agregar que un rol de lector de toohello de aplicación para un grupo de recursos indica que puede leer el grupo de recursos de Hola y los recursos que contenga.</span><span class="sxs-lookup"><span data-stu-id="ff238-166">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="ff238-167">En el portal de Azure pila hello, navegue toohello nivel de ámbito que se va tooassign aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="ff238-167">In hello Azure Stack portal, navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="ff238-168">Por ejemplo, tooassign un rol en el ámbito de la suscripción de hello, seleccione **suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="ff238-168">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="ff238-169">También puede seleccionar un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="ff238-169">You could instead select a resource group or resource.</span></span>

2. <span data-ttu-id="ff238-170">Seleccionar Hola suscripción en particular (grupo de recursos o recursos) tooassign Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff238-170">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![seleccionar suscripción para la asignación](./media/azure-stack-create-service-principal/image16.png)

3. <span data-ttu-id="ff238-172">Seleccione **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="ff238-172">Select **Access Control (IAM)**.</span></span>

     ![seleccionar acceso](./media/azure-stack-create-service-principal/image17.png)

4. <span data-ttu-id="ff238-174">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ff238-174">Select **Add**.</span></span>

5. <span data-ttu-id="ff238-175">Seleccione rol Hola desea tooassign toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff238-175">Select hello role you wish tooassign toohello application.</span></span>

6. <span data-ttu-id="ff238-176">Busque la aplicación y selecciónela.</span><span class="sxs-lookup"><span data-stu-id="ff238-176">Search for your application, and select it.</span></span>

7. <span data-ttu-id="ff238-177">Seleccione **Aceptar** toofinish asignación de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff238-177">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="ff238-178">Verá que su aplicación en la lista de Hola de los usuarios asignados a roles tooa para ese ámbito.</span><span class="sxs-lookup"><span data-stu-id="ff238-178">You see your application in hello list of users assigned tooa role for that scope.</span></span>

<span data-ttu-id="ff238-179">Ahora que ha creado a una entidad de servicio y le asigna un rol, puede empezar a usar esto en los recursos de Azure pila tooaccess de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff238-179">Now that you've created a service principal and assigned a role, you can begin using this within your application tooaccess Azure Stack resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="ff238-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff238-180">Next steps</span></span>

<span data-ttu-id="ff238-181">[Add users for ADFS](azure-stack-add-users-adfs.md) (Agregar usuarios para ADFS)
[Manage user permissions](azure-stack-manage-permissions.md) (Administrar permisos de usuario)</span><span class="sxs-lookup"><span data-stu-id="ff238-181">[Add users for ADFS](azure-stack-add-users-adfs.md)
[Manage user permissions](azure-stack-manage-permissions.md)</span></span>