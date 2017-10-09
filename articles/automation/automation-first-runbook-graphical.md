---
title: "Un runbook gráfico primera aaaMy en automatización de Azure | Documentos de Microsoft"
description: "Tutorial que le guía por la creación de hello, probar y publicar de un runbook gráfico simple."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "runbook, plantilla de runbook, automatización de runbooks, runbook de azure"
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>Mi primer runbook gráfico

> [!div class="op_single_selector"]
> * [Gráfico](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Flujo de trabajo de PowerShell](automation-first-runbook-textual.md)
> 
> 

Este tutorial le guía por la creación de hello de un [runbook gráfico](automation-runbook-types.md#graphical-runbooks) en automatización de Azure.  Empezaremos con un runbook simple que comprueba y publica mientras explicamos cómo tootrack Hola estado de trabajo de runbook de Hola.  Después se modifique Hola runbook tooactually administrar recursos de Azure, en este caso a partir de una máquina virtual de Azure.  A continuación, se complete tutorial Hola realizando más sólida Hola runbook mediante la adición de parámetros del runbook y vínculos condicionales.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesitará Hola después.

* Suscripción de Azure.  Si aún no tiene ninguna, puede [activar las ventajas de la suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o <a href="/pricing/free-account/" target="_blank">[registrarse para obtener una cuenta gratis](https://azure.microsoft.com/free/).
* [Cuenta de automatización de Azure](automation-sec-configure-azure-runas-account.md) toohold Hola runbook y autenticar tooAzure recursos.  Esta cuenta debe tener permiso toostart y detener la máquina virtual de Hola.
* Una máquina virtual de Azure.  Detendremos e iniciaremos esta máquina, por lo que no debería ser de producción.

## <a name="step-1---create-runbook"></a>Paso 1: Creación del runbook
Comenzamos creando un runbook simple que genera texto hello *Hello World*.

1. Hola portal de Azure, abra su cuenta de automatización.  
   página cuenta de automatización de Hello ofrece una vista rápida de los recursos de hello en esta cuenta.  Ya debería tener algunos recursos.  La mayoría de los que es módulos de Hola que se incluyen automáticamente en una nueva cuenta de automatización.  También debe tener activo de credencial de Hola que se menciona en hello [requisitos previos](#prerequisites).
2. Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.<br> ![Control de runbooks](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Crear un nuevo runbook haciendo clic en hello **agregar un runbook** botón y, a continuación, **crear un nuevo runbook**.
4. Asigne Hola runbook Hola nombre *MyFirstRunbook gráfica*.
5. En este caso, vamos toocreate una [runbook gráfico](automation-graphical-authoring-intro.md) así que seleccione **Graphical** para **tipo de Runbook**.<br> ![Nuevo runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. Haga clic en **crear** toocreate Hola runbook y editor gráfico de hello abierto.

## <a name="step-2---add-activities-toohello-runbook"></a>Paso 2: agregar actividades toohello runbook
control de la biblioteca a la izquierda Hola del editor de Hola Hola permite tooselect actividades tooadd tooyour runbook.  Vamos a tooadd un **Write-Output** cmdlet toooutput texto hello runbook.

1. Hola control de la biblioteca, haga clic en el cuadro de texto de búsqueda de Hola y escriba **Write-Output**.  resultados de la búsqueda de Hola se mostrará a continuación. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Desplácese hacia abajo de la parte inferior de toohello de lista de Hola.  Puede que ya sea contextual **Write-Output** y seleccione **agregar toocanvas** o haga clic en hello elipse siguiente toohello cmdlet y, a continuación, seleccione **agregar toocanvas**.
3. Haga clic en hello **Write-Output** actividad en el lienzo de Hola.  Esto abre la hoja de control de configuración de hello, lo que permite la actividad de hello tooconfigure.
4. Hola **etiqueta** tiene como valor predeterminado toohello nombre de cmdlet de hello, pero se puede cambiar toosomething más descriptiva. También cambian*toooutput escribir Hello World*.
5. Haga clic en **parámetros** tooprovide valores para parámetros del cmdlet Hola.  
   Algunos cmdlets de tener varios conjuntos de parámetros, y deberá tooselect qué uno toouse. En este caso, **Write-Output** tiene solo un conjunto de parámetros, por lo que no es necesario tooselect uno. <br> ![Propiedades Write-Output](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. Seleccione hello **InputObject** parámetro.  Es el parámetro de Hola donde especificamos el flujo de salida de hello texto toosend toohello.
7. Hola **origen de datos** lista desplegable, seleccione **expresión de PowerShell**.  Hola **origen de datos** lista desplegable proporciona diferentes orígenes que usar toopopulate un valor de parámetro.  
   Puede usar la salida de esos orígenes como otra actividad, un recurso de Automatización o una expresión de PowerShell.  En este caso, queremos solo texto de hello toooutput *Hello World*. Podemos usar una expresión de PowerShell y especificar una cadena.
8. Hola **expresión** , escriba *"Hola mundo"* y, a continuación, haga clic en **Aceptar** dos veces tooreturn toohello lienzo.<br> ![PowerShell Expression](media/automation-first-runbook-graphical/expression-hello-world.png)
9. Guardar Hola runbook haciendo clic en **guardar**.<br> ![Guardar runbook](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>Paso 3: Hola runbook de prueba
Antes de que publicamos Hola runbook toomake está disponible en producción, queremos tootest se toomake seguro de que funciona correctamente.  Cuando se prueba un runbook, se ejecuta su versión **Borrador** y se visualizan sus resultados de forma interactiva.

1. Haga clic en **panel prueba** hoja de prueba de tooopen Hola.<br> ![Panel Prueba](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. Haga clic en **iniciar** prueba de hello toostart.  Esto debería ser la opción de hello solo está habilitado.
3. A [trabajo del runbook](automation-runbook-execution.md) se crea y su estado aparece en el panel de Hola.  
   estado del trabajo Hola se inicia como *en cola* que indica que está esperando un runbook worker en hello toobecome de nube disponible.  A continuación, mueve demasiado*iniciando* cuando un trabajador notificaciones trabajo hello y, a continuación, *ejecuta* cuando se inicia realmente Hola runbook ejecuta.  
4. Cuando se completa el trabajo de runbook de hello, se muestra su salida. En nuestro caso, deberíamos ver *Hello World*.<br> ![Hello World](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Cierre tooreturn toohello lienzo de hello prueba hoja.

## <a name="step-4---publish-and-start-hello-runbook"></a>Paso 4: publicar e iniciar runbook Hola
runbook Hola que hemos creado aún está en modo de borrador. Necesitamos toopublish antes de poder ejecutarlo en producción.  Cuando se publica un runbook, sobrescribir versión publicada actual de hello con versión de borrador de Hola.  En nuestro caso, no tenemos una versión publicada aún dado que acabamos de crear runbooks Hola.

1. Haga clic en **publicar** toopublish Hola runbook y, a continuación, **Sí** cuando se le solicite.<br> ![Publicar](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. Si se desplaza tooview izquierdo Hola runbook Hola **Runbooks** hoja, muestra un **estado de creación de** de **publicada**.
3. Hoja de Hola de desplazamiento toohello atrás tooview derecho para **MyFirstRunbook**.  
   Hello opciones a través de la parte superior de hello nos permitirá toostart Hola runbook, programar toostart en algún momento futuro hello o cree una [webhook](automation-webhooks.md) por lo que puede iniciarse a través de una llamada HTTP.
4. Solo queremos toostart Hola runbook, haga clic en **iniciar** y, a continuación, **Sí** cuando se le solicite.<br> ![Iniciar runbook](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. Se abre una hoja de trabajo para el trabajo de runbook de Hola que hemos creado.  Podemos cerrar esta hoja, pero en este caso se dejarla abierta por lo que podemos ver progreso del trabajo de Hola.
6. se muestra el estado del trabajo de Hello en **resumen de trabajos** y coincidencias Hola Estados que hemos visto cuando probamos Hola runbook.<br> ![Resumen del trabajo](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. Una vez Hola runbook estado muestra *completado*, haga clic en **salida**. Hola **salida** se abre la hoja, y podemos ver nuestros *Hello World* en el panel de Hola.<br> ![Resumen del trabajo](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. Módulo de salida de hello cerrar.
9. Haga clic en **todos los registros de** hoja de tooopen Hola flujos de trabajo de runbook de Hola.  Sólo deberíamos ver *Hello World* en la salida de hello secuencia, pero esto puede mostrar otros flujos de un trabajo de runbook como detallado y de Error si Hola runbook escribe toothem.<br> ![Resumen del trabajo](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. Cierre la hoja de todos los registros de Hola y hoja de hello trabajo hoja tooreturn toohello MyFirstRunbook.
11. Haga clic en **trabajos** tooopen hoja de trabajos de Hola para este runbook.  Esta acción muestra todos los trabajos de hello creados por este runbook. Sólo deberíamos ver un trabajo enumeran dado que solo ejecutamos trabajo Hola una vez.<br> ![Trabajos](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. Puede hacer clic en este trabajo tooopen Hola mismo panel de trabajo que se ve cuando se inicia runbook Hola.  Esto le permite toogo en el tiempo y ver los detalles de Hola de cualquier trabajo que se ha creado para un runbook determinado.

## <a name="step-5---create-variable-assets"></a>Paso 5: Creación de recursos de variables
Hemos probado y publicado nuestro runbook, pero hasta ahora no hace nada útil. Queremos toohave que administrar recursos de Azure.  Antes de configuramos Hola runbook tooauthenticate, se crea un identificador de suscripción de hello toohold variable y hacer referencia a él después configuramos hello tooauthenticate de actividad en el paso 6 a continuación.  Incluido un contexto de suscripción de referencia toohello permite tooeasily trabajo entre varias suscripciones.  Antes de continuar, copie el identificador de suscripción de hello opción panel de navegación de hello las suscripciones.  

1. En la hoja de cuentas de automatización de hello, haga clic en hello **activos** hello y mosaico **activos** se abre la hoja.
2. En la hoja de activos de hello, haga clic en hello **Variables** icono.
3. En la hoja de Variables de hello, haga clic en **agregar una variable**.<br>![Variable de Automatización](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. En hello nueva variable hoja, en hello **nombre** cuadro, escriba **AzureSubscriptionId** y Hola **valor** escriba su identificador de suscripción.  Mantener *cadena* para hello **tipo** y el valor predeterminado de Hola para **cifrado**.  
5. Haga clic en **crear** toocreate variable de saludo.  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>Paso 6: agregar autenticación toomanage recursos de Azure
Ahora que tenemos una variable toohold nuestro Id. de suscripción, podemos configurar nuestro tooauthenticate runbook con hello las credenciales de ejecución que son los que se hace referencia tooin Hola [requisitos previos](#prerequisites).  Hacerlo agregando hello Azure ejecutar como conexión **Asset** y **AzureRMAccount agregar** cmdlet toohello lienzo.  

1. Editor gráfico de hello abierto, haga clic en **editar** en la hoja de MyFirstRunbook Hola.<br> ![Editar runbook](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. No es necesario hello **escribir Hello World toooutput** ya, por lo que haga clic en él y seleccione **eliminar**.
3. En el control de la biblioteca de hello, expanda **conexiones** y agregue **AzureRunAsConnection** toohello lienzo seleccionando **agregar toocanvas**.
4. En el lienzo de hello, seleccione **AzureRunAsConnection** y en el panel de control de configuración de hello, escriba **obtener ejecutar como conexión** en hello **etiqueta** cuadro de texto.  Se trata de conexión de Hola
5. En el control de la biblioteca de hello, escriba **AzureRmAccount agregar** en el cuadro de texto de búsqueda de Hola.
6. Agregar **AzureRmAccount agregar** toohello lienzo.<br> ![Add-AzureRMAccount](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. Mantenga el mouse sobre **obtener ejecutar como conexión** hasta que aparezca un círculo en parte inferior de Hola de forma de Hola. Haga clic en el círculo de Hola y arrastre la flecha de hello demasiado**AzureRmAccount agregar**.  flecha de Hola que ha creado es un *vínculo*.  Hola runbook se inicia con **obtener ejecutar como conexión** y, a continuación, ejecute **AzureRmAccount agregar**.<br> ![Crear vínculo entre actividades](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. En el lienzo de hello, seleccione **agregar AzureRmAccount** y Hola configuración tipo de panel de control **tooAzure de inicio de sesión** en hello **etiqueta** cuadro de texto.
9. Haga clic en **parámetros** y aparece la hoja de configuración del parámetro de actividad de Hola.
10. **AzureRmAccount agregar** tiene varios conjuntos de parámetros, por lo que necesitamos tooselect uno antes de que podemos proporcionar valores de parámetro.  Haga clic en **parámetro establece** y, a continuación, seleccione hello **ServicePrincipalCertificatewithSubscriptionId** conjunto de parámetros.
11. Una vez que selecciona el conjunto de parámetros de hello, parámetros de Hola se muestran en la hoja de configuración del parámetro de actividad de Hola.  Haga clic en **APPLICATIONID**.<br> ![Agregar parámetros de cuenta de Azure Resource Manager](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. En la hoja del valor del parámetro de hello, seleccione **resultados de actividad** para hello **origen de datos** y seleccione **obtener ejecutar como conexión** en lista Hola Hola **campo ruta de acceso** tipo de cuadro de texto **ApplicationId**y, a continuación, haga clic en **Aceptar**.  Se estamos especificando el nombre de Hola de propiedad de Hola de ruta de acceso del campo Hola porque actividad hello genera un objeto con varias propiedades.
13. Haga clic en **CERTIFICATETHUMBPRINT**y en la hoja del valor del parámetro de hello, seleccione **resultados de actividad** para hello **origen de datos**.  Seleccione **obtener ejecutar como conexión** en lista Hola Hola **ruta de acceso del campo** tipo de cuadro de texto **CertificateThumbprint**y, a continuación, haga clic en **Aceptar**.
14. Haga clic en **SERVICEPRINCIPAL**y en la hoja del valor del parámetro de hello, seleccione **ConstantValue** para hello **origen de datos**, haga clic en la opción de hello **True**y, a continuación, haga clic en **Aceptar**.
15. Haga clic en **TENANTID**y en la hoja del valor del parámetro de hello, seleccione **resultados de actividad** para hello **origen de datos**.  Seleccione **obtener ejecutar como conexión** en lista Hola Hola **ruta de acceso del campo** tipo de cuadro de texto **TenantId**y, a continuación, haga clic en **Aceptar** dos veces.  
16. En el control de la biblioteca de hello, escriba **AzureRmContext conjunto** en el cuadro de texto de búsqueda de Hola.
17. Agregar **AzureRmContext conjunto** toohello lienzo.
18. En el lienzo de hello, seleccione **conjunto AzureRmContext** y Hola configuración tipo de panel de control **especificar Id. de suscripción** en hello **etiqueta** cuadro de texto.
19. Haga clic en **parámetros** y aparece la hoja de configuración del parámetro de actividad de Hola.
20. **Set-AzureRmContext** tiene varios conjuntos de parámetros, por lo que necesitamos tooselect uno antes de que podemos proporcionar valores de parámetro.  Haga clic en **parámetro establece** y, a continuación, seleccione hello **SubscriptionId** conjunto de parámetros.  
21. Una vez que selecciona el conjunto de parámetros de hello, parámetros de Hola se muestran en la hoja de configuración del parámetro de actividad de Hola.  Haga clic en **SubscriptionID**
22. En la hoja del valor del parámetro de hello, seleccione **activo de Variable** para hello **origen de datos** y seleccione **AzureSubscriptionId** en lista de hello y, a continuación, haga clic en **Aceptar**  dos veces.   
23. Mantenga el mouse sobre **tooAzure de inicio de sesión** hasta que aparezca un círculo en parte inferior de Hola de forma de Hola. Haga clic en el círculo de Hola y arrastre la flecha de hello demasiado**especificar Id. de suscripción**.

El runbook debe ser similar después de hello en este momento: <br>![Configuración de autenticación de Runbook](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>Paso 7: agregar la actividad toostart una máquina virtual
Aquí agregamos una **AzureRmVM inicio** actividad toostart una máquina virtual.  Puede elegir cualquier máquina virtual en su suscripción de Azure y para ahora que codificar que asigne nombre al cmdlet Hola.

1. En el control de la biblioteca de hello, escriba **AzureRm inicio** en el cuadro de texto de búsqueda de Hola.
2. Agregar **inicio AzureRmVM** toohello lienzo y, a continuación, haga clic y arrástrelo debajo **especificar Id. de suscripción**.
3. Mantenga el mouse sobre **especificar Id. de suscripción** hasta que aparezca un círculo en parte inferior de Hola de forma de Hola.  Haga clic en el círculo de Hola y arrastre la flecha de hello demasiado**AzureRmVM inicio**.
4. Seleccione **Start-AzureRmVM**.  Haga clic en **parámetros** y, a continuación, **parámetro establece** tooview Hola se establece para **AzureRmVM inicio**.  Seleccione hello **ResourceGroupNameParameterSetName** conjunto de parámetros. Tenga en cuenta que **ResourceGroupName** y **Name** tienen signos de exclamación al lado.  Esto indica que son parámetros necesarios.  Tenga en cuenta que ambos esperan valores de cadena.
5. Seleccione **Name**.  Seleccione **PowerShell expresión** para hello **origen de datos** y escriba Hola nombre de máquina virtual de hello acotado por comillas dobles que se inician con este runbook.  Haga clic en **Aceptar**.<br>![Valor del parámetro de nombre Start-AzureRmVM](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. Seleccione **ResourceGroupName**. Use **PowerShell expresión** para hello **origen de datos** y escriba el nombre de Hola Hola del grupo de recursos acotado por comillas dobles.  Haga clic en **Aceptar**.<br> ![Parámetros Start-AzureRmVM](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. Por lo que podemos probar Hola runbook, haga clic en panel de prueba.
8. Haga clic en **iniciar** prueba de hello toostart.  Una vez que se complete, compruebe que la máquina virtual Hola se inició.

El runbook debe ser similar después de hello en este momento: <br>![Configuración de autenticación de Runbook](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>Paso 8: agregar parámetros de entrada adicionales toohello runbook
Nuestro runbook inicia actualmente máquina virtual de Hola Hola grupo de recursos que se especificó en hello **AzureRmVM inicio** cmdlet.  Nuestro runbook sería más útil si podríamos especificar ambos al iniciar runbook Hola.  Agregamos ahora parámetros de entrada toohello runbook tooprovide esa funcionalidad.

1. Editor gráfico de hello abierto, haga clic en **editar** en hello **MyFirstRunbook** panel.
2. Haga clic en **de entrada y salida** y, a continuación, **Agregar entrada** panel de parámetros de entrada de Runbook de tooopen Hola.<br> ![Entrada y salida de runbook](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. Especifique *VMName* para hello **nombre**.  Mantener *cadena* para hello **tipo**, pero cambiar **obligatorio** demasiado*Sí*.  Haga clic en **Aceptar**.
4. Crear un parámetro de entrada en segundo lugar obligatorio denominado *ResourceGroupName* y, a continuación, haga clic en **Aceptar** tooclose hello **de entrada y salida** panel.<br> ![Parámetros de entrada de runbook](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. Seleccione hello **inicio AzureRmVM** actividad y, a continuación, haga clic en **parámetros**.
6. Hola de cambio **origen de datos** para **nombre** demasiado**Runbook entrada** y, a continuación, seleccione **VMName**.<br>
7. Hola de cambio **origen de datos** para **ResourceGroupName** demasiado**Runbook entrada** y, a continuación, seleccione **ResourceGroupName**.<br> ![Parámetros Start-AzureVM](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Guarde Hola runbook y abra el panel de prueba de Hola.  Tenga en cuenta que puede ahora proporciona valores para hello dos variables de entrada que se utilizan en pruebas de Hola.
9. Panel de prueba de hello cerrar.
10. Haga clic en **publicar** toopublish Hola nueva versión de hello runbook.
11. Detener la máquina virtual de Hola que ha iniciado en el paso anterior de Hola.
12. Haga clic en **iniciar** toostart Hola runbook.  Tipo de hello **VMName** y **ResourceGroupName** para la máquina virtual de Hola que se vayan toostart.<br> ![Start Runbook](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Cuando se completa el runbook de hello, compruebe que la máquina virtual Hola se inició.

## <a name="step-9---create-a-conditional-link"></a>Paso 9: Creación de un vínculo condicional
Ahora se modifique Hola runbook para que la máquina virtual de toostart Hola intenta solo si no se ha iniciado.  Para ello, agregar un **AzureRmVM Get** cmdlet toohello runbook que obtiene el estado del nivel de instancia Hola de máquina virtual de Hola. A continuación, agregar un módulo de código de flujo de trabajo de PowerShell denominado **obtener estado** con un fragmento de código de PowerShell código toodetermine si el estado de la máquina virtual de hello está en ejecución o detenido.  Un vínculo condicional de hello **Get Status** solo se ejecuta el módulo **AzureRmVM inicio** si se detiene el estado de ejecución actual de Hola.  Por último, se envíe un tooinform de mensaje si Hola máquina virtual se ha iniciado correctamente o no usar Hola cmdlet de PowerShell Write-Output.

1. Abra **MyFirstRunbook** en el editor gráfico de Hola.
2. Quitar el vínculo de hello entre **especificar Id. de suscripción** y **inicio AzureRmVM** haciendo clic en él y, a continuación, presionando hello *eliminar* clave.
3. En el control de la biblioteca de hello, escriba **AzureRm Get** en el cuadro de texto de búsqueda de Hola.
4. Agregar **AzureRmVM Get** toohello lienzo.
5. Seleccione **Get AzureRmVM** y, a continuación, **parámetro establece** tooview Hola se establece para **AzureRmVM Get**.  Seleccione hello **GetVirtualMachineInResourceGroupNameParamSet** conjunto de parámetros.  Tenga en cuenta que **ResourceGroupName** y **Name** tienen signos de exclamación al lado.  Esto indica que son parámetros necesarios.  Tenga en cuenta que ambos esperan valores de cadena.
6. En **Origen de datos** de **Nombre**, seleccione **Entrada de runbook** y **VMName**.  Haga clic en **Aceptar**.
7. En **Origen de datos** de **ResourceGroupName**, seleccione **Entrada de runbook** y **ResourceGroupName**.  Haga clic en **Aceptar**.
8. En **Origen de datos** para **Estado**, seleccione **Valor constante** y haga clic en **Verdadero**.  Haga clic en **Aceptar**.  
9. Crear un vínculo desde **especificar Id. de suscripción** demasiado**AzureRmVM Get**.
10. En el control de la biblioteca de hello, expanda **Control de Runbook** y agregue **código** toohello lienzo.  
11. Crear un vínculo desde **Get AzureRmVM** demasiado**código**.  
12. Haga clic en **código** y en el panel de configuración de hello, cambiar etiqueta demasiado**obtener estado de**.
13. Seleccione **código** hello y parámetro **Editor de código** aparece hoja.  
14. En el editor de código de hello, pegue Hola siguiente fragmento de código:
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. Crear un vínculo desde **Get Status** demasiado**AzureRmVM inicio**.<br> ![Runbook con el módulo de código](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Seleccione el vínculo de Hola y en el panel de configuración de hello, cambiar **aplicar la condición** demasiado**Sí**.   Vínculo de nota Hola activa la línea tooa discontinua que indica que la actividad de objetivo de hello solo se ejecuta si condición Hola resuelve tootrue.  
17. Para hello **expresión de condición**, tipo *$ActivityOutput ['Get Status'] - eq "Stopped"*.  **Inicio AzureRmVM** ahora sólo se puede ejecutar si se detiene la máquina virtual de Hola.
18. En el control de la biblioteca de hello, expanda **Cmdlets** y, a continuación, **Microsoft.PowerShell.Utility**.
19. Agregar **Write-Output** toohello lienzo dos veces.<br> ![Runbook con Write-Output](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. En hello primera **Write-Output** de control, haga clic en **parámetros** y cambiar hello **etiqueta** valor demasiado*notificar a la máquina virtual inicia*.
21. Para **InputObject**, cambiar **origen de datos** demasiado**PowerShell expresión** y el tipo de expresión de hello *"$VMName se inició correctamente."* .
22. En hello segundo **Write-Output** de control, haga clic en **parámetros** y cambiar hello **etiqueta** valor demasiado*notificar el error iniciar VM*
23. Para **InputObject**, cambiar **origen de datos** demasiado**PowerShell expresión** y el tipo de expresión de hello *"$VMName no se pudo iniciar."* .
24. Crear un vínculo desde **inicio AzureRmVM** demasiado**notificar a la máquina virtual inicia** y **notificar el error iniciar VM**.
25. Seleccione el vínculo de hello demasiado**notificar a la máquina virtual inicia** y cambiar **aplicar la condición de** demasiado**True**.
26. Para hello **expresión de condición**, tipo *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - eq $true*.  Este Write-Output controlan ahora sólo se puede ejecutar si la máquina virtual de Hola se ha iniciado correctamente.
27. Seleccione el vínculo de hello demasiado**notificar el error iniciar VM** y cambiar **aplicar la condición de** demasiado**True**.
28. Para hello **expresión de condición**, tipo *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - ne $true*.  Este Write-Output controlan ahora solo se ejecuta si la máquina virtual de hello no se ha iniciado correctamente.
29. Guarde Hola runbook y abra el panel de prueba de Hola.
30. Iniciar runbook de hello con la máquina virtual de hello detenido y debe comenzar.

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de la creación de gráficos, consulte [creación gráfica en automatización de Azure](automation-graphical-authoring-intro.md)
* tooget a trabajar con runbooks de PowerShell, consulte [mi primer runbook de PowerShell](automation-first-runbook-textual-powershell.md)
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)

