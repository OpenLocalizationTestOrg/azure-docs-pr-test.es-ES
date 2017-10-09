---
title: aaaIntegrate DNS de Azure con los recursos de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse DNS de Azure a lo largo de tooprovide DNS para los recursos de Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>Usar la configuración de dominio personalizado de tooprovide de DNS de Azure para un servicio de Azure

Azure DNS proporciona DNS para un dominio personalizado de cualquiera de los recursos de Azure que admiten dominios personalizados o que tienen un nombre de dominio completo (FQDN). Un ejemplo es tiene una aplicación web de Azure y desea que los usuarios tooaccess; para ello ya sea mediante contoso.com o www.contoso.com como un FQDN. Este artículo le guiará a través de la configuración del servicio de Azure con Azure DNS para usar dominios personalizados.

## <a name="prerequisites"></a>Requisitos previos

En orden toouse DNS de Azure para su dominio personalizado, se debe delegar su tooAzure de dominio DNS. Visite [delegar un tooAzure de dominio DNS](./dns-delegate-domain-azure-dns.md) para obtener instrucciones sobre cómo tooconfigure sus servidores de nombres para la delegación. Una vez que el dominio es delegado tooyour zona de DNS de Azure, son registros de DNS de hello tooconfigure pueda necesarios.

Puede configurar un dominio personal o personalizado para [aplicaciones de función de Azure](#azure-function-app), [IoT de Azure](#azure-iot), [direcciones IP públicas](#public-ip-address), [App Service (Web Apps)](#app-service-web-apps), [Blob Storage](#blob-storage) y [Azure CDN](#azure-cdn).

## <a name="azure-function-app"></a>Aplicación de función de Azure

tooconfigure un dominio personalizado para las aplicaciones de Azure de función, se crea un registro CNAME, así como la configuración en la propia aplicación de función hello.
 
Navegue demasiado**otros** > **aplicación de la función** y seleccione la aplicación de la función. Haga clic en **Características de la plataforma** y en **REDES** haga clic en **Dominios personalizados**.

![hoja de aplicación de función](./media/dns-custom-domain/functionapp.png)

Observe la dirección url actual de hello en hello **los dominios personalizados** hoja, esta dirección se utiliza como alias de Hola para registro DNS de hello creado.

![Hoja Dominios personalizados](./media/dns-custom-domain/functionshostname.png)

Navegar por la zona de DNS de tooyour y haga clic en **+ grabar conjunto**. Rellene Hola siguiente información en hello **Agregar conjunto de registros** hoja y haga clic en **Aceptar** toocreate lo.

|Propiedad  |Valor  |Descripción  |
|---------|---------|---------|
|Nombre     | myfunctionapp        | Este valor junto con la etiqueta de nombre de dominio de hello es hello FQDN para el nombre de dominio personalizado de Hola.        |
|Tipo     | CNAME        | Use un registro CNAME que use un alias.        |
|TTL     | 1        | 1 se usa para 1 hora        |
|Unidad de TTL     | Horas        | Horas se usan como medida del tiempo de Hola         |
|Alias     | adatumfunction.azurewebsites.net        | nombre DNS de Hello va a crear alias de hello, en este ejemplo es el nombre DNS de hello adatumfunction.azurewebsites.net proporcionada por la aplicación de función de toohello predeterminado.        |

Desplácese atrás tooyour función aplicación, haga clic en **características de la plataforma**y, en **red** haga clic en **dominios personalizados**, a continuación, en **losnombresdehost**haga clic en **+ Agregar nombre de host**.

En hello **Agregar nombre de host** hoja, escriba el registro CNAME de Hola Hola **hostname** campo de texto y haga clic en **validar**. Si el registro de hello era toobe capaz de encontrar, Hola **Agregar nombre de host** aparece el botón. Haga clic en **Agregar nombre de host** alias de hello tooadd.

![hoja agregar nombre de host de aplicaciones de función](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>Azure IoT

IoT de Azure no tiene cualquier personalización que es necesarias en el propio servicio Hola. se necesita toouse un dominio personalizado con un centro de IoT solo un registro CNAME que señala toohello recursos.

Navegue demasiado**Internet de las cosas** > **centro de IoT** y seleccione el centro de IoT. En hello **Introducción** hoja, Hola Nota FQDN del centro de IoT Hola.

![Hoja del Centro de IoT](./media/dns-custom-domain/iot.png)

A continuación, navegue tooyour zona de DNS y haga clic en **+ grabar conjunto**. Rellene Hola siguiente información en hello **Agregar conjunto de registros** hoja y haga clic en **Aceptar** toocreate lo.


|Propiedad  |Valor  |Descripción  |
|---------|---------|---------|
|Nombre     | myiothub        | Este valor junto con la etiqueta de nombre de dominio de hello es hello FQDN para el centro de IoT de Hola.        |
|Tipo     | CNAME        | Use un registro CNAME que use un alias.
|TTL     | 1        | 1 se usa para 1 hora        |
|Unidad de TTL     | Horas        | Horas se usan como medida del tiempo de Hola         |
|Alias     | adatumIOT.azure-devices.net        | nombre DNS de Hello va a crear alias de hello, en este ejemplo es el nombre de host de hello adatumIOT.azure devices.net proporcionado por el centro de IoT Hola.

Una vez que se crea el registro de hello, probar la resolución de nombres con el uso de registro CNAME de Hola`nslookup`

## <a name="public-ip-address"></a>Dirección IP pública

tooconfigure un dominio personalizado para los servicios que utilizan una IP pública redirigir recursos como puerta de enlace de aplicaciones, el equilibrador de carga, servicio de nube, máquinas virtuales del Administrador de recursos, y, utilizan las máquinas virtuales clásico, un registro CNAME.

Navegue demasiado**red** > **dirección IP pública**, seleccione el recurso de dirección IP pública de Hola y haga clic en **configuración**. Anote la dirección IP de hello mostrada.

![hoja ip pública](./media/dns-custom-domain/publicip.png)

Navegar por la zona de DNS de tooyour y haga clic en **+ grabar conjunto**. Rellene Hola siguiente información en hello **Agregar conjunto de registros** hoja y haga clic en **Aceptar** toocreate lo.


|Propiedad  |Valor  |Descripción  |
|---------|---------|---------|
|Nombre     | mywebserver        | Este valor junto con la etiqueta de nombre de dominio de hello es hello FQDN para el nombre de dominio personalizado de Hola.        |
|Tipo     | Una         | Use un registro como recurso de hello es una dirección IP.        |
|TTL     | 1        | 1 se usa para 1 hora        |
|Unidad de TTL     | Horas        | Horas se usan como medida del tiempo de Hola         |
|Dirección IP     | <your ip address>       | dirección IP pública de Hola.|

![creación de un registro A](./media/dns-custom-domain/arecord.png)

Una vez que se crea el registro de hello A, ejecute `nslookup` toovalidate Hola resuelve.

![búsqueda de dns de dirección ip pública](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>App Service (Web Apps)

Hello siguientes pasos le guiarán configurar un dominio personalizado para una aplicación de servicio de aplicaciones web.

Navegue demasiado**Web y móviles** > **servicio de aplicaciones** y seleccione el recurso de Hola que va a configurar un nombre de dominio personalizado y haga clic en **los dominios personalizados**.

Observe la dirección url actual de hello en hello **los dominios personalizados** hoja, esta dirección se utiliza como alias de Hola para registro DNS de hello creado.

![hoja dominios personalizados](./media/dns-custom-domain/url.png)

Navegar por la zona de DNS de tooyour y haga clic en **+ grabar conjunto**. Rellene Hola siguiente información en hello **Agregar conjunto de registros** hoja y haga clic en **Aceptar** toocreate lo.


|Propiedad  |Valor  |Descripción  |
|---------|---------|---------|
|Nombre     | mywebserver        | Este valor junto con la etiqueta de nombre de dominio de hello es hello FQDN para el nombre de dominio personalizado de Hola.        |
|Tipo     | CNAME        | Use un registro CNAME que use un alias. Si el recurso de hello usa una dirección IP, se usaría un registro.        |
|TTL     | 1        | 1 se usa para 1 hora        |
|Unidad de TTL     | Horas        | Horas se usan como medida del tiempo de Hola         |
|Alias     | webserver.azurewebsites.net        | nombre DNS de Hello va a crear alias de hello, en este ejemplo es el nombre DNS de hello webserver.azurewebsites.net proporcionada por la aplicación web de toohello de forma predeterminada.        |


![Crear un registro CNAME](./media/dns-custom-domain/createcnamerecord.png)

Navegue toohello back-servicio de aplicaciones que está configurado para el nombre de dominio personalizado de Hola. Haga clic en **Dominios personalizados** y, a continuación, en **Nombres de host**. registro CNAME de hello tooadd que ha creado, haga clic en **+ Agregar nombre de host**.

![Figura 1](./media/dns-custom-domain/figure1.png)

Una vez completado el proceso de hello, ejecute **nslookup** toovalidate resolución de nombres funciona.

![Figura 1](./media/dns-custom-domain/finalnslookup.png)

visite toolearn más información acerca de la asignación de un servicio, de dominio personalizado tooApp [asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).

Si necesita toopurchase un dominio personalizado, visite [comprar un nombre de dominio personalizado para aplicaciones Web de Azure](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn más acerca de los dominios de servicio de aplicaciones.

## <a name="blob-storage"></a>Almacenamiento de blobs

Hello siguientes pasos le guiarán configurar un registro CNAME para una cuenta de almacenamiento blob mediante el método de hello asverify. Este método garantiza que no hay ningún tiempo de inactividad.

Navegue demasiado**almacenamiento** > **cuentas de almacenamiento**, seleccione la cuenta de almacenamiento y haga clic en **dominio personalizado**. Indicar la existencia de hello FQDN en el paso 2, este valor se utiliza toocreate Hola primer registro CNAME

![dominio personalizado de blob storage](./media/dns-custom-domain/blobcustomdomain.png)

Navegar por la zona de DNS de tooyour y haga clic en **+ grabar conjunto**. Rellene Hola siguiente información en hello **Agregar conjunto de registros** hoja y haga clic en **Aceptar** toocreate lo.


|Propiedad  |Valor  |Descripción  |
|---------|---------|---------|
|Nombre     | asverify.mystorageaccount        | Este valor junto con la etiqueta de nombre de dominio de hello es hello FQDN para el nombre de dominio personalizado de Hola.        |
|Tipo     | CNAME        | Use un registro CNAME que use un alias.        |
|TTL     | 1        | 1 se usa para 1 hora        |
|Unidad de TTL     | Horas        | Horas se usan como medida del tiempo de Hola         |
|Alias     | asverify.adatumfunctiona9ed.blob.core.windows.net        | nombre DNS de Hello va a crear alias de hello, en este ejemplo es el nombre DNS de hello asverify.adatumfunctiona9ed.blob.core.windows.net proporcionada por cuenta de almacenamiento de toohello de forma predeterminada.        |

Navegar por la cuenta de almacenamiento back-tooyour haciendo clic en **almacenamiento** > **cuentas de almacenamiento**, seleccione la cuenta de almacenamiento y haga clic en **dominio personalizado**. Tipo Hola alias que ha creado sin prefijo de asverify de hello en cuadro de texto hello comprobación ** usar validación CNAME indirecta y haga clic en **guardar**. Una vez completado este paso, devolver tooyour zona DNS y cree un registro CNAME sin prefijo de hello asverify.  Después de ese punto, es seguro toodelete Hola registro CNAME con prefijo de cdnverify Hola.

![dominio personalizado de blob storage](./media/dns-custom-domain/indirectvalidate.png)

Valide la resolución de DNS mediante la ejecución de `nslookup`

toolearn más acerca de cómo asignar un punto de conexión de almacenamiento de blobs de dominio personalizado tooa, visite [configurar un nombre de dominio personalizado para el extremo de almacenamiento Blob](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>Red CDN de Azure

Hello siguientes pasos le guiarán configurar un registro CNAME para un punto de conexión de red CDN mediante el método de hello cdnverify. Este método garantiza que no hay ningún tiempo de inactividad.

Navegue demasiado**red** > **perfiles de red CDN**, seleccione el perfil de CDN y haga clic en **extremos** en **General**.

Seleccionar punto de conexión de hello trabaja con y haga clic en **+ dominio personalizado**. Hola Nota **nombre de host del punto de conexión** que este valor sea el registro de hello ese registro CNAME Hola apunta a.

![Dominio personalizado de CDN](./media/dns-custom-domain/endpointcustomdomain.png)

Navegar por la zona de DNS de tooyour y haga clic en **+ grabar conjunto**. Rellene Hola siguiente información en hello **Agregar conjunto de registros** hoja y haga clic en **Aceptar** toocreate lo.

|Propiedad  |Valor  |Descripción  |
|---------|---------|---------|
|Nombre     | cdnverify.mycdnendpoint        | Este valor junto con la etiqueta de nombre de dominio de hello es hello FQDN para el nombre de dominio personalizado de Hola.        |
|Tipo     | CNAME        | Use un registro CNAME que use un alias.        |
|TTL     | 1        | 1 se usa para 1 hora        |
|Unidad de TTL     | Horas        | Horas se usan como medida del tiempo de Hola         |
|Alias     | cdnverify.adatumcdnendpoint.azureedge.net        | nombre DNS de Hello va a crear alias de hello, en este ejemplo es el nombre DNS de hello cdnverify.adatumcdnendpoint.azureedge.net proporcionada por cuenta de almacenamiento de toohello de forma predeterminada.        |

Navegar por extremo de red CDN tooyour atrás haciendo clic en **red** > **perfiles de red CDN**y seleccione el perfil de CDN. Haga clic en **+ dominio personalizado** y escriba el alias de registro CNAME sin prefijo de cdnverify hello y haga clic en **agregar**.

Una vez completado este paso, devolver tooyour zona DNS y cree un registro CNAME sin prefijo de cdnverify Hola.  Después de ese punto, es seguro toodelete Hola registro CNAME con prefijo de cdnverify Hola. Para obtener más información sobre la red CDN y cómo tooconfigure un dominio personalizado sin paso de registro intermedio de hello visite [dominio personalizado de CDN de Azure de mapa tooa contenido](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[configurar DNS inverso para los servicios hospedados en Azure](dns-reverse-dns-for-azure-services.md).
