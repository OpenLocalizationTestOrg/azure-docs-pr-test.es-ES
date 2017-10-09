---
title: 'Hybrid Runbook Worker: un trabajo de runbook finaliza con el estado Suspendido | Microsoft Docs'
description: "Causas de los síntomas y soluciones para error de finalización de trabajo de Hybrid Runbook Worker."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2016
ms.author: magoedte
ms.openlocfilehash: 513a90d144e7ade9c21cd7f3b718578989702c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a>Hybrid Runbook Worker: un trabajo de Runbook finaliza con el estado Suspendido
## <a name="summary"></a>Resumen
Se suspende el runbook poco después de intentar tooexecute que tres veces. Hay condiciones que podrían interrumpir Hola runbook completara correctamente y mensaje de error relacionado con hello no incluye ninguna información adicional que indica por qué. Este artículo proporciona pasos para solucionar problemas de errores de ejecución de runbook de problemas relacionados toohello Hybrid Runbook Worker.

Si el problema de Azure no se trata en este artículo, visite Hola foros de Azure en [MSDN y Hola desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Puede publicar su problema en estos foros o demasiado[ @AzureSupport en Twitter](https://twitter.com/AzureSupport). Además, puede registrar una solicitud de soporte técnico de Azure seleccionando **obtener asistencia** en hello [soporte técnico de Azure](https://azure.microsoft.com/support/options/) sitio.

## <a name="symptom"></a>Síntoma
Se produce un error en la ejecución de un runbook y se ha devuelto un error hello, "hello acción de trabajo 'Activate' no se puede ejecutar porque el proceso de Hola se detuvo inesperadamente. acción de trabajo de Hello intentó 3 veces."

## <a name="cause"></a>Causa
Hay varias causas posibles para el error de hello: 

1. hybrid worker de Hello está detrás de un servidor proxy o firewall
2. Hello hybrid worker de Hola de equipo se está quedando tiene menos de hardware mínima Hola [requisitos](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements) 
3. Hola runbooks no se puede autenticar con recursos locales

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>Causa 1: Hybrid Runbook Worker está detrás de un firewall o proxy
Hola Hola de equipo que se está quedando Hybrid Runbook Worker está detrás de un servidor proxy o firewall y acceso de red saliente no se permitirá o configurado correctamente.

### <a name="solution"></a>Solución
Compruebe que el equipo de hello tiene acceso de salida too*.cloudapp .net en los puertos 443, 9354 y 30000-30199. 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>Causa 2: El equipo no cumple los requisitos mínimos de hardware
Hola a equipos que ejecutan Hola Hybrid Runbook Worker deben cumplir los requisitos mínimos de hardware antes de designar toohost esta característica. En caso contrario, según la utilización de recursos de Hola de otros procesos en segundo plano y la contención porque runbooks durante la ejecución, equipo de Hola se convierten en utilizarán más y provocar retrasos de trabajo de runbook o tiempos de espera. 

### <a name="solution"></a>Solución
Confirmar primero el equipo de hello designado de la característica de Hybrid Runbook Worker de hello toorun cumple requisitos mínimos de hardware de Hola.  Si es así, supervisar toodetermine de uso de CPU y memoria de las posibles correlaciones entre el rendimiento de Hola de procesos de Hybrid Runbook Worker y Windows.  Si no hay presión de CPU o memoria, esto puede indicar Hola necesidad tooupgrade o agregue procesadores adicionales, o aumento de memoria tooaddress Hola cuello de botella de recursos y resolver errores de Hola. Como alternativa, seleccione un recurso de proceso diferente que puede admitir los requisitos mínimos de Hola y escalar cuando las demandas de carga de trabajo indican que un aumento es necesario.         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>Causa 3: No se pueden autenticar los Runbooks con recursos locales.
### <a name="solution"></a>Solución
Comprobar hello **Microsoft SMA** registro de eventos para un evento correspondiente con la descripción *Win32 proceso terminó con el código [4294967295]*.  Hola razón de este error es no ha configurado la autenticación de sus runbooks o especificó Hola ejecutar como credenciales para el grupo de hello Hybrid worker.  Revise [Runbook permisos](automation-hybrid-runbook-worker.md#runbook-permissions) tooconfirm ha configurado correctamente la autenticación para los runbooks.  

