---
title: "Generación y exportación de certificados para conexiones de punto a sitio: MakeCert: Azure | Microsoft Docs"
description: "Este artículo contiene pasos toocreate un certificado raíz autofirmado, exportar la clave pública de Hola y generar los certificados de cliente mediante MakeCert."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>Generación y exportación de certificados para conexiones de punto a sitio con MakeCert

Conexiones de punto a sitio usan certificados tooauthenticate. Este artículo muestra cómo toocreate una firma automática el certificado de raíz y generar los certificados de cliente mediante MakeCert. Si está buscando en pasos de configuración de punto a sitio, como cómo enumerar certificados raíz de tooupload, seleccione uno de los artículos de hello ' Configure Point-to-Site' de hello después de:

> [!div class="op_single_selector"]
> * [Creación de certificados autofirmados: PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Creación de certificados autofirmados: MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configuración de una conexión de punto a sitio: Resource Manager: Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Configuración de una conexión de punto a sitio - Resource Manager - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configuración de una conexión de punto a sitio: Clásico: Azure Portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

Aunque se recomienda usar hello [Windows PowerShell de 10 pasos](vpn-gateway-certificates-point-to-site.md) toocreate los certificados, se dan estas instrucciones de MakeCert como un método opcional. certificados de Hola que generan mediante cualquiera de estos métodos se pueden instalar en [cualquier sistema operativo de cliente admitida](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq). Sin embargo, MakeCert tiene Hola siguiente limitación:

* Makecert está en desuso. Esto significa que se puede quitar esta herramienta en cualquier momento. Los certificados ya generados con MakeCert no se verán afectados si MakeCert ya no está disponible. MakeCert forma solo usa toogenerate Hola certificados, no como un mecanismo de validación.

## <a name="rootcert"></a>Creación de un certificado raíz autofirmado

Hola siguientes pasos muestra cómo toocreate una firma automática de certificado mediante MakeCert. Estos pasos no son específicos del modelo de implementación. Son válidos para el Administrador de recursos y la versión clásica.

1. Descargue e instale [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).
2. Después de la instalación, normalmente puede encontrar utilidad makecert.exe de hello en esta ruta de acceso: ' C:\Program Files (x86) \Windows Kits\10\bin\<arch >'. Sin embargo, es posible que estaba instalado tooanother ubicación. Abra un símbolo del sistema como administrador y navegue toohello ubicación de hello herramienta MakeCert. Puede usar Hola siguiente ejemplo, ajustar la ubicación correcta de hello:

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. Cree e instale un certificado en el almacén de certificados personales de hello en el equipo. Hello en el ejemplo siguiente se crea su correspondiente *.cer* archivo cargue tooAzure al configurar P2S. Reemplace 'P2SRootCert' y 'P2SRootCert.cer' con el nombre de Hola que quiere toouse de certificado de Hola. Hola certificado se encuentra en los 'certificados - actual\Personal\Certificados'.

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>Exportar la clave pública de hello (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

archivo de Hello exported.cer debe ser tooAzure cargado. Para ver las instrucciones, consulte [Configuración de una conexión de punto a sitio](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile). tooadd un certificado raíz de confianza adicionales, consulte [en esta sección](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) de artículo Hola.

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>Exportar el certificado autofirmado de Hola y toostore clave privada se (opcional)

Puede que desee tooexport Hola certificado raíz autofirmado y almacenar de forma segura. Si es necesario, más adelante puede instalarlo en otro equipo y generar más certificados de cliente o exportar otro archivo .cer. Hola tooexport certificado autofirmado de raíz como una .pfx, certificado de raíz de hello seleccione y use Hola mismos pasos tal como se describe en [exportar un certificado de cliente](#clientexport).

## <a name="create-and-install-client-certificates"></a>Creación e instalación de certificados de cliente

No instale el certificado autofirmado de hello directamente en el equipo cliente de Hola. Necesita un certificado de cliente de certificado autofirmado de hello toogenerate. A continuación, exportar e instalar el equipo de cliente de toohello de certificado de cliente de Hola. Hola pasos no es específicos del modelo de implementación. Son válidos para el Administrador de recursos y la versión clásica.

### <a name="clientcert"></a>Generación de un certificado de cliente

Cada equipo cliente que se conecta tooa red virtual con punto a sitio debe tener instalado un certificado de cliente. Genere un certificado de cliente de certificado de raíz autofirmado hello y, a continuación, exportar de instalar el certificado de cliente de Hola. Si no está instalado el certificado de cliente de hello, se produce un error en la autenticación. 

Hello pasos siguientes le guían a través de generar un certificado de cliente de un certificado raíz autofirmado. Puede generar varios certificados de cliente de hello mismo certificado raíz. Al generar certificados de cliente mediante estos pasos hello, certificado de cliente de Hola se instala automáticamente en el equipo de Hola que utiliza certificados de hello toogenerate. Si desea tooinstall un certificado de cliente en otro equipo cliente, puede exportar el certificado de Hola.
 
1. En hello mismo equipo que usa toocreate Hola certificado autofirmado, abra un símbolo del sistema como administrador.
2. Modifique y ejecute toogenerate de ejemplo de Hola un certificado de cliente.
  * Cambio *"P2SRootCert"* toohello nombre de raíz autofirmado Hola que va a generar el certificado de cliente de Hola de. Asegúrese de que está utilizando Hola nombre de certificado de raíz de hello, que es cualquier hello ' CN =' valor era que especificó cuando creó raíz autofirmado Hola.
  * Cambio *P2SChildCert* nombre toohello desea toogenerate una toobe de certificado de cliente.

  Si ejecuta Hola siguiente ejemplo sin modificación alguna, resultado de hello es un certificado de cliente denominado P2SChildcert en el almacén de certificados personales que generó el certificado raíz P2SRootCert.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>Exportación de un certificado de cliente

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>Instalación de un certificado de cliente exportado

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Pasos siguientes

Continúe con la configuración de punto a sitio. 

* Para **el Administrador de recursos** pasos del modelo de implementación, consulte [configurar una tooa de conexión de punto a sitio red virtual](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Para **clásico** pasos del modelo de implementación, consulte [configurar una tooa de conexión de Point-to-Site VPN red virtual (clásica)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
