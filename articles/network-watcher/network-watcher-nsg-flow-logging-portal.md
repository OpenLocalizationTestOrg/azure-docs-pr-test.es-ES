---
title: registros de flujo de grupo de seguridad de aaaManage red con Monitor de red de Azure | Documentos de Microsoft
description: "Esta página explica cómo toomanage flujo de grupo de seguridad de red se registra en el Monitor de red de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>Administrar registros de flujo de grupo de seguridad de red en hello portal de Azure

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API DE REST](network-watcher-nsg-flow-logging-rest.md)

Registros de flujo de grupo de seguridad de red son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red. Estos registros de flujo se escriben con formato JSON y brinda información importante, la que incluye: 

- Flujos de entrada y de salida por regla.
- Hola NIC que Hola flujo se aplica a.
- tupla de 5 información acerca del flujo de hello (dirección IP de origen/destino, puerto de origen/destino, protocolo).
- Información sobre si se permitió o denegó el tráfico.

## <a name="before-you-begin"></a>Antes de empezar

Este escenario se supone que ya ha seguido los pasos de hello en [crear una instancia del Monitor de red](network-watcher-create.md). escenario de Hello también se supone que una tiene un grupo de recursos con una máquina virtual válida.

## <a name="register-insights-provider"></a>Registro del proveedor de Insights

Para el flujo de registro toowork correctamente, Hola **Microsoft.Insights** proveedor debe estar registrado. proveedor de hello tooregister, Hola toman pasos: 

1. Vaya demasiado**suscripciones**y, a continuación, seleccione la suscripción de hello para el que desea que los registros de flujo de tooenable. 
2. En hello **suscripción** hoja, seleccione **proveedores de recursos**. 
3. Mire Hola lista de proveedores y compruebe que hello **microsoft.insights** proveedor está registrado. Si no es así, seleccione **Registrarse**.

![Visualización de proveedores][providers]

## <a name="enable-flow-logs"></a>Habilitar los registros de flujo

Estos pasos le guiarán en proceso de Hola de habilitar registros de flujo en un grupo de seguridad de red.

### <a name="step-1"></a>Paso 1

Vaya tooa instancia de Monitor de red y, a continuación, seleccione **registros de flujo de NSG**.

![Información general de los registros de flujo][1]

### <a name="step-2"></a>Paso 2

Seleccione un grupo de seguridad de red de hello lista.

![Información general de los registros de flujo][2]

### <a name="step-3"></a>Paso 3 

En hello **configuración de registros de flujo de** hoja, establecer el estado de hello demasiado**en**y, a continuación, configure una cuenta de almacenamiento.  Cuando finalice, seleccione **Aceptar**. Después, seleccione **Guardar**.

![Información general de los registros de flujo][3]

## <a name="download-flow-logs"></a>Descarga de registros de flujo

Los registros de flujo se guardan en una cuenta de almacenamiento. Descargue el tooview de registros de flujo ellos.

### <a name="step-1"></a>Paso 1

seleccionar registros de flujo de toodownload, **puede descargar los registros de flujo de las cuentas de almacenamiento configurado**. Este paso le tooa vista de cuentas de almacenamiento donde puede elegir qué toodownload de registros.

![Configuración de registros de flujo][4]

### <a name="step-2"></a>Paso 2

Vaya toohello cuenta de almacenamiento correcta. Luego, seleccione **Contenedores** > **insights-log-networksecuritygroupflowevent**.

![Configuración de registros de flujo][5]

### <a name="step-3"></a>Paso 3

Vaya a toohello ubicación del registro de flujo de hello, selecciónelo y, a continuación, seleccione **descargar**.

![Configuración de registros de flujo][6]

Para obtener información acerca de la estructura de Hola de registro de hello, visite [información general sobre el registro de flujo de red seguridad grupo](network-watcher-nsg-flow-logging-overview.md).

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
