---
title: "Administración y personalización de Servicios de federación de Active Directory con Azure AD Connect | Microsoft Docs"
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
ms.openlocfilehash: 14f03542a6553c5bb697192828368ffe6b96441c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="2f9f5-104">Administre y personalice Servicios de federación de Active Directory con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2f9f5-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="2f9f5-105">En este artículo se describe cómo administrar y personalizar Servicios de federación de Active Directory (AD FS) con Azure Active Directory (Azure AD) Connect.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="2f9f5-106">También se incluyen otras tareas comunes de AD FS que podría tener que hacer para configurar completamente una granja de servidores de AD FS.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="2f9f5-107">Tema.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-107">Topic</span></span> | <span data-ttu-id="2f9f5-108">Qué trata</span><span class="sxs-lookup"><span data-stu-id="2f9f5-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="2f9f5-109">**Administración de AD FS**</span><span class="sxs-lookup"><span data-stu-id="2f9f5-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="2f9f5-110">Reparación de la confianza</span><span class="sxs-lookup"><span data-stu-id="2f9f5-110">Repair the trust</span></span>](#repairthetrust) |<span data-ttu-id="2f9f5-111">Cómo reparar la confianza de federación con Office 365.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-111">How to repair the federation trust with Office 365.</span></span> |
| [<span data-ttu-id="2f9f5-112">Federación con Azure AD mediante un identificador de inicio de sesión alternativo</span><span class="sxs-lookup"><span data-stu-id="2f9f5-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="2f9f5-113">Configuración de la federación con un identificador de inicio de sesión alternativo</span><span class="sxs-lookup"><span data-stu-id="2f9f5-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="2f9f5-114">Adición de un servidor de AD FS</span><span class="sxs-lookup"><span data-stu-id="2f9f5-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="2f9f5-115">Cómo expandir una granja de servidores de AD FS con un servidor de AD FS adicional.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-115">How to expand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="2f9f5-116">Incorporación de un servidor proxy de aplicación web de AD FS</span><span class="sxs-lookup"><span data-stu-id="2f9f5-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="2f9f5-117">Cómo expandir una granja de servidores de AD FS con un servidor proxy de aplicación web (WAP) adicional.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="2f9f5-118">Adición de un dominio federado</span><span class="sxs-lookup"><span data-stu-id="2f9f5-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="2f9f5-119">Cómo agregar un dominio federado.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-119">How to add a federated domain.</span></span> |
| [<span data-ttu-id="2f9f5-120">Actualizar el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="2f9f5-120">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="2f9f5-121">Cómo actualizar el certificado SSL para una granja de servidores de AD FS.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-121">How to update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="2f9f5-122">**Personalización de AD FS**</span><span class="sxs-lookup"><span data-stu-id="2f9f5-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="2f9f5-123">Adición de un logotipo de la compañía personalizado o una ilustración</span><span class="sxs-lookup"><span data-stu-id="2f9f5-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="2f9f5-124">Cómo personalizar una página de inicio de sesión de AD FS con una ilustración y un logotipo de la empresa.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-124">How to customize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="2f9f5-125">Adición de la descripción de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="2f9f5-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="2f9f5-126">Cómo agregar una descripción a la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-126">How to add a sign-in page description.</span></span> |
| [<span data-ttu-id="2f9f5-127">Modificación de las reglas de notificaciones de AD FS</span><span class="sxs-lookup"><span data-stu-id="2f9f5-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="2f9f5-128">Cómo modificar las notificaciones de AD FS en diversos escenarios de federación.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-128">How to modify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="2f9f5-129">Administración de AD FS</span><span class="sxs-lookup"><span data-stu-id="2f9f5-129">Manage AD FS</span></span>
<span data-ttu-id="2f9f5-130">Puede realizar diversas tareas relacionadas con AD FS en Azure AD Connect con mínima intervención por parte del usuario mediante el Asistente para Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span></span> <span data-ttu-id="2f9f5-131">Una vez finalizada la instalación de Azure AD Connect con el asistente, puede ejecutarlo de nuevo para realizar tareas adicionales.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span></span>

## <span data-ttu-id="2f9f5-132">Reparación de la confianza <a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="2f9f5-132">Repair the trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="2f9f5-133">Puede usar Azure AD Connect para comprobar el estado actual de la confianza de AD FS y Azure AD, y tomar las medidas adecuadas para repararla.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span></span> <span data-ttu-id="2f9f5-134">Siga estos pasos para reparar la confianza de Azure AD y AD FS.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-134">Follow these steps to repair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="2f9f5-135">Seleccione **Reparar AAD y confianza de ADFS** en la lista de tareas disponibles.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span></span>
   <span data-ttu-id="2f9f5-136">![Reparar AAD y confianza de ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="2f9f5-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="2f9f5-137">En la página **Conectar con Azure AD**, proporcione las credenciales de administrador global de Azure AD y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="2f9f5-138">![Conectarse a Azure](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="2f9f5-138">![Connect to Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="2f9f5-139">En la página **Credenciales de acceso remoto** , proporcione las credenciales del administrador de dominio.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span></span>

   ![Credenciales de acceso remoto](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="2f9f5-141">Cuando hace clic en **Siguiente**, Azure AD Connect comprueba el estado del certificado y muestra los problemas que existen.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Estado de los certificados](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="2f9f5-143">La página **Listo para configurar** muestra la lista de acciones que se llevarán a cabo para reparar la confianza.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span></span>

    ![Listo para configurar](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="2f9f5-145">Haga clic en **Instalar** para reparar la confianza.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-145">Click **Install** to repair the trust.</span></span>

> [!NOTE]
> <span data-ttu-id="2f9f5-146">Azure AD Connect solo puede reparar o actuar en los certificados autofirmados.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="2f9f5-147">Azure AD Connect no puede reparar certificados de terceros.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="2f9f5-148">Federación con Azure AD mediante un identificador de inicio de sesión alternativo<a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="2f9f5-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="2f9f5-149">Se recomienda que el nombre principal de usuario (UPN) local y el nombre principal de usuario en la nube sean el mismo.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span></span> <span data-ttu-id="2f9f5-150">Si el UPN local usa un dominio no enrutable (p. ej.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-150">If the on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="2f9f5-151">Contoso.local) o no se puede cambiar debido a dependencias de aplicación locales, se recomienda configurar el identificador de inicio de sesión alternativo.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="2f9f5-152">El identificador de inicio de sesión alternativo le permite configurar una experiencia de inicio de sesión donde los usuarios puedan iniciar sesión con un atributo que no sea su UPN, por ejemplo, el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="2f9f5-153">La opción predeterminada de nombre principal de usuario en Azure AD Connect es el atributo userPrincipalName en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="2f9f5-154">Si elige cualquier otro atributo como nombre principal de usuario y está realizando una federación mediante AD FS, Azure AD Connect configurará AD FS para el identificador de inicio de sesión alternativo.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="2f9f5-155">A continuación, se muestra un ejemplo de elección de un atributo diferente para el nombre principal de usuario:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Selección de atributo de identificador alternativo](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="2f9f5-157">La configuración del identificador de inicio de sesión alternativo para AD FS consta de dos pasos principales:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="2f9f5-158">**Configurar el conjunto de notificaciones de emisión correcto**: las reglas de notificación del usuario de confianza de Azure AD se modifican para utilizar el atributo UserPrincipalName seleccionado como identificador alternativo del usuario de confianza.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span></span>
2. <span data-ttu-id="2f9f5-159">**Habilitar el identificador de inicio de sesión alternativo en la configuración de AD FS**: se actualiza la configuración de AD FS para que AD FS pueda buscar usuarios en los bosques correspondientes con el identificador alternativo.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span></span> <span data-ttu-id="2f9f5-160">Esta configuración se admite en AD FS en Windows Server 2012 R2 (con KB2919355) o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="2f9f5-161">Si los servidores de AD FS son 2012 R2, Azure AD Connect comprueba si está presente la KB necesaria.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span></span> <span data-ttu-id="2f9f5-162">Si no se detecta la KB, se mostrará una advertencia cuando finalice la configuración, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Advertencia de que falta la KB en 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="2f9f5-164">Para corregir la configuración en caso de que falte la KB, instale [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) y, a continuación, repare la confianza utilizando [Reparar AAD y confianza de ADFS ](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="2f9f5-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="2f9f5-165">Para más información sobre alternateID y los pasos para configurarlo manualmente, consulte [Configuración del identificador de inicio de sesión alternativo](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="2f9f5-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="2f9f5-166">Adición de un servidor de AD FS <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="2f9f5-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="2f9f5-167">Para agregar un servidor de AD FS, Azure AD Connect necesita el certificado PFX.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="2f9f5-168">Por lo tanto, puede realizar esta operación solamente si ha configurado la granja de servidores de AD FS con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="2f9f5-169">Seleccione **Implementar un servidor de federación adicional** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Servidor de federación adicional](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="2f9f5-171">En la página **Conectar con Azure AD**, proporcione las credenciales de administrador global de Azure AD y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Conectarse a Azure](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="2f9f5-173">Proporcione las credenciales del administrador de dominio.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-173">Provide the domain administrator credentials.</span></span>

   ![Credenciales del administrador de dominio](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="2f9f5-175">Azure AD Connect le pide la contraseña del archivo PFX que proporcionó al configurar la nueva granja de servidores de AD FS con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="2f9f5-176">Haga clic en **Escribir contraseña** para proporcionar la contraseña del archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-176">Click **Enter Password** to provide the password for the PFX file.</span></span>

   ![Contraseña del certificado](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="2f9f5-179">En la página **Servidores de AD FS** , escriba el nombre del servidor o la dirección IP que se agregarán a la granja de servidores de AD FS.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span></span>

   ![Servidores de AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="2f9f5-181">Haga clic en **Siguiente** y recorra la página **Configurar** final.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-181">Click **Next**, and go through the final **Configure** page.</span></span> <span data-ttu-id="2f9f5-182">Una vez que Azure AD Connect haya terminado de agregar los servidores a la granja de servidores de AD FS, se le ofrecerá la opción de comprobar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span></span>

   ![Listo para configurar](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Instalación completada](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="2f9f5-185">Incorporación de un servidor de AD FS <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="2f9f5-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="2f9f5-186">Para agregar un servidor WAP, Azure AD Connecte necesita el certificado PFX.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="2f9f5-187">Por lo tanto, puede realizar esta operación solamente si ha configurado la granja de servidores de AD FS con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="2f9f5-188">Seleccione **Implementar proxy de aplicación web** en la lista de tareas disponibles.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span></span>

   ![Implementación de Proxy de aplicación web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="2f9f5-190">Proporcione las credenciales del administrador global de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-190">Provide the Azure global administrator credentials.</span></span>

   ![Conectarse a Azure](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="2f9f5-192">En la página **Especificar el certificado SSL**, indique la contraseña para el archivo PFX que proporcionó cuando configuró la granja de servidores de AD FS con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="2f9f5-193">![Contraseña del certificado](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="2f9f5-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="2f9f5-195">Incluya el servidor que se agregará como servidor WAP.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-195">Add the server to be added as a WAP server.</span></span> <span data-ttu-id="2f9f5-196">Como el servidor WAP puede no estar unido al dominio, se le pedirán credenciales administrativas para el servidor que se va a agregar.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span></span>

   ![Credenciales administrativas del servidor](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="2f9f5-198">En la página **Credenciales de confianza del proxy**, proporcione credenciales administrativas para configurar la confianza del proxy y tener acceso al servidor principal en la granja de servidores de AD FS.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span></span>

   ![Credenciales de confianza del proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="2f9f5-200">En la página **Listo para configurar**, el asistente muestra la lista de acciones que se realizarán.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span></span>

   ![Listo para configurar](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="2f9f5-202">Haga clic en **Instalar** para finalizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-202">Click **Install** to finish the configuration.</span></span> <span data-ttu-id="2f9f5-203">Una vez completada la configuración, se le ofrece la opción de comprobar la conectividad con los servidores.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span></span> <span data-ttu-id="2f9f5-204">Haga clic en **Comprobar** para validar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-204">Click **Verify** to check connectivity.</span></span>

   ![Instalación completada](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="2f9f5-206">Adición de un dominio federado <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="2f9f5-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="2f9f5-207">Es fácil agregar un dominio para la federación con Azure AD mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="2f9f5-208">Azure AD Connect agrega el dominio para la federación y modifica las reglas de notificaciones para reflejar correctamente el emisor cuando existen varios dominios federados con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="2f9f5-209">Para agregar un dominio federado, seleccione la tarea **Agregar un dominio de Azure AD adicional**.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span></span>

   ![Dominio de Azure AD adicional](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="2f9f5-211">En la siguiente página del asistente, proporcione las credenciales de administrador global para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span></span>

   ![Conectarse a Azure](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="2f9f5-213">En la página **Credenciales de acceso remoto** , proporcione las credenciales del administrador del dominio.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span></span>

   ![Credenciales de acceso remoto](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="2f9f5-215">En la siguiente página del asistente, aparece una lista de dominios de Azure AD con los que puede federar su directorio local.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="2f9f5-216">Elija el dominio en la lista.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-216">Choose the domain from the list.</span></span>

   ![Dominio de Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="2f9f5-218">Después de elegir el dominio, se le proporcionará información adecuada sobre otras acciones que el asistente vaya a llevar a cabo y cómo afectarán a la configuración.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span></span> <span data-ttu-id="2f9f5-219">En algunos casos, si selecciona un dominio que aún no está comprobado en Azure AD, el asistente le proporcionará información para comprobarlo.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span></span> <span data-ttu-id="2f9f5-220">Consulte [Incorporación de su nombre de dominio personalizado a Azure Active Directory](../active-directory-add-domain.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="2f9f5-221">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-221">Click **Next**.</span></span> <span data-ttu-id="2f9f5-222">En la página **Listo para configurar** se muestra la lista de acciones que realizará Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="2f9f5-223">Haga clic en **Instalar** para finalizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-223">Click **Install** to finish the configuration.</span></span>

   ![Listo para configurar](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="2f9f5-225">Los usuarios del dominio federado agregado deben sincronizarse para poder iniciar sesión en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-225">Users from the added federated domain must be synchronized before they will be able to login to Azure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="2f9f5-226">Personalización de AD FS</span><span class="sxs-lookup"><span data-stu-id="2f9f5-226">AD FS customization</span></span>
<span data-ttu-id="2f9f5-227">En las secciones siguientes, se proporcionan detalles sobre algunas de las tareas comunes que probablemente deba realizar cuando personalice la página de inicio de sesión de AD FS.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-227">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="2f9f5-228">Adición de un logotipo de la compañía personalizado o una ilustración <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="2f9f5-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="2f9f5-229">Para cambiar el logotipo de la compañía que se muestra en la página de **inicio de sesión**, use el siguiente cmdlet de Windows PowerShell y la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-229">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="2f9f5-230">Las dimensiones recomendadas para el logotipo son 260 x 35 a 96 ppp con un tamaño de archivo no superior a 10 KB.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-230">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="2f9f5-231">Se requiere el parámetro *TargetName* .</span><span class="sxs-lookup"><span data-stu-id="2f9f5-231">The *TargetName* parameter is required.</span></span> <span data-ttu-id="2f9f5-232">El tema predeterminado que se incluyó con AD FS se llamada Default.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-232">The default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="2f9f5-233">Adición de la descripción de inicio de sesión <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="2f9f5-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="2f9f5-234">Para agregar una descripción de la **página de inicio de sesión**a dicha página, use el siguiente cmdlet de Windows PowerShell y la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-234">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="2f9f5-235">Modificación de las reglas de notificaciones de AD FS <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="2f9f5-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="2f9f5-236">AD FS admite un amplio lenguaje de notificaciones que sirve para crear reglas de notificaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-236">AD FS supports a rich claim language that you can use to create custom claim rules.</span></span> <span data-ttu-id="2f9f5-237">Para más información, consulte [El papel de lenguaje de reglas de notificación](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f9f5-237">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="2f9f5-238">En las secciones siguientes, se describe cómo escribir reglas personalizadas para algunos escenarios relacionados con la federación de Azure AD y AD FS.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-238">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-the-attribute"></a><span data-ttu-id="2f9f5-239">Identificador inmutable dependiente de si hay un valor presente en el atributo</span><span class="sxs-lookup"><span data-stu-id="2f9f5-239">Immutable ID conditional on a value being present in the attribute</span></span>
<span data-ttu-id="2f9f5-240">Azure AD Connect permite especificar un atributo que se usará como delimitador de origen cuando los objetos se sincronicen con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-240">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span></span> <span data-ttu-id="2f9f5-241">Si el valor del atributo personalizado no está vacío, puede emitir una notificación de identificador inmutable.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-241">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span></span>

<span data-ttu-id="2f9f5-242">Por ejemplo, puede seleccionar **ms-ds-consistencyguid** como atributo del delimitador de origen y emitir **ImmutableID** como **ms-ds-consistencyguid** por si el atributo tiene un valor para él.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-242">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span></span> <span data-ttu-id="2f9f5-243">Si no hay ningún valor para el atributo, emita **objectGuid** como identificador inmutable.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-243">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span></span> <span data-ttu-id="2f9f5-244">Puede construir el conjunto de reglas de notificaciones personalizadas, tal como se describe en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-244">You can construct the set of custom claim rules as described in the following section.</span></span>

<span data-ttu-id="2f9f5-245">**Regla 1: Consultar atributos**</span><span class="sxs-lookup"><span data-stu-id="2f9f5-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="2f9f5-246">En esta regla simplemente se consultan los valores de **ms-ds-consistencyguid** y **objectGuid** para el usuario desde Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-246">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span></span> <span data-ttu-id="2f9f5-247">Cambie el nombre del almacén por un nombre adecuado en la implementación de AD FS.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-247">Change the store name to an appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="2f9f5-248">Cambie también el tipo de notificaciones a un tipo correcto para la federación, tal como se define para los atributos **objectGuid** y **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-248">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="2f9f5-249">Además, al usar **add** y no **issue**, no se tiene que agregar una emisión de salida para la entidad y solo se usan los valores como valores intermedios.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span></span> <span data-ttu-id="2f9f5-250">Se emitirá la notificación en una regla posterior después de establecerse el valor que se usará como identificador inmutable.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-250">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span></span>

<span data-ttu-id="2f9f5-251">**Regla 2: comprobar si ms-ds-consistencyguid existe para el usuario**</span><span class="sxs-lookup"><span data-stu-id="2f9f5-251">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="2f9f5-252">Esta regla define un marcador temporal **idflag**, que se establece en **useguid** si no hay ningún atributo **ms-ds-consistencyguid** rellenado para el usuario.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-252">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span></span> <span data-ttu-id="2f9f5-253">Esto se debe a que ADFS no admite notificaciones vacías.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-253">The logic behind this is the fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="2f9f5-254">Por tanto, cuando se agrega http://contoso.com/ws/2016/02/identity/claims/objectguid y http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid en la regla 1, terminará con la notificación **msdsconsistencyguid** solo si el valor está rellenado para el usuario.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span></span> <span data-ttu-id="2f9f5-255">Si no se rellena, AD FS ve que tiene un valor vacío y lo coloca inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="2f9f5-256">Todos los objetos tendrán el atributo **objectGuid**, así que esa notificación seguirá estando después de que se ejecute la regla 1.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="2f9f5-257">**Regla 3: Emitir el atributo ms-ds-consistencyguid como identificador inmutable si está presente**</span><span class="sxs-lookup"><span data-stu-id="2f9f5-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="2f9f5-258">Se trata de una comprobación **Exist** implícita.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="2f9f5-259">Si el valor de la notificación existe, emítalo como identificador inmutable.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-259">If the value for the claim exists, then issue that as the immutable ID.</span></span> <span data-ttu-id="2f9f5-260">En el ejemplo anterior se utiliza la notificación **nameidentifier** .</span><span class="sxs-lookup"><span data-stu-id="2f9f5-260">The previous example uses the **nameidentifier** claim.</span></span> <span data-ttu-id="2f9f5-261">Tendrá que cambiar este valor al tipo de notificación adecuado para un identificador inmutable en su entorno.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-261">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span></span>

<span data-ttu-id="2f9f5-262">**Regla 4: Emitir el atributo objectGUID como identificador inmutable si ms-ds-consistencyguid no está presente**</span><span class="sxs-lookup"><span data-stu-id="2f9f5-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="2f9f5-263">En esta regla, simplemente va a comprobar el atributo **idflag**temporal.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-263">In this rule, you're simply checking the temporary flag **idflag**.</span></span> <span data-ttu-id="2f9f5-264">Decida si va a emitir la notificación basándose en su valor.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-264">You decide whether to issue the claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="2f9f5-265">La secuencia de estas reglas es importante.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-265">The sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="2f9f5-266">SSO con un UPN de subdominio</span><span class="sxs-lookup"><span data-stu-id="2f9f5-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="2f9f5-267">Puede agregar más de un dominio para federarlo mediante Azure AD Connect, tal como se describe en [Incorporación de un nuevo dominio federado](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="2f9f5-267">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="2f9f5-268">Debe modificar la notificación de nombre principal de usuario (UPN) para que el identificador de emisor se corresponda con el dominio raíz y no con el subdominio, ya que el dominio raíz federado cubre también el elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-268">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span></span>

<span data-ttu-id="2f9f5-269">De forma predeterminada, la regla de notificaciones para el identificador de emisor se establece como:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-269">By default, the claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Notificación del identificador de emisor predeterminado](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="2f9f5-271">La regla predeterminada simplemente toma el sufijo UPN y lo utiliza en la notificación de identificador del emisor.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-271">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span></span> <span data-ttu-id="2f9f5-272">Por ejemplo, John es un usuario de sub.contoso.com y contoso.com está federado con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="2f9f5-273">John escribe john@sub.contoso.com como el nombre de usuario mientras inicia sesión en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-273">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span></span> <span data-ttu-id="2f9f5-274">La regla de notificación del id. del emisor predeterminada en AD FS lo controla de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-274">The default issuer ID claim rule in AD FS handles it in the following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="2f9f5-275">**Valor de notificación:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="2f9f5-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="2f9f5-276">Para tener solo el dominio raíz en el valor de notificación del emisor, cambie la regla de notificaciones para que coincida con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-276">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="2f9f5-277">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f9f5-277">Next steps</span></span>
<span data-ttu-id="2f9f5-278">Obtenga más información sobre las [opciones de inicio de sesión del usuario](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="2f9f5-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
