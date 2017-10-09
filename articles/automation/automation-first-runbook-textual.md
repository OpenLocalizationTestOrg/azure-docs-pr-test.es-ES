---
title: "aaaMy primer flujo de trabajo de PowerShell runbook en automatización de Azure | Documentos de Microsoft"
description: "Tutorial que le guía por la creación de hello, probar y publicar de un runbook de texto simple con flujo de trabajo de PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: flujo de trabajo de powershell, ejemplos de flujo de trabajo de powershell, powershell para flujos de trabajo
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;bwren
ms.openlocfilehash: b5a34d363ef4865878f3f68119833367b5280f83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-workflow-runbook"></a>Mi primer runbook de flujo de trabajo de PowerShell

> [!div class="op_single_selector"]
> * [Gráfico](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Flujo de trabajo de PowerShell](automation-first-runbook-textual.md)
> 
> 

Este tutorial le guía por la creación de hello de un [runbook de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) en automatización de Azure. Empezaremos con un runbook simple que se pruebe y publique al explicar cómo tootrack Hola estado de trabajo de runbook de Hola. Después se modifique Hola runbook tooactually administrar recursos de Azure, en este caso a partir de una máquina virtual de Azure. Por último hacemos Hola runbook más sólido mediante la adición de parámetros del runbook.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesitará Hola siguientes:

* Suscripción de Azure. Si aún no tiene ninguna, puede [activar las ventajas de la suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o <a href="/pricing/free-account/" target="_blank">[registrarse para obtener una cuenta gratis](https://azure.microsoft.com/free/).
* [Cuenta de automatización](automation-sec-configure-azure-runas-account.md) toohold Hola runbook y autenticar tooAzure recursos.  Esta cuenta debe tener permiso toostart y detener la máquina virtual de Hola.
* Una máquina virtual de Azure. Detendremos e iniciaremos esta máquina, por lo que no debería ser una máquina virtual de producción.

## <a name="step-1---create-new-runbook"></a>Paso 1: crear nuevo runbook
Comenzaremos creando un runbook simple que genera texto hello *Hello World*.

1. Hola portal de Azure, abra su cuenta de automatización.  
   página cuenta de automatización de Hello ofrece una vista rápida de los recursos de hello en esta cuenta. Ya debería tener algunos recursos. La mayoría de los que es módulos de Hola que se incluyen automáticamente en una nueva cuenta de automatización. También debe tener activo de credencial de Hola que se menciona en hello [requisitos previos](#prerequisites).
2. Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.<br><br> ![Control de runbooks](media/automation-first-runbook-textual/runbooks-control-tiles.png)
3. Crear un nuevo runbook haciendo clic en hello **agregar un runbook** botón y, a continuación, **crear un nuevo runbook**.
4. Asigne Hola runbook Hola nombre *MyFirstRunbook flujo de trabajo*.
5. En este caso, vamos toocreate una [runbook de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) así que seleccione **flujo de trabajo de Powershell** para **tipo de Runbook**.<br><br> ![Nuevo runbook](media/automation-first-runbook-textual/new-runbook-properties.png)
6. Haga clic en **crear** toocreate Hola runbook y editor de texto hello abierto.

## <a name="step-2---add-code-toohello-runbook"></a>Paso 2: agregar código toohello runbook
Puede cualquier código de tipo directamente en runbook hello, o puede seleccionar cmdlets, runbooks y activos de hello control de la biblioteca y se les agregado toohello runbook con los parámetros relacionados. En este tutorial, se tendrá que escribir directamente en hello runbook.

1. Nuestro runbook está vacía actualmente con solo hello necesario *flujo de trabajo* palabra clave, el nombre de Hola de nuestros runbook y llaves de Hola que se encase flujo de trabajo completo de Hola.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. Escriba *Write-Output "Hello World."* entre llaves Hola.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. Guardar Hola runbook haciendo clic en **guardar**.<br><br> ![Guardar runbook](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)

## <a name="step-3---test-hello-runbook"></a>Paso 3: Hola runbook de prueba
Antes de que publicamos Hola runbook toomake está disponible en producción, queremos tootest se toomake seguro de que funciona correctamente. Cuando se prueba un runbook, se ejecuta su versión **Borrador** y se visualizan sus resultados de forma interactiva.

1. Haga clic en **panel prueba** panel de prueba de tooopen Hola.<br><br> ![Panel Prueba](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)
2. Haga clic en **iniciar** prueba de hello toostart. Esto debería ser la opción de hello solo está habilitado.
3. Se crea un [trabajo de runbook](automation-runbook-execution.md) y se muestra su estado.  
   estado del trabajo Hola se iniciará como *en cola* que indica que está esperando un runbook worker en hello toocome de nube disponible. A continuación, moverá demasiado*iniciando* cuando un trabajador notificaciones trabajo hello y, a continuación, *ejecuta* cuando se inicia realmente Hola runbook ejecuta.  
4. Cuando se completa el trabajo de runbook de hello, se muestra su salida. En nuestro caso, deberíamos ver *Hello World*.<br><br> ![Hello World](media/automation-first-runbook-textual/test-output-hello-world.png)
5. Cierre tooreturn toohello lienzo de hello prueba panel.

## <a name="step-4---publish-and-start-hello-runbook"></a>Paso 4: publicar e iniciar runbook Hola
runbook Hola que acabamos de crear aún está en modo de borrador. Necesitamos toopublish antes de poder ejecutarlo en producción. Cuando se publica un runbook, sobrescribir versión publicada actual de hello con versión de borrador de Hola. En nuestro caso, no tenemos una versión publicada aún dado que acabamos de crear runbooks Hola.

1. Haga clic en **publicar** toopublish Hola runbook y, a continuación, **Sí** cuando se le solicite.<br><br> ![Publicar](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)
2. Si se desplaza tooview izquierdo Hola runbook Hola **Runbooks** panel ahora, mostrará un **estado de creación de** de **publicada**.
3. Panel de desplazamiento toohello atrás tooview derecho Hola para **MyFirstRunbook flujo de trabajo**.  
   Hello opciones a través de la parte superior de hello nos permitirá toostart Hola runbook, programar toostart en algún momento futuro hello o cree una [webhook](automation-webhooks.md) por lo que puede iniciarse a través de una llamada HTTP.
4. Solo queremos toostart Hola runbook, haga clic en **iniciar** y, a continuación, **Sí** cuando se le solicite.<br><br> ![Iniciar runbook](media/automation-first-runbook-textual/automation-runbook-controls-start.png)
5. Se abre un panel de trabajo para el trabajo de runbook de Hola que acabamos de crear. Podemos cerrar este panel, pero en este caso le dejaremos abierto por lo que podemos ver progreso del trabajo de Hola.
6. se muestra el estado del trabajo de Hello en **resumen de trabajos** y coincidencias Hola Estados que hemos visto cuando probamos Hola runbook.<br><br> ![Resumen del trabajo](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)
7. Una vez Hola runbook estado muestra *completado*, haga clic en **salida**. se abre el panel de salida de Hello y podemos ver nuestros *Hello World*.<br><br> ![Resumen del trabajo](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)  
8. Panel de salida de hello cerrar.
9. Haga clic en **todos los registros de** panel de tooopen Hola flujos de trabajo de runbook de Hola. Sólo deberíamos ver *Hello World* en la salida de hello secuencia, pero esto puede mostrar otros flujos de un trabajo de runbook como detallado y de Error si Hola runbook escribe toothem.<br><br> ![Resumen del trabajo](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)
10. Cerrar el panel de secuencias de Hola y Hola trabajo tooreturn toohello MyFirstRunbook panel.
11. Haga clic en **trabajos** panel de trabajos de hello tooopen para este runbook. Esto muestra todos los trabajos de hello creados por este runbook. Sólo deberíamos ver un trabajo enumeran dado que solo ejecutamos trabajo Hola una vez.<br><br> ![Trabajos](media/automation-first-runbook-textual/runbook-control-job-tile.png)
12. Puede hacer clic en este Hola de tooopen trabajo mismo panel de trabajo que se ve cuando se inicia runbook Hola. Esto le permite toogo en el tiempo y ver los detalles de Hola de cualquier trabajo que se ha creado para un runbook determinado.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Paso 5: agregar autenticación toomanage recursos de Azure
Hemos probado y publicado nuestro runbook, pero hasta ahora no hace nada útil. Queremos toohave que administrar recursos de Azure. No será capaz de toodo que aunque a menos que se tienen que autenticarse con credenciales de Hola que son referencia hello tooin [requisitos previos](#prerequisites). Esto lo haremos con hello **AzureRMAccount agregar** cmdlet.

1. Editor de texto hello abierto haciendo clic en **editar** en el panel de hello MyFirstRunbook flujo de trabajo.<br><br> ![Editar runbook](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)
2. No es necesario hello **Write-Output** ya de línea, por lo que continúe y elimínelo.
3. Sitúe el cursor de hello en una línea en blanco entre llaves Hola.
4. Escriba o copie y pegue Hola después el código que controlará la autenticación Hola con la automatización de la cuenta de ejecución:

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. Haga clic en **panel prueba** por lo que podemos probar Hola runbook.
6. Haga clic en **iniciar** prueba de hello toostart. Una vez que se complete, debería recibir resultados similares toohello después, mostrar información básica de su cuenta. Esto confirma que esa credencial hello es válida.<br><br> ![Autenticar](media/automation-first-runbook-textual/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Paso 6: agregar código toostart una máquina virtual
Ahora que el runbook está autenticando tooour suscripción de Azure, podemos administrar recursos. Agregamos una toostart comando una máquina virtual. Puede elegir cualquier máquina virtual en su suscripción de Azure y, por ahora nos pondremos codificar ese nombre en hello runbook.

1. Después de *agregar AzureRmAccount*, tipo *AzureRmVM inicio-nombre 'VMName' - ResourceGroupName 'NameofResourceGroup'* proporcionan Hola nombre y grupo de recursos de hello toostart de máquina virtual.  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. Guardar Hola runbook y, a continuación, haga clic en **panel prueba** para que se pueda probar.
3. Haga clic en **iniciar** prueba de hello toostart. Una vez que se complete, compruebe que la máquina virtual Hola se inició.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Paso 7: agregar un runbook de toohello del parámetro de entrada
Actualmente se inicia el runbook Hola virtual automático que nos codificado de forma rígida en runbook hello, pero sería más útil si al iniciar runbook Hola podríamos especificamos máquina virtual de Hola. Ahora agregaremos a parámetros de entrada toohello runbook tooprovide esa funcionalidad.

1. Agregar parámetros para *VMName* y *ResourceGroupName* toohello runbook y usar estas variables con hello **AzureRmVM inicio** cmdlet como en el siguiente ejemplo de Hola.

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. Guarde Hola runbook y abra el panel de prueba de Hola. Tenga en cuenta que puede ahora proporciona valores para hello dos variables de entrada que se utilizarán en la prueba de Hola.
3. Panel de prueba de hello cerrar.
4. Haga clic en **publicar** toopublish Hola nueva versión de hello runbook.
5. Detener la máquina virtual de Hola que ha iniciado en el paso anterior de Hola.
6. Haga clic en **iniciar** toostart Hola runbook. Tipo de hello **VMName** y **ResourceGroupName** para la máquina virtual de Hola que se vayan toostart.<br><br> ![Start Runbook](media/automation-first-runbook-textual/automation-pass-params.png)<br>  
7. Cuando se completa el runbook de hello, compruebe que la máquina virtual Hola se inició.  

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks gráficos, consulte [mi primer runbook gráfico](automation-first-runbook-graphical.md)
* tooget a trabajar con runbooks de PowerShell, consulte [mi primer runbook de PowerShell](automation-first-runbook-textual-powershell.md)
* toolearn más información acerca de los tipos de runbook, sus ventajas y limitaciones, consulte [tipos de runbook de automatización de Azure](automation-runbook-types.md)
* Para obtener más información sobre la característica de compatibilidad con scripts de PowerShell, consulte [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
