---
title: "aaaAzure autenticación basada en certificados de Active Directory: Introducción | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure la autenticación basada en certificados en su entorno"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="9d546-103">Introducción a la autenticación basada en certificados de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d546-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="9d546-104">Autenticación basada en certificados le permite toobe autenticado por Azure Active Directory con un certificado de cliente en un dispositivo de Windows, Android o iOS cuando se conecte a su cuenta de Exchange online para:</span><span class="sxs-lookup"><span data-stu-id="9d546-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="9d546-105">aplicaciones móviles de Office como Microsoft Outlook y Microsoft Word,</span><span class="sxs-lookup"><span data-stu-id="9d546-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="9d546-106">clientes de Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="9d546-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="9d546-107">La configuración de esta característica elimina Hola necesidad tooenter un nombre de usuario y la combinación de contraseña en determinados correo electrónico y aplicaciones de Microsoft Office en su dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="9d546-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="9d546-108">En este tema:</span><span class="sxs-lookup"><span data-stu-id="9d546-108">This topic:</span></span>

- <span data-ttu-id="9d546-109">Proporciona hello tooconfigure los pasos y usar la autenticación basada en certificados para los usuarios de inquilinos de Office 365 Enterprise, Business, educación y planes de gobierno de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="9d546-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="9d546-110">Esta característica se encuentra disponible en versión preliminar en los planes Office 365 China, US Government Defense e US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="9d546-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="9d546-111">Se supone que ya tiene una [infraestructura de clave pública (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) y [AD FS](connect/active-directory-aadconnectfed-whatis.md) configurados.</span><span class="sxs-lookup"><span data-stu-id="9d546-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="9d546-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="9d546-112">Requirements</span></span>

<span data-ttu-id="9d546-113">autenticación basada en certificados tooconfigure, deben cumplirse Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9d546-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="9d546-114">La autenticación basada en certificados (CBA) solo se admite para entornos federados de aplicaciones del explorador o clientes nativos que usan autenticación moderna (ADAL).</span><span class="sxs-lookup"><span data-stu-id="9d546-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="9d546-115">Hola única excepción es Exchange Active Sync (EAS) para EXO que se puede usar para las cuentas de ambos, federadas y administradas.</span><span class="sxs-lookup"><span data-stu-id="9d546-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="9d546-116">entidad de certificación raíz de Hola y las entidades emisoras de certificados intermedios deben configurarse en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d546-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="9d546-117">Cada entidad de certificación debe tener una lista de revocación de certificados (CRL) a la que puede hacerse referencia a través de una dirección URL con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="9d546-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="9d546-118">Debe tener al menos una entidad de certificación configurada en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d546-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="9d546-119">Puede encontrar pasos relacionados en hello [configurar entidades emisoras de certificados de hello](#step-2-configure-the-certificate-authorities) sección.</span><span class="sxs-lookup"><span data-stu-id="9d546-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="9d546-120">Para los clientes de Exchange ActiveSync, certificado de cliente de hello debe tener enrutables correo electrónico Hola usuarios dirección de Exchange en línea en cualquier nombre de entidad de seguridad de Hola u Hola valor RFC822 nombre del campo de nombre alternativo del sujeto Hola.</span><span class="sxs-lookup"><span data-stu-id="9d546-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="9d546-121">Azure Active Directory asigna atributo Hola RFC822 value toohello dirección de Proxy en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d546-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="9d546-122">El dispositivo de cliente debe tener acceso tooat lo menos una emisora que emite certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="9d546-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="9d546-123">Un certificado de cliente para la autenticación de cliente se debe haber emitido a tooyour cliente.</span><span class="sxs-lookup"><span data-stu-id="9d546-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="9d546-124">Paso 1: Selección de la plataforma de dispositivos</span><span class="sxs-lookup"><span data-stu-id="9d546-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="9d546-125">Como primer paso, para la plataforma de dispositivo de Hola que le interesa, necesita tooreview Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="9d546-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="9d546-126">compatibilidad con aplicaciones móviles de Office de Hola</span><span class="sxs-lookup"><span data-stu-id="9d546-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="9d546-127">requisitos de implementación específica de Hola</span><span class="sxs-lookup"><span data-stu-id="9d546-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="9d546-128">Hola relacionados existe información para hello después de plataformas de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="9d546-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="9d546-129">Android</span><span class="sxs-lookup"><span data-stu-id="9d546-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="9d546-130">iOS</span><span class="sxs-lookup"><span data-stu-id="9d546-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="9d546-131">Paso 2: Configurar entidades emisoras de certificados de Hola</span><span class="sxs-lookup"><span data-stu-id="9d546-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="9d546-132">tooconfigure sus entidades emisoras de certificados en Active Directory de Azure, para cada entidad de certificación, cargar Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9d546-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="9d546-133">Hola parte pública del certificado de hello, en *.cer* formato</span><span class="sxs-lookup"><span data-stu-id="9d546-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="9d546-134">Hello orientado a las direcciones URL donde hello Internet listas de revocación de certificados (CRL) residen</span><span class="sxs-lookup"><span data-stu-id="9d546-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="9d546-135">esquema de Hola para una entidad de certificación tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="9d546-135">hello schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="9d546-136">Para la configuración de hello, puede usar hello [Azure Active Directory PowerShell versión 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="9d546-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="9d546-137">Inicie Windows PowerShell con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="9d546-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="9d546-138">Instale el módulo de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d546-138">Install hello Azure AD module.</span></span> <span data-ttu-id="9d546-139">Necesita tooinstall versión [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) o superior.</span><span class="sxs-lookup"><span data-stu-id="9d546-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="9d546-140">Como primer paso de configuración, deberá tooestablish una conexión con su inquilino.</span><span class="sxs-lookup"><span data-stu-id="9d546-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="9d546-141">Tan pronto como exista un inquilino de tooyour de conexión, puede revisar, agregar, eliminar y modificar las entidades emisoras de certificados de Hola de confianza que se definen en el directorio.</span><span class="sxs-lookup"><span data-stu-id="9d546-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="9d546-142">Conectar</span><span class="sxs-lookup"><span data-stu-id="9d546-142">Connect</span></span>

<span data-ttu-id="9d546-143">una conexión con su inquilino, use hello tooestablish [conectar organización](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9d546-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="9d546-144">Recuperar</span><span class="sxs-lookup"><span data-stu-id="9d546-144">Retrieve</span></span> 

<span data-ttu-id="9d546-145">tooretrieve Hola confianza entidades emisoras de certificados que se definen en el directorio, use hello [AzureADTrustedCertificateAuthority Get](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9d546-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="9d546-146">Sumar</span><span class="sxs-lookup"><span data-stu-id="9d546-146">Add</span></span>

<span data-ttu-id="9d546-147">toocreate una entidad de certificación de confianza, utilice hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet conjunto hello y **crlDistributionPoint** tooa correcta valor de atributo:</span><span class="sxs-lookup"><span data-stu-id="9d546-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="9d546-148">Remove</span><span class="sxs-lookup"><span data-stu-id="9d546-148">Remove</span></span>

<span data-ttu-id="9d546-149">tooremove una entidad de certificación de confianza, utilice hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9d546-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="9d546-150">Modificar</span><span class="sxs-lookup"><span data-stu-id="9d546-150">Modfiy</span></span>

<span data-ttu-id="9d546-151">toomodify una entidad de certificación de confianza, utilice hello [AzureADTrustedCertificateAuthority conjunto](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9d546-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="9d546-152">Paso 3: Configuración de revocación</span><span class="sxs-lookup"><span data-stu-id="9d546-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="9d546-153">toorevoke un certificado de cliente, Azure Active Directory captura los certificados de hello lista de revocación (CRL) de las direcciones URL de hello cargado como parte de la información de entidad emisora de certificados y lo almacena en caché.</span><span class="sxs-lookup"><span data-stu-id="9d546-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="9d546-154">Hola publicar última marca de tiempo (**fecha efectiva** propiedad) Hola CRL se utiliza tooensure Hola CRL sigue siendo válida.</span><span class="sxs-lookup"><span data-stu-id="9d546-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="9d546-155">Hola CRL es toocertificates de acceso de toorevoke periódicamente que se hace referencia que forman parte de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d546-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="9d546-156">Si es necesaria (por ejemplo, si un usuario pierde un dispositivo) una revocación más instantánea, se puede invalidar el token de autorización de saludo del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d546-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="9d546-157">tooinvalidate Hola autorización token, establezca Hola **StsRefreshTokenValidFrom** field para este usuario concreto con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d546-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="9d546-158">Debe actualizar hello **StsRefreshTokenValidFrom** field para cada usuario que desea acceso toorevoke para.</span><span class="sxs-lookup"><span data-stu-id="9d546-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="9d546-159">tooensure que persiste revocación hello, debe establecer hello **fecha efectiva** de fecha de hello CRL tooa después del valor de hello establecido por **StsRefreshTokenValidFrom** y asegúrese de hello certificado en cuestión está en Hola CRL.</span><span class="sxs-lookup"><span data-stu-id="9d546-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="9d546-160">Hola siguiendo pasos esquema Hola proceso de actualización e invalidación token de autorización de Hola por establecer hello **StsRefreshTokenValidFrom** campo.</span><span class="sxs-lookup"><span data-stu-id="9d546-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="9d546-161">**revocación de tooconfigure:**</span><span class="sxs-lookup"><span data-stu-id="9d546-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="9d546-162">Conectar con el servicio de administración de credenciales toohello MSOL:</span><span class="sxs-lookup"><span data-stu-id="9d546-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="9d546-163">Recuperar el valor de StsRefreshTokensValidFrom actual de Hola de un usuario:</span><span class="sxs-lookup"><span data-stu-id="9d546-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="9d546-164">Configurar un nuevo valor de StsRefreshTokensValidFrom de marca de tiempo actual de hello usuario toohello iguales:</span><span class="sxs-lookup"><span data-stu-id="9d546-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="9d546-165">fecha de Hello establecida debe estar en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="9d546-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="9d546-166">Si Hola fecha no tiene Hola futuras, Hola **StsRefreshTokensValidFrom** propiedad no está establecida.</span><span class="sxs-lookup"><span data-stu-id="9d546-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="9d546-167">Si es fecha Hola Hola futuras, **StsRefreshTokensValidFrom** se establecen toohello hora actual (no la fecha de hello indicada por el comando Set-MsolUser).</span><span class="sxs-lookup"><span data-stu-id="9d546-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="9d546-168">Paso 4: Prueba de la configuración</span><span class="sxs-lookup"><span data-stu-id="9d546-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="9d546-169">Prueba del certificado</span><span class="sxs-lookup"><span data-stu-id="9d546-169">Testing your certificate</span></span>

<span data-ttu-id="9d546-170">Como una primera prueba de configuración, debe intentar toosign en demasiado[Outlook Web Access](https://outlook.office365.com) o [SharePoint Online](https://microsoft.sharepoint.com) con su **explorador en el dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="9d546-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="9d546-171">Si el inicio de sesión se realiza correctamente, sabrá que:</span><span class="sxs-lookup"><span data-stu-id="9d546-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="9d546-172">certificado de usuario de Hello ha sido aprovisionado tooyour dispositivo de prueba</span><span class="sxs-lookup"><span data-stu-id="9d546-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="9d546-173">AD FS está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9d546-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="9d546-174">Prueba de aplicaciones móviles de Office</span><span class="sxs-lookup"><span data-stu-id="9d546-174">Testing Office mobile applications</span></span>

<span data-ttu-id="9d546-175">**autenticación basada en certificados tootest en la aplicación de Office mobile:**</span><span class="sxs-lookup"><span data-stu-id="9d546-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="9d546-176">En el dispositivo de prueba, instale una aplicación móvil de Office (por ejemplo, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="9d546-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="9d546-177">Inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9d546-177">Launch hello application.</span></span> 
4. <span data-ttu-id="9d546-178">Escriba su nombre de usuario y, a continuación, seleccione el certificado de usuario de Hola que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="9d546-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="9d546-179">Debe haber iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="9d546-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="9d546-180">Prueba de aplicaciones cliente de Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="9d546-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="9d546-181">tooaccess Exchange ActiveSync (EAS) mediante la autenticación basada en certificados, un perfil EAS que contiene el certificado de cliente de hello debe ser aplicación toohello disponible.</span><span class="sxs-lookup"><span data-stu-id="9d546-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="9d546-182">Hola perfil EAS debe contener Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="9d546-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="9d546-183">Hola toobe de certificado de usuario utilizado para la autenticación</span><span class="sxs-lookup"><span data-stu-id="9d546-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="9d546-184">punto de conexión EAS de Hello (por ejemplo, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="9d546-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="9d546-185">Un perfil de EAS se puede configurar y colocar en dispositivo hello mediante la utilización de Hola de administración de dispositivos móviles (MDM) como Intune o colocando manualmente el certificado de Hola Hola perfil EAS en dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="9d546-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="9d546-186">Prueba de aplicaciones cliente de EAS en Android</span><span class="sxs-lookup"><span data-stu-id="9d546-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="9d546-187">**autenticación de certificado de tootest:**</span><span class="sxs-lookup"><span data-stu-id="9d546-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="9d546-188">Configurar un perfil EAS en aplicación Hola que satisface los requisitos de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="9d546-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="9d546-189">Abra la aplicación hello y compruebe que está sincronizando el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="9d546-189">Open hello application, and verify that mail is synchronizing.</span></span> 

