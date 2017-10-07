---
title: "aaaTesting un runbook en automatización de Azure | Documentos de Microsoft"
description: "Antes de publicar un runbook en automatización de Azure, puede probarlo tooensure que funciona según lo previsto.  Este artículo se describe cómo tootest un runbook y ver su resultado."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Prueba de un runbook en Automatización de Azure
Cuando se prueba un runbook, Hola [versión de borrador](automation-creating-importing-runbook.md#publishing-a-runbook) se ejecuta y se completan las acciones que realice. No se crea ningún historial de trabajos, pero Hola [salida](automation-runbook-output-and-messages.md#output-stream) y [advertencia y Error](automation-runbook-output-and-messages.md#message-streams) se muestran las secuencias en hello panel de salida de prueba. Mensajes toohello [flujo detallado](automation-runbook-output-and-messages.md#message-streams) sólo se muestran en el panel de salida de hello si hello [$VerbosePreference variable](automation-runbook-output-and-messages.md#preference-variables) se establece tooContinue.

Incluso si se está ejecutando la versión de borrador de hello, Hola runbook ejecuta normalmente el flujo de trabajo de Hola y lleva a cabo cualquier acción con los recursos en el entorno de Hola. Por este motivo, solo debe probar runbooks en recursos no pertenecientes a entornos de producción.

Hola procedimiento tootest [tipo de runbook](automation-runbook-types.md) es Hola iguales, y no hay ninguna diferencia en las pruebas entre el editor de texto hello y editor gráfico de Hola Hola portal de Azure.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>tootest un runbook en hello portal de Azure
Puede funcionar con cualquier [tipo de runbook](automation-runbook-types.md) Hola portal de Azure.

1. Versión de borrador de hello abierto de runbook de Hola en cualquier hello [editor de texto](automation-edit-textual-runbook.md) o [editor gráfico](automation-graphical-authoring-intro.md).
2. Haga clic en hello **prueba** hoja de prueba de botón tooopen Hola.
3. Si Hola runbook tiene parámetros, se enumerarán en panel izquierdo Hola donde se puede especificar toobe de valores que se usa para pruebas de Hola.
4. Si desea que prueba de hello toorun en un [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), a continuación, cambie **parámetros de ejecución** demasiado**Hybrid Worker** y el nombre de select Hola Hola del grupo de destino.  De lo contrario, mantenga predeterminado hello **Azure** toorun Hola prueba en la nube de Hola.
5. Haga clic en hello **iniciar** prueba de botón toostart Hola.
6. Si runbook Hola está [flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) o [gráficos](automation-runbook-types.md#graphical-runbooks), a continuación, se puede detener o suspender, mientras se está probando con botones de hello debajo Hola panel de salida. Cuando se suspende un runbook de hello, completa la actividad actual de hello antes de suspenderse. Una vez suspendido el runbook de hello, puede detenerlo o reiniciarlo.
7. Inspeccionar la salida de hello de runbook de hello en el panel de salida de hello.

## <a name="next-steps"></a>Pasos siguientes
* toolearn toocreate o importar un runbook, vea [crear o importar un runbook en automatización de Azure](automation-creating-importing-runbook.md)
* toolearn más información acerca de la creación de gráficos, consulte [creación gráfica en automatización de Azure](automation-graphical-authoring-intro.md)
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)
* toolearn más información acerca de la configuración de mensajes de estado de runboks tooreturn y errores, incluidos los procedimientos recomendados, consulte [Runbook salida y mensajes en automatización de Azure](automation-runbook-output-and-messages.md)

