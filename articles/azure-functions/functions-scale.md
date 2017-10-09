---
title: planes de servicio de aplicaciones y de consumo de funciones de aaaAzure | Documentos de Microsoft
description: "Comprender cómo las funciones de Azure escala necesidades de hello toomeet de las cargas de trabajo orientado a eventos."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Plan de consumo y plan de App Service de Azure Functions 

## <a name="introduction"></a>Introducción

Azure Functions se puede ejecutar de dos formas diferentes: plan de consumo y plan de Azure App Service. plan de consumo de Hello asigna automáticamente la capacidad de proceso cuando el código se ejecuta, admita la ampliación horizontal como carga de toohandle necesarios y, a continuación, se escala hacia abajo cuando no se está ejecutando el código. Por lo tanto, no tiene toopay para máquinas virtuales inactivas y no tiene capacidad de tooreserve de antemano. En este artículo se centra en el plan de consumo de Hola. Para obtener más información acerca del funcionamiento de hello plan de servicio de aplicaciones, vea hello [información general detallada de planes de servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Si no está familiarizado con las funciones de Azure, vea hello [información general de las funciones de Azure](functions-overview.md).

Cuando se crea una aplicación de la función, debe configurar un plan de hospedaje para las funciones que contiene esa aplicación Hola. En ambos modos, una instancia de hello *host de las funciones de Azure* ejecuta las funciones hello. tipo de Hola de controles de plan:

* Cómo se escalan horizontalmente las instancias de host.
* recursos de Hola que dependen del host de tooeach disponible.

Actualmente, debe elegir el tipo de plan de Hola durante la creación de hello de aplicación de la función de hello. No se puede cambiar después. 

Puede escalar entre las capas en hello plan de servicio de aplicaciones. Plan de consumo de hello, funciones de Azure controla automáticamente toda la asignación de recursos.

## <a name="consumption-plan"></a>Plan de consumo

Cuando se usa un plan de consumo, instancias de host de las funciones de Azure Hola dinámicamente se agregan y se quitan según Hola número de eventos de entrada. Este plan se escala automáticamente y solo se le cobra por los recursos de proceso cuando se ejecutan las funciones. En un plan de consumo, una función puede ejecutarse durante un máximo de 10 minutos. 

> [!NOTE]
> Hola tiempo de espera predeterminado para las funciones en un plan de consumo es 5 minutos. valor de Hello puede ser mayor too10 minutos Hola función aplicación cambiando la propiedad de hello `functionTimeout` en [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

La facturación se basa en el tiempo de ejecución y memoria que se usa, y se agrega para todas las funciones de una aplicación de función. Para obtener más información, vea hello [funciones de Azure página de precios].

plan de consumo de Hello es el predeterminado de Hola y ofrece Hola siguientes ventajas:
- Pague solo cuando se ejecutan las funciones.
- Escale horizontalmente de forma automática, incluso durante períodos de gran carga.

## <a name="app-service-plan"></a>Plan de App Service

Hola servicio de aplicaciones planear, las función las aplicaciones que se ejecutan en máquinas virtuales dedicadas en Basic, Standard y Premium SKU, tooWeb similar aplicaciones. Máquinas virtuales dedicadas son aplicaciones de servicio de aplicaciones de tooyour asignado, lo que significa que siempre se está ejecutando el host de las funciones de Hola.

Considere la posibilidad de un plan de servicio de aplicaciones en hello casos siguientes:
- Tiene máquinas virtuales infrautilizadas que ya ejecutan otras instancias de App Service.
- Espera que su toorun de aplicaciones de la función continuamente o casi continuamente.
- Necesita más opciones de CPU o memoria que el que se proporciona en el plan de consumo de Hola.
- Es necesario toorun más de tiempo de ejecución máximo de hello permitido en el plan de consumo de Hola.

Una máquina virtual desvincula el costo del tiempo de ejecución y el tamaño de la memoria. Como resultado, no tendrá que pagar más de costo de Hola de instancia de máquina virtual de Hola que asigne. Para obtener más información acerca del funcionamiento de hello plan de servicio de aplicaciones, vea hello [información general detallada de planes de servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Con un plan de App Service, se puede escalar horizontalmente de forma manual mediante la incorporación de más instancias de máquina virtual o se puede habilitar el escalado automático. Para obtener más información, consulte [Escalación del recuento de instancias de forma manual o automática](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). También puede escalar verticalmente eligiendo un plan de App Service diferente. Vea [Escalado vertical de aplicaciones en Azure](../app-service-web/web-sites-scale.md) para obtener más información. Si tiene previsto toorun funciones de JavaScript en un plan de servicio de aplicaciones, debe elegir un plan que tiene menos núcleos. Para obtener más información, vea hello [referencia de JavaScript para funciones](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### Always On

Si se ejecuta en un plan de servicio de aplicaciones, debe habilitar hello **Always On** configuración para que la aplicación de la función se ejecuta correctamente. En un plan de servicio de aplicaciones, en tiempo de ejecución de funciones de hello quedará inactivo después de unos minutos de inactividad, por lo que los desencadenadores HTTP solo se "reactive" sus funciones. Esto es similar toohow que trabajos Web debe tener siempre en habilitado. 

Always On solo está disponible en un plan de App Service. En un plan de consumo, plataforma Hola activa automáticamente aplicaciones de la función.

## <a name="storage-account-requirements"></a>Requisitos de la cuenta de almacenamiento

Tanto en el plan de consumo como en el plan de App Service, una aplicación de función requiere una cuenta de Azure Storage que admita almacenamiento de Azure en blobs, colas y tablas. A nivel interno, Azure Functions usa Azure Storage para operaciones como la administración de desencadenadores y las ejecuciones de la función de registro. Algunas cuentas de almacenamiento no son compatibles con colas ni tablas, como las cuentas de almacenamiento solo para blob (incluido Premium Storage) y las cuentas de almacenamiento de uso general con replicación de almacenamiento con redundancia de zona. Estas cuentas se filtran de hello **cuenta de almacenamiento** hoja al crear una aplicación de la función.

toolearn más información acerca de los tipos de cuenta de almacenamiento, consulte [Introducción a servicios de almacenamiento de Azure de hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-hello-consumption-plan-works"></a>Cómo funciona el plan de consumo de Hola

plan de consumo de Hello escala automáticamente los recursos de CPU y memoria mediante la adición de otras instancias de host de funciones de hello, en función del número de Hola de eventos que se desencadenan sus funciones en. Cada instancia de host de las funciones hello es limitado too1.5 GB de memoria.

Cuando usas Hola consumo plan de hospedaje, archivos de código de función se almacenan en recursos compartidos de archivos de Azure en la cuenta de almacenamiento principal de Hola. Cuando se elimina la cuenta de almacenamiento principal de hello, este contenido se elimina y no se puede recuperar.

> [!NOTE]
> Cuando se usa un desencadenador de blob en un plan de consumo, puede haber una demora de 10 minutos de tooa en el procesamiento de nuevos blobs si una aplicación de la función ha quedado inactiva. Después de que se ejecuta la aplicación de la función de hello, blobs se procesan inmediatamente. tooavoid inicial este retraso, considere una de las siguientes opciones de hello:
> - Usar un plan de App Service con Always On habilitado
> - Utilice otro blob de hello tootrigger mecanismo de procesamiento, por ejemplo, un mensaje de la cola que contiene el nombre del blob Hola. Para ver un ejemplo, consulte [desencadenador de cola con enlace de entrada de blob](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Escalado del entorno de tiempo de ejecución

Las funciones de Azure usa un componente denominado hello *controlador escala* toomonitor Hola tasa de eventos y determinar si tooscale salir o reducir verticalmente. controlador de la escala de Hello usa la heurística para cada tipo de desencadenador. Por ejemplo, cuando se usa un desencadenador de almacenamiento de cola de Azure, se escala en función de la longitud de la cola de Hola y la edad de Hola Hola más antigua del mensaje de cola.

unidad de Hola de escala es la aplicación de la función de hello. Cuando la aplicación de la función de hello es escalar horizontalmente, más recursos están asignados toorun varias instancias de host de las funciones de Azure Hola. Por el contrario, tal y como se reduzca la demanda de proceso, controlador de la escala de hello quita instancias de host de la función. número de Hola de instancias finalmente es reducida toozero cuando no hay funciones que se ejecutan dentro de una aplicación de la función.

![Controlador de escala que supervisa los eventos y la creación de instancias](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Modelo de facturación

Facturación del plan de consumo de Hola se describe detalladamente en hello [funciones de Azure página de precios]. Uso cuando se agrega en el nivel de aplicación de función hello y recuentos de tiempo de presentación que se ejecuta el código de la función. Hola son unidades de facturación: 
* **Consumo de recursos en gigabytes-segundo (GB-s)**. Se calcula como una combinación del tamaño de la memoria y el tiempo de ejecución de todas las funciones de una aplicación de función. 
* **Ejecuciones**. Cuenta cada vez que se ejecuta una función en el evento de respuesta tooan, desencadenado por un enlace.

[funciones de Azure página de precios]: https://azure.microsoft.com/pricing/details/functions
