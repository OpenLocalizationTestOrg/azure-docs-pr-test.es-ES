---
title: aaaSet entornos de ensayo para aplicaciones web en el servicio de aplicaciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse provisionalmente la publicación de las aplicaciones web de servicio de aplicaciones de Azure."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Configuración de entornos de ensayo en Azure App Service
<a name="Overview"></a>

Cuando se implementan la aplicación web, la aplicación web en Linux, móvil back-end y aplicación de API demasiado[servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714), puede implementar tooa ranura de implementación independiente en lugar de la ranura de producción de hello predeterminada cuando se ejecuta en hello **estándar**o **Premium** modo de plan de servicio de aplicaciones. Las ranuras de implementación son realmente aplicaciones activas con sus propios nombres de host. Elementos de contenido y las configuraciones de aplicación se pueden intercambiar entre dos ranuras de implementación, incluida la zona de producción de hello. Implementación de la ranura de implementación de aplicación tooa tiene Hola siguientes ventajas:

* Puede validar los cambios de la aplicación en una ranura de implementación de ensayo antes de cambiarlo a ranura de producción de hello.
* Implementar una ranura de aplicación tooa primero y cambiarlo a producción garantizan que todas las instancias de la ranura de Hola se activa antes de que se va a intercambiar en producción. Esto elimina tiempos de inactividad a la hora de implementar la aplicación. Hola redireccionamiento del tráfico es perfecto y no se anulan solicitudes como resultado de las operaciones de intercambio. Este flujo de trabajo completo puede automatizarse mediante la configuración de [Intercambio automático](#Auto-Swap) .
* Después de un intercambio, ranura Hola con aplicación previamente por fases ahora tiene aplicación de producción de hello anterior. Si hay cambios de hello pasados a la ranura de producción de hello no según lo esperado, puede realizar Hola que mismo intercambio inmediatamente tooget su "último sitio conocido" realizar copias.

Cada modo del plan del Servicio de aplicaciones admite un número distinto de espacios de implementación. toofind out número Hola de ranuras se admite el modo de la aplicación, consulte [precios del servicio de aplicación](https://azure.microsoft.com/pricing/details/app-service/).

* Cuando la aplicación tiene varias ranuras, no se puede cambiar el modo de saludo.
* El escalado no está disponible para los espacios que no son de producción.
* No se admite la administración de recursos vinculados en los espacios que no sean de producción. Hola [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715) solo, puede evitar este posible impacto en una ranura de producción moviendo temporalmente el modo de plan de hello ranura de producción no tooa otro servicio de aplicaciones. Tenga en cuenta esa ranura no sea de producción de hello debe compartir una vez más Hola mismo modo con la ranura de producción de hello antes de que se pueden intercambiar las ranuras de hello dos.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>Incorporación de una ranura de implementación
debe estar ejecutando la aplicación Hello en hello **estándar** o **Premium** modo en orden para tooenable varias ranuras de implementación.

1. Hola [Portal de Azure](https://portal.azure.com/), abra la aplicación [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Elija hello **ranuras de implementación** opción, a continuación, haga clic en **agregar ranura**.
   
    ![Agregar una nueva ranura de implementación][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Si la aplicación hello no está ya en hello **estándar** o **Premium** modo, recibirá un mensaje que indica los modos de hello compatibles para habilitar la publicación de ensayo. En este punto, tiene Hola opción tooselect **actualizar** y navegue toohello **escala** pestaña de la aplicación antes de continuar.
   > 
   > 
3. Hola **agregar una ranura** hoja, asigne un nombre a la ranura de Hola y seleccione si tooclone configuración de la aplicación de otra ranura de implementación existente. Haga clic en hello toocontinue de marca de verificación.
   
    ![Origen de configuración][ConfigurationSource1]
   
    Hello primera vez que agrega una ranura, solo tendrá dos opciones: configuración de clonación de ranura de predeterminado de hello en producción o no en absoluto.
    Después de haber creado varias ranuras, será capaz de tooclone configuración de una ranura distinto de hello en producción:
   
    ![Orígenes de configuración][MultipleConfigurationSources]
4. En la hoja de recursos de la aplicación, haga clic en **ranuras de implementación**, a continuación, haga clic en un tooopen de ranura de implementación hoja de recursos de la ranura, con un conjunto de métricas y la configuración al igual que cualquier otra aplicación. Hello nombre de ranura de Hola se muestra en parte superior de Hola de hello hoja tooremind que está viendo Hola ranura de implementación.
   
    ![Título de la ranura de implementación][StagingTitle]
5. Haga clic en la URL de la aplicación hello en la hoja de la ranura de Hola. Observe la ranura de implementación de hello tiene su propio nombre de host y también es una aplicación activa. ranura de implementación de toolimit acceso público toohello, consulte [aplicación de servicio Web App: ranuras de implementación de producción toonon de bloque web acceso](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).

No hay ningún contenido después de la creación de un espacio de implementación. Puede implementar toohello ranura de una rama del repositorio diferente o un repositorio totalmente diferente. También puede cambiar la configuración de la ranura de Hola. Hola Use Publicar perfil o la implementación de las credenciales asociadas con la ranura de implementación de hello las actualizaciones de contenido.  Por ejemplo, puede [publicar ranura toothis con git](app-service-deploy-local-git.md).

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>Configuración de ranuras de implementación
Al clonar la configuración de otra ranura de implementación, configuración clonado hello es editable. Además, algunos elementos de configuración seguirá contenido Hola a través de un intercambio (no ranura específico) mientras que otros elementos de configuración permanecerá en hello misma ranura después de un intercambio (específico de la ranura). Hello listas siguientes se muestra configuración de Hola que cambiará cuando intercambia las ranuras.

**Configuraciones que se intercambian**:

* Configuración general: por ejemplo, versión de framework, 32 o 64 bits, Web Sockets
* Configuración de la aplicación (puede ser configurado toostick tooa ranura)
* Cadenas de conexión (puede estar configurado toostick tooa ranura)
* Asignaciones de controlador
* Configuración de supervisión y diagnóstico
* Contenido de WebJobs

**Configuraciones que no se intercambian**:

* Extremos de publicación
* Nombres de dominio personalizados
* Certificados SSL y enlaces
* Configuración de escala
* Programadores de WebJobs

tooconfigure una configuración o conexión cadena toostick tooa ranura de aplicación (no intercambiada) Hola acceso **configuración de la aplicación** hoja de una ranura específico, a continuación, seleccione hello **ranura configuración** cuadro Hola elementos de configuración que deben pegar ranura Hola. Tenga en cuenta que un elemento de configuración marcar como ranura específico tiene el efecto de Hola de establecimiento de ese elemento como no intercambiables en todas las ranuras de implementación de hello asociadas con la aplicación hello.

![Configuración de ranura][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>Intercambio de ranuras de implementación 
Puede intercambiar las ranuras de implementación en hello **Introducción** o **ranuras de implementación** vista de hoja de recursos de la aplicación.

> [!IMPORTANT]
> Antes de intercambiar una aplicación desde una ranura de implementación en producción, asegúrese de que todas las configuraciones específicas de ranura no están configuradas exactamente como se desee toohave en el destino de intercambio de Hola.
> 
> 

1. las ranuras de implementación de tooswap, haga clic en hello **intercambiar** botón de barra de comandos de Hola de aplicación hello o en la barra de comandos de Hola de una ranura de implementación.
   
    ![Botón de cambio][SwapButtonBar]

2. Asegúrese de que ese destino de origen y de intercambio de intercambio de hello están establecidos correctamente. Normalmente, el destino de intercambio de hello es ranura de producción de hello. Haga clic en **Aceptar** operación de hello toocomplete. Cuando finaliza la operación de hello, se intercambiaron las ranuras de implementación de Hola.

    ![Intercambio completo](./media/web-sites-staged-publishing/SwapImmediately.png)

    Para hello **intercambio con vista previa** intercambiar tipo, consulte [intercambio con vista previa (intercambio de varias fase)](#Multi-Phase).  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>Intercambio con vista previa (intercambio en varias fases)

Intercambio con vista previa o en varias fases simplifican la validación de elementos de configuración específicos de ranura, como cadenas de conexión.
Para las cargas de trabajo críticas, desea toovalidate que Hola aplicación se comporta según lo esperado cuando se aplica la configuración de la ranura de producción de hello, y debe realizar esta validación *antes de* aplicación hello se intercambia en producción. Intercambio con vista previa es lo que necesita.

> [!NOTE]
> El intercambio con vista previa no se admite en las aplicaciones web en Linux.

Cuando usas hello **intercambio con vista previa** opción (vea [intercambiar ranuras de implementación](#Swap)), servicio de aplicación Hola siguientes:

- No se ve afectado mantiene Hola destino ranura sin modificar por lo que carga de trabajo existente en esa ranura (p. ej., producción).
- Se aplica a los elementos de configuración de Hola de hello ranura toohello origen ranura de destino, incluidas las cadenas de conexión específica de la ranura de Hola y configuración de la aplicación.
- Reinicia los procesos de trabajo de hello en la ranura de origen Hola con estos elementos de configuración mencionados anteriormente.
- Cuando complete el intercambio de hello: ranura de movimientos Hola previa warmed el origen en la ranura de destino de Hola. ranura de destino de Hola se mueve a la ranura de origen de hello como en un intercambio manual.
- Al cancelar el intercambio de hello: vuelve a aplicar los elementos de configuración de Hola de ranura de origen de hello origen ranura toohello.

Puede ver exactamente cómo se comportará aplicación hello con la configuración de la ranura de destino de Hola. Cuando se haya completado la validación, completar intercambio hello en un paso independiente. Este paso ha Hola ventaja adicional que la ranura de origen de hello ya está activa con la configuración deseada de Hola y los clientes no experimentarán ningún tiempo de inactividad.  

Ejemplos de hello cmdlets de PowerShell de Azure disponibles para el intercambio de varias fase se incluyen en hello cmdlets de PowerShell de Azure para la sección de ranuras de implementación.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>Configuración de intercambio automático
Optimiza de intercambio automático escenarios de DevOps donde desea toocontinuously implementa su aplicación con cero arranque en frío y sin tiempo de inactividad para los clientes finales de la aplicación hello. Cuando se configura una ranura de implementación para el intercambio automático al entorno de producción, cada vez que realice una inserción su ranura toothat de actualización de código, servicio de aplicaciones automáticamente intercambiará aplicación hello en producción cuando ya se activa en la ranura de Hola.

> [!IMPORTANT]
> Cuando se habilita para una ranura de intercambio automático, asegúrese de que configuración de la ranura de hello es exactamente la configuración del Hola prevista para la ranura de destino hello (normalmente ranura de producción de hello).
> 
> 

> [!NOTE]
> El intercambio automático no se admite en aplicaciones web en Linux.

Es fácil configurar el intercambio automático para un espacio. Siga los pasos de hello siguientes:

1. En **Ranuras de implementación**, seleccione una ranura que no sea de producción y elija **Configuración de la aplicación** en la hoja de recursos de esa ranura.  
   
    ![][Autoswap1]
2. Seleccione **en** para **intercambio automático**, seleccione la ranura de destino deseado de hello en **la ranura de intercambio automático**y haga clic en **guardar** en la barra de comandos de Hola. Asegúrese de que configuración de ranura de hello es exactamente la configuración del Hola destinada a la ranura de destino Hola.
   
    Hola **notificaciones** ficha parpadeará en un color verde **correcto** una vez completada la operación de Hola.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest intercambio automático de la aplicación, primero puede seleccionar una ranura de destino no es de producción en **la ranura de intercambio automático** toobecome familiarizado con la característica de Hola.  
   > 
   > 
3. Ejecutar una ranura de implementación de toothat de inserción de código. El intercambio automático se realizará después de unos minutos y actualización de Hola se verán reflejado en la dirección URL de la ranura de destino.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>toorollback una aplicación de producción después del intercambio
Si se identifican errores en producción después de un intercambio de ranura, poner las ranuras de hello tootheir atrás intercambio previo Estados intercambiando las ranuras de hello dos mismos inmediatamente.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>Preparación personalizada antes del intercambio
Es posible que algunas aplicaciones necesiten acciones de preparación personalizadas. Hola `applicationInitialization` elemento de configuración en el archivo web.config permite toospecify inicialización personalizada acciones toobe realiza antes de que se recibe una solicitud. operación de intercambio de Hello esperará este toocomplete preparación personalizado. He aquí un fragmento de ejemplo del archivo web.config.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete una ranura de implementación
En la hoja de Hola de una ranura de implementación, hoja de la ranura de implementación de hello abierto, haga clic en **Introducción** (página predeterminada de hello) y haga clic en **eliminar** en la barra de comandos de Hola.  

![Eliminación de una ranura de implementación][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>Cmdlets de PowerShell de Azure para espacios de implementación
Azure PowerShell es un módulo que proporciona cmdlets toomanage Azure a través de Windows PowerShell, incluida la compatibilidad para administrar las ranuras de implementación de servicio de aplicaciones de Azure.

* Para obtener información sobre cómo instalar y configurar Azure PowerShell y sobre la autenticación de Azure PowerShell con su suscripción de Azure, consulte [cómo tooinstall y configurar Microsoft Azure PowerShell](/powershell/azure/overview).  

- - -
### <a name="create-a-web-app"></a>Creación de una aplicación web
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>Creación de una ranura de implementación
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>Iniciar un intercambio con revisión (intercambio de varias fase) y aplicar la ranura de toosource de configuración de ranura de destino
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>Cancelación de un intercambio pendiente (intercambio con vista previa) y restauración de configuración de la ranura de origen
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>Intercambio de ranuras de implementación
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>Eliminación de una ranura de implementación
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>Comandos de la interfaz de la línea de comandos de Azure (CLI de Azure) para ranuras de implementación
Hola CLI de Azure proporciona comandos entre plataformas y para trabajar con Azure, incluida la compatibilidad para administrar las ranuras de implementación de servicio de aplicaciones.

* Para obtener instrucciones sobre cómo instalar y configurar hello CLI de Azure, incluida la información acerca de cómo tooconnect CLI de Azure tooyour suscripción de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md).
* comandos de hello toolist disponibles para el servicio de aplicaciones de Azure en hello CLI de Azure, llame a `azure site -h`.

> [!NOTE] 
> Para los comandos de la [CLI de Azure 2.0](https://github.com/Azure/azure-cli) de espacios de implementación, consulte [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).

- - -
### <a name="azure-site-list"></a>azure site list
Para obtener información acerca de las aplicaciones de hello en la suscripción actual de hello, llame a **lista de sitios de azure**, como en el siguiente ejemplo de Hola.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>azure site create
toocreate una ranura de implementación, llame a **crear sitio azure** y especifique el nombre hello de una aplicación existente y el nombre de Hola de hello ranura toocreate, como en el siguiente ejemplo de Hola.

`azure site create webappslotstest --slot staging`

control de código fuente de tooenable para la nueva ranura hello, use Hola **--git** opción, como en el siguiente ejemplo de Hola.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>azure site swap
toomake Hola aplicación de producción de hello de ranura de implementación actualizadas, use hello **intercambio de sitio de azure** comando tooperform una operación de intercambio, como en el siguiente ejemplo de Hola. aplicación de producción de Hello no experimentará tiempo improductivo, ni sufrirá un arranque en frío.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>azure site delete
toodelete una ranura de implementación que ya no es necesario, utilice hello **delete de sitio de azure** comando, como en el siguiente ejemplo de Hola.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> Vea una aplicación web en acción. [Pruebe el Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/) inmediatamente y cree una aplicación de inicio de corta duración; no se requiere tarjeta de crédito ni se establece ningún compromiso.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
[Web de servicio de aplicaciones de Azure aplicación: bloquear ranuras de implementación de web access producción toonon](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introducción tooApp servicio en Linux](./app-service-linux-intro.md)
[evaluación gratuita de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

