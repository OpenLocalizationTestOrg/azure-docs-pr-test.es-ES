---
title: "aaaMy primer PowerShell runbook en automatización de Azure | Documentos de Microsoft"
description: "Tutorial que le guía por la creación de hello, probar y publicar de un runbook simple de PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "powershell de Azure, tutorial de scripts de powershell, automatización de powershell"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;sngun
ms.openlocfilehash: abff94abe666cd8423c35b970b4162ba9247bcf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-runbook"></a>Mi primer runbook de PowerShell

> [!div class="op_single_selector"]
> * [Gráfico](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Flujo de trabajo de PowerShell](automation-first-runbook-textual.md)
> 
> 

Este tutorial le guía por la creación de hello de un [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) en automatización de Azure. Empezaremos con un runbook simple que se pruebe y publique mientras explicamos cómo tootrack Hola estado de trabajo de runbook de Hola. Después se modifique Hola runbook tooactually administrar recursos de Azure, en este caso a partir de una máquina virtual de Azure. Por último, hacemos Hola runbook más sólido mediante la adición de parámetros del runbook.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita Hola siguientes:

* Suscripción de Azure. Si aún no tiene ninguna, puede [activar las ventajas de la suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o <a href="/pricing/free-account/" target="_blank">[registrarse para obtener una cuenta gratis](https://azure.microsoft.com/free/).
* [Cuenta de automatización](automation-sec-configure-azure-runas-account.md) toohold Hola runbook y autenticar tooAzure recursos.  Esta cuenta debe tener permiso toostart y detener la máquina virtual de Hola.
* Una máquina virtual de Azure. Detendremos e iniciaremos esta máquina, por lo que no debería ser una máquina virtual de producción.

## <a name="step-1---create-new-runbook"></a>Paso 1: crear nuevo runbook
Comenzaremos creando un runbook simple que genera texto hello *Hello World*.

1. Hola portal de Azure, abra su cuenta de automatización.  
   página cuenta de automatización de Hello ofrece una vista rápida de los recursos de hello en esta cuenta. Ya debería tener algunos recursos. La mayoría de los que es módulos de Hola que se incluyen automáticamente en una nueva cuenta de automatización. También debe tener activo de credencial de Hola que se menciona en hello [requisitos previos](#prerequisites).
2. Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.<br><br> ![RunbooksControl](media/automation-first-runbook-textual-powershell/runbooks-control-tiles.png)  
3. Crear un nuevo runbook, haga clic en hello **agregar un runbook** botón y, a continuación, **crear un nuevo runbook**.
4. Asigne Hola runbook Hola nombre *MyFirstRunbook PowerShell*.
5. En este caso, vamos toocreate una [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) así que seleccione **Powershell** para **tipo de Runbook**.<br><br> ![Runbook Type](media/automation-first-runbook-textual-powershell/automation-runbook-type.png)  
6. Haga clic en **crear** toocreate Hola runbook y editor de texto hello abierto.

## <a name="step-2---add-code-toohello-runbook"></a>Paso 2: agregar código toohello runbook
Puede cualquier código de tipo directamente en runbook hello, o puede seleccionar cmdlets, runbooks y activos de hello control de la biblioteca y se les agregado toohello runbook con los parámetros relacionados. En este tutorial, escriba directamente en hello runbook.

1. Nuestro Runbook ahora está vacío, escriba *Write-Output "Hello World"*.<br><br> ![Hello World](media/automation-first-runbook-textual-powershell/automation-helloworld.png)  
2. Guardar Hola runbook haciendo clic en **guardar**.<br><br> ![Botón Guardar](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-save.png)  

## <a name="step-3---test-hello-runbook"></a>Paso 3: Hola runbook de prueba
Antes de que publicamos Hola runbook toomake está disponible en producción, queremos tootest se toomake seguro de que funciona correctamente. Cuando se prueba un runbook, se ejecuta su versión **Borrador** y se visualizan sus resultados de forma interactiva.

1. Haga clic en **panel prueba** panel de prueba de tooopen Hola.<br><br> ![Test Pane](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-test.png)  
2. Haga clic en **iniciar** prueba de hello toostart. Esto debería ser la opción de hello solo está habilitado.
3. Se crea un [trabajo de runbook](automation-runbook-execution.md) y se muestra su estado.  
   estado del trabajo Hola se inicia como *en cola* que indica que está esperando un runbook worker en hello toocome de nube disponible. A continuación, moverá demasiado*iniciando* cuando un trabajador notificaciones trabajo hello y, a continuación, *ejecuta* cuando se inicia realmente Hola runbook ejecuta.  
4. Cuando se completa el trabajo de runbook de hello, se muestra su salida. En nuestro caso, deberíamos ver *Hello World*.<br><br> ![Salida del panel de prueba](media/automation-first-runbook-textual-powershell/automation-testpane-output.png)  
5. Cierre tooreturn toohello lienzo de hello prueba panel.

## <a name="step-4---publish-and-start-hello-runbook"></a>Paso 4: publicar e iniciar runbook Hola
runbook Hola que hemos creado aún está en modo de borrador. Necesitamos toopublish antes de poder ejecutarlo en producción.  Cuando se publica un runbook, sobrescribir versión publicada actual de hello con versión de borrador de Hola.  En nuestro caso, no tenemos una versión publicada aún dado que acabamos de crear runbooks Hola.

1. Haga clic en **publicar** toopublish Hola runbook y, a continuación, **Sí** cuando se le solicite.<br><br> ![Botón Publicar](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-publish.png)  
2. Si se desplaza tooview izquierdo Hola runbook Hola **Runbooks** panel ahora, mostrará un **estado de creación de** de **publicada**.
3. Panel de desplazamiento toohello atrás tooview derecho Hola para **MyFirstRunbook PowerShell**.  
   Hello opciones a través de la parte superior de Hola nos permitirá toostart Hola runbook, ver runbook hello, programar toostart en algún momento futuro hello o crear un [webhook](automation-webhooks.md) por lo que puede iniciarse a través de una llamada HTTP.
4. Se desea toostart Hola runbook, haga clic en **iniciar** y, a continuación, haga clic en **Aceptar** cuando se abre la hoja de hello iniciar Runbook.<br><br> ![Botón Iniciar](media/automation-first-runbook-textual-powershell/automation-runbook-controls-start.png)<br>    
5. Se abre un panel de trabajo para el trabajo de runbook de Hola que hemos creado. Podemos cerrar este panel, pero en este caso se dejarla abierta por lo que podemos ver progreso del trabajo de Hola.
6. se muestra el estado del trabajo de Hello en **resumen de trabajos** y coincidencias Hola Estados que hemos visto cuando probamos Hola runbook.<br><br> ![Resumen del trabajo](media/automation-first-runbook-textual-powershell/job-pane-status-blade-jobsummary.png)<br>  
7. Una vez Hola runbook estado muestra *completado*, haga clic en **salida**. se abre el panel de salida de Hello y podemos ver nuestros *Hello World*.<br><br> ![Salida de trabajo](media/automation-first-runbook-textual-powershell/job-pane-status-blade-outputtile.png)<br> 
8. Panel de salida de hello cerrar.
9. Haga clic en **todos los registros de** panel de tooopen Hola flujos de trabajo de runbook de Hola. Sólo deberíamos ver *Hello World* en la salida de hello secuencia, pero esto puede mostrar otros flujos de un trabajo de runbook como detallado y de Error si Hola runbook escribe toothem.<br><br> ![Todos los registros](media/automation-first-runbook-textual-powershell/job-pane-status-blade-alllogstile.png)<br>   
10. Cerrar el panel de secuencias de Hola y Hola trabajo tooreturn toohello MyFirstRunbook PowerShell panel.
11. Haga clic en **trabajos** panel de trabajos de hello tooopen para este runbook. Esto muestra todos los trabajos de hello creados por este runbook. Sólo deberíamos ver un trabajo enumeran dado que solo ejecutamos trabajo Hola una vez.<br><br> ![Lista de trabajos](media/automation-first-runbook-textual-powershell/runbook-control-job-tile.png)  
12. Puede hacer clic en este trabajo tooopen Hola mismo panel de trabajo que se ve cuando se inicia runbook Hola. Esto le permite toogo en el tiempo y ver los detalles de Hola de cualquier trabajo que se ha creado para un runbook determinado.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Paso 5: agregar autenticación toomanage recursos de Azure
Hemos probado y publicado nuestro runbook, pero hasta ahora no hace nada útil. Queremos toohave que administrar recursos de Azure. No será capaz de toodo que aunque a menos que se tienen que autenticarse con credenciales de Hola que son referencia hello tooin [requisitos previos](#prerequisites). Esto lo haremos con hello **AzureRmAccount agregar** cmdlet.

1. Editor de texto hello abierto haciendo clic en **editar** en el panel de hello MyFirstRunbook PowerShell.<br><br> ![Editar runbook](media/automation-first-runbook-textual-powershell/automation-runbook-controls-edit.png)<br>   
2. No es necesario hello **Write-Output** ya de línea, por lo que continúe y elimínelo.
3. Escriba o copie y pegue Hola después el código que controla la autenticación de hello con la automatización de la cuenta de ejecución:
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
   <br>
4. Haga clic en **panel prueba** por lo que podemos probar Hola runbook.
5. Haga clic en **iniciar** prueba de hello toostart. Una vez que se complete, debería recibir resultados similares toohello después, mostrar información básica de su cuenta. Esto confirma que esa credencial hello es válida.<br><br> ![Autenticar](media/automation-first-runbook-textual-powershell/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Paso 6: agregar código toostart una máquina virtual
Ahora que el runbook está autenticando tooour suscripción de Azure, podemos administrar recursos. Agregamos una toostart comando una máquina virtual. Puede elegir cualquier máquina virtual en su suscripción de Azure, y por ahora le enviaremos codificar ese nombre en hello runbook.

1. Después de *agregar AzureRmAccount*, tipo *AzureRmVM inicio-nombre 'VMName' - ResourceGroupName 'NameofResourceGroup'* proporcionan Hola nombre y grupo de recursos de hello toostart de máquina virtual.  
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   ```
   <br>
2. Guardar Hola runbook y, a continuación, haga clic en **panel prueba** para que se pueda probar.
3. Haga clic en **iniciar** prueba de hello toostart. Una vez que se complete, compruebe que la máquina virtual Hola se inició.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Paso 7: agregar un runbook de toohello del parámetro de entrada
Actualmente se inicia el runbook Hola virtual automático que nos codificado de forma rígida en runbook hello, pero sería más útil si se especifica la máquina virtual de Hola cuando se inicie el runbook de Hola. Ahora agregaremos a parámetros de entrada toohello runbook tooprovide esa funcionalidad.

1. Agregar parámetros para *VMName* y *ResourceGroupName* toohello runbook y usar estas variables con hello **AzureRmVM inicio** cmdlet como en el siguiente ejemplo de Hola.  
   
   ```
   Param(
    [string]$VMName,
    [string]$ResourceGroupName
   )
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   ```
   <br>
2. Guarde Hola runbook y abra el panel de prueba de Hola. Ahora puede proporcionar valores para hello dos variables de entrada que se utilizan en pruebas de Hola.
3. Panel de prueba de hello cerrar.
4. Haga clic en **publicar** toopublish Hola nueva versión de hello runbook.
5. Detener la máquina virtual de Hola que ha iniciado en el paso anterior de Hola.
6. Haga clic en **iniciar** toostart Hola runbook. Tipo de hello **VMName** y **ResourceGroupName** para la máquina virtual de Hola que se vayan toostart.<br><br> ![Pasar parámetro](media/automation-first-runbook-textual-powershell/automation-pass-params.png)<br>  
7. Cuando se completa el runbook de hello, compruebe que la máquina virtual Hola se inició.

## <a name="differences-from-powershell-workflow"></a>Diferencias del flujo de trabajo de PowerShell
PowerShell runbooks ha Hola mismo ciclo de vida, capacidades y la administración como runbooks de flujo de trabajo de PowerShell, pero hay algunas diferencias y limitaciones:

1. PowerShell runbooks ejecutan tooPowerShell comparado rápido runbooks de flujo de trabajo tengan el paso de compilación.
2. Runbooks de flujo de trabajo de PowerShell admite puntos de control, mediante los puntos de control, puede reanudar runbooks de flujo de trabajo de PowerShell de cualquier punto del runbook de hello, mientras que PowerShell runbooks solo puede reanudar desde el principio de Hola.
3. Los runbooks de flujo de trabajo de PowerShell admiten la ejecución en serie y en paralelo, mientras que los runbooks de PowerShell solo puede ejecutar comandos en serie.
4. En un runbook de flujo de trabajo de PowerShell, una actividad, un comando o un bloque de script pueden tener su propio espacio de ejecución, mientras que en un runbook de PowerShell todo lo que hay en el script se ejecuta en un único espacio de ejecución. También se observan algunas [diferencias sintácticas](https://technet.microsoft.com/magazine/dn151046.aspx) entre un runbook de PowerShell nativo y un runbook de flujo de trabajo de PowerShell.

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks gráficos, consulte [mi primer runbook gráfico](automation-first-runbook-graphical.md)
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)
* tooknow más información acerca de los tipos de runbook, sus ventajas y limitaciones, consulte [tipos de runbook de automatización de Azure](automation-runbook-types.md)
* Para obtener más información sobre la característica de compatibilidad con scripts de PowerShell, consulte [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

