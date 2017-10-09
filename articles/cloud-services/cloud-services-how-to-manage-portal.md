---
title: "tareas de administración de servicio de nube aaaCommon | Documentos de Microsoft"
description: "Obtenga información acerca de cómo servicios en la nube toomanage Hola portal de Azure. Estos ejemplos utilizan Hola portal de Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
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

Hola **servicios en la nube (clásico)** área no cliente de hello Azure portal, puede actualizar un rol de servicio o una implementación, promover una implementación de ensayo tooproduction, vincular servicio de recursos tooyour en la nube para que puedan ver recursos de Hola dependencias y la escala Hola recursos juntos y eliminar un servicio de nube o una implementación.

Para obtener más información acerca de cómo tooscale su servicio de nube disponible [aquí](cloud-services-how-to-scale-portal.md).

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Actualización del rol de servicio en la nube o implementación
Si tiene código de la aplicación hello tooupdate para su servicio en la nube, use **actualización** en el módulo de servicio de nube Hola. Puede actualizar un solo rol o todos los roles. tooupdate, puede cargar un nuevo paquete de servicio o un archivo de configuración de servicio.

1. Hola [portal de Azure][Azure portal], seleccione servicio de nube de Hola que desee tooupdate. Este paso abre una hoja de instancia de servicio de nube de Hola.
2. En la hoja de hello, haga clic en hello **actualización** botón.

    ![Botón Actualizar](./media/cloud-services-how-to-manage-portal/update-button.png)

3. Implementación de Hola de actualización con un nuevo archivo de paquete de servicio (.cspkg) y el archivo de configuración de servicio (.cscfg).

    ![Implementación de actualizaciones](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. **Si lo desea** actualizar la etiqueta de implementación de Hola y cuenta de almacenamiento de Hola.
5. Si los roles tienen solo una instancia de rol, seleccione hello **implementar aunque uno o varios roles contengan una sola instancia** tooenable Hola actualización tooproceed.

    Azure solo puede garantizar un 99,95 % de disponibilidad del servicio durante una actualización del servicio en la nube si cada rol tiene al menos dos instancias de rol (máquinas virtuales). Con dos instancias de rol, una máquina virtual procesa las solicitudes de cliente mientras se actualiza Hola otro.

6. Comprobar **comience** actualización de hello toohave aplicada una vez finalizada la carga de hello del paquete de Hola.
7. Haga clic en **Aceptar** toobegin Actualizar servicio Hola.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Cómo: intercambiar implementaciones toopromote un tooproduction de implementación de ensayo
Al decidir toodeploy una nueva versión de un servicio de nube, fase y probar la nueva versión en su entorno de ensayo del servicio de nube. Use **intercambiar** tooswitch hello las direcciones URL por qué Hola dos implementaciones se direccionan y promoción un nuevo tooproduction de versión.

Puede intercambiar las implementaciones de hello **servicios en la nube** panel página u Hola.

1. Hola [portal de Azure][Azure portal], seleccione servicio de nube de Hola que desee tooupdate. Este paso abre una hoja de instancia de servicio de nube de Hola.
2. En la hoja de hello, haga clic en hello **intercambiar** botón.

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. Hello siguiente aviso de confirmación se abre.

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. Después de comprobar la información de implementación de hello, haga clic en **Aceptar** las implementaciones de hello tooswap.

    intercambio de implementación de Hello rápidamente sucede porque Hola única que cambia es hello las direcciones IP virtuales (VIP) para las implementaciones de Hola.

    toosave gastos de proceso, puede eliminar Hola implementación de ensayo después de comprobar que la implementación de producción funciona según lo previsto.

### <a name="common-questions-about-swapping-deployments"></a>Preguntas comunes sobre el intercambio de implementaciones

**¿Cuáles son los requisitos previos de hello para el intercambio de las implementaciones?**

Existen principalmente dos requisitos previos para que el intercambio de implementación se realice de manera correcta:

- Si desea que toouse una dirección IP estática para la zona de producción, debe reservar uno para la zona de ensayo. En caso contrario, se produce un error en el intercambio de Hola.

- Todas las instancias de los roles se deben ejecutar para poder realizar intercambio de Hola. Puede comprobar estado de Hola de sus instancias de la hoja de información general de Hola de hello portal de Azure. Como alternativa, puede usar hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) comando en Windows PowerShell.

Tenga en cuenta que las actualizaciones de SO invitado y la recuperación de las operaciones del servicio también puede producir la implementación intercambia toofail. Para más información, consulte [Solución de problemas de implementación de servicios en la nube](cloud-services-troubleshoot-deployment-problems.md).

**¿Un intercambio conlleva tiempo de inactividad de mi aplicación? ¿Cómo puedo controlarlo?**

Como se describe en la última sección de hello, un intercambio de implementación es suele ser muy rápido porque es un cambio de configuración de equilibrador de carga de Azure Hola. Sin embargo, en algunos casos, puede tardar diez o más segundos y dar lugar a errores de conexión transitorios. los clientes de toolimit impacto tooyour, considere la posibilidad de implementar [lógica de reintento de cliente](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Cómo: vincular un servicio de nube de tooa de recursos
Hola portal de Azure no incluye vínculos a recursos conjuntamente como Hola actual portal de Azure clásico. En lugar de implementar recursos adicionales toohello mismo grupo de recursos usándola Hola servicio en la nube.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Eliminación de implementaciones y un servicio en la nube
Antes de que pueda eliminar un servicio en la nube, debe eliminar cada implementación existente.

toosave gastos de proceso, puede eliminar Hola implementación de ensayo después de comprobar que la implementación de producción funciona según lo previsto. Se le facturarán los costos de proceso de las instancias de rol implementadas que se detengan.

Usar hello siguiendo el procedimiento toodelete una implementación o servicio en la nube.

1. Hola [portal de Azure][Azure portal], seleccione servicio de nube de Hola que desee toodelete. Este paso abre una hoja de instancia de servicio de nube de Hola.
2. En la hoja de hello, haga clic en hello **eliminar** botón.

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. Puede eliminar el servicio en la nube todo Hola activando **servicio y sus implementaciones de nube** o elija cualquier hello **implementación de producción** o hello **implementación de ensayo**.

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. Haga clic en hello **eliminar** situado en la parte inferior de Hola.
5. servicio de nube de hello toodelete, haga clic en **servicio en la nube Delete**. A continuación, en el mensaje de confirmación de hello, haga clic en **Sí**.

> [!NOTE]
> Cuando se elimina un servicio de nube y se configura la supervisión detallada, debe eliminar manualmente los datos de Hola desde su cuenta de almacenamiento. Para obtener información sobre dónde toofind Hola tablas de métricas, vea [esto](cloud-services-how-to-monitor.md) artículo.


## <a name="how-to-find-more-information-about-failed-deployments"></a>Búsqueda de más información acerca de las implementaciones con errores
Hola **Introducción** hoja tiene una barra de estado en la parte superior de Hola. Al hacer clic en la barra de hello, una nueva hoja se abre y muestra cualquier información de error. Si la implementación de hello no contiene los errores, hoja de información de hello está en blanco.

![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>Pasos siguientes
* [Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).
* Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy-portal.md).
* Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).
* Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).
