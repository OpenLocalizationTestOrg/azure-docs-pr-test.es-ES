---
title: "aaaGraphical creación de automatización de Azure | Documentos de Microsoft"
description: "Edición gráfica permite toocreate runbooks de automatización de Azure sin necesidad de trabajar con el código. Este artículo proporciona una introducción de creación de toographical y todos los detalles de hello necesario toostart crear un runbook gráfico."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 4b6f840c-e941-4293-a728-b33407317943
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 6ddf18b992d5e5f7f4af95f344007a63ac498549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="graphical-authoring-in-azure-automation"></a>Creación gráfica en Automatización de Azure
## <a name="introduction"></a>Introducción
Creación gráfica permite toocreate runbooks de automatización de Azure sin las complejidades de Hola de código subyacente de Windows PowerShell o flujo de trabajo de PowerShell Hola. Agregar actividades toohello lienzo desde una biblioteca de cmdlets y runbooks, vincularlas juntos y configurar tooform un flujo de trabajo.  Si alguna vez ha trabajado con System Center Orchestrator o Service Management Automation (SMA), esto debe ser tooyou familiar.   

Este artículo proporciona una introducción toographical hello y creación de los conceptos que se debe tooget iniciado en la creación de un runbook gráfico.

## <a name="graphical-runbooks"></a>Runbooks gráficos
Todos los runbooks de Automatización de Azure son flujos de trabajo de Windows PowerShell.  Gráficos y flujo de trabajo de PowerShell gráfica runbooks generar código de PowerShell que se ejecuta por los trabajadores de la automatización de hello, pero no es capaz de tooview lo o modificarlo directamente.  Puede ser un runbook gráfico runbook de flujo de trabajo de PowerShell gráfica tooa convertido y viceversa, pero no pueden ser runbook textual tooa convertido. No se puede importar un runbook de texto existente en el editor gráfico de Hola.  

## <a name="overview-of-graphical-editor"></a>Información general del editor de gráficos
Puede abrir el editor gráfico de Hola Hola portal de Azure creando o editando un runbook gráfico.

![Área de trabajo gráfica](media/automation-graphical-authoring-intro/runbook-graphical-editor.png)

Hello las secciones siguientes describen los controles de hello en el editor gráfico de Hola.

### <a name="canvas"></a>Lienzo
Hola lienzo es donde se diseña el runbook.  Agregar actividades de los nodos de Hola Hola biblioteca control toohello runbook y conéctelos con vínculos toodefine Hola una lógica de runbook de Hola.

Puede usar controles de hello en parte inferior de Hola de hello lienzo toozoom de entrada y salida.

![Área de trabajo gráfica](media/automation-graphical-authoring-intro/runbook-canvas-controls.png)

### <a name="library-control"></a>Control de Biblioteca
Hola control de la biblioteca es donde se seleccionan [actividades](#activities) tooadd tooyour runbook.  Agréguelos lienzo toohello donde conectarlos tooother actividades.  Incluye cuatro secciones descritas en hello en la tabla siguiente.

| Sección | Descripción |
|:--- |:--- |
| Cmdlets |Incluye todos los cmdlets de Hola que se puede usar en su runbook.  Los cmdlets se organizan por módulo.  Todos los módulos de Hola que ha instalado en su cuenta de automatización de estarán disponibles. |
| Runbooks |Incluye Hola runbooks en su cuenta de automatización. Estos runbooks se pueden agregar toohello lienzo toobe utilizado como runbooks secundarios. Se muestran solo runbooks de hello mismo principales del tipo como Hola runbook que se está editando; para los gráficos se muestran runbooks solo basada en PowerShell runbooks, mientras de runbooks de flujo de trabajo de PowerShell gráfico se muestran solo flujo de trabajo-basada en PowerShell runbooks. |
| Recursos |Incluye hello [activos de automatización](http://msdn.microsoft.com/library/dn939988.aspx) en su cuenta de automatización que se puede usar en su runbook.  Cuando se agrega un runbook de tooa asset, agregará una actividad de flujo de trabajo que obtiene el recurso seleccionado de Hola.  En el caso de hello de activos de variable, puede seleccionar si tooadd un tooget actividad Hola variable Hola variable o está establecida. |
| Control de Runbook |Incluye las actividades de control de runbook que se pueden usar en el runbook actual. A *unión* toma varias entradas y espera hasta que se hayan completado todas antes de flujo de trabajo de hello continuando. A *código* actividad ejecuta una o más líneas de código de PowerShell o flujo de trabajo de PowerShell según el tipo de runbook gráfico Hola.  Puede usar esta actividad de código personalizado o para la funcionalidad que es difícil tooachieve con otras actividades. |

### <a name="configuration-control"></a>Control de Configuración
Hola control de configuración es donde debe proporcionar detalles para un objeto seleccionado en el lienzo de Hola. propiedades de Hello disponibles en este control dependerá de tipo hello del objeto seleccionado.  Cuando selecciona una opción en el control de la configuración de Hola, abrirá módulos adicionales de información adicional de orden tooprovide.

### <a name="test-control"></a>Control de Prueba
Hola control de prueba no se muestra cuando se inicia por primera vez el editor gráfico de Hola. Se abre cuando [prueba un runbook gráfico](#graphical-runbook-procedures)de manera interactiva.  

## <a name="graphical-runbook-procedures"></a>Procedimientos de runbook gráficos
### <a name="exporting-and-importing-a-graphical-runbook"></a>Exportación e importación de un runbook gráfico
Sólo se puede exportar Hola versión publicada de un runbook gráfico.  Si aún no ha publicado el runbook de hello, Hola **exportación publicado** botón se deshabilitará.  Al hacer clic en hello **exportación publicado** botón, runbook hello es equipo local tooyour descargado.  Hola nombre del archivo hello coincide con hello de hello runbook con un *graphrunbook* extensión.

![Exportar publicados](media/automation-graphical-authoring-intro/runbook-export.png)

Puede importar un archivo de runbook gráfico o flujo de trabajo de PowerShell gráfico seleccionando hello **importar** opción al agregar un runbook.   Cuando se selecciona hello tooimport de archivo, puede mantener Hola mismo **nombre** o proporcione uno nuevo.  campo de tipo de Runbook de Hello mostrará tipo hello de runbook después de que evaluación el archivo hello seleccionado y si se intenta realizar tooselect un tipo diferente que no es correcto, que aparecerá un mensaje teniendo en cuenta hay conflictos potenciales y durante la conversión, pueden producirse errores errores de sintaxis.  

![Importar runbook](media/automation-graphical-authoring-intro/runbook-import-revised20165.png)

### <a name="testing-a-graphical-runbook"></a>Prueba de un runbook gráfico
Puede probar versión de un runbook de borrador de Hola Hola portal de Azure mientras deja Hola versión publicada de runbook de hello sin cambios, o puede probar un nuevo runbook antes de que se ha publicado. Esto permite tooverify que Hola runbook funciona correctamente antes de reemplazar la versión publicada de Hola. Cuando se prueba un runbook, se ejecuta el runbook de borrador de Hola y se completan las acciones que realice. No se crea ningún historial de trabajos, pero los resultados se muestran en el panel de resultados de pruebas de Hola. 

Abrir el control de prueba de Hola para un runbook abriendo Hola runbook para su edición y, a continuación, haga clic en hello **panel prueba** botón.

![Botón Panel de prueba](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

Hola control de prueba le pedirá para cualquier parámetros de entrada, y puede iniciar runbook Hola haciendo clic en hello **iniciar** botón.

![Botones Control de Prueba](media/automation-graphical-authoring-intro/runbook-test-start.png)

### <a name="publishing-a-graphical-runbook"></a>Publicación de un runbook gráfico
Cada runbook de Automatización de Azure tiene una versión de borrador y una versión publicada. Versión publicada de hello solo está disponible toobe ejecutar y versión de borrador de hello solo se puede editar. versión publicada de Hola se ve afectado por cualquier versión de borrador de toohello de cambios. Una vez versión de borrador de hello toobe listo disponible, a continuación, se publica y se sobrescribe la versión publicada de hello con versión de borrador de Hola.

Puede publicar un runbook gráfico abriendo runbook Hola para modificar y, a continuación, haga clic en hello **publicar** botón.

![Botón Publicar](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

Cuando todavía no se ha publicado un runbook, tiene un estado de **Nuevo**.  Cuando se publica, su estado es **Publicado**.  Si edita Hola runbook después de que se ha publicado y versiones de borrador y publicada Hola son diferentes, Hola runbook tiene un estado de **en Editar**.

![Estados de runbooks](media/automation-graphical-authoring-intro/runbook-statuses-revised20165.png) 

También tiene versión Hola opción toorevert toohello publicada de un runbook.  Se inicia inmediatamente los cambios realizados desde Hola runbook se publicó por última vez y reemplaza la versión de borrador de Hola de hello runbook con la versión publicada de Hola.

![Botón toopublished revertir](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)

## <a name="activities"></a>Actividades
Las actividades son bloques de creación de hello de un runbook.  Una actividad puede ser un cmdlet de PowerShell, un runbook secundario o una actividad de flujo de trabajo.  Agregue un runbook de toohello de actividad, haga clic en él en el control de la biblioteca de Hola y seleccione **agregar toocanvas**.  A continuación, puede haga clic y arrastre tooplace de actividad de Hola en cualquier parte en hello lienzo que desee.  ubicación de hello de actividad de hello en el lienzo de hello Hello no afecta a operación Hola de runbook de hello en absoluto.  Puede distribuir el runbook pero le resulte más adecuado toovisualize su funcionamiento. 

![Agregar toocanvas](media/automation-graphical-authoring-intro/add-to-canvas-revised20165.png)

Seleccione la actividad de hello en hello lienzo tooconfigure sus propiedades y parámetros en la hoja de configuración de Hola.  Puede cambiar hello **etiqueta** de hello toosomething de actividad que sea descriptivo tooyou.  todavía se está ejecutando Hola original cmdlet, simplemente va a cambiar su nombre para mostrar que se usará en el editor gráfico de Hola.  etiqueta de Hello debe ser único en hello runbook. 

### <a name="parameter-sets"></a>Conjuntos de parámetros
Un conjunto de parámetros define los parámetros obligatorios y opcionales de Hola que acepten valores para un cmdlet en particular.  Todos los cmdlets tienen, al menos, un conjunto de parámetros y algunos tienen varios.  Si un cmdlet tiene varios conjuntos de parámetros, debe seleccionar el que usará antes de poder configurar los parámetros.  parámetros de Hola que puede configurar dependerán de conjunto de parámetros de Hola que elija.  Puede cambiar el conjunto de parámetros de hello utilizado por una actividad seleccionando **parámetro establece** y seleccionar otro conjunto.  En este caso, se pierden todos los valores de parámetro que configuró.

En el siguiente ejemplo de Hola Hola Get AzureRmVM cmdlet tiene tres conjuntos de parámetros.  No se puede configurar valores de parámetro hasta que se seleccione uno de los conjuntos de parámetros de Hola.  Hola ListVirtualMachineInResourceGroupParamSet conjunto de parámetros es para devolver todas las máquinas virtuales en un grupo de recursos y tiene un único parámetro opcional.  Hola GetVirtualMachineInResourceGroupParamSet es para especificar la máquina virtual de Hola que desee tooreturn y tiene dos obligatorio y un parámetro opcional.

![Conjunto de parámetros](media/automation-graphical-authoring-intro/get-azurermvm-parameter-sets.png)

#### <a name="parameter-values"></a>Valores de parámetro
Cuando se especifica un valor para un parámetro, seleccione un toodetermine de origen de datos cómo se especificará el valor de Hola.  orígenes de datos de Hola que están disponibles para un parámetro concreto dependerá de los valores válidos de Hola para ese parámetro.  Por ejemplo, Null no será una opción disponible para un parámetro que no permite valores nulos.

| Origen de datos | Descripción |
|:--- |:--- |
| Valor constante |Escriba un valor para el parámetro hello.  Esto solo está disponible para los siguientes tipos de datos de hello: Int32, Int64, String, Boolean, DateTime, conmutador. |
| Salida de la actividad |Salida de una actividad que precede a la actividad actual de hello en el flujo de trabajo de Hola.  Se mostrarán todas las actividades válidas.  Seleccione solo Hola actividad toouse su salida para el valor del parámetro hello.  Si actividad hello genera un objeto con varias propiedades, escriba en nombre de Hola de propiedad de Hola después de seleccionar la actividad hello. |
| Entrada de Runbook |Seleccione un parámetro de entrada de runbook como parámetro de actividad de entrada toohello. |
| Activo de variable |Seleccione una variable de Automatización como entrada. |
| Activo de credencial |Seleccione una credencial de Automatización como entrada. |
| Activo de certificado |Seleccione un certificado de Automatización como entrada. |
| Activo de conexión |Seleccione una conexión de Automatización como entrada. |
| Expresión de PowerShell |Especifique una [expresión de PowerShell](#powershell-expressions)simple.  Hola expresión se evaluará antes de resultado de hello y actividad de hello utilizado para el valor del parámetro hello.  Puede usar variables toorefer toohello salida de una actividad o un parámetro de entrada de runbook. |
| Sin configurar |Borrar cualquier valor configurado anteriormente. |

#### <a name="optional-additional-parameters"></a>Parámetros adicionales opcionales
Todos los cmdlets tendrán parámetros adicionales de hello opción tooprovide.  Se trata de parámetros comunes de PowerShell u otros parámetros personalizados.  Aparecerá un cuadro de texto en el que podrá proporcionar parámetros con la sintaxis de PowerShell.  Por ejemplo, toouse hello **detallado** parámetro común, especificaría **"-Verbose: $True"**.

### <a name="retry-activity"></a>Vuelva a intentar la actividad
**Comportamiento de reintento** permite un toobe de actividad que se ejecuta varias veces hasta que se cumpla una condición determinada, muy parecida a un bucle.  Puede utilizar esta característica para las actividades que se debe ejecutar varias veces, son propensas a errores y puede necesita más de un intento para lograr el éxito o probar la información de salida de hello de actividad de hello para datos válidos.    

Cuando se habilita el reintento de una actividad, puede establecer un retraso y una condición.  retraso de Hello es hora de hello (medido en segundos o minutos) ese runbook Hola esperará antes de que se ejecuta la actividad de Hola de nuevo.  A continuación, si no se especifica ningún retraso, actividad hello se ejecutará de nuevo inmediatamente después de que se complete. 

![Retraso de reintento de actividades](media/automation-graphical-authoring-intro/retry-delay.png)

condición de reintento de Hello es una expresión de PowerShell que se evalúa después de cada actividad hello en tiempo de ejecución.  Si expresión de hello resuelve tooTrue, a continuación, actividad hello se ejecuta de nuevo.  Si resuelve la expresión de hello tooFalse hello actividad no ejecute de nuevo y Hola runbook se mueve en la actividad siguiente toohello. 

![Retraso de reintento de actividades](media/automation-graphical-authoring-intro/retry-condition.png)

condición de reintento de Hello puede utilizar una variable denominada $RetryData que proporciona acceso tooinformation acerca de los reintentos de la actividad de Hola.  Esta variable no tiene propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| NumberOfAttempts |Número de veces que se ha ejecutado la actividad hello. |
| Salida |Salida de hello la última ejecución de actividad hello. |
| TotalDuration |Ha superado el tiempo transcurrido desde que se inició la actividad de Hola Hola la primera vez. |
| StartedAt |En primer lugar se ha iniciado el tiempo de actividad de hello formato UTC. |

A continuación se muestran ejemplos de las condiciones de reintento de actividades.

    # Run hello activity exactly 10 times.
    $RetryData.NumberOfAttempts -ge 10 

    # Run hello activity repeatedly until it produces any output.
    $RetryData.Output.Count -ge 1 

    # Run hello activity repeatedly until 2 minutes has elapsed. 
    $RetryData.TotalDuration.TotalMinutes -ge 2

Después de configurar una condición de reintento para una actividad, actividad hello incluye dos tooremind indicaciones visuales.  Uno se presenta en la actividad de Hola y Hola otro es cuando revise la configuración de Hola de actividad hello.

![Indicadores visuales de reintento de actividades](media/automation-graphical-authoring-intro/runbook-activity-retry-visual-cue.png)

### <a name="workflow-script-control"></a>Control de Script de flujo de trabajo
Un control de código es una actividad especial que acepta secuencias de comandos de PowerShell y flujo de trabajo de PowerShell según tipo hello de runbook gráfico que se crean en la funcionalidad de tooprovide de orden que en caso contrario, no estén disponible.  No puede aceptar parámetros, pero puede usar variables para los parámetros de entrada de runbook y de salida de actividad.  Se agregan todos los resultados de la actividad hello toohello databus a menos que no tenga ningún vínculo de salida en el que caso se agregó una salida de toohello de runbook de Hola.

Por ejemplo hello código siguiente realiza cálculos de fecha mediante una variable de entrada de runbook llamada $NumberOfDays.  A continuación, envía un tiempo de fecha calculada como toobe de salida utilizado por las actividades siguientes Hola runbook.

    $DateTimeNow = (Get-Date).ToUniversalTime()
    $DateTimeStart = ($DateTimeNow).AddDays(-$NumberOfDays)}
    $DateTimeStart


## <a name="links-and-workflow"></a>Vínculos y flujo de trabajo
Un **vínculo** en un runbook gráfico conecta dos actividades.  Se muestra en el lienzo de hello como una flecha que señala desde la actividad de destino de hello origen actividad toohello.  ejecutan actividades de Hello en dirección de Hola de flecha de hello con actividad de destino de Hola a partir de una vez completada la actividad de origen de hello.  

### <a name="create-a-link"></a>Creación de un vínculo
Crear un vínculo entre dos actividades por seleccionar actividad de origen de hello y un círculo de hello si hace clic en final Hola de forma Hola.  Arrastre la actividad de destino de hello flecha toohello y versión.

![Creación de un vínculo](media/automation-graphical-authoring-intro/create-link-revised20165.png)

Seleccione Hola vínculo tooconfigure sus propiedades en la hoja de configuración de Hola.  Esto incluye el tipo de vínculo de Hola que se describe en hello en la tabla siguiente.

| Tipo de vínculo | Descripción |
|:--- |:--- |
| Canalización |actividad de destino de Hello se ejecuta una vez para cada salida del objeto de actividad de origen Hola.  actividad de destino de Hello no se ejecuta si actividad de origen de hello da como resultado ninguna salida.  Salida de actividad de origen de hello está disponible como un objeto. |
| Secuencia |actividad de destino de Hello se ejecuta solo una vez.  Recibe una matriz de objetos de la actividad de origen de hello.  Resultado de la actividad de origen de hello está disponible como una matriz de objetos. |

### <a name="starting-activity"></a>Actividad de inicio
Un runbook gráfico se iniciará con cualquier actividad que no tenga un vínculo entrante.  A menudo, serán sólo una actividad que actuaría como Hola a partir de la actividad de runbook de Hola.  Si varias actividades no tiene un vínculo entrante, se iniciará runbook Hola si los ejecuta en paralelo.  A continuación, seguirá Hola vínculos toorun otras actividades como cada una se complete.

### <a name="conditions"></a>Condiciones
Al especificar una condición en un vínculo, actividad de destino de hello solo se ejecuta si la condición de hello resuelve tootrue.  Normalmente, usará una variable $ActivityOutput en una salida de hello tooretrieve de condición de actividad de origen Hola.  

Para un vínculo de la canalización, debe especificar una condición para un solo objeto y condición Hola se evalúa para cada salida del objeto por actividad de origen de hello.  actividad de destino de Hello, a continuación, se ejecuta para cada objeto que satisface la condición de Hola.  Por ejemplo, con una actividad en el origen de Get-AzureRmVm, Hola según la sintaxis podría usarse para un tooretrieve de vínculo de canalización condicional solo Hola de máquinas virtuales en el grupo de recursos denominado *Group1*.  

    $ActivityOutput['Get Azure VMs'].Name -match "Group1"

Para un vínculo de la secuencia, condición Hola sólo se evalúa una vez desde que se devuelve una matriz que contiene todos los resultados de los objetos de actividad de origen de hello.  Por este motivo, un vínculo de la secuencia no se puede usar para filtrar como un vínculo de canalización pero simplemente determinará si no se ejecuta la siguiente actividad de Hola. Tomemos como ejemplo Hola siguiendo el conjunto de actividades en nuestro runbook iniciar VM.<br> ![Vínculo condicional con secuencias](media/automation-graphical-authoring-intro/runbook-conditional-links-sequence.png)<br>
Hay tres vínculos secuencia diferente que se proporcionaron valores de los parámetros de entrada de runbook de tootwo que representa el nombre de máquina virtual y nombre de grupo de recursos en orden toodetermine que es hello las acciones apropiadas tootake: iniciar una sola máquina virtual se están comprobando, iniciar todas las máquinas virtuales en hello grupo de recursos, o todas las máquinas virtuales en una suscripción.  Hello secuencia vínculo entre tooAzure conectar y Get sola máquina virtual, aquí es lógica de la condición de hello:

    <# 
    Both VMName and ResourceGroupName runbook input parameters have values 
    #>
    (
    (($VMName -ne $null) -and ($VMName.Length -gt 0))
    ) -and (
    (($ResourceGroupName -ne $null) -and ($ResourceGroupName.Length -gt 0))
    )

Cuando se usa un vínculo condicional, se filtrarán condición Hola datos Hola disponibles en actividades de tooother de la actividad de origen de hello en esa bifurcación.  Si una actividad es vínculos de toomultiple de origen de hello, a continuación, Hola datos tooactivities disponibles en cada rama dependerá de condición de hello en vínculo Hola conectarse toothat bifurcación.

Por ejemplo, hello **AzureRmVm inicio** actividad Hola runbook siguiente inicia todas las máquinas virtuales.  Además, tiene dos vínculos condicionales.  primer vínculo condicional Hello usa la expresión de hello *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - eq $true* toofilter si la actividad de inicio AzureRmVm hello se completó correctamente.  Hola en segundo lugar utiliza la expresión de hello *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - ne $true* toofilter si toostart Hola virtual machine error en la actividad de hello AzureRmVm de inicio.  

![Ejemplo de vínculo condicional](media/automation-graphical-authoring-intro/runbook-conditional-links.png)

Cualquier actividad que sigue el primer vínculo de Hola y utiliza la salida de la actividad de Hola de Get-AzureVM solo obtendrá máquinas virtuales de Hola que se iniciaron en tiempo de Hola que Get-AzureVM se ha ejecutado.  Cualquier actividad que siga el segundo vínculo de hello solo obtendrá máquinas virtuales de Hola Hola que se detuvieron en tiempo de Hola que Get-AzureVM se ha ejecutado.  Cualquier actividad que siga Hola tercer vínculo obtendrá todas las máquinas virtuales, independientemente de su estado de ejecución.

### <a name="junctions"></a>Uniones
Una unión es una actividad especial que esperará hasta que se hayan completado todas las ramas entrantes.  Esto le permite toorun varias actividades en paralelo y asegúrese de que se han completado todas antes de continuar.

A pesar de que una unión puede tener una cantidad ilimitada de vínculos entrantes, solo uno de esos vínculos puede ser una canalización.  no está limitado el número de Hola de vínculos de secuencia entrante.  Se permitirá la unión de hello toocreate con varios vínculos de canalización entrante y se guarda Hola runbook, pero se producirá un error cuando se ejecuta.

ejemplo de Hola siguiente forma parte de un runbook que inicia un conjunto de máquinas virtuales al descargar simultáneamente revisiones toobe aplica toothose máquinas.  Una unión es tooensure usado que ambos procesos se completan antes de que continúe Hola runbook.

![unión](media/automation-graphical-authoring-intro/runbook-junction.png)

### <a name="cycles"></a>Ciclos
Un ciclo es cuando una actividad de destino se vincula volver tooits del origen de actividad de actividad o tooanother que finalmente vínculos copia tooits origen.  La creación gráfica no permite actualmente los ciclos.  Si el runbook tiene un ciclo, lo guardará como corresponde, pero recibirá un error cuando se ejecute.

![Ciclo](media/automation-graphical-authoring-intro/runbook-cycle.png)

### <a name="sharing-data-between-activities"></a>Uso compartido de datos entre actividades
Los datos que se generan mediante una actividad con un vínculo de salida se escriben toohello *databus* Hola runbook.  Las actividades de runbooks Hola pueden utilizar datos en valores de parámetro de hello databus toopopulate o incluir en el código de script.  Una actividad puede tener acceso a la salida de hello de cualquier actividad anterior en el flujo de trabajo de Hola.     

Forma en que los datos de Hola se escriben toohello databus depende de tipo de Hola de vínculo en la actividad de Hola.  Para una **canalización**, datos de hello están la salida como objetos de múltiplos.  Para una **secuencia** vincular, datos hello están resultado como una matriz.  Si solo existe un valor, se generará como una matriz de un solo elemento.

Puede tener acceso a datos en el bus de datos de hello mediante uno de estos dos métodos.  En primer lugar está usando un **resultados de actividad** toopopulate del origen de datos un parámetro de otra actividad.  Si la salida de hello es un objeto, puede especificar una sola propiedad.

![Salida de la actividad](media/automation-graphical-authoring-intro/activity-output-datasource-revised20165.png)

También puede recuperar la salida de hello de una actividad en un **PowerShell expresión** origen de datos o desde una **secuencia de comandos de flujo de trabajo** actividad con una variable ActivityOutput.  Si la salida de hello es un objeto, puede especificar una sola propiedad.  Las variables de ActivityOutput utilizan Hola según la sintaxis.

    $ActivityOutput['Activity Label']
    $ActivityOutput['Activity Label'].PropertyName 

### <a name="checkpoints"></a>Puntos de control
Puede establecer [puntos de control](automation-powershell-workflow.md#checkpoints) en un runbook gráfico de flujo de trabajo de PowerShell; para ello, seleccione *Runbook de punto de control* en cualquier actividad.  Esto hace que un toobe de punto de comprobación establecer después de que se ejecuta la actividad de Hola.

![Punto de control](media/automation-graphical-authoring-intro/set-checkpoint.png)

Los puntos de control solo se habilitan en los runbooks gráficos de flujo de trabajo de PowerShell; no están disponibles en los runbooks gráficos.  Si runbook hello usa cmdlets de Azure, debe seguir cualquier actividad de punto de comprobación con un complemento-AzureRMAccount en caso de hello runbook se suspende y se reinicia desde este punto de comprobación en un trabajo diferente. 

## <a name="authenticating-tooazure-resources"></a>Autenticación de tooAzure de recursos
Runbooks de automatización de Azure que administrar recursos de Azure requerirá autenticación tooAzure.  Hola [cuenta de ejecución](automation-offering-get-started.md#creating-an-automation-account) (también denominado tooas una entidad de servicio) es Hola predeterminado método tooaccess recursos de Azure Resource Manager de la suscripción con runbooks de automatización.  Puede agregar esta funcionalidad tooa un runbook gráfico agregando hello **AzureRunAsConnection** activo de conexión, que está usando PowerShell hello [Get-AutomationConnection](https://technet.microsoft.com/library/dn919922%28v=sc.16%29.aspx) cmdlet y [Agregar AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet toohello lienzo. Esto se ilustra en el siguiente ejemplo de Hola.<br>![Actividades de autenticación de ejecución](media/automation-graphical-authoring-intro/authenticate-run-as-account.png)<br>
Hola actividad obtener ejecutar como conexión (es decir, Get-AutomationConnection) se configura con un origen de datos de valor constante con el nombre AzureRunAsConnection.<br>![Configuración de la conexión de ejecución](media/automation-graphical-authoring-intro/authenticate-runas-parameterset.png)<br>
la actividad siguiente Hello, Add-AzureRmAccount, agrega Hola autenticado cuenta de ejecución para su uso en hello runbook.<br>
![Conjunto de parámetros Add-AzureRmAccount](media/automation-graphical-authoring-intro/authenticate-conn-to-azure-parameter-set.png)<br>
Para los parámetros de hello **APPLICATIONID**, **CERTIFICATETHUMBPRINT**, y **TENANTID** necesitará toospecify Hola nombre de propiedad de hello para la ruta de acceso del campo Hola porque actividad Hello da como resultado un objeto con varias propiedades.  En caso contrario, cuando se ejecuta runbook hello, fallará intentar tooauthenticate.  Esto es lo que necesita en un mínimo tooauthenticate cuenta de identificación de su runbook con hello.

toomaintain hacia atrás cuenta con compatibilidad para los suscriptores que ha creado una automatización un [cuenta de usuario de Azure AD](automation-create-aduser-account.md) toomanage implementación clásico de Azure o para los recursos de Azure Resource Manager, Hola tooauthenticate (método) es el cmdlet Add-AzureAccount Hola con un [activo de credencial](automation-credentials.md) que representa un usuario de Active Directory con acceso toohello cuenta de Azure.

Puede agregar esta funcionalidad tooa un runbook gráfico mediante la adición de un lienzo de toohello de activo de credencial seguido de una actividad de Add-AzureAccount.  Agregar-AzureAccount usa la actividad de la credencial de hello para su entrada.  Esto se ilustra en el siguiente ejemplo de Hola.

![Actividades de autenticación](media/automation-graphical-authoring-intro/authentication-activities.png)

Tiene tooauthenticate en hello inicio del runbook de Hola y después de cada punto de comprobación.  Esto significa agregar una actividad Add-AzureAccount adicional después de toda actividad Checkpoint-Workflow. No necesita una credencial de adición actividad ya que puede utilizar Hola igual 

![Salida de la actividad](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## <a name="runbook-input-and-output"></a>Entrada y salida de runbook
### <a name="runbook-input"></a>Entrada de Runbook
Un runbook puede requerir la entrada desde un usuario cuando se inicia Hola runbook a través de hello portal de Azure o desde otro runbook si Hola actual se utiliza como un elemento secundario.
Por ejemplo, si tiene un runbook que crea una máquina virtual, deberá tooprovide información como el nombre de Hola de máquina virtual de Hola y otras propiedades cada vez que inicie runbook Hola.  

Para aceptar entradas para un runbook, defina uno o más parámetros de entrada.  Se proporcionan valores para estos parámetros que se inicia cada runbook de Hola de tiempo.  Cuando se inicia un runbook con hello portal de Azure, se le pedirá que tooprovide valores de hello del runbook Hola parámetros de entrada.

Puede tener acceso a parámetros de entrada para un runbook, haga clic en hello **de entrada y salida** botón de barra de herramientas de runbook de Hola.  

![Entrada y salida de runbooks](media/automation-graphical-authoring-intro/runbook-edit-input-output.png) 

Se abrirá hello **de entrada y salida** control donde puede editar un parámetro de entrada existente o cree uno nuevo haciendo clic en **Agregar entrada**. 

![Agregar entrada](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

Cada parámetro de entrada se define mediante propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Nombre |nombre único de Hello del parámetro hello.  Solo puede contener caracteres alfanuméricos y no puede contener un espacio. |
| Descripción |Una descripción opcional para el parámetro de entrada de Hola. |
| Tipo |Tipo de datos esperado para el valor del parámetro hello.  Hola portal de Azure proporcionará un control adecuado para su tipo de datos de Hola para cada parámetro cuando se pida confirmación para la entrada. |
| Obligatorio |Especifica si se debe proporcionar un valor para el parámetro hello.  no se puede iniciar runbook Hola si no proporciona un valor para cada parámetro obligatorio que no tiene definido un valor predeterminado. |
| Valor predeterminado |Especifica qué valor se utiliza para el parámetro hello si no se proporciona uno.  Puede ser Null o un valor específico. |

### <a name="runbook-output"></a>Salida de runbook
Se agregarán datos creados por cualquier actividad que no tiene un vínculo de salida toohello [salida del runbook de hello](http://msdn.microsoft.com/library/azure/dn879148.aspx).  salida de Hello se guarda con el trabajo del runbook de Hola y el runbook primario tooa disponible resulta Hola runbook se utiliza como un elemento secundario.  

## <a name="powershell-expressions"></a>Expresiones de PowerShell
Una de las ventajas de Hola de edición gráfica es proporcionarle Hola capacidad toobuild un runbook con conocimiento mínimo de PowerShell.  Actualmente, es necesario tooknow un poco de PowerShell aunque para rellenar determinados [valores de parámetro](#activities) y de configuración [vincular condiciones](#links-and-workflow).  Esta sección proporciona una introducción rápida tooPowerShell expresiones para los usuarios que no estén familiarizadas con él.  En [Scripting con Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx)están disponibles todos los detalles sobre PowerShell. 

### <a name="powershell-expression-data-source"></a>Origen de datos de expresiones de PowerShell
Puede usar una expresión de PowerShell como un valor de hello toopopulate de origen de datos de un [parámetro de actividad](#activities) con resultados de Hola de algún código de PowerShell.  Podría tratarse de una sola línea de código que realizara alguna función simple o varias líneas que desarrollaran cierta lógica compleja.  Los resultados de un comando que no está asignan tooa variable es el valor del parámetro de salida toohello. 

Por ejemplo, hello siguiente comando generaría Hola fecha actual. 

    Get-Date

Hello siguientes comandos de generación una cadena de hello fecha actual y asígnela tooa variable.  contenido de Hola de variable de hello, a continuación, se envía toohello salida 

    $string = "hello current date is " + (Get-Date)
    $string

Hello siguientes comandos evaluación Hola fecha actual y devuelven una cadena que indica si Hola día actual es un fin de semana o el día de la semana. 

    $date = Get-Date
    if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
    else { "Weekday" }


### <a name="activity-output"></a>Salida de la actividad
salida de hello toouse desde una actividad anterior en runbook hello, usar la variable de hello $ActivityOutput con hello según la sintaxis.

    $ActivityOutput['Activity Label'].PropertyName

Por ejemplo, puede tener una actividad con una propiedad que requiere el nombre de Hola de una máquina virtual en cuyo caso podría utilizar la siguiente expresión de Hola.

    $ActivityOutput['Get-AzureVm'].Name

Si la propiedad de Hola que requieren el objeto de máquina virtual de hello en lugar de simplemente una propiedad, a continuación, se devolvería Hola objeto completo mediante Hola según la sintaxis.

    $ActivityOutput['Get-AzureVm']

También puede utilizar la salida de hello de una actividad en una expresión más compleja como siguiente Hola que concatena el nombre de máquina virtual de toohello de texto.

    "hello computer name is " + $ActivityOutput['Get-AzureVm'].Name


### <a name="conditions"></a>Condiciones
Use [operadores de comparación](https://technet.microsoft.com/library/hh847759.aspx) toocompare valores o para determinar si un valor coincide con un patrón especificado.  Una comparación devuelve un valor de $true o $false.

Por ejemplo, hello después condición determina si Hola virtual desde una actividad denominada *Get-AzureVM* está actualmente *detenido*. 

    $ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

siguiente Hola condición comprueba si hello misma máquina virtual está en cualquier estado distinto de *detenido*.

    $ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

Puede combinar varias condiciones, mediante un [operador lógico](https://technet.microsoft.com/library/hh847789.aspx) como **-and** u**-or**.  Por ejemplo, siguiente Hola condición comprueba si hello misma máquina virtual en el ejemplo anterior de hello está en un estado de *detenido* o *detener*.

    ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### <a name="hashtables"></a>Tablas hash
[Tablas hash](http://technet.microsoft.com/library/hh847780.aspx) son pares de nombre-valor que son útiles para devolver un conjunto de valores.  Las propiedades de ciertas actividades pueden esperar una tabla hash en lugar de un valor simple.  También puede ver contemplados hashtable tooas un diccionario. 

Crear una tabla hash con la sintaxis de hello.  Una tabla hash puede contener cualquier número de entradas, pero cada una se define mediante un nombre y valor.

    @{ <name> = <value>; [<name> = <value> ] ...}

Por ejemplo, hello expresión siguiente crea un toobe de tabla hash utilizado en el origen de datos de Hola para un parámetro de actividad que se esperaba un objeto hashtable con valores para una búsqueda de internet.

    $query = "Azure Automation"
    $count = 10
    $h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
    $h

Hello en el ejemplo siguiente se utiliza la salida de una actividad denominada *obtener conexión de Twitter* toopopulate una tabla hash.

    @{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
      'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
      'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
      'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md) 
* tooget a trabajar con runbooks gráficos, consulte [mi primer runbook gráfico](automation-first-runbook-graphical.md)
* tooknow más información acerca de los tipos de runbook, sus ventajas y limitaciones, consulte [tipos de runbook de automatización de Azure](automation-runbook-types.md)
* toounderstand cómo usar tooauthenticate Hola automatización de la cuenta de ejecución, consulte [configurar ejecutar como cuenta de Azure](automation-sec-configure-azure-runas-account.md)

