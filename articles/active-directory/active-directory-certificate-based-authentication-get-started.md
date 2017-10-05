---
title: "Autenticación basada en certificados de Azure Active Directory - Introducción | Microsoft Docs"
description: "Obtenga información sobre cómo configurar la autenticación basada en certificados en su entorno"
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
ms.openlocfilehash: 8ebc6f2dd7502fd75ffdd4d5d68338382cb1a46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="8ebe0-103">Introducción a la autenticación basada en certificados de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ebe0-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="8ebe0-104">La autenticación basada en certificados le permite autenticarse mediante Azure Active Directory con un certificado de cliente en un dispositivo Windows, Android o iOS al conectar su cuenta de Exchange Online a:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="8ebe0-105">aplicaciones móviles de Office como Microsoft Outlook y Microsoft Word,</span><span class="sxs-lookup"><span data-stu-id="8ebe0-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="8ebe0-106">clientes de Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="8ebe0-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="8ebe0-107">Al configurar esta función, no tendrá que escribir una combinación de nombre de usuario y contraseña en determinadas aplicaciones de correo electrónico y Microsoft Office de su dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="8ebe0-108">En este tema:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-108">This topic:</span></span>

- <span data-ttu-id="8ebe0-109">Se indican los pasos para configurar y utilizar la autenticación basada en certificados para usuarios de los inquilinos de los planes de Office 365 Enterprise, Empresa, Educación e US Government.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="8ebe0-110">Esta característica se encuentra disponible en versión preliminar en los planes Office 365 China, US Government Defense e US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="8ebe0-111">Se supone que ya tiene una [infraestructura de clave pública (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) y [AD FS](connect/active-directory-aadconnectfed-whatis.md) configurados.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="8ebe0-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="8ebe0-112">Requirements</span></span>

<span data-ttu-id="8ebe0-113">Para configurar la autenticación basada en certificados, deben cumplirse las siguientes condiciones:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-113">To configure certificate-based authentication, the following must be true:</span></span>  

- <span data-ttu-id="8ebe0-114">La autenticación basada en certificados (CBA) solo se admite para entornos federados de aplicaciones del explorador o clientes nativos que usan autenticación moderna (ADAL).</span><span class="sxs-lookup"><span data-stu-id="8ebe0-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="8ebe0-115">La excepción es Exchange Active Sync (EAS) para EXO, que se puede usar tanto para cuentas federadas como para cuentas administradas.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-115">The one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="8ebe0-116">La entidad de certificación raíz y las intermedias deben configurarse en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-116">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="8ebe0-117">Cada entidad de certificación debe tener una lista de revocación de certificados (CRL) a la que puede hacerse referencia a través de una dirección URL con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="8ebe0-118">Debe tener al menos una entidad de certificación configurada en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="8ebe0-119">Puede encontrar pasos relacionados en la sección [Configuración de las entidades de certificación](#step-2-configure-the-certificate-authorities).</span><span class="sxs-lookup"><span data-stu-id="8ebe0-119">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="8ebe0-120">En Exchange Online, el certificado de cliente debe tener la dirección de correo electrónico enrutable del usuario en el valor de Nombre de la entidad de seguridad o Nombre RFC822 del campo Nombre alternativo del titular (para clientes de Exchange ActiveSync).</span><span class="sxs-lookup"><span data-stu-id="8ebe0-120">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span></span> <span data-ttu-id="8ebe0-121">Azure Active Directory asigna el valor de RFC822 al atributo de dirección de Proxy del directorio.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-121">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span></span>  

- <span data-ttu-id="8ebe0-122">El dispositivo cliente debe tener acceso al menos a una entidad de certificación que emite los certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-122">Your client device must have access to at least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="8ebe0-123">Se debe haber emitido al cliente un certificado de cliente para la autenticación de cliente.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-123">A client certificate for client authentication must have been issued to your client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="8ebe0-124">Paso 1: Selección de la plataforma de dispositivos</span><span class="sxs-lookup"><span data-stu-id="8ebe0-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="8ebe0-125">Como primer paso, en la plataforma de dispositivos que le interesa, debe revisar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-125">As a first step, for the device platform you care about, you need to review the following:</span></span>

- <span data-ttu-id="8ebe0-126">Compatibilidad con aplicaciones móviles de Office</span><span class="sxs-lookup"><span data-stu-id="8ebe0-126">The Office mobile applications support</span></span> 
- <span data-ttu-id="8ebe0-127">Requisitos de implementación específicos</span><span class="sxs-lookup"><span data-stu-id="8ebe0-127">The specific implementation requirements</span></span>  

<span data-ttu-id="8ebe0-128">Existe información relacionada para las siguientes plataformas de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-128">The related information exists for the following device platforms:</span></span>

- [<span data-ttu-id="8ebe0-129">Android</span><span class="sxs-lookup"><span data-stu-id="8ebe0-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="8ebe0-130">iOS</span><span class="sxs-lookup"><span data-stu-id="8ebe0-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-the-certificate-authorities"></a><span data-ttu-id="8ebe0-131">Paso 2: Configuración de las entidades de certificación</span><span class="sxs-lookup"><span data-stu-id="8ebe0-131">Step 2: Configure the certificate authorities</span></span> 

<span data-ttu-id="8ebe0-132">Para configurar las entidades de certificación en Azure Active Directory, para cada entidad de certificación, cargue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-132">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span></span> 

* <span data-ttu-id="8ebe0-133">La parte pública del certificado en formato *.cer* .</span><span class="sxs-lookup"><span data-stu-id="8ebe0-133">The public portion of the certificate, in *.cer* format</span></span> 
* <span data-ttu-id="8ebe0-134">Las direcciones URL con conexión a Internet en las que se encuentran las listas de revocación de certificados (CRL).</span><span class="sxs-lookup"><span data-stu-id="8ebe0-134">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="8ebe0-135">A continuación se presenta el esquema para una entidad de certificación:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-135">The schema for a certificate authority looks as follows:</span></span> 

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

<span data-ttu-id="8ebe0-136">Para la configuración, puede usar la [versión 2 de Azure Active Directory PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="8ebe0-136">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="8ebe0-137">Inicie Windows PowerShell con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="8ebe0-138">Instale el módulo de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-138">Install the Azure AD module.</span></span> <span data-ttu-id="8ebe0-139">Es preciso instalar la versión [2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33), o una superior.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-139">You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="8ebe0-140">El primer paso de configuración consiste en establecer una conexión con el inquilino.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-140">As a first configuration step, you need to establish a connection with your tenant.</span></span> <span data-ttu-id="8ebe0-141">En cuanto se establece la conexión con el inquilino, puede revisar, agregar, eliminar y modificar las entidades de certificación de confianza definidas en el directorio.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-141">As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="8ebe0-142">Conectar</span><span class="sxs-lookup"><span data-stu-id="8ebe0-142">Connect</span></span>

<span data-ttu-id="8ebe0-143">Para establecer una conexión con el inquilino, use el cmdlet [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="8ebe0-143">To establish a connection with your tenant, use the [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="8ebe0-144">Recuperar</span><span class="sxs-lookup"><span data-stu-id="8ebe0-144">Retrieve</span></span> 

<span data-ttu-id="8ebe0-145">Para recuperar las entidades de certificación de confianza definidas en el directorio, use el cmdlet [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="8ebe0-145">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="8ebe0-146">Sumar</span><span class="sxs-lookup"><span data-stu-id="8ebe0-146">Add</span></span>

<span data-ttu-id="8ebe0-147">Para crear una entidad de certificación de confianza, use el cmdlet [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) y establezca el atributo **crlDistributionPoint** en un valor correcto:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-147">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set the **crlDistributionPoint** attribute to a correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="8ebe0-148">Remove</span><span class="sxs-lookup"><span data-stu-id="8ebe0-148">Remove</span></span>

<span data-ttu-id="8ebe0-149">Para quitar una entidad de certificación de confianza, use el cmdlet [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="8ebe0-149">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="8ebe0-150">Modificar</span><span class="sxs-lookup"><span data-stu-id="8ebe0-150">Modfiy</span></span>

<span data-ttu-id="8ebe0-151">Para modificar una entidad de certificación de confianza, use el cmdlet [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="8ebe0-151">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="8ebe0-152">Paso 3: Configuración de revocación</span><span class="sxs-lookup"><span data-stu-id="8ebe0-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="8ebe0-153">Para revocar un certificado de cliente, Azure Active Directory recupera la lista de revocación de certificados (CRL) de las direcciones URL cargadas como parte de la información de la entidad de certificación y la almacena en caché.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-153">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="8ebe0-154">La última marca de tiempo de publicación (propiedad**Effective Date** ) de la CRL se utiliza para garantizar que esta es aún es válida.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-154">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span></span> <span data-ttu-id="8ebe0-155">De forma periódica, se hace referencia a la CRL para revocar el acceso a los certificados que forman parte de la lista.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-155">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span></span>

<span data-ttu-id="8ebe0-156">Si se requiere realizar una revocación más instantánea (por ejemplo, si un usuario pierde un dispositivo), se puede invalidar el token de autorización del usuario.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-156">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span></span> <span data-ttu-id="8ebe0-157">Para ello, establezca el valor del campo **StsRefreshTokenValidFrom** de este usuario concreto mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-157">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="8ebe0-158">Tiene que actualizar el campo **StsRefreshTokenValidFrom** para cada usuario cuyo acceso desee revocar.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-158">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span></span>

<span data-ttu-id="8ebe0-159">Para asegurarse de que la revocación persiste, debe establecer la **fecha de vigencia** de la CRL en una fecha posterior al valor que establece **StsRefreshTokenValidFrom** y asegurarse de que el certificado en cuestión se encuentra en la CRL.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-159">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span></span>

<span data-ttu-id="8ebe0-160">En los siguientes pasos se describe el proceso de actualización e invalidación del token de autorización mediante el establecimiento del campo **StsRefreshTokenValidFrom** .</span><span class="sxs-lookup"><span data-stu-id="8ebe0-160">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="8ebe0-161">**Para configurar la revocación:**</span><span class="sxs-lookup"><span data-stu-id="8ebe0-161">**To configure revocation:**</span></span> 

1. <span data-ttu-id="8ebe0-162">Conéctese con credenciales de administrador al servicio MSOL:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-162">Connect with admin credentials to the MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="8ebe0-163">Recupere el valor actual de StsRefreshTokensValidFrom de un usuario:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-163">Retrieve the current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="8ebe0-164">Configure que el campo StsRefreshTokensValidFrom del usuario tenga el mismo valor que la marca de tiempo actual.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-164">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="8ebe0-165">La fecha establecida debe ser futura.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-165">The date you set must be in the future.</span></span> <span data-ttu-id="8ebe0-166">De lo contrario, no se establece la propiedad **StsRefreshTokensValidFrom** .</span><span class="sxs-lookup"><span data-stu-id="8ebe0-166">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="8ebe0-167">Si la fecha es futura, el valor de **StsRefreshTokensValidFrom** se establece en la hora actual (no la fecha que indica el comando Set-MsolUser).</span><span class="sxs-lookup"><span data-stu-id="8ebe0-167">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="8ebe0-168">Paso 4: Prueba de la configuración</span><span class="sxs-lookup"><span data-stu-id="8ebe0-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="8ebe0-169">Prueba del certificado</span><span class="sxs-lookup"><span data-stu-id="8ebe0-169">Testing your certificate</span></span>

<span data-ttu-id="8ebe0-170">Como primera prueba de configuración, debe tratar de iniciar sesión en [Outlook Web Access](https://outlook.office365.com) o [SharePoint Online](https://microsoft.sharepoint.com) con el **explorador del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-170">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="8ebe0-171">Si el inicio de sesión se realiza correctamente, sabrá que:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="8ebe0-172">El certificado de usuario se ha aprovisionado en el dispositivo de prueba.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-172">The user certificate has been provisioned to your test device</span></span>
- <span data-ttu-id="8ebe0-173">AD FS está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="8ebe0-174">Prueba de aplicaciones móviles de Office</span><span class="sxs-lookup"><span data-stu-id="8ebe0-174">Testing Office mobile applications</span></span>

<span data-ttu-id="8ebe0-175">**Para probar la autenticación basada en certificados en su aplicación móvil de Office:**</span><span class="sxs-lookup"><span data-stu-id="8ebe0-175">**To test certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="8ebe0-176">En el dispositivo de prueba, instale una aplicación móvil de Office (por ejemplo, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="8ebe0-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="8ebe0-177">Inicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-177">Launch the application.</span></span> 
4. <span data-ttu-id="8ebe0-178">Escriba su nombre de usuario y, luego, seleccione el certificado de usuario que quiera utilizar.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-178">Enter your user name, and then select the user certificate you want to use.</span></span> 

<span data-ttu-id="8ebe0-179">Debe haber iniciado sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="8ebe0-180">Prueba de aplicaciones cliente de Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8ebe0-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="8ebe0-181">Para acceder a Exchange ActiveSync (EAS) mediante la autenticación basada en certificados, debe estar disponible en la aplicación un perfil de EAS que contenga el certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-181">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span></span> 

<span data-ttu-id="8ebe0-182">El perfil de EAS debe contener la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ebe0-182">The EAS profile must contain the following information:</span></span>

- <span data-ttu-id="8ebe0-183">El certificado de cliente que se usará para la autenticación</span><span class="sxs-lookup"><span data-stu-id="8ebe0-183">The user certificate to be used for authentication</span></span> 

- <span data-ttu-id="8ebe0-184">El punto de conexión de EAS (por ejemplo, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="8ebe0-184">The EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="8ebe0-185">Puede configurar un perfil de EAS y colocarlo en el dispositivo utilizando el servicio Administración de dispositivos móviles (MDM) como Intune o agregando el certificado manualmente al perfil de EAS del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-185">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="8ebe0-186">Prueba de aplicaciones cliente de EAS en Android</span><span class="sxs-lookup"><span data-stu-id="8ebe0-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="8ebe0-187">**Para probar la autenticación de certificados:**</span><span class="sxs-lookup"><span data-stu-id="8ebe0-187">**To test certificate authentication:**</span></span>  

1. <span data-ttu-id="8ebe0-188">Configure un perfil de EAS en la aplicación que cumpla los requisitos anteriores.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-188">Configure an EAS profile in the application that satisfies the requirements above.</span></span>  
2. <span data-ttu-id="8ebe0-189">Abra la aplicación y verifique que el correo electrónico se esté sincronizando.</span><span class="sxs-lookup"><span data-stu-id="8ebe0-189">Open the application, and verify that mail is synchronizing.</span></span> 

