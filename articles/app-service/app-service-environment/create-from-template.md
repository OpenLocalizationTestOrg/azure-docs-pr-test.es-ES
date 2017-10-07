---
title: aaaCreate un entorno de servicio de aplicaciones de Azure mediante una plantilla de administrador de recursos
description: "Explica cómo toocreate un entorno externo o servicio de aplicaciones de Azure de ILB mediante una plantilla de administrador de recursos"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>Creación de una instancia de ASE mediante el uso de una plantilla de Azure Resource Manager

## <a name="overview"></a>Información general
Las instancias de Azure App Service Environment (ASE) pueden crearse con un punto de conexión accesible de Internet o un punto de conexión en una dirección interna en una red virtual de Azure (VNet). Cuando se crea con un punto de conexión interno, ese punto de conexión siempre lo proporciona un componente de Azure denominado equilibrador de carga interno (ILB). Hola ASE en una dirección IP interna se denomina una ASE de ILB. Hola ASE con un punto de conexión público se denomina un ASE externo. 

Un ASE puede crearse mediante el uso de Hola portal de Azure o una plantilla de Azure Resource Manager. Este artículo le guía a través de pasos de Hola y sintaxis necesita toocreate un ASE externo o ASE de ILB con plantillas de administrador de recursos. toolearn toocreate un ASE Hola portal de Azure, vea [realizar una ASE externo] [ MakeExternalASE] o [realizar una ASE de ILB][MakeILBASE].

Cuando se crea un ASE Hola portal de Azure, puede crear la red virtual en hello al mismo tiempo o elija un toodeploy de red virtual preexistente en. Cuando crea un ASE desde una plantilla, debe comenzar por: 

* Una red virtual de Resource Manager.
* Una subred de esa red virtual. Se recomienda un tamaño de la subred de ASE de `/25` con el crecimiento futuro de 128 direcciones tooaccomodate. Después de crea ASE hello, no se puede cambiar tamaño de Hola.
* Hola Id. de recurso de la red virtual. Puede obtener esta información de hello portal de Azure en las propiedades de red virtual.
* suscripción de Hola que desea toodeploy en.
* ubicación de Hello toodeploy en la que desea.

tooautomate la creación de ASE:

1. Crear Hola ASE desde una plantilla. Si crea un ASE externo, habrá terminado después de este paso. Si crea una ASE de ILB, existen unos toodo cosas más.

2. Una vez creado el ASE con un ILB, se carga un certificado SSL que coincide con su dominio de ASE con un ILB.

3. Hello cargado certificado SSL esté asignado toohello ILB ASE como su propio certificado SSL "default".  Este certificado se usa para tooapps de tráfico SSL en hello ASE de ILB cuando utiliza el dominio raíz común hello es ASE toohello asignado (por ejemplo, https://someapp.mycustomrootcomain.com).


## <a name="create-hello-ase"></a>Crear Hola ASE
En GitHub, encontrará [un ejemplo][quickstartasev2create] de plantilla de Resource Manager que crea un ASE y su archivo de parámetros asociado.

Si desea toomake una ASE de ILB, use estas plantillas de administrador de recursos [ejemplos][quickstartilbasecreate]. Atienden toothat caso de uso. La mayoría de los parámetros de Hola Hola *azuredeploy.parameters.json* archivo son comunes toohello creación de ILB ASEs y ASEs externo. Hello lista siguiente llama a los parámetros de nota especial, o que son únicos, cuando se crea una ASE de ILB:

* *interalLoadBalancingMode*: en la mayoría de los casos, establezca este too3, lo que significa que tanto el tráfico HTTP/HTTPS en los puertos 80/443, y puertos de canal de datos de control/hello escuchaba tooby servicio FTP Hola Hola ASE, será asignado ILB tooan enlazados de red virtual dirección interna. Si esta propiedad se establece too2, puertos de relacionados con el servicio de hello FTP (canales de datos y de control) solo son direcciones ILB tooan enlazado. Hola tráfico HTTP/HTTPS permanece en Hola pública VIP.
* *sufijo DNS*: este parámetro define el dominio raíz de hello predeterminado que está asignado toohello ASE. En variación pública de hello del servicio de aplicaciones de Azure, Hola raíz dominio predeterminado para todas las aplicaciones web es *azurewebsites.net*. Dado que una ASE de ILB es red virtual del cliente de tooa interno, que no tiene dominio de raíz del servicio de sentido toouse Hola público predeterminado. En su lugar, un ASE de ILB debe tener un dominio raíz predeterminado que tenga sentido usar en la red virtual interna de una compañía. Por ejemplo, Contoso Corporation podría usar un dominio de raíz predeterminado de *contoso.com interna* para las aplicaciones que están toobe previsto pueda resolverse y accesible únicamente dentro de la red virtual de Contoso. 
* *ipSslAddressCount*: este parámetro establece de forma automática tooa el valor 0 en hello *azuredeploy.json* archivo porque ILB ASEs sólo tiene una única dirección ILB. No hay direcciones IP-SSL explícitas para un ASE con ILB. Por lo tanto, se debe establecer Hola grupo de direcciones IP SSL para un ASE ILB toozero. En caso contrario, se produce un error de aprovisionamiento. 

Después de hello *azuredeploy.parameters.json* se llena el archivo, cree Hola ASE mediante el uso de fragmento de código de PowerShell de Hola. Cambiar Hola archivo rutas de acceso toomatch Hola Administrador de recursos de archivo de plantilla ubicaciones en su equipo. Recuerde toosupply sus propios valores para nombre de implementación del Administrador de recursos de Hola y el nombre de grupo de recursos de hello:

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Tarda aproximadamente una hora Hola ASE toobe creado. A continuación, Hola ASE mostrarán en portal de hello en lista de Hola de ASEs para la suscripción de Hola que desencadenó la implementación de Hola.

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>Cargar y configurar un certificado SSL de Hola "default"
Un certificado SSL debe asociarse con hello ASE como Hola "default" certificado SSL usado tooestablish SSL conexiones tooapps. Si el sufijo DNS de Hola de ASE predeterminada es *contoso.com interna*, un toohttps://some-random-app.internal-contoso.com conexión requiere un certificado SSL válido para **.internal contoso.com* . 

Obtenga un certificado SSL válido a través de las autoridades de certificados internas, adquiriendo un certificado de un emisor externo o usando un certificado autofirmado. Independientemente del origen de hello del certificado SSL de hello, Hola siguientes atributos de certificado debe estar configurado correctamente:

* **Asunto**: este atributo debe establecerse demasiado **.your-raíz-dominio-here.com*.
* **Nombre alternativo del firmante**: este atributo debe incluir tanto **.your-root-domain-here.com* como **.scm.your-root-domain-here.com*. Toohello de las conexiones SSL sitio SCM/Kudu asociado a cada aplicación usa una dirección del formulario de hello *your-app-name.scm.your-root-domain-here.com*.

Con un certificado SSL válido, se necesitan dos pasos preparatorios adicionales. Certificado SSL de Hola de Convert/Guardar como un archivo. pfx. Recuerde ese archivo .pfx de hello debe incluir todos los intermedio y raíz certificados. Protéjalo con una contraseña.

archivo .pfx de Hello debe toobe convertir en una cadena base64 porque el certificado SSL de Hola se carga mediante una plantilla de administrador de recursos. Dado que las plantillas de administrador de recursos son archivos de texto, archivo .pfx de hello debe convertirse en una cadena de base64. De esta forma que se puede incluir como un parámetro de plantilla de Hola.

Usar hello siguiente fragmento de código de PowerShell:

* Generar un certificado autofirmado.
* Exporte el certificado de Hola como un archivo. pfx.
* Convertir archivo .pfx de hello en una cadena codificada en base64.
* Guardar archivo independiente de hello cadena codificada en base64 tooa. 

Este código de PowerShell para la codificación base64 se adaptó del hello [blog de secuencias de comandos de PowerShell][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Después de certificado SSL de Hola se genera correctamente y convertir la cadena con codificación base64 de tooa, usar plantilla de administrador de recursos de ejemplo de Hola [certificado SSL de configurar Hola predeterminado] [ quickstartconfiguressl] en GitHub. 

Hola parámetros Hola *azuredeploy.parameters.json* archivo se muestran aquí:

* *appServiceEnvironmentName*: nombre de Hola de hello ASE de ILB que se está configurando.
* *existingAseLocation*: cadena de texto que contiene Hola región de Azure donde hello ASE de ILB se implementó.  Por ejemplo: "Centro-Sur de EE.UU.".
* *pfxBlobString*: Hola representación en forma de cadena codificada en based64 del archivo .pfx de Hola. Use el fragmento de código de hello mostrado anteriormente y copie cadena Hola incluido en "exportedcert.pfx.b64". Péguelo como valor de Hola de hello *pfxBlobString* atributo.
* *contraseña*: Hola contraseña utilizada toosecure hello archivo.pfx.
* *certificateThumbprint*: Hola huella digital del certificado. Si este valor se recupera desde PowerShell (por ejemplo, *$certificate. Huella digital* de hello fragmento de código anterior), puede usar el valor de hello tal cual. Si copia el valor de Hola desde el cuadro de diálogo de certificado de Windows hello, recuerde toostrip out espacios Hola. Hola *certificateThumbprint* debería ser similar a AF3143EB61D43F6727842115BB7F17BBCECAECAE.
* *nombre de certificado*: un identificador de cadena descriptivo de su propia elección usa certificados de hello tooidentity. nombre de Hola se usa como parte del identificador de administrador de recursos de Hola para hello *Microsoft.Web/certificates* entidad que representa el certificado SSL de Hola. nombre de Hello *debe* finalizar con hello siguiente sufijo: \_yourASENameHere_InternalLoadBalancingASE. Hola portal de Azure usa este sufijo como un indicador que Hola certificado es toosecure usado un ASE habilitado ILB.

Aquí se muestra un ejemplo abreviado de *azuredeploy.parameters.json* :

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

Después de hello *azuredeploy.parameters.json* se llena el archivo, configure el certificado SSL de hello predeterminado mediante el uso de fragmento de código de PowerShell de Hola. Cambiar toomatch de rutas de acceso de archivo Hola donde se encuentran los archivos de plantilla del Administrador de recursos de hello en su equipo. Recuerde toosupply sus propios valores para nombre de implementación del Administrador de recursos de Hola y el nombre de grupo de recursos de hello:

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Se tarda aproximadamente 40 minutos por cambio de ASE front-end tooapply Hola. Por ejemplo, para un ASE tamaño predeterminado que usa dos servidores front-end, plantilla de hello toma alrededor de una hora y toocomplete de 20 minutos. Mientras se ejecuta la plantilla de hello, no se puede escalar Hola ASE.  

Una vez finalizada la plantilla de hello, aplicaciones en hello ASE de ILB pueden tener acceso a través de HTTPS. las conexiones de Hello están protegidas mediante el uso de certificado SSL de hello predeterminado. certificado SSL de Hello predeterminado se utiliza cuando las aplicaciones en hello ASE de ILB se direccionan mediante una combinación de nombre de la aplicación hello más el nombre de host predeterminado de Hola. Por ejemplo, https://mycustomapp.internal-contoso.com utiliza el certificado SSL predeterminado de Hola para **.internal contoso.com*.

Sin embargo, al igual que las aplicaciones que se ejecutan en el servicio de varios inquilinos públicos de hello, los desarrolladores pueden configurar los nombres de host personalizados para las aplicaciones individuales. También pueden configurar enlaces de certificado SSL SNI únicos para las aplicaciones individuales.

## <a name="app-service-environment-v1"></a>App Service Environment v1 ##
App Service Environment tiene dos versiones: ASEv1 y ASEv2. Hola información anterior se basa en ASEv2. Esta sección se muestra hello diferencias entre ASEv1 y ASEv2.

En ASEv1, administre todos los recursos de hello manualmente. Que incluye servidores front-end de hello, los trabajadores y direcciones IP usadas para SSL basado en IP. Antes de que puede escalar horizontalmente su plan de servicio de aplicaciones, se debe escalar grupo de trabajo de Hola que desea que toohost lo.

ASEv1 utiliza un modelo de precios diferente al de ASEv2. En ASEv1, paga por cada núcleo asignado. Esto incluye los núcleos que usan para los servidores front-end y trabajos que no hospedan ninguna carga de trabajo. En ASEv1, tamaño de escala máximo predeterminado de Hola de un ASE es 55 total de hosts. Esto incluye servidores front-end y trabajos. Una tooASEv1 ventaja es que se puede implementar en una red virtual clásica y una red virtual del Administrador de recursos. toolearn más información sobre ASEv1, consulte [introducción de v1 entono][ASEv1Intro].

toocreate un ASEv1 mediante una plantilla de administrador de recursos, consulte [crear un v1 ASE de ILB con una plantilla de administrador de recursos][ILBASEv1Template].


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
