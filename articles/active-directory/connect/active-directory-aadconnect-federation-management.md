---
title: "aaaActive Directory Federation Services personalización con Azure AD Connect y administración | Documentos de Microsoft"
description: "Administración de AD FS con Azure AD Connect y personalización del inicio de sesión de AD FS del usuario con Azure AD Connect y PowerShell."
keywords: "AD FS, ADFS, administración de AD FS, AAD Connect, Connect, inicio de sesión, personalización de AD FS, reparación de la confianza, Office 365, federación, usuario de confianza"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="380fd-104">Administre y personalice Servicios de federación de Active Directory con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="380fd-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="380fd-105">Este artículo se describe cómo toomanage y personalizar los servicios de federación de Active Directory (AD FS) mediante el uso de Connect de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="380fd-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="380fd-106">También incluye otras tareas habituales de AD FS que puede ser necesario toodo para completar la configuración de una granja de servidores de AD FS.</span><span class="sxs-lookup"><span data-stu-id="380fd-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="380fd-107">Tema.</span><span class="sxs-lookup"><span data-stu-id="380fd-107">Topic</span></span> | <span data-ttu-id="380fd-108">Qué trata</span><span class="sxs-lookup"><span data-stu-id="380fd-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="380fd-109">**Administración de AD FS**</span><span class="sxs-lookup"><span data-stu-id="380fd-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="380fd-110">Confianza de Hola de reparación</span><span class="sxs-lookup"><span data-stu-id="380fd-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="380fd-111">La federación de hello toorepair confiar con Office 365.</span><span class="sxs-lookup"><span data-stu-id="380fd-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="380fd-112">Federación con Azure AD mediante un identificador de inicio de sesión alternativo</span><span class="sxs-lookup"><span data-stu-id="380fd-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="380fd-113">Configuración de la federación con un identificador de inicio de sesión alternativo</span><span class="sxs-lookup"><span data-stu-id="380fd-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="380fd-114">Adición de un servidor de AD FS</span><span class="sxs-lookup"><span data-stu-id="380fd-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="380fd-115">¿Cómo tooexpand AD FS de granja de servidores con un servidor de AD FS adicional.</span><span class="sxs-lookup"><span data-stu-id="380fd-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="380fd-116">Incorporación de un servidor proxy de aplicación web de AD FS</span><span class="sxs-lookup"><span data-stu-id="380fd-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="380fd-117">¿Cómo tooexpand AD FS de granja de servidores con un servidor Proxy de aplicación Web (WAP) adicional.</span><span class="sxs-lookup"><span data-stu-id="380fd-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="380fd-118">Adición de un dominio federado</span><span class="sxs-lookup"><span data-stu-id="380fd-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="380fd-119">¿Cómo tooadd un dominio federado.</span><span class="sxs-lookup"><span data-stu-id="380fd-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="380fd-120">Actualiza el certificado SSL de Hola</span><span class="sxs-lookup"><span data-stu-id="380fd-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="380fd-121">¿Cómo tooupdate Hola SSL de certificados para una granja de servidores de AD FS.</span><span class="sxs-lookup"><span data-stu-id="380fd-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="380fd-122">**Personalización de AD FS**</span><span class="sxs-lookup"><span data-stu-id="380fd-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="380fd-123">Adición de un logotipo de la compañía personalizado o una ilustración</span><span class="sxs-lookup"><span data-stu-id="380fd-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="380fd-124">¿Cómo inicio de sesión toocustomize AD FS en la página con un logotipo de empresa y la ilustración.</span><span class="sxs-lookup"><span data-stu-id="380fd-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="380fd-125">Adición de la descripción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="380fd-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="380fd-126">¿Cómo tooadd un inicio de sesión en la página de descripción.</span><span class="sxs-lookup"><span data-stu-id="380fd-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="380fd-127">Modificación de las reglas de notificaciones de AD FS</span><span class="sxs-lookup"><span data-stu-id="380fd-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="380fd-128">¿Cómo toomodify AD FS notificaciones para los distintos escenarios de federación.</span><span class="sxs-lookup"><span data-stu-id="380fd-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="380fd-129">Administración de AD FS</span><span class="sxs-lookup"><span data-stu-id="380fd-129">Manage AD FS</span></span>
<span data-ttu-id="380fd-130">Puede realizar diversas tareas de AD FS-relacionados en Azure AD Connect con intervención mínima del usuario mediante el Asistente de hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="380fd-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="380fd-131">Cuando haya terminado de instalar Azure AD Connect mediante la ejecución del Asistente para hello, puede ejecutar el Asistente de hello nuevo tooperform las tareas adicionales.</span><span class="sxs-lookup"><span data-stu-id="380fd-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="380fd-132">Confianza de Hola de reparación<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="380fd-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="380fd-133">Puede usar Azure AD Connect toocheck Hola actual estado Hola AD FS y confianza de Azure AD y tomar las medidas oportunas toorepair Hola confianza.</span><span class="sxs-lookup"><span data-stu-id="380fd-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="380fd-134">Siga estos pasos toorepair Azure AD y AD FS de confianza.</span><span class="sxs-lookup"><span data-stu-id="380fd-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="380fd-135">Seleccione **AAD de reparación y confiar en AD FS** de lista de Hola de tareas adicionales.</span><span class="sxs-lookup"><span data-stu-id="380fd-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="380fd-136">![Reparar AAD y confianza de ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="380fd-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="380fd-137">En hello **conectar tooAzure AD** página, proporcione las credenciales de administrador global de Azure AD y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="380fd-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="380fd-138">![Conectar tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="380fd-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="380fd-139">En hello **las credenciales de acceso remoto** página, escriba las credenciales de hello para el Administrador de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![Credenciales de acceso remoto](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="380fd-141">Cuando hace clic en **Siguiente**, Azure AD Connect comprueba el estado del certificado y muestra los problemas que existen.</span><span class="sxs-lookup"><span data-stu-id="380fd-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Estado de los certificados](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="380fd-143">Hola **tooconfigure listo** página muestra hello lista de acciones que realiza la confianza de hello toorepair.</span><span class="sxs-lookup"><span data-stu-id="380fd-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![Tooconfigure listo](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="380fd-145">Haga clic en **instalar** confianza de hello toorepair.</span><span class="sxs-lookup"><span data-stu-id="380fd-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="380fd-146">Azure AD Connect solo puede reparar o actuar en los certificados autofirmados.</span><span class="sxs-lookup"><span data-stu-id="380fd-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="380fd-147">Azure AD Connect no puede reparar certificados de terceros.</span><span class="sxs-lookup"><span data-stu-id="380fd-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="380fd-148">Federación con Azure AD mediante un identificador de inicio de sesión alternativo<a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="380fd-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="380fd-149">Se recomienda que hello Principal de usuario Name(UPN) local y nombre Principal de usuario se mantienen en la nube Hola Hola igual.</span><span class="sxs-lookup"><span data-stu-id="380fd-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="380fd-150">Si Hola UPN local usa un dominio no enrutables (p. ej.</span><span class="sxs-lookup"><span data-stu-id="380fd-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="380fd-151">Contoso.local) o no se puede cambiar debido a las dependencias de aplicación toolocal, se recomienda configurar el Id. de inicio de sesión alternativo.</span><span class="sxs-lookup"><span data-stu-id="380fd-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="380fd-152">Id. de inicio de sesión alternativo permite tooconfigure un inicio de sesión de experimentar donde los usuarios puedan iniciar sesión con un atributo que no sea su UPN, por ejemplo, correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="380fd-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="380fd-153">elección de Hello para el nombre Principal de usuario en el atributo de Azure AD Connect valores predeterminados toohello userPrincipalName en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="380fd-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="380fd-154">Si elige cualquier otro atributo como nombre principal de usuario y está realizando una federación mediante AD FS, Azure AD Connect configurará AD FS para el identificador de inicio de sesión alternativo.</span><span class="sxs-lookup"><span data-stu-id="380fd-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="380fd-155">A continuación, se muestra un ejemplo de elección de un atributo diferente para el nombre principal de usuario:</span><span class="sxs-lookup"><span data-stu-id="380fd-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Selección de atributo de identificador alternativo](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="380fd-157">La configuración del identificador de inicio de sesión alternativo para AD FS consta de dos pasos principales:</span><span class="sxs-lookup"><span data-stu-id="380fd-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="380fd-158">**Configurar el conjunto correcto de Hola de notificaciones de emisión**: reglas de notificación de emisión de Hola de usuario de confianza de hello Azure AD de confianza son atributo UserPrincipalName de toouse modificado Hola seleccionado como Hola Id. alternativo del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="380fd-159">**Habilitar el Id. de inicio de sesión alternativo en la configuración de AD FS Hola**: Hola AD FS configuración se ha actualizado para que AD FS puede buscar usuarios en bosques adecuado hello mediante identificador de hello alternativo.</span><span class="sxs-lookup"><span data-stu-id="380fd-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="380fd-160">Esta configuración se admite en AD FS en Windows Server 2012 R2 (con KB2919355) o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="380fd-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="380fd-161">Si hay servidores de hello AD FS 2012 R2, las comprobaciones de Azure AD Connect presencia de Hola de hello necesarias KB.</span><span class="sxs-lookup"><span data-stu-id="380fd-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="380fd-162">Si hello KB no se detecta, se mostrará una advertencia cuando finalice la configuración, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="380fd-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Advertencia de que falta la KB en 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="380fd-164">toorectify configuración de hello en el caso de KB que faltan, instalar Hola necesario [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) y, a continuación, repare Hola confianza usando [reparar AAD y confianza de AD FS](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="380fd-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="380fd-165">Para obtener más información sobre toomanually alternateID y pasos, configurar, leer [configurar Id. de inicio de sesión alternativo](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="380fd-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="380fd-166">Adición de un servidor de AD FS <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="380fd-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="380fd-167">servidor de tooadd AD FS, Azure AD Connect requiere el certificado PFX Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="380fd-168">Por lo tanto, puede realizar esta operación solo si configuró la granja de servidores de hello AD FS mediante el uso de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="380fd-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="380fd-169">Seleccione **Implementar un servidor de federación adicional** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="380fd-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Servidor de federación adicional](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="380fd-171">En hello **conectar tooAzure AD** página, escriba sus credenciales de administrador global de Azure AD y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="380fd-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Conectar tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="380fd-173">Proporcione las credenciales de administrador de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-173">Provide hello domain administrator credentials.</span></span>

   ![Credenciales del administrador de dominio](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="380fd-175">Azure AD Connect pedirá una contraseña de hello del archivo PFX de Hola que proporcionó al configurar la nueva granja de AD FS con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="380fd-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="380fd-176">Haga clic en **escribir la contraseña** tooprovide contraseña de hello para el archivo PFX de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![Contraseña del certificado](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="380fd-179">En hello **servidores de AD FS** página, escriba el nombre del servidor de Hola o toobe de dirección IP agrega granja de servidores de toohello AD FS.</span><span class="sxs-lookup"><span data-stu-id="380fd-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![Servidores de AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="380fd-181">Haga clic en **siguiente**y pasar por hello final **configurar** página.</span><span class="sxs-lookup"><span data-stu-id="380fd-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="380fd-182">Después de Azure AD Connect ha terminado de agregar el conjunto de servidores de hello servidores toohello AD FS, se le ofrecerá la conectividad de hello opción tooverify Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![Tooconfigure listo](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Instalación completada](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="380fd-185">Incorporación de un servidor de AD FS <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="380fd-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="380fd-186">tooadd un servidor WAP, Azure AD Connect requiere el certificado PFX Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="380fd-187">Por lo tanto, solo puede realizar esta operación si configuró la granja de servidores de hello AD FS mediante el uso de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="380fd-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="380fd-188">Seleccione **implementar Web Application Proxy** desde la lista de Hola de tareas disponibles.</span><span class="sxs-lookup"><span data-stu-id="380fd-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![Implementación de Proxy de aplicación web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="380fd-190">Proporcione las credenciales de administrador global de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-190">Provide hello Azure global administrator credentials.</span></span>

   ![Conectar tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="380fd-192">En hello **certificado SSL especificar** página, proporcione la contraseña de hello para el archivo PFX de Hola que proporcionó cuando configuró la granja de servidores de hello AD FS con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="380fd-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="380fd-193">![Contraseña del certificado](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="380fd-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="380fd-195">Agregar Hola server toobe agregado como un servidor WAP.</span><span class="sxs-lookup"><span data-stu-id="380fd-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="380fd-196">Como servidor WAP de hello no puede ser toohello Unidos a un dominio, Hola asistente pregunta server toohello de credenciales administrativas que se va a agregar.</span><span class="sxs-lookup"><span data-stu-id="380fd-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![Credenciales administrativas del servidor](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="380fd-198">En hello **las credenciales de confianza de Proxy** , proporcione el proxy de credenciales administrativas tooconfigure Hola confianza y el acceso de servidor principal hello en la granja de servidores de AD FS Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![Credenciales de confianza del proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="380fd-200">En hello **tooconfigure listo** página, el Asistente de hello muestra lista Hola de acciones que se llevará a cabo.</span><span class="sxs-lookup"><span data-stu-id="380fd-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![Tooconfigure listo](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="380fd-202">Haga clic en **instalar** configuración de toofinish Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="380fd-203">Una vez completada la configuración de hello, Hola asistente le proporciona Hola tooverify opción Hola servidores toohello de conectividad.</span><span class="sxs-lookup"><span data-stu-id="380fd-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="380fd-204">Haga clic en **compruebe** toocheck conectividad.</span><span class="sxs-lookup"><span data-stu-id="380fd-204">Click **Verify** toocheck connectivity.</span></span>

   ![Instalación completada](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="380fd-206">Adición de un dominio federado <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="380fd-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="380fd-207">Es fácil tooadd toobe de un dominio federado con Azure AD mediante el uso de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="380fd-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="380fd-208">Azure AD Connect agrega el dominio de hello para la federación y modifica la notificación de hello toocorrectly reglas reflejar a emisor hello cuando tiene varios dominios federados con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="380fd-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="380fd-209">tooadd un dominio federado, tarea hello seleccione **agregar otro dominio de Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="380fd-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![Dominio de Azure AD adicional](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="380fd-211">En hello siguiente página del Asistente de hello, proporcione las credenciales de administrador global de Hola para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="380fd-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![Conectar tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="380fd-213">En hello **las credenciales de acceso remoto** , proporcione credenciales de administrador de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![Credenciales de acceso remoto](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="380fd-215">En la página siguiente de hello, Asistente Hola proporciona una lista de dominios de Azure AD que se pueden federar su directorio local con.</span><span class="sxs-lookup"><span data-stu-id="380fd-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="380fd-216">Elija el dominio de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-216">Choose hello domain from hello list.</span></span>

   ![Dominio de Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="380fd-218">Después de elegir el dominio de hello, Asistente Hola proporciona información adecuada sobre otras acciones que Hola asistente tomará y Hola impacto de la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="380fd-219">En algunos casos, si selecciona un dominio que aún no está comprobado en Azure AD, Hola le proporciona información toohelp comprobar dominio Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="380fd-220">Vea [agregar su tooAzure de nombre de dominio personalizado Active Directory](../active-directory-add-domain.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="380fd-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="380fd-221">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="380fd-221">Click **Next**.</span></span> <span data-ttu-id="380fd-222">Hola **tooconfigure listo** página muestra la lista de Hola de acciones que llevará a cabo Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="380fd-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="380fd-223">Haga clic en **instalar** configuración de toofinish Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-223">Click **Install** toofinish hello configuration.</span></span>

   ![Tooconfigure listo](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="380fd-225">Agregar usuarios de hello debe estar sincronizada dominio federado para que puedan estar tooAzure toologin capaz de AD.</span><span class="sxs-lookup"><span data-stu-id="380fd-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="380fd-226">Personalización de AD FS</span><span class="sxs-lookup"><span data-stu-id="380fd-226">AD FS customization</span></span>
<span data-ttu-id="380fd-227">Hello las secciones siguientes se proporcionan detalles sobre algunas de las tareas comunes de Hola que es posible que tenga tooperform si desea personalizar la página de inicio de sesión de AD FS.</span><span class="sxs-lookup"><span data-stu-id="380fd-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="380fd-228">Adición de un logotipo de la compañía personalizado o una ilustración <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="380fd-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="380fd-229">logotipo de hello toochange de empresa de Hola que se muestra en hello **inicio de sesión** , utilice el siguiente cmdlet de Windows PowerShell y la sintaxis de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="380fd-230">Hola recomendada dimensiones para el logotipo de hello son 260 × 35 a 96 PPP con un tamaño de archivo no superior a 10 KB.</span><span class="sxs-lookup"><span data-stu-id="380fd-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="380fd-231">Hola *TargetName* parámetro es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="380fd-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="380fd-232">tema predeterminado de Hola que se lanzó con AD FS se denomina de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="380fd-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="380fd-233">Adición de la descripción de inicio de sesión <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="380fd-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="380fd-234">tooadd un toohello de descripción de la página de inicio de sesión **página de inicio de sesión**, usar hello siguiente cmdlet de Windows PowerShell y la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="380fd-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="380fd-235">Modificación de las reglas de notificaciones de AD FS <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="380fd-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="380fd-236">AD FS es compatible con un lenguaje de notificación enriquecida que puede usar las reglas de notificación toocreate personalizado.</span><span class="sxs-lookup"><span data-stu-id="380fd-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="380fd-237">Para obtener más información, consulte [Hola rol de lenguaje de reglas de notificación de hello](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="380fd-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="380fd-238">Hello secciones siguientes describen cómo se pueden escribir reglas personalizadas para algunos escenarios que relacionan tooAzure AD y federación de AD FS.</span><span class="sxs-lookup"><span data-stu-id="380fd-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="380fd-239">Id. inmutable condicional en un valor que esté presente en el atributo de Hola</span><span class="sxs-lookup"><span data-stu-id="380fd-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="380fd-240">Azure AD Connect le permite especificar un toobe de atributo que se utiliza como un delimitador de origen cuando los objetos están sincronizados tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="380fd-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="380fd-241">Si el valor de hello en el atributo personalizado de hello no está vacío, conviene tooissue una notificación de identificador inmutable.</span><span class="sxs-lookup"><span data-stu-id="380fd-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="380fd-242">Por ejemplo, puede seleccionar **ms-ds-consistencyguid** como atributo de hello para el delimitador de origen de Hola y emitir **ImmutableID** como **ms-ds-consistencyguid** en mayúscula Hola el atributo tiene un valor en él.</span><span class="sxs-lookup"><span data-stu-id="380fd-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="380fd-243">Si no hay ningún valor en el atributo de hello, emitir **objectGuid** como Hola inmutable identificador.</span><span class="sxs-lookup"><span data-stu-id="380fd-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="380fd-244">Puede crear conjunto de Hola de reglas de notificación personalizada tal y como se describe en los pasos de la sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="380fd-245">**Regla 1: Consultar atributos**</span><span class="sxs-lookup"><span data-stu-id="380fd-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="380fd-246">En esta regla, que está consultando los valores de hello de **ms-ds-consistencyguid** y **objectGuid** para el usuario de Hola desde Active Directory.</span><span class="sxs-lookup"><span data-stu-id="380fd-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="380fd-247">Cambiar nombre hello almacén nombre tooan almacén adecuado en la implementación de AD FS.</span><span class="sxs-lookup"><span data-stu-id="380fd-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="380fd-248">Cambiar tipo hello notificaciones tipo tooa notificaciones adecuadas para la federación, tal como se define para **objectGuid** y **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="380fd-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="380fd-249">Además, mediante el uso de **agregar** y no **problema**, evitar la adición de un problema saliente para la entidad de Hola y pueden usar valores de hello como valores intermedios.</span><span class="sxs-lookup"><span data-stu-id="380fd-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="380fd-250">Se van a emitir notificaciones de hello en una regla más adelante después de establecer qué toouse valor como identificador inmutable de Hola</span><span class="sxs-lookup"><span data-stu-id="380fd-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="380fd-251">**Regla 2: Comprobar si ms-ds-consistencyguid existe para el usuario de Hola**</span><span class="sxs-lookup"><span data-stu-id="380fd-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="380fd-252">Esta regla define una marca temporal denominada **idflag** que se establece demasiado**useguid** si no hay ningún **ms-ds-consistencyguid** rellena para usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="380fd-253">lógica de Hello detrás de esto es hechos Hola que AD FS no permitir notificaciones vacías.</span><span class="sxs-lookup"><span data-stu-id="380fd-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="380fd-254">Por lo que al agregar notificaciones http://contoso.com/ws/2016/02/identity/claims/objectguid y http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid en la regla 1, terminará con un **msdsconsistencyguid** notificación solo si valor de Hola se rellena para usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="380fd-255">Si no se rellena, AD FS ve que tiene un valor vacío y lo coloca inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="380fd-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="380fd-256">Todos los objetos tendrán el atributo **objectGuid**, así que esa notificación seguirá estando después de que se ejecute la regla 1.</span><span class="sxs-lookup"><span data-stu-id="380fd-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="380fd-257">**Regla 3: Emitir el atributo ms-ds-consistencyguid como identificador inmutable si está presente**</span><span class="sxs-lookup"><span data-stu-id="380fd-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="380fd-258">Se trata de una comprobación **Exist** implícita.</span><span class="sxs-lookup"><span data-stu-id="380fd-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="380fd-259">Si existe el valor de Hola de notificación de Hola, a continuación, emita que como Hola inmutable identificador.</span><span class="sxs-lookup"><span data-stu-id="380fd-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="380fd-260">Hola anterior en el ejemplo se usa hello **nameidentifier** de notificación.</span><span class="sxs-lookup"><span data-stu-id="380fd-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="380fd-261">Tendrá toochange este tipo de notificación adecuadas toohello de identificador inmutable de hello en su entorno.</span><span class="sxs-lookup"><span data-stu-id="380fd-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="380fd-262">**Regla 4: Emitir el atributo objectGUID como identificador inmutable si ms-ds-consistencyguid no está presente**</span><span class="sxs-lookup"><span data-stu-id="380fd-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="380fd-263">En esta regla, simplemente está comprobando marca temporal hello **idflag**.</span><span class="sxs-lookup"><span data-stu-id="380fd-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="380fd-264">Decide si tooissue Hola notificación basada en su valor.</span><span class="sxs-lookup"><span data-stu-id="380fd-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="380fd-265">secuencia de Hola de estas reglas es importante.</span><span class="sxs-lookup"><span data-stu-id="380fd-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="380fd-266">SSO con un UPN de subdominio</span><span class="sxs-lookup"><span data-stu-id="380fd-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="380fd-267">Puede agregar más de un toobe de dominio federado mediante el uso de Azure AD Connect, tal y como se describe en [agregar un nuevo dominio federado](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="380fd-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="380fd-268">Deberá modificar notificación de nombre principal (UPN) del usuario de Hola para que hello Id. del emisor corresponde toohello dominio de raíz y no el subdominio de hello, porque dominio federado raíz de hello también cubre a secundarios Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="380fd-269">De forma predeterminada, Hola de reglas de notificaciones para emisor Id. se establece como:</span><span class="sxs-lookup"><span data-stu-id="380fd-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Notificación del identificador de emisor predeterminado](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="380fd-271">regla predeterminada de Hello simplemente toma el sufijo UPN de Hola y utiliza en la notificación de Id. de emisor de Hola.</span><span class="sxs-lookup"><span data-stu-id="380fd-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="380fd-272">Por ejemplo, John es un usuario de sub.contoso.com y contoso.com está federado con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="380fd-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="380fd-273">Entra en John john@sub.contoso.com como Hola nombre de usuario al iniciar sesión en tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="380fd-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="380fd-274">regla de notificación de Id. de emisor de Hola de forma predeterminada en AD FS lo tratará de hello siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="380fd-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="380fd-275">**Valor de notificación:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="380fd-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="380fd-276">toohave solo dominio de raíz de hello en emisor Hola valor de notificación, cambiar Hola notificación regla toomatch Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="380fd-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="380fd-277">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="380fd-277">Next steps</span></span>
<span data-ttu-id="380fd-278">Obtenga más información sobre las [opciones de inicio de sesión del usuario](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="380fd-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
