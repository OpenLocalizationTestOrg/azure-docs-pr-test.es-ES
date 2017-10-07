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
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Generación y exportación de certificados para conexiones de punto a sitio con PowerShell en Windows 10

Conexiones de punto a sitio usan certificados tooauthenticate. Este artículo muestra cómo toocreate una firma automática el certificado de raíz y generar los certificados de cliente mediante PowerShell en Windows 10. Si está buscando en pasos de configuración de punto a sitio, como cómo enumerar certificados raíz de tooupload, seleccione uno de los artículos de hello ' Configure Point-to-Site' de hello después de:

> [!div class="op_single_selector"]
> * [Creación de certificados autofirmados: PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Creación de certificados autofirmados: MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configuración de una conexión de punto a sitio: Resource Manager: Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Configuración de una conexión de punto a sitio - Resource Manager - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configuración de una conexión de punto a sitio: Clásico: Azure Portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


Debe realizar los pasos de hello en este artículo en un equipo que ejecute Windows 10. cmdlets de PowerShell de Hola que utilice certificados toogenerate forman parte del sistema operativo de Windows 10 hello y no funcionan en otras versiones de Windows. equipo de Hello Windows 10 es únicamente los certificados necesarios toogenerate Hola. Una vez que se generan certificados hello, puede cargarlos o instalarlos en cualquier sistema operativo de cliente admitidos. 

Si no tiene el equipo de acceso tooa Windows 10, puede usar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificados. Hello certificados que generan mediante cualquiera de estos métodos pueden estar instalados en cualquier [admite](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) sistema operativo del cliente.

## <a name="rootcert"></a>Creación de un certificado raíz autofirmado

Utilice toocreate de cmdlet New-SelfSignedCertificate de hello un certificado raíz autofirmado. Para obtener información adicional sobre los parámetros, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. En un equipo con Windows 10, abra una consola de Windows PowerShell con privilegios elevados.
2. Usar hello siguiendo el certificado raíz autofirmado de ejemplo toocreate Hola. Hello en el ejemplo siguiente se crea un certificado raíz firmado automáticamente con el nombre 'P2SRootCert' que se instala automáticamente en 'Actual\Personal\Certificados certificados-usuario actual'. Puede ver el certificado de hello abriendo *certmgr.msc*, o *administrar certificados de usuario*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Exportar la clave pública de hello (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

archivo de Hello exported.cer debe ser tooAzure cargado. Para ver las instrucciones, consulte [Configuración de una conexión de punto a sitio](vpn-gateway-howto-point-to-site-rm-ps.md#upload). un certificado raíz de confianza adicionales, tooadd [en esta sección](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) de artículo Hola.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Exportar el certificado raíz autofirmado de Hola y toostore de clave pública se (opcional)

Puede que desee tooexport Hola certificado raíz autofirmado y almacenar de forma segura. Si es necesario, más adelante puede instalarlo en otro equipo y generar más certificados de cliente o exportar otro archivo .cer. Hola tooexport certificado autofirmado de raíz como una .pfx, certificado de raíz de hello seleccione y use Hola mismos pasos tal como se describe en [exportar un certificado de cliente](#clientexport).

## <a name="clientcert"></a>Generación de un certificado de cliente

Cada equipo cliente que se conecta tooa red virtual con punto a sitio debe tener instalado un certificado de cliente. Genere un certificado de cliente de certificado de raíz autofirmado hello y, a continuación, exportar de instalar el certificado de cliente de Hola. Si no está instalado el certificado de cliente de hello, se produce un error en la autenticación. 

Hello pasos siguientes le guían a través de generar un certificado de cliente de un certificado raíz autofirmado. Puede generar varios certificados de cliente de hello mismo certificado raíz. Al generar certificados de cliente mediante estos pasos hello, certificado de cliente de Hola se instala automáticamente en el equipo de Hola que utiliza certificados de hello toogenerate. Si desea tooinstall un certificado de cliente en otro equipo cliente, puede exportar el certificado de Hola.

ejemplos de Hello usan Hola New-SelfSignedCertificate cmdlet toogenerate un certificado de cliente que expira un año. Para obtener información adicional de los parámetros, como establecer un valor de caducidad diferentes para el certificado de cliente de hello, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Ejemplo 1

Este ejemplo utiliza Hola declarado la variable '$cert' desde la sección anterior de Hola. Si ha cerrado la consola de PowerShell de hello después de crear Hola certificado raíz autofirmado o va a crear cliente adicional certificados en una nueva sesión de consola de PowerShell, siga los pasos de hello en [ejemplo 2](#ex2).

Modifique y ejecute toogenerate de ejemplo de Hola un certificado de cliente. Si ejecuta Hola siguiente ejemplo sin modificación alguna, resultado de hello es un certificado de cliente con el nombre 'P2SChildCert'.  Si desea que el certificado de secundario de hello tooname algo más, modifique el valor CN de Hola. No cambie hello TextExtension cuando se ejecuta este ejemplo. certificado de cliente de Hola que genere automáticamente se instala en 'Certificados - actual\Personal\Certificados' en el equipo.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Ejemplo 2

Si está creando certificados de cliente adicionales, o no se usa bienvenida a misma sesión de PowerShell que usa toocreate su certificado raíz autofirmado, Hola uso pasos:

1. Identificar el certificado raíz autofirmado de Hola que está instalado en el equipo de Hola. Este cmdlet devuelve una lista de certificados que están instalados en el equipo.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Busque el nombre del sujeto Hola Hola devuelve la lista y, a continuación, huella digital de Hola de copia es encuentra texto de tooa tooit siguiente archivo. En el siguiente ejemplo de Hola, hay dos certificados. nombre CN Hello es Hola Hola con firma automática del certificado de raíz desde el que desea toogenerate un certificado secundario. En este caso, "P2SRootCert".

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Declare una variable para el certificado de raíz de hello mediante huella digital de saludo del paso anterior Hola. Reemplace la huella digital con la huella digital de Hola Hola del certificado de raíz desde el que desea toogenerate un certificado secundario.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Por ejemplo, con huella digital de Hola para P2SRootCert en el paso anterior de hello, variable Hola aspecto:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Modifique y ejecute toogenerate de ejemplo de Hola un certificado de cliente. Si ejecuta Hola siguiente ejemplo sin modificación alguna, resultado de hello es un certificado de cliente con el nombre 'P2SChildCert'. Si desea que el certificado de secundario de hello tooname algo más, modifique el valor CN de Hola. No cambie hello TextExtension cuando se ejecuta este ejemplo. certificado de cliente de Hola que genere automáticamente se instala en 'Certificados - actual\Personal\Certificados' en el equipo.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Exportación de un certificado de cliente   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>Instalación de un certificado de cliente exportado

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Pasos siguientes

Continúe con la configuración de punto a sitio. 

* Para **el Administrador de recursos** pasos del modelo de implementación, consulte [configurar una tooa de conexión de punto a sitio red virtual](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Para **clásico** pasos del modelo de implementación, consulte [configurar una tooa de conexión de Point-to-Site VPN red virtual (clásica)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
