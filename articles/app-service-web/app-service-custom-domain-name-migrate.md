---
title: nombre de aaaMigrate un DNS de active tooAzure servicio de aplicaciones | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomigrate un nombre de dominio DNS personalizado que ya está asignado tooa live sitio tooAzure servicio de aplicaciones sin tiempo de inactividad."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>Migrar un active tooAzure de nombre DNS servicio de aplicaciones

Este artículo muestra cómo un DNS de active toomigrate nombre demasiado[servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) sin tiempo de inactividad.

Cuando se migran un sitio en vivo y su nombre de dominio DNS tooApp servicio, ese nombre DNS ya está atendiendo a tráfico en vivo. Puede evitar tiempos de inactividad en la resolución DNS durante la migración de hello enlazando Hola active DNS nombre tooyour aplicación de servicio de aplicaciones de forma preferente.

Si no le preocupa el tiempo de inactividad en la resolución de DNS, consulte [asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](app-service-web-tutorial-custom-domain.md).

## <a name="prerequisites"></a>Requisitos previos

toocomplete este procedimiento:

- [Asegúrese de que la aplicación de App Service no esté en el nivel GRATIS](app-service-web-tutorial-custom-domain.md#checkpricing).

## <a name="bind-hello-domain-name-preemptively"></a>Enlazar el nombre de dominio de hello forma preferente

Al enlazar un dominio personalizado de forma preferente, realizar dos procedimientos siguientes de hello antes de realizar cambios en los registros DNS:

- Comprobar la propiedad del dominio
- Habilitar el nombre de dominio de hello para la aplicación

Cuando finalmente se migra el nombre DNS personalizado de Hola antiguo sitio toohello aplicación de servicio de aplicaciones, no habrá ningún tiempo de inactividad en la resolución de DNS.

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>Creación de un registro de comprobación de dominio

propiedad del dominio tooverify, agregar un TXT grabar. Hola registro TXT se asigna desde _awverify.&lt; subdominio >_ too_&lt;appname >. azurewebsites.net_. 

Hola registro TXT que necesita depende de hello desea toomigrate de registro DNS. Para obtener ejemplos, vea hello en la tabla siguiente (`@` normalmente representa Hola dominio raíz):  

| Ejemplo de registro DNS | Host TXT | Valor TXT |
| - | - | - |
| @ (raíz) | _awverify_ | _&lt;nombreaplic&gt;.azurewebsites.net_ |
| www (sub) | _awverify.www_ | _&lt;nombreaplic&gt;.azurewebsites.net_ |
| \* (comodín) | _awverify.\*_ | _&lt;nombreaplic&gt;.azurewebsites.net_ |

En la página de registros DNS, tenga en cuenta los tipo de registro de hello de hello nombre DNS que desea toomigrate. App Service es compatible con las asignaciones de CNAME y registros A.

### <a name="enable-hello-domain-for-your-app"></a>Habilitar el dominio de hello para la aplicación

Hola [portal de Azure](https://portal.azure.com), en Hola de navegación izquierdo de la página de la aplicación hello, seleccione **los dominios personalizados**. 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Hola **los dominios personalizados** página, seleccione hello  **+**  icono siguiente demasiado**Agregar nombre de host**.

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Nombre de dominio completo de tipo hello que agregó el registro TXT de hello, como `www.contoso.com`. Para un dominio con caracteres comodín (como \*. contoso.com), puede utilizar cualquier nombre DNS que coincide con el dominio comodín Hola. 

Seleccione **Validar**.

Hola **Agregar nombre de host** se activa el botón. 

Asegúrese de que **tipo de registro de nombre de host** se establece los tipo de registro de DNS de toohello desea toomigrate.

Seleccione **Agregar nombre de host**.

![Agregar aplicación de toohello de nombre DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Puede tardar algún tiempo Hola nuevo nombre de host toobe reflejado en la aplicación hello **los dominios personalizados** página. Intente actualizar los datos de saludo explorador tooupdate Hola.

![Registro CNAME agregado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

El nombre DNS personalizado ya estará habilitado en la aplicación de Azure. 

## <a name="remap-hello-active-dns-name"></a>Asignar nombre de DNS de active Hola

Hello solo lo izquierdo toodo es reasignación su tooApp de toopoint registros DNS servicio activo. Derecha ahora, todavía señala tooyour del sitio antiguo.

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>Copie la dirección IP de la aplicación hello (solo para un registro)

Si va a reasignar un registro CNAME, omita esta sección. 

tooremap un registro, deberá dirección IP externa de la aplicación de servicio de aplicaciones de hello, que se muestra en hello **los dominios personalizados** página.

Hola cerrar **Agregar nombre de host** página seleccionando **X** en la esquina superior derecha de Hola. 

Hola **los dominios personalizados** página, copie la dirección IP de la aplicación hello.

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>Actualizar el registro de DNS de Hola

Nuevo en la página de registros DNS de Hola de su proveedor de dominio, seleccione tooremap de registro de DNS de Hola.

Para hello `contoso.com` raíz del ejemplo de un dominio, vuelva a asignar un registro A o CNAME hello como hello en los ejemplos de hello en la tabla siguiente: 

| Ejemplo de FQDN | Tipo de registro | Host | Valor |
| - | - | - | - |
| contoso.com (raíz) | Una  | `@` | Dirección IP de [dirección IP de la aplicación de copia Hola](#info) |
| www.contoso.com (sub) | CNAME | `www` | _&lt;nombreaplic&gt;.azurewebsites.net_ |
| \*.contoso.com (comodín) | CNAME | _\*_ | _&lt;nombreaplic&gt;.azurewebsites.net_ |

Guarde la configuración.

Consultas de DNS deben comenzar a resolver tooyour aplicación de servicio de aplicaciones inmediatamente después de que ocurra la propagación de DNS.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toobind un personalizado SSL certificate tooApp servicio.

> [!div class="nextstepaction"]
> [Enlazar un tooAzure de certificado SSL personalizado aplicaciones Web existente](app-service-web-tutorial-custom-ssl.md)
