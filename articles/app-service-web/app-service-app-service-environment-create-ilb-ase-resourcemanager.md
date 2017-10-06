---
title: aaaHow tooCreate un ILB ASE usar Azure Resource Manager plantillas | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un interno cargar ASE equilibrador usando plantillas del Administrador de recursos de Azure."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>¿Cómo tooCreate un ILB ASE usar Azure Resource Manager plantillas

> [!NOTE] 
> Este artículo trata sobre Hola v1 de entorno del servicio de aplicaciones. Hay una versión más reciente de hello entorno del servicio de aplicación que es más fácil toouse y se ejecuta en una infraestructura más eficaz. toolearn más información acerca de la nueva versión de hello iniciar con hello [toohello Introducción entono](../app-service/app-service-environment/intro.md).
>

## <a name="overview"></a>Información general
Los entornos del Servicio de aplicaciones pueden crearse con una dirección de red virtual interna, en lugar de una VIP pública.  Esta dirección interna se proporciona un componente de Azure denominado equilibrador de carga interno de hello (ILB).  Un ASE ILB pueden crearse con hello portal de Azure.  También se puede crear de forma automática por medio de las plantillas de Azure Resource Manager.  En este artículo se describe los pasos de Hola y sintaxis necesario toocreate una ASE de ILB con plantillas del Administrador de recursos de Azure.

Hay tres pasos implicados en la automatización de la creación de un ASE de ILB:

1. Primer ASE de base de Hola se crea en una red virtual con una dirección de equilibrador de carga interno en lugar de una VIP pública.  Como parte de este paso, se asigna a un nombre de dominio de raíz toohello ASE de ILB.
2. Una vez cargado Hola que ase de ILB se crea, un certificado SSL.  
3. Hello cargado certificado SSL esté explícitamente asignado toohello ILB ASE como su propio certificado SSL "default".  Este certificado SSL se usará para tooapps de tráfico SSL en hello ILB ASE cuando aplicaciones Hola se direccionan con hello comunes raíz dominio asignado toohello ASE (p. ej. https://someapp.mycustomrootcomain.com)

## <a name="creating-hello-base-ilb-ase"></a>Creación de hello Base ILB ASE
Hay un ejemplo de plantilla de Azure Resource Manager y su archivo de parámetros asociado en GitHub, [aquí][quickstartilbasecreate].

La mayoría de los parámetros de Hola Hola *azuredeploy.parameters.json* archivo es comunes toocreating ambos ASEs ILB, así como ASEs enlazado VIP pública tooa.  lista de Hello aparece a continuación llama a parámetros de nota especial, o que sean únicos, cuando se crea una ASE de ILB:

* *interalLoadBalancingMode*: en la mayoría de los casos, establece este too3, lo que significa que tanto el tráfico HTTP/HTTPS en los puertos 80/443, y puertos de canal de datos de control/hello escuchan tooby servicio FTP Hola Hola ASE, tooan enlazado ILB asignará red virtual dirección interna.  Si esta propiedad se establece en su lugar too2, Hola solo servicio FTP relacionada con puertos (canales de datos y de control) se enlazarán direcciones tooan ILB mientras Hola tráfico HTTP/HTTPS, permanecerá en la VIP pública Hola.
* *sufijo DNS*: este parámetro define el dominio raíz de hello predeterminado que se va a asignar toohello ASE.  En variación pública de hello del servicio de aplicaciones de Azure, Hola raíz dominio predeterminado para todas las aplicaciones web es *azurewebsites.net*.  Sin embargo puesto que una ASE de ILB es red virtual del cliente de tooa interno, que no tiene dominio de raíz del servicio de sentido toouse Hola público predeterminado.  En su lugar, un ASE de ILB debe tener un dominio raíz predeterminado que tenga sentido usar en la red virtual interna de una compañía.  Por ejemplo, una hipotética Contoso Corporation podría usar un dominio de raíz predeterminado de *contoso.com interna* para las aplicaciones que están tooonly previsto pueden resolverse y es accesible dentro de la red virtual de Contoso. 
* *ipSslAddressCount*: este parámetro es automáticamente su valor predeterminado tooa el valor 0 en hello *azuredeploy.json* archivo porque ILB ASEs sólo tiene una única dirección ILB.  Hay direcciones IP SSL explícitos para una ASE de ILB, y por lo tanto, Hola grupo de direcciones IP SSL para un ASE ILB debe establecerse toozero, en caso contrario, se producirá un error de aprovisionamiento. 

Una vez Hola *azuredeploy.parameters.json* archivo ha sido rellenado para una ASE de ILB, Hola ASE de ILB, a continuación, pueden crearse con el siguiente fragmento de código de Powershell de Hola.  Cambiar toomatch de rutas de acceso de archivo Hola donde se encuentran los archivos de plantilla de hello Azure Resource Manager en su equipo.  Recuerde también toosupply sus propios valores para nombre de la implementación de hello Azure Resource Manager y el nombre del grupo de recursos.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Después de hello Azure Resource Manager plantilla se envía tardará unas pocas horas para hello ILB ASE toobe creado.  Después de finalizar la creación de hello, Hola ASE de ILB se mostrará en el portal de hello UX en lista de Hola de entornos del servicio de aplicación para la suscripción de Hola que desencadenó la implementación de Hola.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>Cargar y configurar Hola "Default" certificado de SSL
Una vez Hola que ase de ILB se crea un certificado SSL debe asociarse a Hola ASE como predeterminada"hello" uso de los certificados SSL para establecer tooapps de las conexiones SSL.  Siguiendo con el ejemplo de Contoso Corporation hipotético hello, si Hola de ASE DNS como valor predeterminado es de sufijo *contoso.com interna*, a continuación, una conexión demasiado*https://some-random-app.internal-contoso.com*requiere un certificado SSL válido para **.internal contoso.com*. 

Hay una variedad de formas tooobtain un certificado SSL válido como entidades de certificación internas, la adquisición de un certificado de un emisor externo y usando un certificado autofirmado.  Independientemente del origen de hello del certificado SSL de hello, hello siguientes atributos de certificado necesitan toobe configurado correctamente:

* *Asunto*: este atributo debe establecerse demasiado **.your-raíz-dominio-here.com*
* *Nombre alternativo del firmante*: este atributo debe incluir tanto **.your-raíz-dominio-here.com*, y **.scm.your-raíz-dominio-here.com*.  motivo de la segunda entrada de Hola Hola es que toohello de las conexiones SSL sitio SCM/Kudu asociado a cada aplicación se realiza mediante una dirección de formulario de hello *your-app-name.scm.your-root-domain-here.com*.

Con un certificado SSL válido, se necesitan dos pasos preparatorios adicionales.  certificado SSL de Hello debe toobe convertir/guarda como un archivo. pfx.  Recuerde ese archivo .pfx de hello necesita tooinclude todo intermedio y certificados raíz y también es necesario toobe protegido con una contraseña.

A continuación, archivo .pfx resultante de hello debe toobe convertir en una cadena base64 porque el certificado SSL de Hola se cargará usando una plantilla de Azure Resource Manager.  Puesto que las plantillas de Azure Resource Manager son archivos de texto, archivo .pfx de hello debe toobe convierten en una cadena base64 de modo que puede incluirse como un parámetro de plantilla de Hola.

Hola Powershell siguiente fragmento de código muestra un ejemplo de cómo generar un certificado autofirmado, exportar el certificado de Hola como un archivo .pfx, convertir el archivo .pfx de hello en base64 codificado cadena y, a continuación, guardar en base64 de hello archivo independiente de cadena tooa.  Hola código de Powershell para la codificación base64 se adaptó del hello [Blog de secuencias de comandos de Powershell][examplebase64encoding].

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

Una vez que se generó correctamente el certificado SSL de Hola y cadena codificada en base64 tooa convertido, Hola ejemplo de plantilla de administrador de recursos de Azure en GitHub para [configurar certificado SSL de hello predeterminado] [ configuringDefaultSSLCertificate] se puede utilizar.

Hola parámetros Hola *azuredeploy.parameters.json* archivo se enumeran a continuación:

* *appServiceEnvironmentName*: nombre de Hola de hello ASE de ILB que se está configurando.
* *existingAseLocation*: cadena de texto que contiene Hola región de Azure donde hello ASE de ILB se implementó.  Por ejemplo, "centro-sur de EE. UU.".
* *pfxBlobString*: Hola based64 codificado representación de cadena del archivo PFX de hello.  Mediante el fragmento de código de hello mostrado anteriormente, debería copiar cadena Hola incluido en "exportedcert.pfx.b64" y péguelo en como valor de Hola de hello *pfxBlobString* atributo.
* *contraseña*: Hola contraseña utilizada toosecure hello archivo.pfx.
* *certificateThumbprint*: Hola huella digital del certificado.  Si este valor se recupera desde Powershell (p. ej. *$certificate. Huella digital* de hello fragmento de código anterior), puede usar el valor de hello como-es.  Sin embargo si copia el valor de hello del cuadro de diálogo de certificado de Windows hello, recuerde toostrip out espacios Hola.  Hola *certificateThumbprint* debe ser similar: AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *nombre de certificado*: un identificador de cadena descriptivo de su propia elección usa certificados de hello tooidentity.  nombre de Hola se usa como parte del identificador único de Azure Resource Manager de Hola para hello *Microsoft.Web/certificates* entidad que representa el certificado SSL de Hola.  nombre de Hello **debe** finalizar con hello siguiente sufijo: \_yourASENameHere_InternalLoadBalancingASE.  Portal de hello usa este sufijo como un indicador que Hola certificado se utiliza para asegurar un ASE habilitado ILB.

A continuación se muestra un ejemplo abreviado de *azuredeploy.parameters.json* :

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Una vez Hola *azuredeploy.parameters.json* archivo ha sido rellenado, certificado SSL de saludo predeterminado se puede configurar con hello siguiente fragmento de código de Powershell.  Cambiar toomatch de rutas de acceso de archivo Hola donde se encuentran los archivos de plantilla de hello Azure Resource Manager en su equipo.  Recuerde también toosupply sus propios valores para nombre de la implementación de hello Azure Resource Manager y el nombre del grupo de recursos.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Después de hello Azure Resource Manager plantilla se envía tardará aproximadamente cuarenta minutos minutos por cambio Hola de ASE tooapply front-end.  Por ejemplo, su valor predeterminado es ASE tamaño con dos servidores front-end, plantilla de Hola tomará alrededor de una hora y toocomplete de veinte minutos.  Mientras se ejecuta la plantilla de Hola Hola ASE no estará tooscaled pueda.  

Una vez completada la plantilla de hello, aplicaciones en hello ILB ASE son accesibles a través de HTTPS y las conexiones de Hola se protegerán con certificado SSL de hello predeterminado.  certificado SSL de Hello predeterminado se usará cuando las aplicaciones en hello ASE de ILB se direccionan con una combinación de nombre de la aplicación hello más el nombre de host de hello predeterminado.  Por ejemplo *https://mycustomapp.internal-contoso.com* usaría el certificado SSL predeterminado de Hola para **.internal contoso.com*.

Sin embargo, como aplicaciones que se ejecutan en el servicio de varios inquilinos públicos de hello, los programadores pueden configurar también los nombres de host personalizado para aplicaciones individuales y, a continuación, configurar los enlaces de certificado SSL SNI únicos para las aplicaciones individuales.  

## <a name="getting-started"></a>Introducción
tooget iniciado con el entorno de servicio de aplicación, consulte [Introducción tooApp entorno del servicio](app-service-app-service-environment-intro.md)

Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

