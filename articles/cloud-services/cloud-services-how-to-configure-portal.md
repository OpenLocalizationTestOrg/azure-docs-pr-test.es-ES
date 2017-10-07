---
title: aaaHow tooconfigure un servicio de nube (portal) | Documentos de Microsoft
description: "Obtenga información acerca de cómo servicios en la nube tooconfigure en Azure. Obtenga información acerca de la configuración del servicio de nube de tooupdate hello y configurar instancias de toorole de acceso remoto. Estos ejemplos utilizan Hola portal de Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>Cómo tooConfigure los servicios de nube
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-how-to-configure-portal.md)
> * [Portal de Azure clásico](cloud-services-how-to-configure.md)
>
>

Puede configurar valores de hello suelen usada para un servicio de nube en hello portal de Azure. O bien, si le gusta tooupdate los archivos de configuración directamente, descargar una tooupdate de archivo de configuración de servicio y, a continuación, cargar Hola Actualizar archivo y actualización Hola servicio en la nube con los cambios de configuración de Hola. En cualquier caso, se insertan las actualizaciones de configuración de hello tooall instancias de rol.

También puede administrar instancias de Hola de los roles de servicio de nube o el escritorio remoto en ellos.

Azure solo puede asegurar de disponibilidad de servicio del 99,95 por ciento durante hello las actualizaciones de configuración si tiene al menos dos instancias de rol para cada rol. Que permite las solicitudes de cliente de tooprocess de máquina virtual mientras se está actualizando Hola otro. Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Cambiar un servicio en la nube
Después de abrir hello [portal de Azure](https://portal.azure.com/), navegar por el servicio en la nube tooyour. Desde aquí puede administrar muchos aspectos de este.

![Página de configuración](./media/cloud-services-how-to-configure-portal/cloud-service.png)

Hola **configuración** o **toda la configuración de** vínculos se abrirán hello **configuración** hoja donde puedes cambiar hello **propiedades**, cambiar Hola **Configuración**, administrar hello **certificados**, el programa de instalación **reglas de alerta**y administrar hello **usuarios** que tienen acceso toothis servicio en la nube.

![Hoja de configuración del servicio en la nube de Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Administración de la versión del SO invitado

De forma predeterminada, Azure actualiza periódicamente la toohello más reciente compatible imagen del SO invitado en hello familia del SO que haya especificado en la configuración del servicio (.cscfg), como Windows Server 2016.

Si necesita tootarget una versión específica del sistema operativo, puede establecerlo en hello **configuración** hoja.

![Establecimiento de la versión del sistema operativo](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> Si elige una versión específica del sistema operativo deshabilitará las actualizaciones automáticas y hará que la aplicación de revisiones sea responsabilidad suya. Debe asegurarse de que las instancias de rol están recibiendo actualizaciones o puede exponer sus vulnerabilidades de toosecurity de aplicación.

## <a name="monitoring"></a>Supervisión
Puede agregar el servicio de alertas tooyour en la nube. Haga clic en **Configuración** > **Reglas de alerta** > **Agregar alerta**.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

Desde aquí puede configurar una alerta. Con hello **métrica** cuadro de lista desplegable, puede configurar una alerta para hello siguientes tipos de datos.

* Lectura de disco
* Escritura de disco
* Red interna
* Red externa
* Porcentaje de CPU

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Configuración de la supervisión desde un icono de métrica
En lugar de usar **configuración** > **reglas de alerta**, puede hacer clic en uno de los mosaicos de métrica de Hola Hola **supervisión** sección de hello **en la nube servicio** hoja.

![Supervisión de servicios en la nube](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

Desde aquí puede personalizar el gráfico de Hola que se usa con icono de hello, o agregar una regla de alerta.

## <a name="reboot-reimage-or-remote-desktop"></a>Reinicio, restablecimiento de imagen inicial o conexión mediante Escritorio remoto
En este momento no se puede configurar Escritorio remoto con hello **portal de Azure**. Sin embargo, puede configurarlo a través de hello [portal de Azure clásico](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), o a través [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

En primer lugar, haga clic en la instancia de servicio de nube de Hola.

![Instancia del servicio en la nube](./media/cloud-services-how-to-configure-portal/cs-instance.png)

De hello hoja que se abrirá, puede iniciar una conexión a escritorio remota, reiniciar la instancia de Hola o de forma remota instancia Hola de restablecimiento de imagen inicial (comenzar con una nueva imagen) de forma remota.

![Botones de instancia del servicio en la nube](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>Reconfiguración del archivo .cscfg
Puede que necesite tooreconfigure su servicio de nube a través de hello [la configuración de servicio (cscfg)](cloud-services-model-and-package.md#cscfg) archivo. En primer lugar debe toodownload su .cscfg de archivo, modificarlo y cargarlo.

1. Haga clic en hello **configuración** icono o hello **toda la configuración de** vincular tooopen seguridad hello **configuración** hoja.

    ![Página de configuración](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Haga clic en hello **configuración** elemento.

    ![Hoja de configuración](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Haga clic en hello **descargar** botón.

    ![Descargar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. Después de actualizar el archivo de configuración de servicio de hello, cargar y aplicar las actualizaciones de configuración de hello:

    ![Cargar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Seleccione el archivo de .cscfg de hello y haga clic en **Aceptar**.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy-portal.md).
* Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).
* [Administración de su servicio en la nube](cloud-services-how-to-manage-portal.md).
* Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).
