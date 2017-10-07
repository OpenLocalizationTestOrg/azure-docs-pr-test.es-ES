---
title: "aaaCreate una aplicación de la función de hello Portal de Azure | Documentos de Microsoft"
description: "Crear una nueva aplicación de función en el servicio de aplicación de Azure desde el portal de Hola."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a>Crear una aplicación de la función de hello portal de Azure

Las aplicaciones de Azure función usa la infraestructura de servicio de aplicaciones de Azure de Hola. Este tema muestra cómo toocreate una aplicación de la función en hello portal de Azure. Una aplicación de la función es contenedor de Hola que hospeda la ejecución de Hola de las funciones individuales. Cuando se crea una aplicación de la función en hello plan de hospedaje de servicio de aplicaciones, la aplicación de la función puede usar todas las características de Hola de servicio de aplicaciones.

## <a name="create-a-function-app"></a>Creación de una aplicación de función

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

Cuando cree una instancia de Function App, brinde un **nombre de aplicación** válido, que solo puede incluir letras, números y guiones. El carácter de subrayado (**_**) no se permite.

Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas. El nombre de la cuenta de almacenamiento debe ser único dentro de Azure. 

Después de crea la aplicación de la función de hello, puede crear funciones individuales en uno o más idiomas diferentes. Crear funciones [mediante el portal de hello](functions-create-first-azure-function.md#create-function), [implementación continua](functions-continuous-deployment.md), o por [cargar con FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).

## <a name="service-plans"></a>Planes de servicio

Azure Functions tiene dos planes de servicio diferentes: plan de consumo y plan de App Service. plan de consumo de Hello asigna automáticamente la capacidad de proceso cuando se ejecuta el código, escalas horizontal como carga de toohandle es necesario y, a continuación, escalas de cuando no se está ejecutando el código. Hola plan de servicio de aplicaciones proporciona la función de instalaciones de Hola de tooall de acceso de aplicación de servicio de aplicaciones. Debe elegir el plan de servicio cuando crea la instancia de Function App y actualmente no se puede cambiar. Para más información, consulte [Elección de un plan de hospedaje de Azure Functions](functions-scale.md).

Si tiene previsto toorun funciones de JavaScript en un plan de servicio de aplicaciones, debe elegir un plan con menos núcleos. Para obtener más información, vea hello [referencia de JavaScript para funciones](functions-reference-node.md#choose-single-core-app-service-plans).

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a>Requisitos de la cuenta de almacenamiento

Al crear una aplicación de la función en el servicio de aplicaciones, debe crear o vincular la cuenta del almacenamiento de Azure de propósito general tooa que admite el almacenamiento de Blob, cola y tabla. A nivel interno, Functions usa Storage para operaciones como la administración de desencadenadores y las ejecuciones de la función de registro. Algunas cuentas de almacenamiento no son compatibles con colas ni tablas, como las cuentas de almacenamiento solo para blob, Almacenamiento Premium de Azure y cuentas de almacenamiento de uso general con replicación ZRS. Estas cuentas se filtran de hoja de la cuenta de almacenamiento de hello al crear una aplicación de la función.

>[!NOTE]
>Cuando se usa el plan de hospedaje de consumo de hello, se almacenan los archivos de configuración de código y el enlace de función en el almacenamiento de archivos de Azure en la cuenta de almacenamiento principal de Hola. Cuando se elimina la cuenta de almacenamiento principal de hello, este contenido se elimina y no se puede recuperar.

toolearn más información acerca de los tipos de cuenta de almacenamiento, consulte [Introducción a servicios de almacenamiento de Azure de hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services). 

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



