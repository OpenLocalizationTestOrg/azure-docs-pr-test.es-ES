---
title: "aaaHow tooconfigure el registro automático de dispositivos Unidos a un dominio de Windows con Azure Active Directory | Documentos de Microsoft"
description: "Configurar los dispositivos de Windows Unidos a un dominio, tooregister automática y silenciosa con Azure Active Directory."
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
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="c4b1f-103">Cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4b1f-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="c4b1f-104">toouse [acceso condicional basado en dispositivos de Azure Active Directory](active-directory-conditional-access-azure-portal.md), los equipos deben registrarse con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c4b1f-105">Puede obtener una lista de dispositivos registrados en su organización mediante el uso de hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet Hola [módulo de Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="c4b1f-106">Este artículo proporciona pasos de Hola para configurar el registro automático de dispositivos Unidos a un dominio de Windows hello con Azure AD en su organización.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="c4b1f-107">Para más información acerca de:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-107">For more information about:</span></span>

- <span data-ttu-id="c4b1f-108">Acceso condicional, consulte [Acceso condicional en Azure Active Directory: versión preliminar](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="c4b1f-109">Dispositivos Windows 10 en un área de trabajo de Hola y experiencias de hello mejorado cuando se registra con Azure AD, consulte [Windows 10 para empresa hello: usar dispositivos para el trabajo](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="c4b1f-110">Windows 10 Enterprise E3 en CSP, vea hello [Windows 10 Enterprise E3 en información general de CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="c4b1f-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="c4b1f-111">Before you begin</span></span>

<span data-ttu-id="c4b1f-112">Antes de empezar a configurar el registro automático de dispositivos Unidos a un dominio de Windows hello en su entorno, debe familiarizarse con las restricciones de Hola y escenarios de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="c4b1f-113">mejorar la legibilidad tooimprove Hola de descripciones de hello, en este tema se utiliza Hola después término:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="c4b1f-114">**Dispositivos de Windows actuales** -este término hace referencia a los dispositivos Unidos a un toodomain ejecutan Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="c4b1f-115">**Dispositivos de bajo nivel de Windows** -este término hace referencia tooall **admite** dispositivos Windows Unidos a un dominio que se está ejecutando Windows 10 ni Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="c4b1f-116">Dispositivos de Windows actuales</span><span class="sxs-lookup"><span data-stu-id="c4b1f-116">Windows current devices</span></span>

- <span data-ttu-id="c4b1f-117">Para dispositivos que ejecutan el sistema operativo de escritorio de Windows de hello, se recomienda usar la actualización de aniversario de Windows 10 (versión 1607) o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="c4b1f-118">Hola registro de dispositivos de Windows actuales **es** admite en entornos de no federadas, como las configuraciones de sincronización de hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="c4b1f-119">Dispositivos de Windows de nivel inferior</span><span class="sxs-lookup"><span data-stu-id="c4b1f-119">Windows down-level devices</span></span>

- <span data-ttu-id="c4b1f-120">se admite Hola después de dispositivos de bajo nivel de Windows:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="c4b1f-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c4b1f-121">Windows 8.1</span></span>
    - <span data-ttu-id="c4b1f-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c4b1f-122">Windows 7</span></span>
    - <span data-ttu-id="c4b1f-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c4b1f-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="c4b1f-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c4b1f-124">Windows Server 2012</span></span>
    - <span data-ttu-id="c4b1f-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c4b1f-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="c4b1f-126">Hola registro de dispositivos de Windows inferiores **es** admite en entornos de no federadas a través de perfecta Single Sign On [Azure Active Directory sin problemas Single Sign-On](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="c4b1f-127">Hola registro de dispositivos de Windows inferiores **no es** compatible con dispositivos con perfiles móviles.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="c4b1f-128">Si confía en la itinerancia de la configuración o de los perfiles, use Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="c4b1f-129">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c4b1f-129">Prerequisites</span></span>

<span data-ttu-id="c4b1f-130">Antes de empezar a habilitar el registro automático de Hola de dispositivos Unidos a un dominio de su organización, deberá toomake seguro de que está ejecutando una versión actualizada de Azure AD conectarse.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="c4b1f-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-131">Azure AD Connect:</span></span>

- <span data-ttu-id="c4b1f-132">Mantiene la asociación de hello entre la cuenta de equipo de hello en el local de Active Directory (AD) y el objeto de dispositivo de hello en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="c4b1f-133">Habilita otras características relacionadas del dispositivo como Windows Hello para empresas.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="c4b1f-134">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="c4b1f-134">Configuration steps</span></span>

<span data-ttu-id="c4b1f-135">Este tema incluye los pasos de hello necesaria para todos los escenarios de configuración típica.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="c4b1f-136">Usar hello después de la tabla tooget una visión general de los pasos de Hola que son necesarios para su escenario:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="c4b1f-137">Pasos</span><span class="sxs-lookup"><span data-stu-id="c4b1f-137">Steps</span></span>                                      | <span data-ttu-id="c4b1f-138">Dispositivos actuales de Windows y sincronización de hash de contraseña</span><span class="sxs-lookup"><span data-stu-id="c4b1f-138">Windows current and password hash sync</span></span> | <span data-ttu-id="c4b1f-139">Dispositivos actuales de Windows y federación</span><span class="sxs-lookup"><span data-stu-id="c4b1f-139">Windows current and federation</span></span> | <span data-ttu-id="c4b1f-140">Dispositivos de Windows de nivel inferior</span><span class="sxs-lookup"><span data-stu-id="c4b1f-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="c4b1f-141">Paso 1: Configuración del punto de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="c4b1f-141">Step 1: Configure service connection point</span></span> | ![Comprobar][1]                            | ![Comprobar][1]                    | ![Comprobar][1]        |
| <span data-ttu-id="c4b1f-145">Paso 2: Configuración de la emisión de notificaciones</span><span class="sxs-lookup"><span data-stu-id="c4b1f-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Comprobar][1]                    | ![Comprobar][1]        |
| <span data-ttu-id="c4b1f-148">Paso 3: Habilitación de dispositivos que no tengan Windows 10</span><span class="sxs-lookup"><span data-stu-id="c4b1f-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Comprobar][1]        |
| <span data-ttu-id="c4b1f-150">Paso 4: Control de implementación y lanzamiento</span><span class="sxs-lookup"><span data-stu-id="c4b1f-150">Step 4: Control deployment and rollout</span></span>     | ![Comprobar][1]                            | ![Comprobar][1]                    | ![Comprobar][1]        |
| <span data-ttu-id="c4b1f-154">Paso 5: Comprobación de los dispositivos registrados</span><span class="sxs-lookup"><span data-stu-id="c4b1f-154">Step 5: Verify registered devices</span></span>          | ![Comprobar][1]                            | ![Comprobar][1]                    | ![Comprobar][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="c4b1f-158">Paso 1: Configurar el punto de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="c4b1f-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="c4b1f-159">objeto de punto de conexión de servicio de Hola se usa por sus dispositivos durante el registro de hello toodiscover información del inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="c4b1f-160">En el local Active Directory (AD), objeto SCP de hello para el registro automático de Hola de dispositivos Unidos a un dominio debe existir en hello nomenclatura contexto partición de configuración bosque del equipo de hello.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="c4b1f-161">Hay solo un contexto de nomenclatura de configuración por bosque.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="c4b1f-162">En una configuración de Active Directory de bosques múltiples, el punto de conexión de servicio de hello debe existir en todos los bosques que contienen equipos unidos a un dominio.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="c4b1f-163">Puede usar hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve Hola configuración contexto de nomenclatura de su bosque.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="c4b1f-164">Para un bosque con el nombre de dominio de Active Directory de hello *fabrikam.com*, contexto de nomenclatura de configuración de hello es:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="c4b1f-165">En el bosque, objeto de hello SCP para hello el registro automático de dispositivos Unidos a un dominio se encuentra en:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="c4b1f-166">Según cómo ha implementado Azure AD Connect, objeto SCP de hello puede que ya se configuraron.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="c4b1f-167">Puede comprobar la existencia de hello del objeto de Hola y recuperar los valores de detección de hello mediante Hola siguiente secuencia de comandos de Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="c4b1f-168">Hola **$scp. Palabras clave** salida muestra información del inquilino hello Azure AD, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="c4b1f-169">Si no existe el punto de conexión de servicio de hello, puede crear mediante la ejecución de hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet en el servidor de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="c4b1f-170">Credenciales de administrador de empresa es necesario toorun este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="c4b1f-171">Hola cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-171">hello cmdlet:</span></span>

- <span data-ttu-id="c4b1f-172">Crea el punto de conexión de servicio de hello en el bosque de Active Directory de hello A que Azure AD Connect está conectado.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="c4b1f-173">Requiere toospecify hello `AdConnectorAccount` parámetro.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="c4b1f-174">Esta es la cuenta de hello que está configurada como cuenta de conector de Azure AD conectarse de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="c4b1f-175">Hello secuencia de comandos siguiente muestra un ejemplo para usar el cmdlet de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="c4b1f-176">En esta secuencia de comandos, `$aadAdminCred = Get-Credential` requiere tootype un nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="c4b1f-177">Necesita el nombre de usuario de hello tooprovide en formato de nombre principal (UPN) del usuario de hello (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="c4b1f-178">Hola `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="c4b1f-179">Usa el módulo de Active Directory PowerShell hello, que se basa en los servicios Web de Active Directory ejecutándose en un controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="c4b1f-180">Active Directory Web Services es compatible con los controladores de dominio en los que se ejecuta Windows Server 2008 R2, y las versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="c4b1f-181">Solo es compatible con hello **MSOnline PowerShell versión del módulo 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="c4b1f-182">toodownload este módulo, utilícelo [vínculo](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="c4b1f-183">Controladores de dominio ejecutan Windows Server 2008 o versiones anteriores, usar script de Hola por debajo del punto de conexión de servicio de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="c4b1f-184">En una configuración de varios bosques, debe usar Hola después de la secuencia de comandos toocreate Hola service connection point en cada bosque donde existen equipos:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="c4b1f-185">Paso 2: Configuración de la emisión de notificaciones</span><span class="sxs-lookup"><span data-stu-id="c4b1f-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="c4b1f-186">De Azure federado utilizan los dispositivos de la configuración de AD, en los servicios de federación de Active Directory (AD FS) o una entidad 3rd tooAzure de tooauthenticate de servicio de federación AD local.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="c4b1f-187">Los dispositivos autentican tooget un tooregister de token de acceso con hello Azure Active Directory Device Registration Service (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="c4b1f-188">Dispositivos actuales autentican mediante autenticación de Windows integrada tooan WS-Trust extremo activo (versiones 1.3 o 2005) hospedada por el servicio de federación de hello local de Windows.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="c4b1f-189">Si se usa AD FS, es preciso habilitar **adfs/services/trust/13/windowstransport** o **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="c4b1f-190">Si usas hello Web autenticación Proxy, asegurarse de que este extremo se publica a través de proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="c4b1f-191">Puede ver qué extremos están habilitadas a través de la consola de administración de AD FS de hello en **servicio > extremos**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="c4b1f-192">Si no dispone de AD FS como el servicio de federación local, siga las instrucciones de Hola de su toomake de proveedores que admiten WS-Trust 1.3 o extremos de 2005 y que se publican a través de hello archivo de intercambio de metadatos (MEX).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="c4b1f-193">Hello deben existir siguientes notificaciones en el símbolo (token) de hello recibido por Azure DRS para toocomplete de registro de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="c4b1f-194">DRS Azure creará un objeto de dispositivo en Azure AD con parte de esta información que se usa por objeto de dispositivo de Azure AD Connect tooassociate Hola recién creado con hello equipo cuenta local.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="c4b1f-195">Si tiene más de un nombre de dominio comprobado, debe hello tooprovide después de la notificación para equipos:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="c4b1f-196">Si ya esté emitiendo una notificación de ImmutableID (p. ej., Id. de inicio de sesión alternativo) debe tooprovide una notificación correspondiente para los equipos:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="c4b1f-197">En las secciones siguientes de hello, encontrará información sobre:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="c4b1f-198">valores de Hello deben tener todas las notificaciones</span><span class="sxs-lookup"><span data-stu-id="c4b1f-198">hello values each claim should have</span></span>
- <span data-ttu-id="c4b1f-199">El aspecto de una definición en AD FS</span><span class="sxs-lookup"><span data-stu-id="c4b1f-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="c4b1f-200">definición de Hello ayuda a tooverify si los valores de hello están presentes, o si necesita toocreate ellos.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="c4b1f-201">Si no utiliza AD FS para el servidor de federación local, siga tooissue configuración adecuada de su proveedor instrucciones toocreate Hola estas notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="c4b1f-202">Emisión de notificación de tipo de cuenta</span><span class="sxs-lookup"><span data-stu-id="c4b1f-202">Issue account type claim</span></span>

<span data-ttu-id="c4b1f-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Esta notificación debe contener un valor de **DJ**, que identifica el dispositivo de Hola como un equipo unido al dominio.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="c4b1f-204">En AD FS, puede agregar una regla de transformación de emisión como esta:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="c4b1f-205">Emitir objectGUID de hello equipo cuenta local</span><span class="sxs-lookup"><span data-stu-id="c4b1f-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="c4b1f-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Esta notificación debe contener hello **objectGUID** valor de hello cuenta de equipo local.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="c4b1f-207">En AD FS, puede agregar una regla de transformación de emisión como esta:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="c4b1f-208">Emitir objectSID de hello equipo cuenta local</span><span class="sxs-lookup"><span data-stu-id="c4b1f-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="c4b1f-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Esta notificación debe contener Hola Hola **objectSid** valor de hello cuenta de equipo local.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="c4b1f-210">En AD FS, puede agregar una regla de transformación de emisión como esta:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="c4b1f-211">Emisión de issuerID para un equipo cuando haty varios nombres de dominio comprobados en Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4b1f-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="c4b1f-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Esta notificación debe contener Hola identificador uniforme de recursos (URI) de cualquiera de hello comprobar nombres de dominio que se conectan con hello federation service (AD FS o 3ª parte) emisora Hola símbolo (token) local.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="c4b1f-213">En AD FS, puede agregar reglas de transformación que parecen los Hola siguiente en ese orden específico después Hola los anteriores.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="c4b1f-214">Tenga en cuenta que una regla tooexplicitly problema Hola regla para los usuarios es necesario.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="c4b1f-215">En reglas de Hola a continuación, se agrega una regla primera identificación de usuario frente a la autenticación del equipo.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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


<span data-ttu-id="c4b1f-216">En la notificación de hello anterior,</span><span class="sxs-lookup"><span data-stu-id="c4b1f-216">In hello claim above,</span></span>

- <span data-ttu-id="c4b1f-217">`$<domain>`es la dirección URL del servicio de hello AD FS</span><span class="sxs-lookup"><span data-stu-id="c4b1f-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="c4b1f-218">`<verified-domain-name>`es un marcador de posición que necesita tooreplace con uno de los nombres de dominio comprobado en Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4b1f-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="c4b1f-219">Para obtener más información acerca de los nombres de dominio comprobado, consulte [agregar un tooAzure de nombre de dominio personalizado Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="c4b1f-220">tooget una lista de los dominios de la compañía comprobados, puede usar hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="c4b1f-222">Emisión de ImmutableID para un equipo cuando existe uno para los usuarios (por ejemplo, se ha establecido el identificador de inicio de sesión alternativo)</span><span class="sxs-lookup"><span data-stu-id="c4b1f-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="c4b1f-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**: esta notificación debe contener un valor válido para los equipos.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="c4b1f-224">En AD FS, se puede crear una regla de transformación de emisión como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="c4b1f-225">Aplicación auxiliar script toocreate Hola AD FS reglas de transformación</span><span class="sxs-lookup"><span data-stu-id="c4b1f-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="c4b1f-226">Hello siguiente secuencia de comandos le ayuda con la creación de hello de emisión de hello transformar las reglas descritas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="c4b1f-227">Comentarios</span><span class="sxs-lookup"><span data-stu-id="c4b1f-227">Remarks</span></span> 

- <span data-ttu-id="c4b1f-228">Este script anexa reglas existentes de hello reglas toohello.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="c4b1f-229">Script de Hola no se ejecutan dos veces porque Hola un conjunto de reglas se debe agregar dos veces.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="c4b1f-230">Asegúrese de que no existe ninguna regla correspondiente de estas notificaciones (condiciones Hola correspondiente) antes de ejecutar script de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="c4b1f-231">Si tiene varios nombres de dominio verificado (como se muestra en el portal de hello Azure AD o a través del cmdlet Get-MsolDomains Hola), establecer valor de Hola de **$multipleVerifiedDomainNames** Hola script demasiado**$true**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="c4b1f-232">Además, asegúrese de que quita cualquier notificación issuerid existente que pueda haber creado Azure AD Connect o a través de otros medios.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="c4b1f-233">Este es un ejemplo de esta regla:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="c4b1f-234">Si ya ha emitido una **ImmutableID** de notificación para las cuentas de usuario, establezca el valor de Hola de **$immutableIDAlreadyIssuedforUsers** Hola script demasiado**$true**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="c4b1f-235">Paso 3: Habilitación de dispositivos de Windows de nivel inferior</span><span class="sxs-lookup"><span data-stu-id="c4b1f-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="c4b1f-236">Si algunos de los dispositivos unidos a un dominio son dispositivos de Windows de nivel inferior, necesitará:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="c4b1f-237">Establecer una directiva de Azure AD tooenable tooregister dispositivos de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="c4b1f-238">Configurar el toosupport de notificaciones local tooissue de servicio de federación **autenticación de Windows integrada (IWA)** para el registro de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="c4b1f-239">Agregue hello Azure AD dispositivo autenticación extremo toohello local Intranet zonas tooavoid certificado pide al autenticar el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="c4b1f-240">Establezca la directiva en Azure AD tooenable dispositivos de los usuarios tooregister</span><span class="sxs-lookup"><span data-stu-id="c4b1f-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="c4b1f-241">dispositivos de nivel inferior de tooregister Windows, debe toomake que ese Hola establecer a tooallow usuarios tooregister dispositivos en Azure AD esté establecido.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="c4b1f-242">Hola portal de Azure, puede encontrar esta configuración en:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="c4b1f-243">Hello siguiente directiva debe establecerse demasiado**todos los**: **los usuarios pueden registrar sus dispositivos con Azure AD**</span><span class="sxs-lookup"><span data-stu-id="c4b1f-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Registro de dispositivos](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="c4b1f-245">Configuración de un servicio de federación local</span><span class="sxs-lookup"><span data-stu-id="c4b1f-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="c4b1f-246">El servicio de federación local debe ser compatible con hello emisora **authenticationmehod** y **wiaormultiauthn** notificaciones al recibir una autenticación solicitud de usuario de confianza de Azure AD toohello que contiene un resouce_params parámetro con un valor codificado como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="c4b1f-247">Cuando llega una solicitud de este tipo, servicio de federación local Hola debe autenticar usuario hello mediante la autenticación integrada de Windows y cuando se realiza correctamente, debe emitir Hola siguiendo dos notificaciones:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="c4b1f-248">En AD FS, debe agregar ese método de autenticación de hello pasa a través de una regla de transformación de emisión.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="c4b1f-249">**tooadd esta regla:**</span><span class="sxs-lookup"><span data-stu-id="c4b1f-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="c4b1f-250">En la consola de administración de hello AD FS, vaya demasiado`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="c4b1f-251">Haga clic en hello plataforma de identidad de Microsoft Office 365 confianza para usuario autenticado y, a continuación, seleccione **editar reglas de notificación**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="c4b1f-252">En hello **reglas de transformación de emisión** ficha, seleccione **Agregar regla**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="c4b1f-253">Hola **regla de notificación** lista de plantillas, seleccione **enviar notificaciones mediante una regla personalizada**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="c4b1f-254">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-254">Select **Next**.</span></span>
6. <span data-ttu-id="c4b1f-255">Hola **nombre de la regla de notificación** , escriba **Auth Method Claim Rule**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="c4b1f-256">Hola **regla de notificación** cuadro, Hola de tipo siguiente regla:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="c4b1f-257">En el servidor de federación, escriba el comando de PowerShell de Hola a continuación después de reemplazar ** \<RPObjectName\> ** con nombre de objeto de usuario autenticado de Hola para su Azure AD confianza para usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="c4b1f-258">Normalmente, este objeto se llama **Plataforma de identidad de Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="c4b1f-259">Agregar zonas de Intranet Local de hello Azure AD dispositivo autenticación extremo toohello</span><span class="sxs-lookup"><span data-stu-id="c4b1f-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="c4b1f-260">certificado tooavoid pide al autentican a los usuarios de dispositivos de registro tooAzure AD puede insertar un hello tooadd de directiva tooyour dispositivos Unidos a un dominio después de la zona de Intranet Local toohello de dirección URL en Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="c4b1f-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="c4b1f-261">Paso 4: Control de implementación y lanzamiento</span><span class="sxs-lookup"><span data-stu-id="c4b1f-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="c4b1f-262">Cuando se hayan completado los pasos necesario de hello, los dispositivos Unidos a un dominio son register tooautomatically listo con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="c4b1f-263">Todos los dispositivos unidos a un dominio en que se ejecuten la Actualización de aniversario de Windows 10 y Windows Server 2016 se registran automáticamente en Azure AD cuando el dispositivo se reinicie o el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="c4b1f-264">Registran nuevos dispositivos con Azure AD al dispositivo de hello reinicia una vez completada la operación de unión de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="c4b1f-265">Dispositivos que estaban previamente unido al área de trabajo tooAzure AD (por ejemplo, para Intune) transición demasiado"*Unidos a un dominio, registrado en AAD*"; sin embargo tarda algún tiempo para este proceso toocomplete en todos los dispositivos pendientes toohello normal flujo de actividad de usuario y dominio.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="c4b1f-266">Comentarios</span><span class="sxs-lookup"><span data-stu-id="c4b1f-266">Remarks</span></span>

- <span data-ttu-id="c4b1f-267">Puede usar una implementación de Hola de toocontrol de objeto de directiva de grupo de registro automático de Windows 10 y equipos unidos a un dominio de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="c4b1f-268">Windows 10 de noviembre de 2015 actualización automáticamente registros con Azure AD **sólo** si se establece el objeto de directiva de grupo de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="c4b1f-269">toorollout Hola el registro automático de los equipos de nivel inferior de Windows, puede implementar un [paquete de Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers que seleccione.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="c4b1f-270">Si se insertan Hola directiva de grupo objeto tooWindows 8.1 dispositivos Unidos a dominio, se volverá a intentar el registro; Sin embargo, se recomienda que utilice hello [paquete de Windows Installer](#windows-installer-packages-for-non-windows-10-computers) tooregister todos los dispositivos de bajo nivel de Windows.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="c4b1f-271">Creación de un objeto de directiva de grupo</span><span class="sxs-lookup"><span data-stu-id="c4b1f-271">Create a Group Policy object</span></span> 

<span data-ttu-id="c4b1f-272">implementación de hello toocontrol de inscripción automática de equipos actuales de Windows, debe implementar hello **registrar equipos unidos a un dominio como dispositivos** dispositivos de toohello de objeto de directiva de grupo que desee tooregister.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="c4b1f-273">Por ejemplo, puede implementar el grupo de seguridad de tooa o unidad organizativa de hello directiva tooan.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="c4b1f-274">**Directiva de Hola tooset:**</span><span class="sxs-lookup"><span data-stu-id="c4b1f-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="c4b1f-275">Abra **el administrador del servidor**y, a continuación, vaya demasiado`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="c4b1f-276">Vaya toohello nodo del dominio que se corresponde el dominio toohello donde desea que el registro automático de tooactivate de equipos de Windows actuales.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="c4b1f-277">Haga clic con el botón derecho en **Objetos de directiva de grupo** y seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="c4b1f-278">Escriba un nombre para el objeto de directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="c4b1f-279">Por ejemplo, *tooAzure el registro automático AD*.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="c4b1f-280">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-280">Select **OK**.</span></span>
5. <span data-ttu-id="c4b1f-281">Haga clic con el botón derecho en el nuevo objeto de directiva de grupo y seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="c4b1f-282">Vaya demasiado**configuración del equipo** > **directivas** > **plantillas administrativas** > **Windows Componentes** > **el registro de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="c4b1f-283">Haga clic con el botón derecho en **Registrar los equipos asociados a un dominio como dispositivos** y seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c4b1f-284">Esta plantilla de directiva de grupo se ha cambiado desde las versiones anteriores de la consola de administración de directivas de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="c4b1f-285">Si está utilizando una versión anterior de la consola de hello, vaya demasiado`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="c4b1f-286">Seleccione **Habilitado** y luego **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="c4b1f-287">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-287">Select **OK**.</span></span>
9. <span data-ttu-id="c4b1f-288">Hola de vínculo tooa ubicación de objeto de directiva de grupo de su elección.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="c4b1f-289">Por ejemplo, puede vincular tooa determinada unidad organizativa.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="c4b1f-290">También puede vincularlo tooa el grupo de seguridad específico de equipos que se registren automáticamente con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="c4b1f-291">tooset esta directiva para todos los equipos de Windows 10 y Windows Server 2016 Unidos a un dominio de su organización, dominio de toohello de objeto de directiva de grupo de Hola de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="c4b1f-292">Paquetes de Windows Installer para equipos sin Windows 10</span><span class="sxs-lookup"><span data-stu-id="c4b1f-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="c4b1f-293">equipos unidos a un dominio de nivel inferior de Windows de tooregister en un entorno federado, puede descargar e instalar estos paquetes de Windows Installer (.msi) desde el centro de descarga en hello [área de trabajo de Microsoft para equipos que no sean Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554) página.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="c4b1f-294">Puede implementar el paquete de hello mediante el uso de un sistema de distribución de software como System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="c4b1f-295">paquete Hello admite opciones de instalación silenciosa estándar Hola con hello *silencioso* parámetro.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="c4b1f-296">Rama actual de System Center Configuration Manager ofrece ventajas adicionales de versiones anteriores, como registros de hello capacidad tootrack completado.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="c4b1f-297">Para más información, consulte [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="c4b1f-298">instalador de Hello crea una tarea programada en sistema de Hola que se ejecuta en el contexto del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="c4b1f-299">tarea Hello se desencadena cuando Hola usuario inicia sesión en tooWindows.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="c4b1f-300">tarea Hello registra automáticamente el dispositivo de hello con Azure AD con credenciales de usuario de hello tras la autenticación mediante la autenticación integrada de Windows.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="c4b1f-301">toosee tarea programada de hello, en el dispositivo de hello, vaya demasiado**Microsoft** > **unión**, y, a continuación, vaya biblioteca del programador de tareas de toohello.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="c4b1f-302">Paso 5: Comprobación de los dispositivos registrados</span><span class="sxs-lookup"><span data-stu-id="c4b1f-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="c4b1f-303">Puede comprobar los dispositivos registrados correctamente en su organización mediante hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet Hola [módulo de Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="c4b1f-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="c4b1f-304">salida de Hello de este cmdlet muestra dispositivos registrados en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="c4b1f-305">tooget todos los dispositivos, use hello **-todos los** parámetro y, a continuación, filtrar mediante hello **deviceTrustType** propiedad.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="c4b1f-306">Los dispositivos unidos a un dominio tienen el valor **Unido a dominio**.</span><span class="sxs-lookup"><span data-stu-id="c4b1f-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4b1f-307">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4b1f-307">Next steps</span></span>

* <span data-ttu-id="c4b1f-308">[Azure Active Directory automatic device registration FAQ](active-directory-device-registration-faq.md) (Preguntas más frecuentes acerca del registro automático de dispositivos)</span><span class="sxs-lookup"><span data-stu-id="c4b1f-308">[Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span>
* [<span data-ttu-id="c4b1f-309">Solución de problemas de registro automático de dominio unido equipos tooAzure AD – Windows 10 y Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c4b1f-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="c4b1f-310">Solución de problemas de registro automático de dominio unido equipos tooAzure AD – distinta de Windows 10</span><span class="sxs-lookup"><span data-stu-id="c4b1f-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="c4b1f-311">Acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4b1f-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
