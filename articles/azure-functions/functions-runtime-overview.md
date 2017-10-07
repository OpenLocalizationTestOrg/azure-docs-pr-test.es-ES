---
title: "información general de las funciones en tiempo de ejecución aaaAzure | Documentos de Microsoft"
description: "Información general de hello vista previa en tiempo de ejecución de funciones de Azure"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Introducción al Sistema en ejecución de Azure Functions

Hola en tiempo de ejecución de funciones de Azure proporciona una nueva forma para tootake aprovechar simplicidad de Hola y la flexibilidad de las funciones de Azure de hello en local de modelo de programación. Basado en hello mismo abra raíces de origen como funciones de Azure, en tiempo de ejecución de funciones de Azure es tooprovide implementado de forma local un desarrollo casi idéntico experiencia como servicio en la nube Hola.

![Portal del Sistema en ejecución de Azure Functions (versión preliminar)][1]

Hola en tiempo de ejecución de funciones de Azure proporciona una manera para que las funciones de Azure tooexperience antes de confirmar toohello en la nube. De esta manera, recursos de código de hello que compilar, a continuación, pueden considerarse con se toohello en la nube cuando se migra.  en tiempo de ejecución de Hello también abre nuevas opciones para usted, como el uso de capacidad de proceso de reserva de Hola de los procesos de lote de toorun de equipos local durante la noche. También puede usar dispositivos dentro de sus organización tooconditionally envío datos tooother los sistemas, tanto de forma local y en la nube de Hola.

Hola en tiempo de ejecución de funciones de Azure consta de dos partes:
* Rol de administración del Sistema en ejecución de Azure Functions
* Rol de trabajo del Sistema en ejecución de Azure Functions

## <a name="azure-functions-management-role"></a>Rol de administración de Azure Functions

Hola rol de administración de funciones de Azure proporciona un host para la administración de Hola de funciones local. Esta función realiza Hola siguientes tareas:

* Hospedaje del Portal de administración de funciones de Azure, que es Hola Hola Hola misma vea Hola [portal de Azure](https://portal.azure.com). Esto permite desarrollar sus funciones en Hola igual manera que lo haría en hello portal de Azure.
* Distribución de funciones entre varios trabajadores de Functions.
* Proporciona un punto de conexión de publicación para que pueda publicar sus funciones directamente desde Microsoft Visual Studio.

## <a name="azure-functions-worker-role"></a>Rol de trabajo de Azure Functions

Roles de trabajo de Hello Azure funciones se implementan en los contenedores de Windows y es donde se ejecuta el código de función.  Puede implementar varios roles de trabajo en toda la organización; se trata de una manera clave en que los clientes pueden hacer uso de la capacidad de proceso que sobra.

## <a name="minimum-requirements"></a>Requisitos mínimos

tooget partió hello en tiempo de ejecución las funciones de Azure debe tener una máquina con **Windows Server 2016 o Windows 10 creadores Update** con acceso tooa **SQL Server** instancia.

## <a name="next-steps"></a>Pasos siguientes

Instalar hello [vista previa en tiempo de ejecución de funciones de Azure](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
