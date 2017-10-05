---
title: "Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory | Microsoft Docs"
description: "Configure sus dispositivos Windows unidos a un dominio para registrarse de forma automática y silenciosa en Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: dccd7df6a5f85df4179c7ea7cfc476cfb57f48c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="68f2a-103">Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68f2a-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="68f2a-104">Para usar el [acceso condicional basado en dispositivo de Azure Active Directory](active-directory-conditional-access-azure-portal.md), los dispositivos deben estar registrados en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68f2a-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="68f2a-105">Para obtener una lista de los dispositivos registrados de una organización, utilice el cmdlet [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) en el [módulo de PowerShell de Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="68f2a-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="68f2a-106">Este artículo le proporciona los pasos para configurar el registro automático de dispositivos unidos a un dominio de Windows con Azure AD en su organización.</span><span class="sxs-lookup"><span data-stu-id="68f2a-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="68f2a-107">Para más información acerca de:</span><span class="sxs-lookup"><span data-stu-id="68f2a-107">For more information about:</span></span>

- <span data-ttu-id="68f2a-108">Acceso condicional, consulte [Acceso condicional en Azure Active Directory: versión preliminar](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68f2a-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="68f2a-109">Dispositivos con Windows 10 en el área de trabajo y las experiencias mejoradas al registrarse en Azure AD, consulte [Windows 10 para empresa: formas de usar dispositivos para trabajar](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68f2a-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="68f2a-110">Windows 10 Enterprise E3 en CSP, consulte la [Introducción a Windows 10 Enterprise E3 en CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="68f2a-110">Windows 10 Enterprise E3 in CSP, see the [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="68f2a-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="68f2a-111">Before you begin</span></span>

<span data-ttu-id="68f2a-112">Antes de empezar a configurar el registro automático de los dispositivos unidos a un dominio de Windows en su entorno, debe familiarizarse con los escenarios admitidos y las restricciones.</span><span class="sxs-lookup"><span data-stu-id="68f2a-112">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="68f2a-113">Para mejorar la legibilidad de las descripciones, en este tema se utiliza el término siguiente:</span><span class="sxs-lookup"><span data-stu-id="68f2a-113">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="68f2a-114">**Dispositivos de Windows actuales**: este término indica los dispositivos unidos a un dominio en los que se ejecutan Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="68f2a-114">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="68f2a-115">**Dispositivos de Windows de nivel inferior**: este término indica todos los dispositivos de Windows unidos a un dominio **compatibles** en los que no se ejecutan Windows 10 ni Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="68f2a-115">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="68f2a-116">Dispositivos de Windows actuales</span><span class="sxs-lookup"><span data-stu-id="68f2a-116">Windows current devices</span></span>

- <span data-ttu-id="68f2a-117">Para los dispositivos en los que se ejecuta el sistema operativo de escritorio Windows, se recomienda usar la Actualización de aniversario de Windows 10 (versión 1607), o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="68f2a-117">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="68f2a-118">El registro de los dispositivos de Windows actuales **se** admite en entornos de no federadas, como las configuraciones de sincronización de hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="68f2a-118">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="68f2a-119">Dispositivos de Windows de nivel inferior</span><span class="sxs-lookup"><span data-stu-id="68f2a-119">Windows down-level devices</span></span>

- <span data-ttu-id="68f2a-120">Se admiten los siguientes dispositivos de nivel inferior de Windows:</span><span class="sxs-lookup"><span data-stu-id="68f2a-120">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="68f2a-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="68f2a-121">Windows 8.1</span></span>
    - <span data-ttu-id="68f2a-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="68f2a-122">Windows 7</span></span>
    - <span data-ttu-id="68f2a-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="68f2a-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="68f2a-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="68f2a-124">Windows Server 2012</span></span>
    - <span data-ttu-id="68f2a-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="68f2a-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="68f2a-126">El registro de dispositivos de Windows de nivel inferior **se** admite en entornos no federados a través del inicio de sesión único de conexión directa [Inicio de sesión único de conexión directa de Azure Active Directory](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="68f2a-126">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="68f2a-127">El registro de dispositivos de Windows de nivel inferior **no se** admite en dispositivos que usan perfiles móviles.</span><span class="sxs-lookup"><span data-stu-id="68f2a-127">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="68f2a-128">Si confía en la itinerancia de la configuración o de los perfiles, use Windows 10.</span><span class="sxs-lookup"><span data-stu-id="68f2a-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="68f2a-129">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="68f2a-129">Prerequisites</span></span>

<span data-ttu-id="68f2a-130">Antes de empezar a habilitar el registro automático de los dispositivos unidos a un dominio de su organización, es preciso asegurarse de que se ejecuta una versión actualizada de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="68f2a-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="68f2a-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="68f2a-131">Azure AD Connect:</span></span>

- <span data-ttu-id="68f2a-132">Mantiene la asociación entre la cuenta del equipo en la instancia local de Active Directory (AD) y el objeto de dispositivo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f2a-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="68f2a-133">Habilita otras características relacionadas del dispositivo como Windows Hello para empresas.</span><span class="sxs-lookup"><span data-stu-id="68f2a-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="68f2a-134">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="68f2a-134">Configuration steps</span></span>

<span data-ttu-id="68f2a-135">En este tema se incluye los pasos requeridos para todos los escenarios de configuración típicos.</span><span class="sxs-lookup"><span data-stu-id="68f2a-135">This topic includes the required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="68f2a-136">Utilice la tabla siguiente para obtener una visión general de los pasos necesarios para su escenario:</span><span class="sxs-lookup"><span data-stu-id="68f2a-136">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="68f2a-137">Pasos</span><span class="sxs-lookup"><span data-stu-id="68f2a-137">Steps</span></span>                                      | <span data-ttu-id="68f2a-138">Dispositivos actuales de Windows y sincronización de hash de contraseña</span><span class="sxs-lookup"><span data-stu-id="68f2a-138">Windows current and password hash sync</span></span> | <span data-ttu-id="68f2a-139">Dispositivos actuales de Windows y federación</span><span class="sxs-lookup"><span data-stu-id="68f2a-139">Windows current and federation</span></span> | <span data-ttu-id="68f2a-140">Dispositivos de Windows de nivel inferior</span><span class="sxs-lookup"><span data-stu-id="68f2a-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="68f2a-141">Paso 1: Configuración del punto de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="68f2a-141">Step 1: Configure service connection point</span></span> | ![Comprobar][1]                            | ![Comprobar][1]                    | ![Comprobar][1]        |
| <span data-ttu-id="68f2a-145">Paso 2: Configuración de la emisión de notificaciones</span><span class="sxs-lookup"><span data-stu-id="68f2a-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Comprobar][1]                    | ![Comprobar][1]        |
| <span data-ttu-id="68f2a-148">Paso 3: Habilitación de dispositivos que no tengan Windows 10</span><span class="sxs-lookup"><span data-stu-id="68f2a-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Comprobar][1]        |
| <span data-ttu-id="68f2a-150">Paso 4: Control de implementación y lanzamiento</span><span class="sxs-lookup"><span data-stu-id="68f2a-150">Step 4: Control deployment and rollout</span></span>     | ![Comprobar][1]                            | ![Comprobar][1]                    | ![Comprobar][1]        |
| <span data-ttu-id="68f2a-154">Paso 5: Comprobación de los dispositivos registrados</span><span class="sxs-lookup"><span data-stu-id="68f2a-154">Step 5: Verify registered devices</span></span>          | ![Comprobar][1]                            | ![Comprobar][1]                    | ![Comprobar][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="68f2a-158">Paso 1: Configurar el punto de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="68f2a-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="68f2a-159">El objeto de punto de conexión de servicio (SCP) lo usan los dispositivos durante el registro para detectar la información del inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f2a-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="68f2a-160">En la instancia de Active Directory (AD) local, el objeto de SCP para el registro automático de dispositivos unidos a un dominio debe existir en la partición del contexto de nomenclatura de la configuración del bosque del equipo.</span><span class="sxs-lookup"><span data-stu-id="68f2a-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="68f2a-161">Hay solo un contexto de nomenclatura de configuración por bosque.</span><span class="sxs-lookup"><span data-stu-id="68f2a-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="68f2a-162">En una configuración de Active Directory con varios bosques, el punto de conexión debe existir en todos los bosques que contengan equipos unidos a un dominio.</span><span class="sxs-lookup"><span data-stu-id="68f2a-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="68f2a-163">Se puede usar el comando [**Get ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) para recuperar el contexto de nomenclatura de configuración del bosque.</span><span class="sxs-lookup"><span data-stu-id="68f2a-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="68f2a-164">En el caso de un bosque con el nombre de dominio de Active Directory *fabrikam.com*, el contexto de nomenclatura de configuración es:</span><span class="sxs-lookup"><span data-stu-id="68f2a-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="68f2a-165">En el bosque, el objeto de SCP para el registro automático de los dispositivos unidos a un dominio se encuentra en:</span><span class="sxs-lookup"><span data-stu-id="68f2a-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="68f2a-166">En función de cómo se haya implementado Azure AD Connect, el objeto SCP puede que ya se haya configurado.</span><span class="sxs-lookup"><span data-stu-id="68f2a-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="68f2a-167">Con el siguiente script de Windows PowerShell se puede comprobar la existencia del objeto y recuperar los valores de detección:</span><span class="sxs-lookup"><span data-stu-id="68f2a-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="68f2a-168">La salida de **$scp.Keywords** muestra la información del inquilino de Azure AD, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="68f2a-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="68f2a-169">Si el punto de conexión de servicio no existe, se puede crear mediante la ejecución del cmdlet `Initialize-ADSyncDomainJoinedComputerSync` en un servidor de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="68f2a-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="68f2a-170">Se necesitan las credenciales de administrador de organización para ejecutar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68f2a-170">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="68f2a-171">El cmdlet:</span><span class="sxs-lookup"><span data-stu-id="68f2a-171">The cmdlet:</span></span>

- <span data-ttu-id="68f2a-172">Crea el punto de conexión de servicio en el bosque de Active Directory al que está conectado Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="68f2a-172">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="68f2a-173">Requiere que se especifique el parámetro `AdConnectorAccount`.</span><span class="sxs-lookup"><span data-stu-id="68f2a-173">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="68f2a-174">Se trata de la cuenta configurada como cuenta de conector de Active Directory en Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="68f2a-174">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="68f2a-175">El siguiente script muestra un ejemplo de uso del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68f2a-175">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="68f2a-176">En este script, `$aadAdminCred = Get-Credential` requiere que escriba un nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="68f2a-176">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="68f2a-177">Es proceso que use el formato de nombre principal de usuario (UPN) (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="68f2a-177">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="68f2a-178">El cmdlet `Initialize-ADSyncDomainJoinedComputerSync`:</span><span class="sxs-lookup"><span data-stu-id="68f2a-178">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="68f2a-179">Usa el módulo de PowerShell de Active Directory, que usa Active Directory Web Services que se ejecuta en un controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="68f2a-179">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="68f2a-180">Active Directory Web Services es compatible con los controladores de dominio en los que se ejecuta Windows Server 2008 R2, y las versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="68f2a-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="68f2a-181">Solo es compatible con la **versión 1.1.166.0 del módulo de MSOnline PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-181">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="68f2a-182">Para descargar este módulo, use este [vínculo](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="68f2a-182">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="68f2a-183">En los casos de los controladores de dominio en los que se ejecuta Windows Server 2008 R2, o alguna versión anterior, use el siguiente script para crear el punto de conexión de servicio.</span><span class="sxs-lookup"><span data-stu-id="68f2a-183">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="68f2a-184">En una configuración con varios bosques, debe usar el script siguiente para crear el punto de conexión de servicio en cada bosque en el que existan equipos:</span><span class="sxs-lookup"><span data-stu-id="68f2a-184">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="68f2a-185">Paso 2: Configuración de la emisión de notificaciones</span><span class="sxs-lookup"><span data-stu-id="68f2a-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="68f2a-186">En una configuración de Azure AD federada, los dispositivos usan Active Directory Federation Services (AD FS) o un servicio de federación local de terceros para autenticarse en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f2a-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="68f2a-187">Los dispositivos se autentican para obtener un token de acceso para registrarse en Azure Active Directory Device Registration Service (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="68f2a-187">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="68f2a-188">Los dispositivos de Windows actuales se autentican mediante la autenticación integrada de Windows en un punto de conexión de WS-Trust activo (versiones 1.3 o 2005) hospedado por el servicio de federación local.</span><span class="sxs-lookup"><span data-stu-id="68f2a-188">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="68f2a-189">Si se usa AD FS, es preciso habilitar **adfs/services/trust/13/windowstransport** o **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="68f2a-190">Si usa el proxy de autenticación web, asegúrese también de que este punto de conexión se publique a través del proxy.</span><span class="sxs-lookup"><span data-stu-id="68f2a-190">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="68f2a-191">Para ver qué puntos de conexión están habilitados, vaya a **Servicio > Puntos de conexión** en la consola de administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="68f2a-191">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="68f2a-192">Si AD FS no es el servicio de federación local, siga las instrucciones de su proveedor para asegurarse de que admite puntos de conexión de WS-Trust 1.3 o 2005 y que estos se publican a través del archivo de intercambio de metadatos (MEX).</span><span class="sxs-lookup"><span data-stu-id="68f2a-192">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="68f2a-193">Para que se complete el registro del dispositivo, las siguientes notificaciones deben existir en el token que recibe Azure DRS.</span><span class="sxs-lookup"><span data-stu-id="68f2a-193">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="68f2a-194">Azure DRS creará un objeto de dispositivo en Azure AD con una parte de esta información, que después usa Azure AD Connect para asociar el objeto de dispositivo recién creado con la cuenta local del equipo.</span><span class="sxs-lookup"><span data-stu-id="68f2a-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="68f2a-195">Si hay más de un nombre de dominio comprobado, es preciso proporcionar la siguiente notificación para los equipos:</span><span class="sxs-lookup"><span data-stu-id="68f2a-195">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="68f2a-196">Si ya se emite una notificación de ImmutableID (p. ej., identificador de inicio de sesión alternativo), será preciso proporcionar una notificación correspondiente para los equipos:</span><span class="sxs-lookup"><span data-stu-id="68f2a-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="68f2a-197">En las siguientes secciones encontrará información acerca de:</span><span class="sxs-lookup"><span data-stu-id="68f2a-197">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="68f2a-198">Los valores que deben tener todas las notificaciones</span><span class="sxs-lookup"><span data-stu-id="68f2a-198">The values each claim should have</span></span>
- <span data-ttu-id="68f2a-199">El aspecto de una definición en AD FS</span><span class="sxs-lookup"><span data-stu-id="68f2a-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="68f2a-200">La definición le ayuda a comprobar si los valores están presentes o si debe crearlos.</span><span class="sxs-lookup"><span data-stu-id="68f2a-200">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="68f2a-201">Si no usa AD FS como servidor de federación local, siga las instrucciones de su proveedor para crear la configuración apropiada para emitir estas notificaciones.</span><span class="sxs-lookup"><span data-stu-id="68f2a-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="68f2a-202">Emisión de notificación de tipo de cuenta</span><span class="sxs-lookup"><span data-stu-id="68f2a-202">Issue account type claim</span></span>

<span data-ttu-id="68f2a-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**: esta notificación debe contener un valor de **DJ**, que identifica el dispositivo como equipo unido a un dominio.</span><span class="sxs-lookup"><span data-stu-id="68f2a-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="68f2a-204">En AD FS, puede agregar una regla de transformación de emisión como esta:</span><span class="sxs-lookup"><span data-stu-id="68f2a-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="68f2a-205">Emisión de objectGUID de la cuenta local del equipo</span><span class="sxs-lookup"><span data-stu-id="68f2a-205">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="68f2a-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**: esta notificación debe contener el valor **objectGUID** de la cuenta local del equipo.</span><span class="sxs-lookup"><span data-stu-id="68f2a-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="68f2a-207">En AD FS, puede agregar una regla de transformación de emisión como esta:</span><span class="sxs-lookup"><span data-stu-id="68f2a-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="68f2a-208">Emisión de objectSID de la cuenta local del equipo</span><span class="sxs-lookup"><span data-stu-id="68f2a-208">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="68f2a-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**: esta notificación debe contener el valor **objectSid** de la cuenta local del equipo.</span><span class="sxs-lookup"><span data-stu-id="68f2a-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="68f2a-210">En AD FS, puede agregar una regla de transformación de emisión como esta:</span><span class="sxs-lookup"><span data-stu-id="68f2a-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="68f2a-211">Emisión de issuerID para un equipo cuando haty varios nombres de dominio comprobados en Azure AD</span><span class="sxs-lookup"><span data-stu-id="68f2a-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="68f2a-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**: esta notificación debe contener el identificador uniforme de recursos (URI) de cualquiera de los nombres de dominio comprobados que se conectan al servicio de federación local (AD FS o uno de terceros) que emite el token.</span><span class="sxs-lookup"><span data-stu-id="68f2a-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="68f2a-213">En AD FS, puede agregar reglas de transformación de emisión que se parecen a las que verá a continuación en ese orden específico después de las anteriores.</span><span class="sxs-lookup"><span data-stu-id="68f2a-213">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="68f2a-214">Tenga en cuenta que se necesita una regla que emita explícitamente la regla para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="68f2a-214">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="68f2a-215">En las reglas siguientes, se agrega una primera regla que identifique al usuario frente a la autenticación del equipo.</span><span class="sxs-lookup"><span data-stu-id="68f2a-215">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="68f2a-216">En la notificación anterior,</span><span class="sxs-lookup"><span data-stu-id="68f2a-216">In the claim above,</span></span>

- <span data-ttu-id="68f2a-217">`$<domain>` corresponde a la dirección URL del servicio AD FS.</span><span class="sxs-lookup"><span data-stu-id="68f2a-217">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="68f2a-218">`<verified-domain-name>` corresponde a un marcador de posición que se debe reemplazar con uno de los nombres de dominio comprobados en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f2a-218">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="68f2a-219">Consulte [Incorporación de su nombre de dominio personalizado a Azure Active Directory](active-directory-add-domain.md) para más información sobre nombres de dominios comprobados.</span><span class="sxs-lookup"><span data-stu-id="68f2a-219">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="68f2a-220">Para obtener una lista de los dominios comprobados de la compañía, puede usar el cmdlet [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="68f2a-220">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="68f2a-222">Emisión de ImmutableID para un equipo cuando existe uno para los usuarios (por ejemplo, se ha establecido el identificador de inicio de sesión alternativo)</span><span class="sxs-lookup"><span data-stu-id="68f2a-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="68f2a-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**: esta notificación debe contener un valor válido para los equipos.</span><span class="sxs-lookup"><span data-stu-id="68f2a-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="68f2a-224">En AD FS, se puede crear una regla de transformación de emisión como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="68f2a-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="68f2a-225">Script de aplicación auxiliar para crear reglas de transformación de emisión de AD FS</span><span class="sxs-lookup"><span data-stu-id="68f2a-225">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="68f2a-226">El siguiente script le ayuda con la creación de las reglas de transformación de emisión que se han descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="68f2a-226">The following script helps you with the creation of the issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="68f2a-227">Comentarios</span><span class="sxs-lookup"><span data-stu-id="68f2a-227">Remarks</span></span> 

- <span data-ttu-id="68f2a-228">Este script anexa las reglas a las reglas existentes.</span><span class="sxs-lookup"><span data-stu-id="68f2a-228">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="68f2a-229">No ejecute el script dos veces porque el conjunto de reglas se agregaría dos veces.</span><span class="sxs-lookup"><span data-stu-id="68f2a-229">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="68f2a-230">Asegúrese de que no existe ninguna regla correspondiente para estas notificaciones (en las condiciones correspondientes) antes de volver a ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="68f2a-230">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="68f2a-231">Si tiene varios nombres de dominio comprobados (como se muestra en el portal de Azure AD o mediante el cmdlet Get-MsolDomains), establezca el valor de **$multipleVerifiedDomainNames** en el script en **$true**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-231">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="68f2a-232">Además, asegúrese de que quita cualquier notificación issuerid existente que pueda haber creado Azure AD Connect o a través de otros medios.</span><span class="sxs-lookup"><span data-stu-id="68f2a-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="68f2a-233">Este es un ejemplo de esta regla:</span><span class="sxs-lookup"><span data-stu-id="68f2a-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="68f2a-234">Si ya ha emitido una notificación **ImmutableID** para las cuentas de usuario, establezca el valor de **$immutableIDAlreadyIssuedforUsers** en el script en **$true**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-234">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="68f2a-235">Paso 3: Habilitación de dispositivos de Windows de nivel inferior</span><span class="sxs-lookup"><span data-stu-id="68f2a-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="68f2a-236">Si algunos de los dispositivos unidos a un dominio son dispositivos de Windows de nivel inferior, necesitará:</span><span class="sxs-lookup"><span data-stu-id="68f2a-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="68f2a-237">Establecer una directiva en Azure AD que permita a los usuarios registrar dispositivos.</span><span class="sxs-lookup"><span data-stu-id="68f2a-237">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="68f2a-238">Configurar el servicio de federación local para emitir notificaciones para admitir la **autenticación integrada de Windows (IWA)** para el registro de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="68f2a-238">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="68f2a-239">Agregar el punto de conexión de autenticación de dispositivos de Azure AD a las zonas de la intranet locales para evitar las solicitudes de certificado al autenticar el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="68f2a-239">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="68f2a-240">Establecer una directiva de Azure AD que permita a los usuarios registrar dispositivos</span><span class="sxs-lookup"><span data-stu-id="68f2a-240">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="68f2a-241">Para registrar dispositivos de Windows de nivel inferior, es preciso asegurarse de que está establecida la configuración que permite a los usuarios registrar dispositivos en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f2a-241">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="68f2a-242">En Azure Portal, esta configuración se encuentra en:</span><span class="sxs-lookup"><span data-stu-id="68f2a-242">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="68f2a-243">En la siguiente directiva se debe elegir **Todos**: **Los usuarios pueden registrar sus dispositivos con Azure AD**</span><span class="sxs-lookup"><span data-stu-id="68f2a-243">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Registro de dispositivos](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="68f2a-245">Configuración de un servicio de federación local</span><span class="sxs-lookup"><span data-stu-id="68f2a-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="68f2a-246">Un servicio de federación local debe admitir la emisión de las notificaciones **authenticationmehod** y **wiaormultiauthn** al recibir una solicitud de autenticación para el usuario de confianza de Azure AD que contiene un parámetro resouce_params con un valor codificado, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="68f2a-246">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="68f2a-247">Cuando llega una solicitud de este tipo, el servicio de federación local debe autenticar al usuario mediante la autenticación integrada de Windows y una vez que la autenticación se haya realiza correctamente, debe emitir las dos notificaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="68f2a-247">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="68f2a-248">En AD FS, debe agregar una regla de transformación de emisión que atraviesa el método de autenticación.</span><span class="sxs-lookup"><span data-stu-id="68f2a-248">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="68f2a-249">**Para agregar esta regla:**</span><span class="sxs-lookup"><span data-stu-id="68f2a-249">**To add this rule:**</span></span>

1. <span data-ttu-id="68f2a-250">En la consola de administración de AD FS, vaya a `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="68f2a-250">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="68f2a-251">Haga clic con el botón derecho en el objeto de confianza para usuario de confianza de la Plataforma de identidad de Microsoft Office 365 y seleccione **Editar reglas de notificación**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-251">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="68f2a-252">En la pestaña **Reglas de transformación de emisión**, seleccione **Agregar regla**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-252">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="68f2a-253">Seleccione **Enviar notificaciones con una regla personalizada** en la lista de plantillas **Regla de notificación**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-253">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="68f2a-254">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-254">Select **Next**.</span></span>
6. <span data-ttu-id="68f2a-255">En el cuadro **Nombre de regla de notificación**, escriba **Regla de notificaciones del método de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-255">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="68f2a-256">En el cuadro **Regla de notificación** escriba la siguiente regla:</span><span class="sxs-lookup"><span data-stu-id="68f2a-256">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="68f2a-257">En el servidor de federación, escriba el comando de PowerShell siguiente después de reemplazar **\<RPObjectName\>** por el nombre de objeto de usuario de confianza del objeto de confianza del usuario de confianza de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f2a-257">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="68f2a-258">Normalmente, este objeto se llama **Plataforma de identidad de Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="68f2a-259">Adición del punto de conexión de autenticación de dispositivos de Azure AD a las zonas de intranet locales</span><span class="sxs-lookup"><span data-stu-id="68f2a-259">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="68f2a-260">Para evitar las peticiones de certificados cuando los usuarios de dispositivos registrados se autentican en Azure AD se puede insertar una directiva en los dispositivos unidos a un dominio para agregar la siguiente dirección URL a la zona de intranet local en Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="68f2a-260">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="68f2a-261">Paso 4: Control de implementación y lanzamiento</span><span class="sxs-lookup"><span data-stu-id="68f2a-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="68f2a-262">Cuando se hayan completado los pasos requeridos, los dispositivos unidos a un dominio están listos para registrarse automáticamente en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f2a-262">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span></span> <span data-ttu-id="68f2a-263">Todos los dispositivos unidos a un dominio en que se ejecuten la Actualización de aniversario de Windows 10 y Windows Server 2016 se registran automáticamente en Azure AD cuando el dispositivo se reinicie o el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="68f2a-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="68f2a-264">Los dispositivos nuevos se registran en Azure AD al reiniciarse después de que finaliza la operación de unión al dominio.</span><span class="sxs-lookup"><span data-stu-id="68f2a-264">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

<span data-ttu-id="68f2a-265">Los dispositivos que anteriormente estaban unidos a un área de trabajo en Azure AD (por ejemplo, para Intune) pasan a estar "*unidos a dominio, registrados en AAD*". Sin embargo, este proceso tarda algún tiempo en completarse en todos los dispositivos debido al flujo normal de actividades de dominio y de usuario.</span><span class="sxs-lookup"><span data-stu-id="68f2a-265">Devices that were previously workplace-joined to Azure AD (for example for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="68f2a-266">Comentarios</span><span class="sxs-lookup"><span data-stu-id="68f2a-266">Remarks</span></span>

- <span data-ttu-id="68f2a-267">Para controlar el lanzamiento del registro automático de los equipos con Windows 10 y Windows Server 2016 unidos a un dominio, se puede usar un objeto de directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="68f2a-267">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="68f2a-268">La actualización de noviembre de 2015 de Windows 10 se registra automáticamente en Azure AD **solo** si se establece el objeto de directiva de grupo del lanzamiento.</span><span class="sxs-lookup"><span data-stu-id="68f2a-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="68f2a-269">Para el lanzamiento del registro automático de los equipos de Windows de nivel inferior, se puede implementar un [paquete de Windows Installer](#windows-installer-packages-for-non-windows-10-computers) en los equipos que se seleccionen.</span><span class="sxs-lookup"><span data-stu-id="68f2a-269">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="68f2a-270">Si se inserta el objeto de directiva de grupo en dispositivos unidos a un dominio de Windows 8.1, se volverá a intentar el registro; sin embargo, se recomienda usar el [paquete de Windows Installer](#windows-installer-packages-for-non-windows-10-computers) para registrar todos los dispositivos de Windows de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="68f2a-270">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="68f2a-271">Creación de un objeto de directiva de grupo</span><span class="sxs-lookup"><span data-stu-id="68f2a-271">Create a Group Policy object</span></span> 

<span data-ttu-id="68f2a-272">Para controlar el lanzamiento del registro automático de los equipos actuales de Windows, es preciso que implemente el objeto de la directiva de grupo **Registrar los equipos asociados a un dominio como dispositivos** en los equipos que desee registrar.</span><span class="sxs-lookup"><span data-stu-id="68f2a-272">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="68f2a-273">Por ejemplo, puede implementar la directiva en un grupo de seguridad o en una unidad organizativa.</span><span class="sxs-lookup"><span data-stu-id="68f2a-273">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="68f2a-274">**Para establecer la directiva:**</span><span class="sxs-lookup"><span data-stu-id="68f2a-274">**To set the policy:**</span></span>

1. <span data-ttu-id="68f2a-275">Abra el **Administrador del servidor**y vaya a `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="68f2a-275">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="68f2a-276">Vaya al nodo del dominio correspondiente al dominio en el que desee activar el registro automático de los equipos actuales de Windows.</span><span class="sxs-lookup"><span data-stu-id="68f2a-276">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="68f2a-277">Haga clic con el botón derecho en **Objetos de directiva de grupo** y seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="68f2a-278">Escriba un nombre para el objeto de directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="68f2a-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="68f2a-279">Por ejemplo, *Registro automático de Azure AD*.</span><span class="sxs-lookup"><span data-stu-id="68f2a-279">For example, *Automatic Registration to Azure AD*.</span></span> <span data-ttu-id="68f2a-280">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-280">Select **OK**.</span></span>
5. <span data-ttu-id="68f2a-281">Haga clic con el botón derecho en el nuevo objeto de directiva de grupo y seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="68f2a-282">Vaya a **Configuración del equipo** > **Directivas** > **Plantillas administrativas** > **Componentes de Windows** > **Registro de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-282">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="68f2a-283">Haga clic con el botón derecho en **Registrar los equipos asociados a un dominio como dispositivos** y seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="68f2a-284">Esta plantilla de directiva de grupo ha cambiado de nombre desde versiones anteriores de la consola de Administración de directivas de grupo.</span><span class="sxs-lookup"><span data-stu-id="68f2a-284">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="68f2a-285">Si utiliza una versión anterior de la consola, vaya a `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="68f2a-285">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="68f2a-286">Seleccione **Habilitado** y luego **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="68f2a-287">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-287">Select **OK**.</span></span>
9. <span data-ttu-id="68f2a-288">Vincule el objeto de la directiva de grupo a una ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="68f2a-288">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="68f2a-289">Por ejemplo, puede vincularlo a una unidad organizativa específica.</span><span class="sxs-lookup"><span data-stu-id="68f2a-289">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="68f2a-290">También puede vincularlo a un grupo de seguridad específico de equipos que se registren automáticamente en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f2a-290">You also could link it to a specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="68f2a-291">Para establecer esta directiva para todos los equipos con Windows 10 y Windows Server 2016 unidos a un dominio en su organización, vincule el objeto de directiva de grupo al dominio.</span><span class="sxs-lookup"><span data-stu-id="68f2a-291">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="68f2a-292">Paquetes de Windows Installer para equipos sin Windows 10</span><span class="sxs-lookup"><span data-stu-id="68f2a-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="68f2a-293">Para registrar equipos de Windows de nivel inferior unidos a un dominio en un entorno federado, puede descargar e instalar este paquetes de Windows Installer (.msi) desde la opción Download Center (Centro de descarga) de la página [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) (Microsoft Workplace Join para equipos sin Windows 10).</span><span class="sxs-lookup"><span data-stu-id="68f2a-293">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="68f2a-294">El paquete se puede implementar mediante un sistema de distribución de software como System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="68f2a-294">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="68f2a-295">El paquete admite las opciones de instalación silenciosa estándar mediante el parámetro *quiet*.</span><span class="sxs-lookup"><span data-stu-id="68f2a-295">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="68f2a-296">La rama actual de System Center Configuration Manager ofrece ventajas adicionales con respecto a las versiones anteriores, como la capacidad de realizar el seguimiento de los registros completados.</span><span class="sxs-lookup"><span data-stu-id="68f2a-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="68f2a-297">Para más información, consulte [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="68f2a-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="68f2a-298">El instalador crea una tarea programada en el sistema que se ejecuta en el contexto del usuario.</span><span class="sxs-lookup"><span data-stu-id="68f2a-298">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="68f2a-299">La tarea se desencadena cuando el usuario inicia sesión en Windows.</span><span class="sxs-lookup"><span data-stu-id="68f2a-299">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="68f2a-300">La tarea registra de forma silenciosa el dispositivo en Azure AD con las credenciales de usuario después de realizar la autenticación mediante la autenticación integrada de Windows.</span><span class="sxs-lookup"><span data-stu-id="68f2a-300">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="68f2a-301">Para ver la tarea programada, en el dispositivo, vaya a **Microsoft** > **Workplace Join** y, después, vaya a la biblioteca del Programador de tareas.</span><span class="sxs-lookup"><span data-stu-id="68f2a-301">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="68f2a-302">Paso 5: Comprobación de los dispositivos registrados</span><span class="sxs-lookup"><span data-stu-id="68f2a-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="68f2a-303">Para comprobar los dispositivos registrados correctamente de una organización, utilice el cmdlet [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) en el [módulo de PowerShell de Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="68f2a-303">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="68f2a-304">La salida de este cmdlet muestra los dispositivos registrados en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f2a-304">The output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="68f2a-305">Para obtener todos los dispositivos, use el parámetro **-All** y, después, fíltrelos mediante la propiedad **deviceTrustType**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-305">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="68f2a-306">Los dispositivos unidos a un dominio tienen el valor **Unido a dominio**.</span><span class="sxs-lookup"><span data-stu-id="68f2a-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68f2a-307">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="68f2a-307">Next steps</span></span>

* <span data-ttu-id="68f2a-308">[Azure Active Directory automatic device registration FAQ](active-directory-device-registration-faq.md) (Preguntas más frecuentes acerca del registro automático de dispositivos)</span><span class="sxs-lookup"><span data-stu-id="68f2a-308">[Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span>
* <span data-ttu-id="68f2a-309">[Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md) (Solución de problemas de registro automático de equipos unidos a un dominio en Azure AD: Windows 10 y Windows Server 2016)</span><span class="sxs-lookup"><span data-stu-id="68f2a-309">[Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)</span></span>
* <span data-ttu-id="68f2a-310">[Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10](active-directory-device-registration-troubleshoot-windows-legacy.md) (Solución de problemas de registro automático de equipos unidos a un dominio en Azure AD: sin Windows 10)</span><span class="sxs-lookup"><span data-stu-id="68f2a-310">[Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10](active-directory-device-registration-troubleshoot-windows-legacy.md)</span></span>
* [<span data-ttu-id="68f2a-311">Acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68f2a-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
