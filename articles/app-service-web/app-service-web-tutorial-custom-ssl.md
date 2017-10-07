---
title: aaaBind SSL personalizada existente tooAzure las aplicaciones Web de certificados | Documentos de Microsoft
description: "Obtenga información acerca de tootoobind una aplicación personalizada de web tooyour de certificado SSL, un back-end de aplicación móvil o una aplicación de API en el servicio de aplicación de Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>Enlazar un tooAzure de certificado SSL personalizado aplicaciones Web existente

Azure Web Apps proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático. Este tutorial muestra cómo toobind un SSL personalizado de certificado que ha adquirido en una entidad de certificación de confianza demasiado[aplicaciones Web de Azure](app-service-web-overview.md). Cuando haya terminado, podrá tooaccess capaz de tu aplicación web en el punto de conexión de hello HTTPS del dominio DNS personalizado.

![Aplicación web con certificado SSL personalizado](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Actualizar el plan de tarifa de la aplicación
> * Enlazar el tooApp de certificado SSL servicio personalizado
> * Implementar HTTPS en la aplicación
> * Automatizar el enlace de certificado SSL con scripts

> [!NOTE]
> Si necesita tooget un certificado SSL personalizado, puede obtenerla en hello portal de Azure directamente y enlazar tooyour web app. Siga hello [tutorial de certificados del servicio de aplicación](web-sites-purchase-ssl-web-site.md).

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

- [Crear una aplicación de App Service](/azure/app-service/)
- [Asignar una aplicación de web de tooyour de nombre DNS personalizada](app-service-web-tutorial-custom-domain.md)
- Adquirir un certificado SSL de una entidad de certificación de confianza

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>Requisitos para el certificado SSL

toouse un certificado de servicio de aplicaciones, el certificado de hello debe cumplir Hola todos los siguientes requisitos:

* Estar firmado por una entidad de certificación de confianza
* Haberse exportado como archivo PFX protegido por contraseña
* Contener una clave privada con una longitud de al menos 2048 bits
* Contiene todos los certificados intermedios de la cadena de certificados de Hola

> [!NOTE]
> Los **certificados de criptografía de curva elíptica (ECC)** pueden funcionar con App Service, pero están fuera del ámbito de este artículo. Trabajar con la entidad emisora de certificados en certificados de hello pasos exactos toocreate ECC.

## <a name="prepare-your-web-app"></a>Preparar la aplicación web

toobind un SSL personalizado de certificados tooyour web app, su [plan de servicio de aplicaciones](https://azure.microsoft.com/pricing/details/app-service/) debe estar en hello **básica**, **estándar**, o **Premium** capa. En este paso, asegúrese de que la aplicación web se Hola admite nivel de precios.

### <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Abra hello [portal de Azure](https://portal.azure.com).

### <a name="navigate-tooyour-web-app"></a>Navegar por la aplicación web de tooyour

Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de hello de la aplicación web.

![Seleccionar la aplicación web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

Ha llegado a página de administración de hello de la aplicación web.  

### <a name="check-hello-pricing-tier"></a>Hola de comprobación de nivel de precios

En la navegación del lado izquierdo de saludo de la página de aplicación web, desplácese toohello **configuración** sección y seleccione **escalar verticalmente (plan de servicio de aplicaciones)**.

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

Comprobar toomake seguro de que la aplicación web no está en hello **libre** o **Shared** capa. El nivel actual de la aplicación web aparece resaltado con un cuadro azul oscuro.

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

SSL personalizado no se admite en hello **libre** o **Shared** capa. Si necesita tooscale seguridad, siga los pasos de hello en la sección siguiente Hola. De lo contrario, cierre hello **elegir el nivel de precios** página y omitir demasiado[cargar y enlazar el certificado SSL](#upload).

### <a name="scale-up-your-app-service-plan"></a>Escalar verticalmente el plan de App Service

Seleccione uno de hello **básica**, **estándar**, o **Premium** niveles.

Haga clic en **Seleccionar**.

![Elegir plan de tarifa](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

Cuando vea Hola siguientes a la notificación, la operación de escalado de hello está completa.

![Notificación de escalado vertical](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>Enlazar el certificado SSL

Se está tooupload preparado su aplicación web SSL certificado tooyour.

### <a name="merge-intermediate-certificates"></a>Combinación de certificados intermedios

Si la entidad emisora de certificados ofrece varios certificados en la cadena de certificados de hello, deberá toomerge certificados de hello en orden. 

toodo esto, abra cada certificado que haya recibido en un editor de texto. 

Crear un archivo de certificado combinada de hello, denominado _mergedcertificate.crt_. En un editor de texto, copie el contenido de Hola de cada certificado en este archivo. orden de Hola de los certificados debería ser similar Hola después de plantilla:

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>Exportar certificado tooPFX

Exporte el certificado SSL combinado con clave privada de Hola que la solicitud de certificado se generó con.

Si la solicitud de certificado se genera con OpenSSL, se crea un archivo de clave privada. tooexport su tooPFX de certificado, ejecute el siguiente comando de Hola. Reemplace los marcadores de posición de hello _ &lt;archivo de clave privada >_ y _ &lt;archivo de certificado combinado >_.

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

Cuando se le pida, defina una contraseña de exportación. Deberá usar esta contraseña al cargar la SSL certificado tooApp servicio más adelante.

Si usa IIS o _Certreq.exe_ toogenerate su solicitud de certificado, la instalación Hola certificado tooyour local machine y, a continuación, [exportar Hola certificado tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).

### <a name="upload-your-ssl-certificate"></a>Cargar el certificado SSL

tooupload su certificado SSL, haga clic en **certificados SSL** Hola a la izquierda de la aplicación web.

Haga clic en **Cargar certificado**.

En **Archivo de certificado PFX**, seleccione el archivo PFX. En **contraseña del certificado**, escriba la contraseña Hola que creó al exportar el archivo PFX de Hola.

Haga clic en **Cargar**.

![Carga del certificado](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

Cuando el servicio de aplicación termina de cargar el certificado, aparece en hello **certificados SSL** página.

![Certificado cargado](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>Enlazar el certificado SSL

Hola **enlaces SSL** sección, haga clic en **Agregar enlace**.

Hola **Agregar enlace SSL** , utilice toosecure de nombre de dominio de hello listas desplegables tooselect Hola y Hola certificado toouse.

> [!NOTE]
> Si se ha cargado el certificado pero no ve los nombres de dominio de Hola Hola **Hostname** lista desplegable, pruebe a actualizar la página del explorador Hola.
>
>

En **SSL tipo**, seleccione si toouse ** [indicación de nombre de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication) ** o SSL basado en IP.

- **SSL basada en SNI**: pueden agregarse varios enlaces SSL basados en SNI. Esta opción permite que varios toosecure de certificados SSL varios dominios en hello misma dirección IP. Los exploradores más modernos (como Internet Explorer, Chrome, Firefox y Opera) admiten SNI (encontrará información de compatibilidad con exploradores más completa en [Indicación de nombre de servidor](http://wikipedia.org/wiki/Server_Name_Indication)).
- **SSL basada en IP**: solo pueden agregarse enlaces SSL basados en IP. Esta opción permite toosecure de certificados SSL solo una dirección IP pública dedicada. toosecure varios dominios, deben protegerlos todos mediante Hola mismo certificado SSL. Esta es la opción tradicional de hello para el enlace de SSL.

Haga clic en **Agregar enlace**.

![Enlazar certificado SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

Cuando el servicio de aplicación termina de cargar el certificado, aparece en hello **enlaces SSL** secciones.

![Certificado enlazado tooweb aplicación](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>Reasignar un registro D en SSL de IP

Si no usa SSL basado en IP en la aplicación web, omitir demasiado[HTTPS de prueba para su dominio personalizado](#test).

De manera predeterminada, la aplicación web usa una dirección IP pública compartida. Cuando se enlaza un certificado con SSL basada en IP, App Service crea otra dirección IP dedicada para la aplicación web.

Si ha asignado una aplicación de web de un registro tooyour, actualizar el registro de dominio con esta dirección IP nueva y dedicada.

La aplicación web **dominio personalizado** página se actualiza con la dirección IP de hello nueva y dedicada. [Copie esta dirección IP](app-service-web-tutorial-custom-domain.md#info), a continuación, [Hola de reasignación de un registro](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nueva dirección IP.

<a name="test"></a>

## <a name="test-https"></a>Probar HTTPS

Todo lo que ha dejado toodo ahora es toomake seguro de que funciona HTTPS para su dominio personalizado. En distintos exploradores, examinar demasiado`https://<your.custom.domain>` toosee que sirve de seguridad de la aplicación web.

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> Si la aplicación web genera errores de validación del certificado, probablemente se esté usando un certificado autofirmado.
>
> Si no es el caso de hello, que ha dejado los certificados intermedios al exportar el archivo PFX del certificado toohello.

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>Aplicación de HTTPS

App Service *no* exige HTTPS, por lo que cualquier usuario todavía puede acceder a la aplicación web mediante HTTP. tooenforce HTTPS para la aplicación web, definir una regla de reescritura en hello _web.config_ archivo de la aplicación web. Servicio de aplicaciones usa este archivo, independientemente del marco del lenguaje de saludo de la aplicación web.

> [!NOTE]
> Hay una redirección específica del lenguaje de las solicitudes. ASP.NET MVC puede usar hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtro en lugar de la regla de reescritura de hello en _web.config_.

Si es un desarrollador de .NET, debe estar relativamente familiarizado con este archivo. Se encuentra en la raíz de saludo de la solución.

Además, si desarrolla con PHP, Node.js, Python o Java, existe la posibilidad de que generemos este archivo en su nombre en App Service.

Conectar el punto de conexión de la aplicación web tooyour FTP siguiendo las instrucciones de hello en [implementar el servicio de aplicaciones mediante FTP/S de aplicación tooAzure](app-service-deploy-ftp.md).

Este archivo debe encontrarse en _/home/site/wwwroot_. Si no es así, cree una _web.config_ archivo en esta carpeta con hello continuación de XML:

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

Para una existente _web.config_ de archivos, copiar todo hello `<rule>` elemento en su _web.config_del `configuration/system.webServer/rewrite/rules` elemento. Si hay otras `<rule>` elementos en su _web.config_, Hola lugar copian `<rule>` elemento antes de hello otro `<rule>` elementos.

Esta regla devuelve un protocolo HTTPS de toohello HTTP 301 (Redireccionamiento) cada vez que el usuario de hello hace que una aplicación de web de tooyour de solicitud HTTP. Por ejemplo, redirige desde `http://contoso.com` demasiado`https://contoso.com`.

Para obtener más información sobre el módulo URL Rewrite para IIS de hello, vea hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentación.

## <a name="enforce-https-for-web-apps-on-linux"></a>Exigencia de HTTPS para Web Apps en Linux

App Service en Linux *no* exige HTTPS, por lo que cualquier usuario todavía puede acceder a la aplicación web mediante HTTP. tooenforce HTTPS para la aplicación web, definir una regla de reescritura en hello _.htaccess_ archivo de la aplicación web. 

Conectar el punto de conexión de la aplicación web tooyour FTP siguiendo las instrucciones de hello en [implementar el servicio de aplicaciones mediante FTP/S de aplicación tooAzure](app-service-deploy-ftp.md).

En _/home/site/wwwroot_, cree un _.htaccess_ archivo con el siguiente código de hello:

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

Esta regla devuelve un protocolo HTTPS de toohello HTTP 301 (Redireccionamiento) cada vez que el usuario de hello hace que una aplicación de web de tooyour de solicitud HTTP. Por ejemplo, redirige desde `http://contoso.com` demasiado`https://contoso.com`.

## <a name="automate-with-scripts"></a>Automatizar con scripts

Puede automatizar enlaces SSL para su aplicación web con secuencias de comandos, mediante hello [CLI de Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).

### <a name="azure-cli"></a>CLI de Azure

Hola siguiente comando carga un archivo PFX exportado y obtiene la huella digital de Hola.

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

Hello siguiente comando agrega un enlace SSL basado en SNI, con huella digital de hello del comando anterior Hola.

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

Hello siguiente comando carga un archivo PFX exportado y agrega un enlace SSL basado en SNI.

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Actualizar el plan de tarifa de la aplicación
> * Enlazar el tooApp de certificado SSL servicio personalizado
> * Implementar HTTPS en la aplicación
> * Automatizar el enlace de certificado SSL con scripts

Avanzar toohello siguiente tutorial toolearn cómo toouse red de entrega de contenido de Azure.

> [!div class="nextstepaction"]
> [Agregar un servicio de aplicaciones de Azure tooan de red de entrega de contenido (CDN)](app-service-web-tutorial-content-delivery-network.md)
