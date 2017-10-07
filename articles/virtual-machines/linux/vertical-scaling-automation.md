---
title: "escala aaaVertically máquina virtual de Azure con la automatización de Azure | Documentos de Microsoft"
description: "¿Cómo toovertically escalar una máquina Virtual Linux en alertas de respuesta de toomonitoring con automatización de Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a>Escalado vertical de máquinas virtuales Linux de Azure con Azure Automation
Escalado vertical es el proceso de Hola de aumentar o disminuir los recursos de Hola de un equipo de carga de trabajo de respuesta toohello. En Azure, esto puede realizarse mediante el cambio de tamaño Hola de hello Máquina Virtual. Esto puede ayudar a los escenarios siguientes de Hola

* Si no se utiliza con frecuencia Hola Máquina Virtual, éste se pueden cambiar hacia abajo tooa menor tamaño tooreduce los costos mensuales
* Si Hola Máquina Virtual ve una carga máxima, puede ser tooincrease de tamaño mayor de tooa cuyo tamaño ha cambiado su capacidad máxima

esquema de Hola para hello pasos tooaccomplish se trata como a continuación

1. La instalación de las máquinas virtuales tooaccess de automatización de Azure
2. Importar runbooks de escala Vertical de automatización de Azure de hello en su suscripción
3. Agregar un runbook de tooyour de webhook
4. Agregar una alerta tooyour Máquina Virtual

> [!NOTE]
> Debido a un tamaño de Hola Hola primera máquina Virtual, se puede escalar, los tamaños de Hola puede ser limitada debido toohello disponibilidad de hello otros tamaños de clúster de hello actual Máquina Virtual está implementada en. Hola publicado runbooks de automatización que se usan en este artículo se encargará de este caso y solo escalar dentro hello debajo de pares de tamaño de máquina virtual. Esto significa que una máquina Virtual de Standard_D1v2 no repentinamente puede aumentarse tooStandard_G5 o reducida tooBasic_A0.
> 
> | Pares de escalado de tamaños de VM |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | Standard_D1 |Standard_D4 |
> | Standard_D11 |Standard_D14 |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>La instalación de las máquinas virtuales tooaccess de automatización de Azure
Hola primera cosa que necesita toodo es crear una cuenta de automatización de Azure que hospedará Hola runbooks usan tooscale Hola conjunto de escalado de VM instancias. Servicio de automatización de hello había introducido recientemente característica "Ejecutar como cuenta de" hello lo que facilita configurar Hola entidad de servicio automáticamente runbooks en ejecución hello en nombre de usuario de hello muy fácil. Puede leer más sobre esto en el siguiente artículo de hello:

* [Autenticación de Runbooks con una cuenta de ejecución de Azure](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importar runbooks de escala Vertical de automatización de Azure de hello en su suscripción
Hola runbooks que son necesarios para escalar verticalmente la máquina Virtual ya se han publicado en hello Galería de runbooks de automatización de Azure. Deberá tooimport en su suscripción. Puede obtener información sobre cómo tooimport runbooks leyendo Hola artículo siguiente.

* [Galerías de runbooks y módulos para la automatización de Azure](../../automation/automation-runbook-gallery.md)

Hola runbooks que necesitan toobe importado se muestran en la imagen Hola siguiente

![Importar runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Agregar un runbook de tooyour de webhook
Una vez que haya importado Hola runbooks deberá tooadd un runbook de toohello webhook por lo que se puede desencadenar una alerta de una máquina Virtual. detalles de Hola de cómo crear un webhook para el Runbook se pueden leer aquí

* [Webhooks de Automatización de Azure](../../automation/automation-webhooks.md)

Asegúrese de que copiar hello webhook antes de cerrar el cuadro de diálogo de hello webhook ya que será necesario en la sección siguiente Hola.

## <a name="add-an-alert-tooyour-virtual-machine"></a>Agregar una alerta tooyour Máquina Virtual
1. Seleccione la configuración de la máquina virtual.
2. Seleccione "Reglas de alerta".
3. Seleccione "Agregar alerta".
4. Seleccione una alerta de hello toofire métrica en
5. Seleccionar una condición que, cuando cumple will provocar Hola alerta toofire
6. Seleccione un umbral para la condición de hello en el paso 5. toobe cumplido
7. Seleccionar un período sobre qué Hola supervisar el servicio comprobará de condición de Hola y el umbral en los pasos 5 y 6
8. Pegue en webhook Hola que copió desde la sección anterior de Hola.

![Agregar alerta tooVirtual máquina 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Agregar alerta tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

