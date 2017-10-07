---
title: aaaMap un DNS personalizado existente nombre de las aplicaciones Web tooAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooadd un dominio DNS personalizado existente nombre de aplicación de web (dominio personal) tooa, back-end de aplicación móvil o aplicación de API de servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web

[Azure Web Apps](app-service-web-overview.md) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático. Este tutorial muestra cómo toomap un DNS personalizado existente nombre tooAzure las aplicaciones Web.

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Asignar un subdominio (por ejemplo, `www.contoso.com`) mediante el uso de un registro CNAME
> * Asignar un dominio raíz (por ejemplo, `contoso.com`) mediante el uso de un registro D
> * Asignar un dominio con comodín (por ejemplo, `*.contoso.com`) mediante el uso de un registro CNAME
> * Automatizar la asignación de dominio con scripts

Puede usar un **registro CNAME** o un **un registro** toomap un DNS personalizado nombre tooApp servicio. 

> [!NOTE]
> Se recomienda usar un CNAME para todos los nombres DNS personalizados, excepto un dominio raíz (por ejemplo, `contoso.com`).

toomigrate un sitio en vivo y su nombre de dominio DNS tooApp servicio, consulte [migrar un tooAzure de nombre DNS servicio de aplicaciones active](app-service-custom-domain-name-migrate.md).

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

* [Cree una aplicación de App Service](/azure/app-service/) o use alguna aplicación que haya creado para otro tutorial.
* Comprar un nombre de dominio y asegúrese de que dispone del registro DNS de acceso toohello para su proveedor de dominio (por ejemplo, GoDaddy).

  Por ejemplo, tooadd entradas DNS para `contoso.com` y `www.contoso.com`, debe ser la configuración de DNS de hello tooconfigure capaz de hello `contoso.com` dominio raíz.

  > [!NOTE]
  > Si no tiene un dominio existente de nombres, considere la posibilidad de [comprar un dominio con Hola portal de Azure](custom-dns-web-site-buydomains-web-app.md). 

## <a name="prepare-hello-app"></a>Preparar la aplicación hello

toomap una personalizado DNS nombre tooa la aplicación web, aplicación web de hello [plan de servicio de aplicaciones](https://azure.microsoft.com/pricing/details/app-service/) debe ser una capa de pagada (**Shared**, **básica**, **estándar**, o  **Premium**). En este paso, asegúrese de que ese servicio de aplicaciones de aplicación se encuentre en Hola Hola admite el nivel de precios.

### <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure

Abra hello [portal de Azure](https://portal.azure.com) e inicie sesión con su cuenta de Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Navegue toohello aplicación Hola portal de Azure

En el menú izquierdo de hello, seleccione **servicios de aplicaciones**y, a continuación, seleccione nombre de Hola de aplicación hello.

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/select-app.png)

Verá que la página de administración de Hola de hello aplicación de servicio de aplicaciones.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>Hola de comprobación de nivel de precios

Hola a la izquierda de la página de la aplicación hello, desplácese toohello **configuración** sección y seleccione **escalar verticalmente (plan de servicio de aplicaciones)**.

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

nivel actual de la aplicación Hello aparece resaltado por un borde azul. Compruebe que dicha aplicación hello no esté en hello toomake **libre** capa. DNS personalizado no se admite en hello **libre** capa. 

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Si hello plan de servicio de aplicaciones no es **libre**, cierre hello **elegir el nivel de precios** página y omitir demasiado[asignar un registro CNAME](#cname).

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>Escalar verticalmente Hola plan de servicio de aplicaciones

Seleccione cualquiera de los niveles de hello no disponibles (**Shared**, **básica**, **estándar**, o **Premium**). 

Haga clic en **Seleccionar**.

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Cuando vea Hola siguientes a la notificación, la operación de escalado de hello está completa.

![Confirmación de la operación de escalado](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>Asignar un registro CNAME

En el ejemplo hello del tutorial, agregará un registro CNAME para hello `www` subdominio (por ejemplo, `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Crear registro CNAME Hola

Agregar un toomap registro CNAME en el nombre de host de la aplicación de toohello subdominio predeterminado (`<app_name>.azurewebsites.net`).

Para hello `www.contoso.com` ejemplo de un dominio, agregue un registro CNAME que asigna nombre hello `www` demasiado`<app_name>.azurewebsites.net`.

Después de agregar Hola CNAME, página de registros DNS de hello aspecto Hola siguiente ejemplo:

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Habilitar asignación de registro CNAME de hello en Azure

Hola dejado de navegación de página de la aplicación Hola Hola portal de Azure, seleccione **los dominios personalizados**. 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Hola **los dominios personalizados** página de la aplicación hello, agregar Hola personalizado nombre DNS completo (`www.contoso.com`) toohello lista.

Seleccione hello  **+**  icono siguiente demasiado**Agregar nombre de host**.

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Nombre de dominio completo de tipo hello que ha agregado un registro CNAME, como `www.contoso.com`. 

Seleccione **Validar**.

Hola **Agregar nombre de host** se activa el botón. 

Asegúrese de que **tipo de registro de nombre de host** se establece demasiado**CNAME (www.example.com o cualquier subdominio)**.

Seleccione **Agregar nombre de host**.

![Agregar aplicación de toohello de nombre DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Puede tardar algún tiempo Hola nuevo nombre de host toobe reflejado en la aplicación hello **los dominios personalizados** página. Intente actualizar los datos de saludo explorador tooupdate Hola.

![Registro CNAME agregado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Si falta un paso o cometió un alguna versión anterior, verá un error de comprobación en parte inferior de Hola de página Hola.

![Error de comprobación](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>Asignar un registro A

En el ejemplo de tutorial de hello, agregar un registro a para el dominio raíz de hello (por ejemplo, `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Copie la dirección IP de la aplicación hello

toomap un registro, necesita la dirección IP externa de la aplicación hello. Puede encontrar esta dirección IP en la aplicación hello **los dominios personalizados** página Hola portal de Azure.

Hola dejado de navegación de página de la aplicación Hola Hola portal de Azure, seleccione **los dominios personalizados**. 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Hola **los dominios personalizados** página, copie la dirección IP de la aplicación hello.

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Crear registro Hola

toomap un registro tooan aplicación, servicio de aplicaciones requiere **dos** registros DNS:

- Un **A** registrar la dirección IP de la aplicación de toomap toohello.
- A **TXT** registrar el nombre de host de la aplicación de toomap toohello predeterminado `<app_name>.azurewebsites.net`. Servicio de aplicaciones usa este registro solo durante la configuración, tooverify que posee el dominio personalizado de Hola. Después de que el dominio personalizado se valida y se configura en App Service, puede eliminar el registro TXT. 

Para hello `contoso.com` ejemplo de un dominio, crear registros de A y TXT Hola según toohello en la tabla siguiente (`@` normalmente representa Hola dominio raíz). 

| Tipo de registro | Host | Valor |
| - | - | - |
| Una  | `@` | Dirección IP de [dirección IP de la aplicación de copia Hola](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

Cuando se agregan registros hello, Hola página de registros DNS es similar a Hola siguiente ejemplo:

![Página de registros DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Habilitar una asignación de registro de la aplicación hello Hola

En la aplicación hello **los dominios personalizados** página Hola portal de Azure, agregue Hola personalizado nombre DNS completo (por ejemplo, `contoso.com`) toohello lista.

Seleccione hello  **+**  icono siguiente demasiado**Agregar nombre de host**.

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

Nombre de dominio completo de tipo hello que ha configurado como registro de hello A, `contoso.com`.

Seleccione **Validar**.

Hola **Agregar nombre de host** se activa el botón. 

Asegúrese de que **tipo de registro de nombre de host** se establece demasiado**un registro (ejemplo.com)**.

Seleccione **Agregar nombre de host**.

![Agregar aplicación de toohello de nombre DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Puede tardar algún tiempo Hola nuevo nombre de host toobe reflejado en la aplicación hello **los dominios personalizados** página. Intente actualizar los datos de saludo explorador tooupdate Hola.

![Registro D agregado](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

Si falta un paso o cometió un alguna versión anterior, verá un error de comprobación en parte inferior de Hola de página Hola.

![Error de comprobación](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>Asignar un dominio con caracteres comodín

En el ejemplo de tutorial de hello, asigne un [nombre DNS de carácter comodín](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (por ejemplo, `*.contoso.com`) toohello aplicación de servicio de aplicaciones mediante la adición de un registro CNAME. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Crear registro CNAME Hola

Agregar un toomap registro CNAME en el nombre de host de la aplicación toohello de nombre de carácter comodín predeterminado (`<app_name>.azurewebsites.net`).

Para hello `*.contoso.com` ejemplo de un dominio, Hola registro CNAME asignará el nombre de hello `*` demasiado`<app_name>.azurewebsites.net`.

Cuando se agrega Hola CNAME, Hola página de registros DNS es similar a Hola siguiente ejemplo:

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Habilitar asignación de registro CNAME de hello en la aplicación hello

Ahora puede agregar cualquier subdominio que coincida con la aplicación de hello comodín nombre toohello (por ejemplo, `sub1.contoso.com` y `sub2.contoso.com` coincide con `*.contoso.com`). 

Hola dejado de navegación de página de la aplicación Hola Hola portal de Azure, seleccione **los dominios personalizados**. 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Seleccione hello  **+**  icono siguiente demasiado**Agregar nombre de host**.

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Escriba un nombre de dominio completo que coincide con el dominio de hello comodín (por ejemplo, `sub1.contoso.com`) y, a continuación, seleccione **validar**.

Hola **Agregar nombre de host** se activa el botón. 

Asegúrese de que **tipo de registro de nombre de host** se establece demasiado**registro CNAME (www.example.com o cualquier subdominio)**.

Seleccione **Agregar nombre de host**.

![Agregar aplicación de toohello de nombre DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Puede tardar algún tiempo Hola nuevo nombre de host toobe reflejado en la aplicación hello **los dominios personalizados** página. Intente actualizar los datos de saludo explorador tooupdate Hola.

Seleccione hello  **+**  icono nuevo tooadd otro nombre de host que coincide con el dominio comodín Hola. Por ejemplo, agregue `sub2.contoso.com`.

![Registro CNAME agregado](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>Probar en el explorador

Examinar toohello nombres DNS que configuró anteriormente (por ejemplo, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, y `sub2.contoso.com`).

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>Automatizar con scripts

Se puede automatizar la administración de dominios personalizados con secuencias de comandos, mediante hello [CLI de Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview). 

### <a name="azure-cli"></a>CLI de Azure 

Hola siguiente comando agrega un tooan de nombre DNS personalizado configurado aplicación de servicio de aplicaciones. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

Para obtener más información, consulte [asignar una aplicación web de tooa de dominio personalizado](scripts/app-service-cli-configure-custom-domain.md). 

### <a name="azure-powershell"></a>Azure PowerShell 

Hola siguiente comando agrega un tooan de nombre DNS personalizado configurado aplicación de servicio de aplicaciones. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

Para obtener más información, consulte [asignar una aplicación web de tooa de dominio personalizado](scripts/app-service-powershell-configure-custom-domain.md).

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Asignar un subdominio mediante el uso de un registro CNAME
> * Asignar un dominio raíz mediante el uso de un registro D
> * Asignar un dominio con comodín mediante el uso de un registro CNAME
> * Automatizar la asignación de dominio con scripts

Avanzar toohello siguiente tutorial toolearn cómo toobind un personalizado SSL certificate tooa web app.

> [!div class="nextstepaction"]
> [Enlazar un tooAzure de certificado SSL personalizado aplicaciones Web existente](app-service-web-tutorial-custom-ssl.md)
