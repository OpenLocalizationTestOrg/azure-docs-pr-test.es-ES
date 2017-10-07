---
title: "Generación y exportación de certificados para conexiones de punto a sitio: PowerShell: Azure | Microsoft Docs"
description: "Este artículo contiene pasos toocreate un certificado raíz autofirmado, exportar la clave pública de Hola y generar los certificados de cliente mediante PowerShell en Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="5f65f-103">Generación y exportación de certificados para conexiones de punto a sitio con PowerShell en Windows 10</span><span class="sxs-lookup"><span data-stu-id="5f65f-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="5f65f-104">Conexiones de punto a sitio usan certificados tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="5f65f-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="5f65f-105">Este artículo muestra cómo toocreate una firma automática el certificado de raíz y generar los certificados de cliente mediante PowerShell en Windows 10.</span><span class="sxs-lookup"><span data-stu-id="5f65f-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="5f65f-106">Si está buscando en pasos de configuración de punto a sitio, como cómo enumerar certificados raíz de tooupload, seleccione uno de los artículos de hello ' Configure Point-to-Site' de hello después de:</span><span class="sxs-lookup"><span data-stu-id="5f65f-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f65f-107">Creación de certificados autofirmados: PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f65f-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="5f65f-108">Creación de certificados autofirmados: MakeCert</span><span class="sxs-lookup"><span data-stu-id="5f65f-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="5f65f-109">Configuración de una conexión de punto a sitio: Resource Manager: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5f65f-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="5f65f-110">Configuración de una conexión de punto a sitio - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f65f-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="5f65f-111">Configuración de una conexión de punto a sitio: Clásico: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5f65f-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="5f65f-112">Debe realizar los pasos de hello en este artículo en un equipo que ejecute Windows 10.</span><span class="sxs-lookup"><span data-stu-id="5f65f-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="5f65f-113">cmdlets de PowerShell de Hola que utilice certificados toogenerate forman parte del sistema operativo de Windows 10 hello y no funcionan en otras versiones de Windows.</span><span class="sxs-lookup"><span data-stu-id="5f65f-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="5f65f-114">equipo de Hello Windows 10 es únicamente los certificados necesarios toogenerate Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="5f65f-115">Una vez que se generan certificados hello, puede cargarlos o instalarlos en cualquier sistema operativo de cliente admitidos.</span><span class="sxs-lookup"><span data-stu-id="5f65f-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="5f65f-116">Si no tiene el equipo de acceso tooa Windows 10, puede usar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificados.</span><span class="sxs-lookup"><span data-stu-id="5f65f-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="5f65f-117">Hello certificados que generan mediante cualquiera de estos métodos pueden estar instalados en cualquier [admite](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) sistema operativo del cliente.</span><span class="sxs-lookup"><span data-stu-id="5f65f-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="5f65f-118"><a name="rootcert"></a>Creación de un certificado raíz autofirmado</span><span class="sxs-lookup"><span data-stu-id="5f65f-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="5f65f-119">Utilice toocreate de cmdlet New-SelfSignedCertificate de hello un certificado raíz autofirmado.</span><span class="sxs-lookup"><span data-stu-id="5f65f-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="5f65f-120">Para obtener información adicional sobre los parámetros, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="5f65f-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="5f65f-121">En un equipo con Windows 10, abra una consola de Windows PowerShell con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="5f65f-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="5f65f-122">Usar hello siguiendo el certificado raíz autofirmado de ejemplo toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="5f65f-123">Hello en el ejemplo siguiente se crea un certificado raíz firmado automáticamente con el nombre 'P2SRootCert' que se instala automáticamente en 'Actual\Personal\Certificados certificados-usuario actual'.</span><span class="sxs-lookup"><span data-stu-id="5f65f-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="5f65f-124">Puede ver el certificado de hello abriendo *certmgr.msc*, o *administrar certificados de usuario*.</span><span class="sxs-lookup"><span data-stu-id="5f65f-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="5f65f-125"><a name="cer"></a>Exportar la clave pública de hello (.cer)</span><span class="sxs-lookup"><span data-stu-id="5f65f-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="5f65f-126">archivo de Hello exported.cer debe ser tooAzure cargado.</span><span class="sxs-lookup"><span data-stu-id="5f65f-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="5f65f-127">Para ver las instrucciones, consulte [Configuración de una conexión de punto a sitio](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="5f65f-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="5f65f-128">un certificado raíz de confianza adicionales, tooadd [en esta sección](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) de artículo Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="5f65f-129">Exportar el certificado raíz autofirmado de Hola y toostore de clave pública se (opcional)</span><span class="sxs-lookup"><span data-stu-id="5f65f-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="5f65f-130">Puede que desee tooexport Hola certificado raíz autofirmado y almacenar de forma segura.</span><span class="sxs-lookup"><span data-stu-id="5f65f-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="5f65f-131">Si es necesario, más adelante puede instalarlo en otro equipo y generar más certificados de cliente o exportar otro archivo .cer.</span><span class="sxs-lookup"><span data-stu-id="5f65f-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="5f65f-132">Hola tooexport certificado autofirmado de raíz como una .pfx, certificado de raíz de hello seleccione y use Hola mismos pasos tal como se describe en [exportar un certificado de cliente](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="5f65f-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="5f65f-133"><a name="clientcert"></a>Generación de un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="5f65f-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="5f65f-134">Cada equipo cliente que se conecta tooa red virtual con punto a sitio debe tener instalado un certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="5f65f-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="5f65f-135">Genere un certificado de cliente de certificado de raíz autofirmado hello y, a continuación, exportar de instalar el certificado de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="5f65f-136">Si no está instalado el certificado de cliente de hello, se produce un error en la autenticación.</span><span class="sxs-lookup"><span data-stu-id="5f65f-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="5f65f-137">Hello pasos siguientes le guían a través de generar un certificado de cliente de un certificado raíz autofirmado.</span><span class="sxs-lookup"><span data-stu-id="5f65f-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="5f65f-138">Puede generar varios certificados de cliente de hello mismo certificado raíz.</span><span class="sxs-lookup"><span data-stu-id="5f65f-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="5f65f-139">Al generar certificados de cliente mediante estos pasos hello, certificado de cliente de Hola se instala automáticamente en el equipo de Hola que utiliza certificados de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="5f65f-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="5f65f-140">Si desea tooinstall un certificado de cliente en otro equipo cliente, puede exportar el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="5f65f-141">ejemplos de Hello usan Hola New-SelfSignedCertificate cmdlet toogenerate un certificado de cliente que expira un año.</span><span class="sxs-lookup"><span data-stu-id="5f65f-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="5f65f-142">Para obtener información adicional de los parámetros, como establecer un valor de caducidad diferentes para el certificado de cliente de hello, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="5f65f-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="5f65f-143">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="5f65f-143">Example 1</span></span>

<span data-ttu-id="5f65f-144">Este ejemplo utiliza Hola declarado la variable '$cert' desde la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="5f65f-145">Si ha cerrado la consola de PowerShell de hello después de crear Hola certificado raíz autofirmado o va a crear cliente adicional certificados en una nueva sesión de consola de PowerShell, siga los pasos de hello en [ejemplo 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="5f65f-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="5f65f-146">Modifique y ejecute toogenerate de ejemplo de Hola un certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="5f65f-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="5f65f-147">Si ejecuta Hola siguiente ejemplo sin modificación alguna, resultado de hello es un certificado de cliente con el nombre 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="5f65f-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="5f65f-148">Si desea que el certificado de secundario de hello tooname algo más, modifique el valor CN de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="5f65f-149">No cambie hello TextExtension cuando se ejecuta este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5f65f-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="5f65f-150">certificado de cliente de Hola que genere automáticamente se instala en 'Certificados - actual\Personal\Certificados' en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5f65f-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="5f65f-151"><a name="ex2"></a>Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="5f65f-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="5f65f-152">Si está creando certificados de cliente adicionales, o no se usa bienvenida a misma sesión de PowerShell que usa toocreate su certificado raíz autofirmado, Hola uso pasos:</span><span class="sxs-lookup"><span data-stu-id="5f65f-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="5f65f-153">Identificar el certificado raíz autofirmado de Hola que está instalado en el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="5f65f-154">Este cmdlet devuelve una lista de certificados que están instalados en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5f65f-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="5f65f-155">Busque el nombre del sujeto Hola Hola devuelve la lista y, a continuación, huella digital de Hola de copia es encuentra texto de tooa tooit siguiente archivo.</span><span class="sxs-lookup"><span data-stu-id="5f65f-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="5f65f-156">En el siguiente ejemplo de Hola, hay dos certificados.</span><span class="sxs-lookup"><span data-stu-id="5f65f-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="5f65f-157">nombre CN Hello es Hola Hola con firma automática del certificado de raíz desde el que desea toogenerate un certificado secundario.</span><span class="sxs-lookup"><span data-stu-id="5f65f-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="5f65f-158">En este caso, "P2SRootCert".</span><span class="sxs-lookup"><span data-stu-id="5f65f-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="5f65f-159">Declare una variable para el certificado de raíz de hello mediante huella digital de saludo del paso anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="5f65f-160">Reemplace la huella digital con la huella digital de Hola Hola del certificado de raíz desde el que desea toogenerate un certificado secundario.</span><span class="sxs-lookup"><span data-stu-id="5f65f-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="5f65f-161">Por ejemplo, con huella digital de Hola para P2SRootCert en el paso anterior de hello, variable Hola aspecto:</span><span class="sxs-lookup"><span data-stu-id="5f65f-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="5f65f-162">Modifique y ejecute toogenerate de ejemplo de Hola un certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="5f65f-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="5f65f-163">Si ejecuta Hola siguiente ejemplo sin modificación alguna, resultado de hello es un certificado de cliente con el nombre 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="5f65f-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="5f65f-164">Si desea que el certificado de secundario de hello tooname algo más, modifique el valor CN de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f65f-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="5f65f-165">No cambie hello TextExtension cuando se ejecuta este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5f65f-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="5f65f-166">certificado de cliente de Hola que genere automáticamente se instala en 'Certificados - actual\Personal\Certificados' en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5f65f-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="5f65f-167"><a name="clientexport"></a>Exportación de un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="5f65f-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="5f65f-168"><a name="install"></a>Instalación de un certificado de cliente exportado</span><span class="sxs-lookup"><span data-stu-id="5f65f-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5f65f-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5f65f-169">Next steps</span></span>

<span data-ttu-id="5f65f-170">Continúe con la configuración de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="5f65f-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="5f65f-171">Para **el Administrador de recursos** pasos del modelo de implementación, consulte [configurar una tooa de conexión de punto a sitio red virtual](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5f65f-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="5f65f-172">Para **clásico** pasos del modelo de implementación, consulte [configurar una tooa de conexión de Point-to-Site VPN red virtual (clásica)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5f65f-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
