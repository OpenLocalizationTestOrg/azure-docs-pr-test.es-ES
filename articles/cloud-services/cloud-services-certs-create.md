---
title: "los certificados de servicios y la administración de aaaCloud | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y el uso de certificados con Microsoft Azure"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a>Introducción a los certificados para Azure Cloud Services
Los certificados se usan en Azure para servicios en la nube ([certificados de servicio](#what-are-service-certificates)) y para autenticar con la API de administración de hello ([certificados de administración](#what-are-management-certificates) cuando utilizando Hola portal de Azure clásico y no Hola no clásico portal de Azure). Este tema proporciona información general de ambos tipos de certificados, cómo demasiado[crear](#create) y [implementar](#deploy) les tooAzure.

Los certificados usados en Azure son certificados x.509 v3 y pueden estar firmados por otro certificado de confianza o estar autofirmados. Un certificado autofirmado está firmado por su propio creador; por lo tanto, no es de confianza de forma predeterminada. La mayoría de los exploradores pueden pasar por alto este problema. Solo debe usar certificados autofirmados cuando desarrolle y pruebe sus servicios en la nube. 

Los certificados utilizados por Azure pueden contener una clave privada o pública. Los certificados tienen una huella digital que proporciona un medio tooidentify ellas de forma inequívoca. Esta huella digital se utiliza en hello Azure [archivo de configuración](cloud-services-configure-ssl-certificate.md) tooidentify que un servicio de nube de certificado debe usar. 

## <a name="what-are-service-certificates"></a>¿Qué son los certificados de servicio?
Certificados de servicio son servicios de toocloud adjunto y habilitar una comunicación segura tooand del servicio de Hola. Por ejemplo, si implementa un rol web, sería conveniente toosupply un certificado que se puede autenticar a un extremo HTTPS expuesto. Certificados de servicio, definidos en la definición de servicio, son la máquina virtual de toohello implementadas automáticamente que se está ejecutando una instancia del rol. 

Puede cargar clásico de tooAzure certificados de servicio portal usando Hola clásico Azure portal o mediante el modelo de implementación clásica de Hola. Los certificados de servicio están asociados a un servicio en la nube específico. Se les asignan tooa implementación en el archivo de definición de servicio de Hola.

Los certificados de servicio se pueden administrar independientemente de los servicios y pueden ser administrados por distintas personas. Por ejemplo, un desarrollador puede cargar un paquete de servicio que hace referencia el certificado tooa que un administrador de TI ha cargado previamente tooAzure. Un administrador de TI puede administrar y renovar el certificado (cambiando la configuración de hello del servicio de hello) sin necesidad de tooupload un nuevo paquete de servicio. Es posible actualizar sin un nuevo paquete de servicio dado nombre lógico de Hola, nombre del almacén y ubicación del certificado de hello es en el archivo de definición de servicio de Hola y mientras la huella digital del certificado Hola se especifica en el archivo de configuración de servicio de Hola. certificado de hello tooupdate, es solo es necesario tooupload un nuevo certificado y la huella digital de Hola de cambio de valor en el archivo de configuración de servicio de Hola.

>[!Note]
>Hola [preguntas más frecuentes sobre servicios de nube](cloud-services-faq.md) artículo tiene cierta información útil acerca de los certificados.

## <a name="what-are-management-certificates"></a>¿Qué son los certificados de administración?
Certificados de administración le permiten tooauthenticate con el modelo de implementación clásica de Hola. Muchos programas y herramientas (como Visual Studio o hello Azure SDK) utilizan estos configuración tooautomate de certificados y la implementación de varios servicios de Azure. Estos no son servicios de toocloud realmente relacionados. 

> [!WARNING]
> Por lo tanto, tenga cuidado. Estos tipos de certificados permiten a ningún usuario que se autentica con su suscripción de hello toomanage que están asociados. 
> 
> 

### <a name="limitations"></a>Limitaciones
Hay un límite de 100 certificados de administración por suscripción. También hay un límite de 100 certificados de administración para todas las suscripciones bajo un identificador de usuario de un administrador de servicio específico. Si Hola Id. de usuario de administrador de la cuenta de hello ya ha sido usado tooadd 100 certificados de administración y es necesario más certificados, puede agregar un Coadministrador tooadd Hola hay certificados adicionales. 

Antes de agregar más de 100 certificados, vea si puede reutilizar un certificado existente. Uso de coadministradores agrega una complejidad probablemente innecesaria tooyour proceso de administración de certificados.

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>Creación de un nuevo certificado autofirmado
Puede usar cualquier toocreate disponible un certificado autofirmado de herramienta siempre que adhiera configuración toothese:

* Un certificado X.509.
* Contiene una clave privada.
* Creado para intercambio de claves (archivo .pfx).
* Nombre de sujeto debe coincidir con servicio de nube de hello dominio utilizado tooaccess Hola.

    > No se puede adquirir un certificado SSL para cloudapp.net hello (o para cualquier relacionadas con Azure) dominio; nombre de sujeto del certificado de Hello debe coincidir con tooaccess de usa el nombre de dominio personalizado de Hola la aplicación. Por ejemplo, **contoso.net**, no **contoso.cloudapp.net**.

* Mínimo de cifrado de 2.048 bits.
* **Servicio de certificado sólo**: certificado de cliente debe encontrarse en hello *Personal* almacén de certificados.

Hay dos toocreate formas sencillas un certificado en Windows, con hello `makecert.exe` utilidad o IIS.

### <a name="makecertexe"></a>Makecert.exe
Esta utilidad ha quedado en desuso y ya no se documenta aquí. Para obtener más información, consulte [este artículo de MSDN](https://msdn.microsoft.com/library/windows/desktop/aa386968).

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> Si desea que el certificado de hello toouse con una dirección IP en lugar de un dominio, use la dirección IP de hello en el parámetro - DnsName de hello.


Si desea toouse [certificado con el portal de administración de hello](../azure-api-management-certs.md), exportarlo tooa **.cer** archivo:

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)
Hay muchas páginas en hello internet que abarcan cómo toodo esto con IIS. [Aquí](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) hay una excelente que encontré en la que se explica bien. 

### <a name="java"></a>Java
Puede usar Java demasiado[crear un certificado](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).

### <a name="linux"></a>Linux
[Esto](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artículo describe cómo toocreate certificados mediante SSH.

## <a name="next-steps"></a>Pasos siguientes
[Cargar su toohello de certificado de servicio portal de Azure clásico](cloud-services-configure-ssl-certificate.md) (o hello [portal de Azure](cloud-services-configure-ssl-certificate-portal.md)).

Cargar un [certificado de la API de administración](../azure-api-management-certs.md) toohello portal de Azure clásico. Hola portal de Azure no utiliza certificados de administración para la autenticación.

