---
title: "aaaAdd SSL certificate tooyour aplicación de servicio de aplicaciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd SSL certificate tooyour aplicación de servicio de aplicaciones."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>Compra y configuración de un certificado SSL para el Servicio de aplicaciones de Azure

En este tutorial, protegerá su aplicación web comprando un certificado SSL para su instancia de  **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)** almacenándolo de forma segura en [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)y asociándolo a un dominio personalizado.

## <a name="step-1---log-in-tooazure"></a>Paso 1: inicio de sesión tooAzure

Inicie sesión en toohello portal de Azure en http://portal.azure.com

## <a name="step-2---place-an-ssl-certificate-order"></a>Paso 2: Realización de un pedido de certificado SSL

Puede hacer un pedido de certificado SSL al crear un nuevo [certificado de servicio de aplicación](https://portal.azure.com/#create/Microsoft.SSL) en hello **portal de Azure**.

![Creación de certificados](./media/app-service-web-purchase-ssl-web-site/createssl.png)

Escriba descriptivo **nombre** para la SSL de los certificados y escriba hello **nombre de dominio**

> [!NOTE]
> Este es uno de los elementos más importantes de hello del proceso de compra de Hola. Asegúrese de que tooenter corrija el nombre de host (dominio personalizado) que desea que tooprotect con este certificado. **NO** anexar el nombre de Host de hello con World Wide Web. 
>

Seleccione la **suscripción**, el **grupo de recursos** y la **SKU de certificado**.

> [!WARNING]
> Certificados de servicio de aplicación solo puede usarse por otros servicios de aplicación dentro de hello misma suscripción.  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>Paso 3: almacenar el certificado de hello en el almacén de claves de Azure

> [!NOTE]
> [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) es un servicio de Azure que ayuda a proteger claves criptográficas y secretos que emplean servicios y aplicaciones en la nube.
>

Una vez completada la Hola compra de certificado SSL, necesita tooopen [certificados de servicio de aplicación](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) hoja de recursos.

![Insertar imagen de toostore listo en KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

Observará que el estado del certificado es **"Emisión pendiente"** ya que hay algunos pasos más necesita toocomplete antes de poder empezar a usar este certificado.

Haga clic en **configuración de certificado** dentro de la hoja de propiedades del certificado y haga clic en **paso 1: almacén de** toostore este certificado en el almacén de claves de Azure.

De **clave de almacén de estado** hoja, haga clic en **repositorio de almacén de claves** toochoose un toostore de almacén de claves existente este certificado **o crear nuevo almacén de claves** toocreate nueva clave de seguridad del almacén en el mismo grupo de recursos y de suscripción.

> [!NOTE]
> Azure Key Vault tiene gastos mínimos por almacenar este certificado.
> Para obtener más información, consulte **[Detalles de precios de Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.
>

Una vez haya seleccionado toostore de repositorio de almacén de claves de hello en este certificado, Hola **almacén** opción debería mostrar correcto.

![insert image of store success in KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>Paso 4: comprobar Hola propiedad del dominio

> [!NOTE]
> Los tres tipos de comprobación de dominios compatibles con los certificados de App Service son Comprobación de dominio, Comprobación de correo y Comprobación manual. Estos se explican con más detalle en hello [avanzada sección](#advanced).

De Hola mismo **configuración de certificado** hoja usa en el paso 3, haga clic en **paso 2: comprobar**.

**Comprobación del dominio** se trata de proceso más conveniente de hello **sólo si** tiene  **[adquirido su dominio personalizado de servicio de aplicaciones de Azure.](custom-dns-web-site-buydomains-web-app.md)**
Haga clic en **compruebe** botón toocomplete este paso.

![insert image of domain verification](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

Después de hacer clic **compruebe**, usar hello **actualizar** botón hasta hello **compruebe** opción debería mostrar correcto.

![insert image of verify success in KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>Paso 5: asignar tooApp de certificado del servicio de aplicaciones

> [!NOTE]
> Antes de realizar los pasos de hello en esta sección, debe tener asociado un nombre de dominio personalizado a la aplicación. Para más información, consulte **[Configuración de un nombre de dominio personalizado para una aplicación web](app-service-web-tutorial-custom-domain.md)**
>

Hola  **[portal de Azure](https://portal.azure.com/)**, haga clic en hello **servicio de aplicaciones** opción izquierda Hola de página Hola.

Haga clic en el nombre de Hola de su toowhich de aplicación que desea tooassign este certificado.

Hola **configuración**, haga clic en **certificados SSL**.

Haga clic en **importar certificado de servicio de aplicación** y seleccione Hola certificado que acaba de comprar.

![insertar imagen de Importar certificado](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

Hola **enlaces ssl** sección haga clic en **agregar enlaces**, utilice toosecure de nombre de dominio de hello listas desplegables tooselect Hola con SSL y Hola toouse de certificado. También puede seleccionar si toouse  **[indicación de nombre de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  o SSL basada en IP.

![insertar imagen de enlaces de SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

Haga clic en **Agregar enlace** toosave Hola cambios y habilitar SSL.

> [!NOTE]
> Si seleccionó **SSL basada en IP** y su dominio personalizado se configura mediante un registro, debe realizar pasos adicionales de Hola. Estos se explican con más detalle en hello [avanzada sección](#Advanced).

En este momento, también debe ser capaz de toovisit la aplicación con `HTTPS://` en lugar de `HTTP://` tooverify que Hola certificado se ha configurado correctamente.

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>Paso 6: Tareas de administración

### <a name="azure-cli"></a>CLI de Azure

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>Avanzado

### <a name="verifying-domain-ownership"></a>Comprobación de la propiedad del dominio

Hay dos tipos más de comprobación de dominio que admiten los certificados de App Service: Comprobación de correo electrónico y Comprobación manual.

#### <a name="mail-verification"></a>Comprobación de correo electrónico

Correo electrónico de comprobación ya se ha enviado toohello que direcciones de correo electrónico asociado a este dominio personalizado.
paso de verificación de correo electrónico de hello toocomplete, abra el correo electrónico de Hola y haga clic en vínculo de comprobación de Hola.

![insert image of email verification](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

Si necesita correo electrónico de comprobación de hello tooresend, haga clic en hello **reenviar correo electrónico** botón.

#### <a name="manual-verification"></a>Comprobación manual

> [!IMPORTANT]
> Comprobación de página web HTML (solo funciona con la SKU de certificados estándar)
>

1. Creación de un archivo HTML denominado "**starfield.html**"

1. Contenido de este archivo debe ser Hola nombre exacto de hello Token de comprobación del dominio. (Puede copiar token Hola de hello hoja de estado de comprobación de dominio)

1. Cargar este archivo en la raíz de Hola de servidor de web de Hola que aloja el dominio`/.well-known/pki-validation/starfield.html`

1. Haga clic en **actualizar** estado una vez completada la comprobación del certificado de hello tooupdate. Pueden tardar varios minutos para toocomplete de comprobación.

> [!TIP]
> Compruebe en un formulario mediante terminal `curl -G http://<domain>/.well-known/pki-validation/starfield.html` respuesta Hola debe contener hello `<verification-token>`.

#### <a name="dns-txt-record-verification"></a>Comprobación del registro TXT de DNS

1. Con el Administrador de DNS, crear un registro TXT en hello `@` subdominio con valor toohello igual Token de comprobación del dominio.
1. Haga clic en **"Actualizar"** tooupdate Hola estado una vez completada la comprobación del certificado.

> [!TIP]
> Necesita un registro TXT toocreate en `@.<domain>` con valor `<verification-token>`.

### <a name="assign-certificate-tooapp-service-app"></a>Asignar tooApp de certificado del servicio de aplicaciones

Si seleccionó **SSL basada en IP** y su dominio personalizado se configura mediante un registro, debe realizar pasos adicionales de hello:

Después de configurar el enlace SSL basado en una dirección IP, una dirección IP dedicada se asigna tooyour aplicación. Puede encontrar esta dirección IP en hello **dominio personalizado** página en la configuración de la aplicación, justo encima de hello **los nombres de host** sección. Figurará como **Dirección IP externa**.

![insertar imagen de SSL de IP](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

Tenga en cuenta que esta dirección IP es diferente de la dirección IP virtual de hello había usado anteriormente registro tooconfigure hello para el dominio. Si se configuran toouse SSL basada en SNI o no están configurado toouse SSL, no se mostrará ninguna dirección para esta entrada.

Mediante herramientas de hello proporcionadas por el registrador de nombres de dominio, modificar un registro para la dirección IP de dominio personalizado nombre toopoint toohello del paso anterior Hola Hola.

## <a name="rekey-and-sync-hello-certificate"></a>Regeneración de claves y sincronización Hola certificado

Si alguna vez necesitas tooRekey su certificado, seleccione **regenerar y sincronización** opción de **propiedades de certificado** hoja.

Haga clic en **regenerar** botón proceso de hello tooinitiate. Este proceso puede tardar toocomplete 1-10 minutos.

![insertar imagen de SSL de regeneración de claves](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

El certificado de regeneración de claves agrupa el certificado Hola con un nuevo certificado emitido por la entidad emisora de certificados de Hola.

## <a name="next-steps"></a>Pasos siguientes

* [Adición de una red de entrega de contenido](app-service-web-tutorial-content-delivery-network.md)