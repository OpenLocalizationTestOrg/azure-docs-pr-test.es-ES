---
title: aaaBuy un nombre de dominio personalizado para aplicaciones Web de Azure
description: "Obtenga información acerca de cómo el nombre de toobuy un dominio personalizado con una aplicación web en el servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Comprar un nombre de dominio personalizado para Azure Web Apps

Los dominios de App Service (versión preliminar) son dominios de nivel superior que se administran directamente en Azure. Hacen que los dominios personalizados fácil toomanage [aplicaciones Web de Azure](app-service-web-overview.md). Este tutorial muestra cómo toobuy un dominio de servicio de aplicaciones y asigne DNS nombres tooAzure las aplicaciones Web.

Este artículo trata sobre Azure App Service (Web Apps, API Apps, Mobile Apps y Logic Apps). Para la máquina virtual de Azure o el almacenamiento de Azure, consulte [tooAzure de dominio de servicio de aplicaciones asignar VM o almacenamiento de Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/). Para Cloud Services, vea [Configuración de un nombre de dominio personalizado para un servicio en la nube de Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

* [Cree una aplicación de App Service](/azure/app-service/) o use alguna aplicación que haya creado para otro tutorial.

## <a name="prepare-hello-app"></a>Preparar la aplicación hello

toouse dominios personalizados en aplicaciones Web de Azure, la aplicación web [plan de servicio de aplicaciones](https://azure.microsoft.com/pricing/details/app-service/) debe ser una capa de pagada (**Shared**, **básica**, **estándar**, o **Premium**). En este paso, asegúrese de que dicha aplicación hello es Hola admitido nivel de precios.

### <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure

Abra hello [portal de Azure](https://portal.azure.com) e inicie sesión con su cuenta de Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Navegue toohello aplicación Hola portal de Azure

En el menú izquierdo de hello, seleccione **servicios de aplicaciones**y, a continuación, seleccione nombre de Hola de aplicación hello.

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/select-app.png)

Verá que la página de administración de Hola de hello aplicación de servicio de aplicaciones.  

### <a name="check-hello-pricing-tier"></a>Hola de comprobación de nivel de precios

Hola a la izquierda de la página de la aplicación hello, desplácese toohello **configuración** sección y seleccione **escalar verticalmente (plan de servicio de aplicaciones)**.

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

nivel actual de la aplicación Hello aparece resaltado por un borde azul. Compruebe que dicha aplicación hello no esté en hello toomake **libre** capa. DNS personalizado no se admite en hello **libre** capa. 

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Si hello plan de servicio de aplicaciones no es **libre**, cierre hello **elegir el nivel de precios** página y omitir demasiado[dominio Hola de compra](#buy-the-domain).

### <a name="scale-up-hello-app-service-plan"></a>Escalar verticalmente Hola plan de servicio de aplicaciones

Seleccione cualquiera de los niveles de hello no disponibles (**Shared**, **básica**, **estándar**, o **Premium**). 

Haga clic en **Seleccionar**.

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Cuando vea Hola siguientes a la notificación, la operación de escalado de hello está completa.

![Confirmación de la operación de escalado](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>Comprar Hola dominio

### <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure
Abra hello [portal de Azure](https://portal.azure.com/) e inicie sesión con su cuenta de Azure.

### <a name="launch-buy-domains"></a>Iniciar Comprar dominios
Hola **aplicaciones Web** , haga clic en nombre de saludo de la aplicación web, seleccione **configuración**y, a continuación, seleccione **los dominios personalizados**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Hola **los dominios personalizados** página, haga clic en **comprar dominios**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>Configurar la compra de dominio Hola

Hola **dominio de aplicación de servicio** página Hola **Buscar dominio** cuadro, nombre de dominio de tipo hello desea toobuy y el tipo de `Enter`. Hello sugeridos dominios disponibles aparecen justo debajo de cuadro de texto de Hola. Seleccione uno o varios dominios que desee toobuy. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Haga clic en hello **información de contacto** y rellene el formulario de información de contacto del dominio Hola. Cuando termine, haga clic en **Aceptar** página de dominio de aplicación de servicio de tooreturn toohello.
   
Es importante que rellene todos los campos obligatorios con la mayor precisión posible. Dominios de error toopurchase pueden producir datos incorrectos para la información de contacto. 

A continuación, seleccione opciones de hello deseado para el dominio. Vea Hola para obtener una explicación en la tabla siguiente:

| Configuración | Valor sugerido | Descripción |
|-|-|-|
|Renovación automática | **Habilitación** | Renueva automáticamente el dominio de App Service cada año. La tarjeta de crédito se cobra Hola mismo precio de compra en tiempo de Hola de renovación. |
|Protección de la privacidad | Habilitar | Participar en demasiado "Protección de la privacidad", que se incluye en el precio de compra de hello _gratuitamente_ (excepto para los dominios de nivel superior cuyo registro no admiten la protección de la privacidad, como _. co.in_, _. Co.uk_, y así sucesivamente). |
| Asignar nombres de host predeterminados | **www** y **@** | Seleccione Hola deseado enlaces de nombre de host, si lo desea. Cuando se completa la operación de compra de dominio de hello, la aplicación web puede tener acceso en los nombres de host de hello seleccionado. Si la aplicación de hello web está detrás de [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), no ve el dominio raíz Hola de hello opción tooassign (@), ya que el Administrador de tráfico no no registros a soporte técnico. Puede realizar cambios en las asignaciones de nombre de host toohello una vez completada la compra de dominio Hola. |

### <a name="accept-terms-and-purchase"></a>Aceptar los términos y comprar

Haga clic en **condiciones legales** tooreview términos de Hola y cargos de hello, a continuación, haga clic en **comprar**.

> [!NOTE]
> Los dominios de servicio de aplicaciones utilizan dominios de DNS de Azure toohost Hola. Además toohello dominio la inscripción, aplicarán cargos de uso de DNS de Azure. Para obtener más información, vea [DNS de Azure Precios](https://azure.microsoft.com/pricing/details/dns/).
>
>

Nuevo en hello **dominio de aplicación de servicio** página, haga clic en **Aceptar**. Mientras está en curso la operación de hello, vea Hola siguientes notificaciones:

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>Nombres de host de prueba Hola

Si ha asignado la aplicación web de forma predeterminada los nombres de host tooyour, verá una notificación de éxito para cada nombre de host seleccionado. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

También verá los nombres de host seleccionado de Hola Hola **los dominios personalizados** página Hola **los nombres de host** sección. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

nombres de host de hello tootest, navegue toohello muestran los nombres de host en el Explorador de Hola. En el ejemplo de Hola Hola anterior captura de pantalla, intente navegar too_kontoso.net_ y _www.kontoso.net_.

## <a name="assign-hostnames-tooweb-app"></a>Asignar nombres de host tooweb aplicación

Si elige no tooassign uno o más de forma predeterminada los nombres de host tooyour web app durante Hola proceso de compra, o si necesita un nombre de host tooassign no aparece, puede asignar un nombre de host en cualquier momento.

También puede asignar nombres de host en hello tooany de dominio de aplicación de servicio de otra aplicación web. Hello pasos dependen de si Hola dominio de aplicación de servicio y aplicación web de hello pertenecen toohello misma suscripción.

- Otra suscripción: asignar los registros DNS personalizados de dominio de aplicación de servicio de aplicación web hello toohello como un dominio externamente adquirido. Para obtener información acerca de DNS personalizado agregar nombres tooan dominio de aplicación de servicio, consulte [administrar registros DNS personalizados](#custom). toomap una aplicación web de tooa dominio adquiridas externo, vea [asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](app-service-web-tutorial-custom-domain.md). 
- Misma suscripción: Hola uso pasos.

### <a name="launch-add-hostname"></a>Iniciar Agregar nombre de host
Hola **servicios de aplicaciones** página, el nombre de hello select de la aplicación web que desee tooassign los nombres de host, seleccione **configuración**y, a continuación, seleccione **los dominios personalizados**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Asegúrese de que su dominio adquirida en hello **dominios del servicio de aplicación** sección, pero no seleccionarlo. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Todos los dominios de servicio de aplicación Hola misma suscripción se muestran en la aplicación web de hello **los dominios personalizados** página. Si el dominio está en la suscripción de la aplicación de hello web, pero no puede verlo en la aplicación web de hello **los dominios personalizados** página, intente volver a abrir hello **los dominios personalizados** página o actualice la página Web de Hola. Además, compruebe la campana de notificación Hola princip Hola de hello portal de Azure para errores de progreso o de creación.
>
>

Seleccione **Agregar nombre de host**.

### <a name="configure-hostname"></a>Configurar el nombre de host
Hola **Agregar nombre de host** cuadro de diálogo, escribe el nombre de dominio completo de Hola de su dominio de aplicación de servicio o cualquier subdominio. Por ejemplo:

- kontoso.net
- www.kontoso.net
- abc.kontoso.net

Cuando termine, seleccione **Validar**. tipo de registro de nombre de host de Hola se selecciona automáticamente.

Seleccione **Agregar nombre de host**.

Cuando se completa la operación de hello, verá una notificación de éxito para hello asigna el nombre de host.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>Cerrar Agregar nombre de host
Hola **Agregar nombre de host** página, asignar cualquier otro nombre de host tooyour aplicación web, según sea necesario. Cuando haya terminado, cierre hello **Agregar nombre de host** página.

Ahora debería ver Hola acaban de asignar hostname(s) en la aplicación **los dominios personalizados** página.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>Nombres de host de prueba Hola

Navegar por los nombres de host toohello aparece en el Explorador de Hola. En el ejemplo de Hola Hola anterior captura de pantalla, pruebe a navegar por too_abc.kontoso.net_.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>Administrar los registros DNS personalizados

En Azure, los registros DNS para un dominio de App Service se administran mediante [DNS de Azure](https://azure.microsoft.com/services/dns/). Puede agregar, quitar y actualizar los registros DNS, al igual que para un dominio comprado de forma externa.

### <a name="open-app-service-domain"></a>Abrir Dominio de App Service

En el portal de Azure, desde el menú de la izquierda, Hola Hola seleccione **más servicios** > **dominios de aplicación de servicio**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Seleccione Hola dominio toomanage. 

### <a name="access-dns-zone"></a>Obtener acceso a la zona DNS

En el menú de la izquierda del dominio hello, seleccione **zona DNS**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Esta acción abre hello [zona DNS](../dns/dns-zones-records.md) página de su dominio de aplicación de servicio en DNS de Azure. Para obtener información acerca de cómo tooedit los registros DNS, consulte [cómo toomanage zonas de DNS en Hola portal de Azure](../dns/dns-operations-dnszones-portal.md).

## <a name="cancel-purchase-delete-domain"></a>Cancelar la compra (eliminar el dominio)

Después de adquirir Hola dominio de aplicación de servicio, tendrá cinco días toocancel la compra para obtener un reembolso completo. Después de cinco días, puede eliminar Hola dominio de aplicación de servicio, pero no puede recibir un reembolso.

### <a name="open-app-service-domain"></a>Abrir Dominio de App Service

En el portal de Azure, desde el menú de la izquierda, Hola Hola seleccione **más servicios** > **dominios de aplicación de servicio**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Hola seleccione dominio tooyou desea toocancel o eliminar. 

### <a name="delete-hostname-bindings"></a>Eliminación de enlaces de nombre de host

En el menú de la izquierda del dominio hello, seleccione **enlaces de nombre de host**. aquí se muestran los enlaces de nombre de host de Hola de todos los servicios de Azure.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

No se puede eliminar Hola dominio de aplicación de servicio hasta que se eliminen todos los enlaces de nombre de host.

Para eliminar todos los enlaces de nombre de host, seleccione **...** > **Eliminar**. Después de eliminarán todos los enlaces de hello, seleccione **guardar**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>Cancelar o eliminar

En el menú de la izquierda del dominio hello, seleccione **Introducción**. 

Si no ha transcurrido el período de cancelación de hello en el dominio de hello adquirida, seleccione **Cancelar compra**. De lo contrario, en su lugar verá el botón **Eliminar**. dominio de hello toodelete sin un reembolso, seleccione **eliminar**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

Seleccione **Aceptar** operación de hello tooconfirm. Si no desea tooproceed, haga clic en cualquier lugar fuera del cuadro de diálogo de confirmación de Hola.

Una vez completada la operación de hello, dominio hello es publicadas desde su suscripción y están disponibles para todo aquel que toopurchase de nuevo. 
