---
title: "tareas de administración de servicio de nube de aaaCommon (clásico) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo servicios en la nube toomanage Hola portal de Azure clásico."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a>Cómo tooManage los servicios de nube
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-how-to-manage-portal.md)
> * [Portal de Azure clásico](cloud-services-how-to-manage.md)
>
>

Hola **servicios en la nube** área no cliente de Azure clásico Hola portal, puede actualizar un rol de servicio o una implementación, promover una implementación de ensayo tooproduction, vincular servicio de recursos tooyour en la nube para que puedan ver recursos de Hola dependencias y la escala Hola recursos juntos y eliminar un servicio de nube o una implementación.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Actualización del rol de servicio en la nube o implementación
Si tiene código de la aplicación hello tooupdate para su servicio en la nube, use **actualización** en el panel de hello, **servicios en la nube** página, o **instancias** página. Puede actualizar un solo rol o todos los roles. Deberá tooupload un nuevo paquete de servicio y el archivo de configuración de servicio.

1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), en el panel de hello, **servicios en la nube** página, o **instancias** página, haga clic en **actualización**.

    ![Implementación de actualizaciones](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. En **etiqueta de implementación**, escriba una implementación de hello tooidentify nombre (por ejemplo, mycloudservice4). Encontrará la etiqueta de implementación de hello en **inicio rápido** en el panel de Hola.
3. En **paquete**, use **examinar** archivo de paquete de servicio (.cspkg) de tooupload Hola.
4. En **configuración**, use **examinar** archivo de configuración de servicio (.cscfg) de tooupload Hola.
5. En **rol**, seleccione **todos los** si desea que tooupgrade todos los roles de hello servicio en la nube. tooperform un solo rol de actualizar, rol Hola seleccione desea tooupdate. Incluso si selecciona un rol específico tooupdate, las actualizaciones de hello en el archivo de configuración de servicio de hello son roles de tooall aplicado.
6. Si los cambios de actualización de Hola Hola número de roles o el tamaño de Hola de cualquier rol, seleccione hello **permitir la actualización si cambia el tamaño de rol o un número de roles** tooproceed de actualización de casilla de verificación tooenable Hola.

    Tenga en cuenta que si cambia el tamaño de Hola de un rol (es decir, el tamaño de Hola de una máquina virtual que hospeda una instancia de rol) u Hola número de roles, cada instancia de rol (máquina virtual) se debe volver a crear la imagen y se perderán los datos locales.

7. Si los roles de servicio tienen solo una instancia de rol, seleccione hello **actualizar aunque uno o varios roles contengan una casilla de verificación de instancia única** tooenable Hola actualización tooproceed.

    Azure solo puede garantizar un 99,95 % de disponibilidad del servicio durante una actualización del servicio en la nube si cada rol tiene al menos dos instancias de rol (máquinas virtuales). Que permite las solicitudes de cliente de tooprocess de máquina virtual mientras se está actualizando Hola otro.

8. Haga clic en **Aceptar** toobegin (marca de verificación) Actualizar servicio Hola.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Cómo: intercambiar implementaciones toopromote un tooproduction de implementación de ensayo
Use **intercambiar** toopromote una implementación de ensayo de un tooproduction de servicio de nube. Cuando decida toodeploy una nueva versión de un servicio de nube, puede almacenar provisionalmente y probar la nueva versión en su entorno de ensayo del servicio de nube mientras los clientes están utilizando la versión actual de hello en producción. Cuando esté listo toopromote Hola tooproduction nueva versión, puede usar **intercambiar** por qué Hola se tratan dos implementaciones de las direcciones URL de tooswitch Hola.

Puede intercambiar las implementaciones de hello **servicios en la nube** panel página u Hola.

1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **servicios en la nube**.
2. En lista de hello de servicios en la nube, haga clic en tooselect de servicio de nube de Hola.
3. Haga clic en **Intercambiar**.

    Hello siguiente aviso de confirmación se abre.

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. Después de comprobar la información de implementación de hello, haga clic en **Sí** las implementaciones de hello tooswap.

    intercambio de implementación de Hello rápidamente sucede porque Hola única que cambia es hello las direcciones IP virtuales (VIP) para las implementaciones de Hola.

    toosave gastos de proceso, puede eliminar la implementación de Hola Hola entorno de ensayo si estás seguro de que está realizando la nueva implementación de producción de hello según lo previsto.

### <a name="common-questions-about-swapping-deployments"></a>Preguntas comunes sobre el intercambio de implementaciones

**¿Cuáles son los requisitos previos de hello para el intercambio de las implementaciones?**

Existen principalmente dos requisitos previos para que el intercambio de implementación se realice de manera correcta:

- Si desea que toouse una dirección IP estática para la zona de producción, debe reservar uno para la zona de ensayo. En caso contrario, se producirá un error de intercambio de Hola.

- Todas las instancias de los roles se deben ejecutar para poder realizar intercambio de Hola. Puede comprobar el estado de Hola de las instancias en el portal de Azure clásico de Hola o mediante [Hola comando Get-AzureRole en Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).

Tenga en cuenta que las actualizaciones del SO invitado y la recuperación de las operaciones del servicio pueden provocar también toofail de intercambios de implementación. Consulte [Solución de problemas de implementación de servicios en la nube](cloud-services-troubleshoot-deployment-problems.md) para más información.

**¿Un intercambio conlleva tiempo de inactividad de mi aplicación? ¿Cómo puedo controlarlo?**

Tal y como se describe en la última sección de hello, un intercambio de implementación suele ser muy rápido ya que es un cambio de configuración de equilibrador de carga de Azure de Hola. Sin embargo, en algunos casos, puede tardar diez o más segundos y dar lugar a errores de conexión transitorios. los clientes de toolimit impacto tooyour, considere la posibilidad de implementar [lógica de reintento de cliente](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Cómo: vincular un servicio de nube de tooa de recursos
tooshow las dependencias del servicio en la nube de otros recursos, puede vincular una instancia de base de datos de SQL Azure o un servicio de nube de toohello de cuenta de almacenamiento. Puede vincular y desvincular los recursos en hello **recursos vinculados** página y, a continuación, supervisar su uso en el panel de servicio de nube de Hola. Si una cuenta de almacenamiento vinculado tiene supervisión activado, puede supervisar el número Total de solicitudes en panel de servicio de nube de Hola.

Use **vínculo** toolink un nuevo o existente base de datos SQL instancia o almacenamiento cuenta tooyour servicio de nube. A continuación, puede escalar la base de datos de hello junto con el rol de servicio de nube de Hola que está usando en hello **escala** página. (Una cuenta de almacenamiento escala automáticamente a medida que aumenta el uso). Para obtener más información, consulte [cómo tooScale un servicio en la nube y recursos vinculados](cloud-services-how-to-scale.md).

También puede supervisar, administrar y escalar la base de datos de Hola Hola **bases de datos** nodo de hello portal de Azure clásico.

No "Vincular" un recurso en este sentido, conecta el recurso de toohello de aplicación. Si crea una nueva base de datos mediante **vínculo**, necesitará tooadd Hola conexión cadenas tooyour código de aplicación y servicio en la nube a continuación, actualice Hola. También necesitará las cadenas de conexión de tooadd si su aplicación usa los recursos en una cuenta de almacenamiento vinculado.

Hola procedimiento describe cómo toolink una nueva instancia de base de datos SQL, implementado en un nuevo servidor de base de datos SQL, tooa servicio en la nube.

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a>toolink un servicio de nube de tooa de instancia de base de datos SQL
1. Hola [portal de Azure clásico](http://manage.windowsazure.com/), haga clic en **servicios en la nube**. A continuación, haga clic en el nombre de Hola Hola nube tooopen Hola de panel de servicio.
2. Haga clic en **Recursos vinculados**.

    Hola **recursos vinculados** se abre la página.

    ![Página de recursos vinculados](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. Haga clic en **Vincular un recurso** o **Vincular**.

    Hola **vincular recurso** inicia el Asistente para.

    ![Vincular página1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. Haga clic en **Crear un nuevo recurso** o **Vincular un recurso existente**.
5. Elija el tipo de saludo de toolink de recursos. Hola [portal de Azure clásico](http://manage.windowsazure.com/), haga clic en **base de datos SQL**. (Solo Hola portal de Azure clásico admite la vinculación de un servicio de nube de tooa de cuenta de almacenamiento.)
6. configuración de base de datos de hello toocomplete, siga las instrucciones en la Ayuda de hello **bases de datos SQL** área no cliente de hello portal de Azure clásico.

    Puede seguir Hola progreso del programa Hola a vincular la operación en el área de mensajes de Hola.

    Cuando se completa la vinculación, puede supervisar estado de hello del recurso de hello vinculado en el panel de servicio de nube de Hola. Para obtener información acerca de cómo escalar una base de datos de SQL vinculado, vea [cómo tooScale un servicio en la nube y recursos vinculados](cloud-services-how-to-scale.md).

### <a name="toounlink-a-linked-resource"></a>toounlink un recurso vinculado
1. Hola [portal de Azure clásico](http://manage.windowsazure.com/), haga clic en **servicios en la nube**. A continuación, haga clic en el nombre de Hola Hola nube tooopen Hola de panel de servicio.
2. Haga clic en **recursos vinculados**y, a continuación, seleccione el recurso de Hola.
3. Haga clic en **Desvincular**. A continuación, haga clic en **Sí** en mensaje de confirmación de Hola.

    Desvinculación de una base de datos de SQL no tiene ningún efecto en la base de datos de Hola o base de datos de la aplicación hello conexiones toohello. Aun así, puede administrar base de datos de Hola Hola **bases de datos SQL** área no cliente de hello portal de Azure clásico.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Eliminación de implementaciones y un servicio en la nube
Antes de que pueda eliminar un servicio en la nube, debe eliminar cada implementación existente.

toosave gastos de proceso, puede eliminar la implementación de ensayo después de comprobar que la implementación de producción funciona según lo previsto. Se le cobrarán los costes de proceso de las instancias de rol aunque un servicio en la nube no esté funcionando.

Usar hello siguiendo el procedimiento toodelete una implementación o servicio en la nube.

1. Hola [portal de Azure clásico](http://manage.windowsazure.com/), haga clic en **servicios en la nube**.
2. Seleccione servicio de nube de hello y, a continuación, haga clic en **eliminar**. (tooselect un servicio en la nube sin tener que abrir el panel de hello, haga clic en cualquier lugar excepto en nombre de hello en la entrada del servicio de nube de Hola.)

    Si tiene una implementación de ensayo o de producción, verá un menú de opciones toohello similar siguiendo uno en la parte inferior de Hola de ventana hello. Antes de poder eliminar el servicio en la nube hello, debe eliminar las implementaciones existentes.

    ![Menú para eliminar](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. toodelete una implementación, haga clic en **eliminar la implementación de producción** o **eliminar la implementación de ensayo**. A continuación, en el mensaje de confirmación de hello, haga clic en **Sí**.
4. Si piensa que el servicio de nube de hello toodelete, repita el paso 3, si es necesario, toodelete su otra implementación.
5. servicio de nube de hello toodelete, haga clic en **servicio en la nube Delete**. A continuación, en el mensaje de confirmación de hello, haga clic en **Sí**.

> [!NOTE]
> Si se configura la supervisión detallada para el servicio de nube, Azure no elimina Hola datos de supervisión de la cuenta de almacenamiento cuando se elimina el servicio en la nube Hola. Necesitará datos de hello toodelete manualmente. Para obtener información sobre dónde toofind Hola tablas de métricas, vea "Cómo: obtener acceso a los datos de supervisión detallada fuera Hola portal de Azure clásico" en [cómo los servicios de nube tooMonitor](cloud-services-how-to-monitor.md).
>
>

## <a name="next-steps"></a>Pasos siguientes
* [Configuración general de su servicio en la nube](cloud-services-how-to-configure.md).
* Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy.md).
* Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name.md).
* Configuración de [certificados ssl](cloud-services-configure-ssl-certificate.md).
