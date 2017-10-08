---
title: "aaaConfigure un nombre de dominio personalizado en el servicio de aplicación de Azure (GoDaddy)"
description: "Obtenga información acerca de cómo nombre toouse un dominio de GoDaddy con aplicaciones Web de Azure"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Configuración de un nombre de dominio personalizado en Azure App Service (adquirido directamente de GoDaddy)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Si ha adquirido el dominio a través de aplicaciones de Web del servicio de aplicación de Azure, consulte toohello paso final de [comprar dominio para las aplicaciones Web](custom-dns-web-site-buydomains-web-app.md).

Este artículo ofrece instrucciones acerca del uso de un nombre de dominio personalizado adquirido directamente en [Go Daddy](https://godaddy.com) con [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Descripción de los registros DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Incorporación de un registro DNS para el dominio personalizado
tooassociate su dominio personalizado con una aplicación web en el servicio de aplicaciones, debe agregar una nueva entrada en la tabla de hello DNS para su dominio personalizado mediante el uso de herramientas proporcionadas por GoDaddy. Usar hello siguiendo las herramientas DNS de pasos toolocate Hola para GoDaddy.com

1. Iniciar sesión en tooyour cuenta con GoDaddy.com y seleccione **mi cuenta** y, a continuación, **administrar Mis dominios**. Menú de lista desplegable seleccione Hola Hola nombre de dominio que desea toouse con la aplicación web de Azure y seleccione **administrar DNS**.
   
    ![Página de dominio personalizado para GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. De hello **detalles del dominio** página, desplácese toohello **archivo de zona DNS** ficha. Se trata de una sección de hello usado para agregar y modificar registros de DNS para el nombre de dominio.
   
    ![Pestaña de archivo de zona DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Seleccione **Add Record** tooadd un registro existente.
   
    demasiado**editar** un registro existente, el icono de lápiz y papel de hello seleccione situado junto al registro de hello.
   
   > [!NOTE]
   > Antes de agregar nuevos registros, tenga en cuenta que GoDaddy ya ha creado registros DNS de subdominios populares (llamados **Host** en el editor), como **email**, **files**, **mail** y otros. Si el nombre de hello desea toouse ya existe, modificar registro existente de hello en lugar de crear uno nuevo.
   > 
   > 
3. Al agregar un registro, primero debe seleccionar el tipo de registro de hello.
   
    ![seleccione el tipo de registro](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    A continuación, debe proporcionar hello **Host** (Hola personalizado dominio o subdominio) y lo que **apunta a**.
   
    ![agregue un registro de zona.](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Cuando se agrega un **un registro (host)** -debe establecer hello **Host** campo tooeither  **@**  (Esto representa como nombre del dominio raíz,  **contoso.com**,) * (un carácter comodín para la coincidencia de varios subdominios) u Hola subdominio que se va a toouse (por ejemplo, **www**.) Debe establecer hello **apunta a** campo toohello dirección IP de la aplicación web de Azure.
   * Cuando se agrega un **registro CNAME (alias)** -debe establecer hello **Host** campo toohello subdominio que se va toouse. Por ejemplo, **www**. Debe establecer hello **apunta a** campo toohello **. azurewebsites.net** nombre de dominio de la aplicación web de Azure. Por ejemplo, **contoso.azurewebsites.net**.
4. Haga clic en **Agregar otro**.
5. Seleccione **TXT** como tipo de registro de hello, a continuación, especifique un **Host** valo  **@**  y un **apunta a** valo  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Este registro TXT se usa por Azure toovalidate que posee el dominio Hola descrito por hello un registro TXT primer registro u Hola. Una vez que el dominio de hello ha sido asignada toohello web aplicación Hola Portal de Azure, se puede quitar esta entrada de registro TXT.
   > 
   > 
6. Cuando haya terminado de agregar o modificar registros, haga clic en **finalizar** toosave cambios.

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a>Habilitar el nombre de dominio de hello en la aplicación web
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

