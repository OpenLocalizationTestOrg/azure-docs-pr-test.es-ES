---
title: "aaaError control en runbooks gráficos de automatización de Azure | Documentos de Microsoft"
description: "Este artículo se describe cómo error tooimplement lógica en runbooks gráficos de automatización de Azure de control."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a>Control de errores en runbooks gráficos de Azure Automation

Un tooconsider principal de diseño clave runbook está identificando problemas diferentes que puede experimentar un runbook. Dichos problemas pueden incluir condiciones de correcto, estados de error esperado y condiciones de error inesperado.

Los runbooks deben incluir el control de errores. toovalidate Hola de salida de una actividad o administrar un error con runbooks gráficos, puede usar una actividad de código de Windows PowerShell, defina la lógica condicional en el vínculo de salida de hello de actividad de Hola o aplicar otro método.          

A menudo, si se produce un error de no terminación que se produce con una actividad de runbook, se procesa cualquier actividad que siga sin tener en cuenta el error de Hola. error de Hello es toogenerate es probable que una excepción, pero actividad siguiente Hola se sigue permitiendo que toorun. Esta es manera Hola que PowerShell está diseñado toohandle errores.    

tipos de Hola de errores de PowerShell que se pueden producir durante la ejecución se finaliza o no terminación. diferencias de Hello entre errores de terminación y de no terminación son los siguientes:

* **Error de terminación**: un error grave durante la ejecución que se detiene completamente comando hello (o ejecución del script). Entre los ejemplos se incluyen cmdlets inexistentes, errores de sintaxis que impiden la ejecución de un cmdlet u otros errores irrecuperables.

* **Error de no terminación**: un error no grave que permite la ejecución toocontinue a pesar del error de Hola. Entre los ejemplos se incluyen errores operativos, como los errores de archivos no encontrados y problemas de permisos.

Automatización de Azure se han mejorado runbooks gráficos con control de errores de hello capacidad tooinclude. Ahora es posible convertir las excepciones en errores de no terminación y crear vínculos de error entre las actividades. Este proceso permite al autor de un runbook toocatch errores y administra las condiciones realizadas o inesperadas.  

## <a name="when-toouse-error-handling"></a>Cuando el control de errores toouse

Siempre que hay una actividad crítica que produce un error o una excepción, es importante tooprevent Hola siguiente actividad del runbook de procesamiento y toohandle error Hola adecuadamente. Esto es especialmente crítico cuando los runbooks dan soporte a un proceso de operaciones de un negocio o un servicio.

Para todas las actividades que pueden producir un error, el autor del runbook de hello puede agregar un vínculo de error que señala tooany otra actividad.  actividad de destino de Hello puede ser de cualquier tipo, incluidas las actividades de código, la invocación de un cmdlet, invocar otro runbook y así sucesivamente.

Además, la actividad de destino de hello también puede tener vínculos salientes. Dichos vínculos pueden ser normales o de error, Esto significa que el autor del runbook de hello puede implementar lógica compleja de control de errores sin ordenar de nuevo tooa actividad de código. Hola recomienda práctica es toocreate un runbook de control de errores dedicado con funcionalidad común, pero no es obligatorio. Lógica de control de errores en una actividad de código de PowerShell no es Hola solo opción.  

Por ejemplo, considere la posibilidad de un runbook que intenta toostart una máquina virtual e instale una aplicación en él. Si hello VM no se inicia correctamente, realiza dos acciones:

1. Envía una notificación acerca de este problema.
2. Inicia otro runbook que aprovisiona automáticamente una nueva máquina virtual.

Una solución es toohave un vínculo de error que señala la actividad de tooan que controla el paso uno. Por ejemplo, podría conectarse hello **Write-Warning** cmdlet tooan actividad para el paso dos, por ejemplo, hello **AzureRmAutomationRunbook inicio** cmdlet.

También puede generalizar este comportamiento para su uso en número de runbooks colocando estas dos actividades en un runbook de control de errores independiente y la siguiente directriz de hello sugerido anteriormente. Antes de llamar a este runbook de control de errores, puede construir un mensaje personalizado de datos Hola Hola original runbook y, a continuación, páselo como un runbook de control de errores de parámetro toohello.

## <a name="how-toouse-error-handling"></a>Cómo el control de errores toouse

Todas las actividades tienen una opción de configuración que convierte las excepciones en errores que no provocan la terminación. De manera predeterminada esta opción está deshabilitada. Se recomienda que habilite a esta configuración en cualquier actividad que desea que los errores de toohandle.  

Al habilitar esta configuración, se le asegura que los errores de terminación y de no terminación en actividad hello se tratan como errores de no terminación y pueden controlarse con un vínculo de error.  

Después de configurar esta opción, crear una actividad que controla el error de Hola. Si produce algún error en una actividad, Hola, a continuación, error saliente se siguen los vínculos y vínculos regulares de hello no es así, son aunque actividad hello genera así la salida normal.<br><br> ![Ejemplo de vínculo de error de runbook de Automation](media/automation-runbook-graphical-error-handling/error-link-example.png)

En el siguiente ejemplo de Hola, un runbook recupera una variable que contiene el nombre del equipo Hola de una máquina virtual. A continuación, intentar toostart Hola virtual machine con la siguiente actividad de Hola.<br><br> ![Ejemplo de control de errores de runbook de Automation](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

Hola **Get-AutomationVariable** actividad y **AzureRmVm inicio** son tooconvert configurado excepciones tooerrors.  Si hay problemas para conseguir saludo inicial o variable Hola VM, a continuación, se generan errores.<br><br> ![Configuración de la actividad de control de errores de runbook de Automation](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)

Fluyan de vínculos de errores de estos tooa de actividades único **la administración de errores** actividad (actividad de código). Esta actividad se configura con una expresión simple de PowerShell que usa hello *Throw* toostop palabra clave de procesamiento, junto con *$Error.Exception.Message* tooget mensaje de Hola que describe Hola excepción actual.<br><br> ![Ejemplo de código de control de errores de runbook de Automation](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)


## <a name="next-steps"></a>Pasos siguientes

* toolearn más información acerca de los vínculos y tipos de vínculo en runbooks gráficos, consulte [edición gráfica en automatización de Azure](automation-graphical-authoring-intro.md#links-and-workflow).

* más información acerca de la ejecución de un runbook, cómo toomonitor runbook trabajos y otros detalles técnicos, consulte toolearn [realizar un seguimiento de un trabajo de runbook](automation-runbook-execution.md).
