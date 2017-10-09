---
title: "aaaTroubleshooting problemas comunes de automatización de Azure | Documentos de Microsoft"
description: "Este artículo proporciona información toohelp solucionar y corregir los errores comunes de automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: "error de automatización, solución de problemas, problema"
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Solución de problemas comunes en Azure Automation 
Este artículo proporciona ayuda para solucionar los errores comunes que puede experimentar en automatización de Azure y sugiere posibles soluciones tooresolve ellos.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Errores de autenticación al trabajar con runbooks de Azure Automation
### <a name="scenario-sign-in-tooazure-account-failed"></a>Escenario: Error de la cuenta de inicio de sesión tooAzure
**Error:** recibe el error de Hola "Unknown_user_type: desconocido usuario tipo" al trabajar con los cmdlets Add-AzureAccount o AzureRmAccount de inicio de sesión de Hola.

**Razón para el error de hello:** este error se produce si el nombre de activo de credencial de hello no es válido o si hello nombre de usuario y contraseña que utilizó activo de credencial de automatización de hello toosetup no son válidos.

**Sugerencias para solucionar problemas:** en orden toodetermine cuál es el problema, tomar Hola pasos:  

1. Asegúrese de que no tiene caracteres especiales, incluidos hello  **@**  carácter de nombre de activo de credencial Hola automatización que está usando tooconnect tooAzure.  
2. Compruebe que puede utilizar el nombre de usuario de Hola y la contraseña que se almacenan en la credencial de automatización de Azure de hello en el editor de ISE de PowerShell local. Puede hacerlo ejecutando Hola siguientes cmdlets de PowerShell ISE hello:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Si la autenticación falla localmente, esto significa que no ha configurado correctamente las credenciales de Azure Active Directory. Consulte demasiado[autenticar con Azure Active Directory de tooAzure](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) cuenta blog post tooget hello Azure Active Directory configurado correctamente.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>Escenario: Hola no se puede toofind suscripción de Azure
**Error:** recibirá un error de Hola "Hola suscripción denominada ``<subscription name>`` no se puede encontrar" cuando se trabaja con los cmdlets de Select-AzureSubscription o seleccione AzureRmSubscription Hola.

**Razón para el error de hello:** este error se produce si el nombre de la suscripción de hello no es válido o si el usuario de Azure Active Directory de Hola que esté intentando tooget detalles de la suscripción de hello no está configurado como un administrador de suscripción de Hola.

**Sugerencias para solucionar problemas:** en orden toodetermine si se han autenticado correctamente tooAzure y tener acceso toohello suscripción que está tratando de tooselect, tomar Hola pasos:  

1. Asegúrese de que se ejecute hello **Add-AzureAccount** antes de ejecutar hello **Select-AzureSubscription** cmdlet.  
2. Si todavía aparece este mensaje de error, modifique el código agregando hello **Get-AzureSubscription** cmdlet siguiendo hello **Add-AzureAccount** cmdlet y, a continuación, ejecutar el código de hello.  Ahora, compruebe si la salida de hello de Get-AzureSubscription contiene los detalles de la suscripción.  

   * Si no ve los detalles de la suscripción en la salida de hello, esto significa que todavía no está inicializado suscripción Hola.  
   * Si ve los detalles de la suscripción de hello en la salida de hello, compruebe que estén usando Hola suscripción correcta nombre o identificador con hello **Select-AzureSubscription** cmdlet.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>Escenario: Autenticación tooAzure error porque está habilitada la autenticación multifactor
**Error:** recibirá un error de Hola "Add-AzureAccount: AADSTS50079: se requiere la inscripción de una autenticación firme (prueba-arriba)" al autenticar tooAzure con el nombre de usuario de Azure y la contraseña.

**Razón para el error de hello:** si tiene la autenticación multifactor en su cuenta de Azure, no puede usar un tooAzure de tooauthenticate de usuario de Azure Active Directory.  En su lugar, debe toouse un certificado o una tooAzure tooauthenticate principal de servicio.

**Sugerencias para solucionar problemas:** toouse un certificado con hello cmdlets de administración de servicios de Azure, consulte demasiado[creando y agregando un toomanage certificado Azure servicios.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) toouse una entidad de servicio con los cmdlets de Azure Resource Manager, consulte demasiado[crear servicio principal mediante el portal de Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md) y [autenticar una entidad de servicio con el Administrador de recursos de Azure.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Errores comunes al trabajar con runbooks
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>Escenario: inicio del trabajo de runbook de hello intentó tres veces, pero no pudo toostart cada vez
**Error:** su runbook genera el error de Hola "" trabajo Hola se ha intentado realizar tres veces, pero se produjo un error."

**Razón para el error de hello:** este error puede deberse a Hola siguientes motivos:  

1. Límite de memoria.  Se han documentado límites en la cantidad de memoria asignada tooa espacio aislado [límites de servicio de automatización](../azure-subscription-service-limits.md#automation-limits) para un trabajo puede producir un error, si está utilizando más de 400 MB de memoria. 

2. Módulo incompatible.  Puede ocurrir si las dependencias del módulo no son correctas. En este caso, el runbook normalmente devolverá un mensaje similar a "Comando no encontrado" o "No se puede enlazar el parámetro". 

**Sugerencias para solucionar problemas:** cualquiera de hello siguiendo las soluciones solucionará el problema de hello:  

* Métodos sugeridos toowork dentro del límite de memoria de hello son carga de trabajo de toosplit Hola entre varios runbooks, no procesar mayor cantidad de datos en memoria, toowrite salida innecesarios de sus runbooks o que tenga en cuenta cuántos puntos de control que se escriben en el PowerShell runbooks de flujo de trabajo.  

* Necesita tooupdate los módulos de Azure siguiendo los pasos de hello [cómo tooupdate módulos de PowerShell de Azure en automatización de Azure](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Escenario: error en runbook debido a un objeto deserializado
**Error:** su runbook genera el error de hello "no se puede enlazar el parámetro ``<ParameterName>``. No se puede convertir hello ``<ParameterType>`` valor de tipo Deserialized ``<ParameterType>`` tootype ``<ParameterType>``".

**Razón para el error de hello:** si su runbook es un flujo de trabajo de PowerShell, almacena objetos complejos en un formato deserializado en orden toopersist el estado del runbook si se suspende el flujo de trabajo de Hola.  

**Sugerencias de solución de problemas:**  
Cualquiera de hello después de tres soluciones solucionará este problema:

1. Si se canaliza objetos complejos de tooanother de un cmdlet, ajustar estos cmdlets en un InlineScript.  
2. Pase el nombre de Hola o el valor que debe de objeto complejo de hello en lugar de pasar el objeto completo Hola.  
3. Use un runbook de PowerShell en lugar de un runbook de flujo de trabajo de PowerShell.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>Escenario: Error en el trabajo de Runbook porque Hola asignadas superada la cuota
**Error:** el trabajo del runbook se produce un error error Hola "se ha alcanzado la cuota de Hola de trabajo total mensual Hola tiempo de ejecución para esta suscripción".

**Razón para el error de hello:** este error se produce cuando hello ejecución del trabajo excede la cuota de libre de 500 minutos de Hola para su cuenta. Esta cuota aplica a tipos de tooall de tareas de ejecución de trabajo, como probar un trabajo a partir de un trabajo desde el portal de hello, ejecutando un trabajo mediante webhooks y programar un trabajo tooexecute mediante cualquier Hola portal de Azure o en su centro de datos. toolearn más sobre los precios para la automatización, vea [automatización precios](https://azure.microsoft.com/pricing/details/automation/).

**Sugerencias para solucionar problemas:** si desea toouse más de 500 minutos de procesamiento al mes debe toochange su suscripción de nivel básico de hello nivel gratuito toohello. Puede actualizar nivel básico toohello Hola realizar pasos:  

1. Inicie sesión en tooyour suscripción de Azure  
2. Seleccione la cuenta de automatización de hello que desea tooupgrade  
3. Haga clic en **Configuración** > **Plan de tarifa y uso** > **Plan de tarifa**.  
4. En hello **elegir el nivel de precios** hoja, seleccione **básica**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Escenario: No se reconoce el Cmdlet cuando se ejecuta un runbook
**Error:** se produce un error en el trabajo de runbook con error de Hola "``<cmdlet name>``: término hello ``<cmdlet name>`` no se reconoce como nombre de Hola de cmdlet, función, archivo de script o programa ejecutable."

**Razón para el error de hello:** este error se produce cuando el motor de PowerShell de hello no puede encontrar el cmdlet de Hola que usa en su runbook.  Esto puede deberse a módulo de Hola que contiene Hola cmdlet no está presente en la cuenta de hello, hay un conflicto de nombres con un nombre de runbook, u Hola cmdlet también existe en otro módulo y automatización no puede resolver el nombre de Hola.

**Sugerencias para solucionar problemas:** cualquiera de hello siguiendo las soluciones solucionará el problema de hello:  

* Compruebe que ha escrito correctamente el nombre de cmdlet Hola.  
* Asegúrese de que existe cmdlet hello en su cuenta de automatización y que no hay ningún conflicto. tooverify si hay Hola cmdlet, abra un runbook en modo de edición y busque Hola cmdlet que desea toofind en la biblioteca de Hola o ejecuta **Get-Command ``<CommandName>``** .  Una vez que valide cmdlet hello es cuenta toohello disponibles, y que no hay ningún conflicto de nombre con otros cmdlets o runbooks, agréguelo toohello lienzo y asegúrese de que está usando un parámetro válido establecido en su runbook.  
* Si tiene un conflicto de nombres y Hola cmdlet está disponible en dos módulos diferentes, puede resolver este problema mediante el uso de nombre completo de Hola Hola cmdlet. Por ejemplo, puede usar **NombreDeMódulo\NombredeCmdlet**.  
* Si Hola runbook local se están ejecutando en un grupo de hybrid worker, asegúrese de que ese Hola/cmdlet del módulo está instalado en equipo de Hola que hospeda hybrid worker de Hola.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>Escenario: Un runbook de larga ejecución constantemente se produce un error con excepción de hello: "trabajo Hola no puede continuar ejecutándose porque se expulsó repetidamente desde Hola mismo punto de control".
**Razón para el error de hello:** es una característica del comportamiento de diseño debido toohello "Distribución equilibrada" supervisión de procesos en la automatización de Azure, que automáticamente se suspende un runbook si ejecuta durante más de 3 horas. Sin embargo, Hola devuelve el mensaje de error no proporciona "¿qué más" opciones. Un runbook se puede suspender por varios motivos. Suspende conseguirlo principalmente due tooerrors. Por ejemplo, una excepción no detectada en un runbook, un error de red o un bloqueo en Hola Runbook Worker ejecuta Hola runbook, se provocar Hola runbook toobe suspendido e iniciar desde su último punto de comprobación cuando reanuda.

**Sugerencias para solucionar problemas:** Hola documentados solución tooavoid este problema es que los puntos de control de toouse en un flujo de trabajo.  toolearn más consulte demasiado[flujos de trabajo de aprendizaje PowerShell](automation-powershell-workflow.md#checkpoints).  Encontrará una explicación más completa del "reparto equitativo" y los puntos de control en este artículo de blog [Using Checkpoints in Runbooks](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/)(Uso de puntos de control en los runbooks).

## <a name="common-errors-when-importing-modules"></a>Errores comunes al importar módulos
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>Escenario: Módulo genera un error tooimport o no se puede ejecutar cmdlets después de importar
**Error:** un módulo genera un error tooimport o se importa correctamente, pero no se extrae ningún cmdlet.

**Razón para el error de hello:** algunas razones por las que un módulo podría importar correctamente tooAzure automatización son:  

* estructura de Hello no coincide con la estructura de Hola que automatización necesita toobe en.  
* módulo de Hello es dependiente de otro módulo que no se ha implementado tooyour cuenta de automatización.  
* módulo de Hello falta sus dependencias en la carpeta de Hola.  
* Hola **AzureRmAutomationModule New** cmdlet se va a módulo de hello tooupload utilizado y no se han proporcionado la ruta de acceso de almacenamiento total de Hola o no se ha cargado el módulo de hello mediante una dirección URL accesible públicamente.  

**Sugerencias de solución de problemas:**  
Cualquiera de hello siguiendo las soluciones solucionará el problema de hello:  

* Asegúrese de que ese módulo Hola sigue Hola siguiendo el formato:  
  nombreDeMódulo.Zip **->** nombreDeMódulo o un número de versión **->** (nombreDeMódulo.psm1, nombreDeMódulo.psd1)
* Abra el archivo. psd1 de hello y compruebe si el módulo de hello tiene todas las dependencias.  Si es así, cargar estos toohello módulos cuenta de automatización.  
* Asegúrese de que los archivos .dll que se hace referencia están presentes en la carpeta del módulo de Hola.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>Errores comunes al trabajar con la Configuración de estado deseado (DSC)
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Escenario: el nodo se encuentra en estado de error con el error "No encontrado"
**Error:** nodo hello tiene un informe con **error** estado y que contiene el error de Hola "Hola intento tooget Hola acción de servidor https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction error debido a una configuración válida ``<guid>`` no se encuentra. "

**Razón para el error de hello:** este error suele producirse cuando hello nodo se asigna el nombre de la configuración de tooa (por ejemplo, ABC) en lugar de un nombre de configuración de nodo (por ejemplo, ABC. Servidor Web).  

**Sugerencias de solución de problemas:**  

* Asegúrese de que se está asignando nodo Hola con "nombre de configuración del nodo" y no Hola "nombre de configuración".  
* Puede asignar un nodo tooa de la configuración mediante el portal de Azure o con un cmdlet de PowerShell.

  * En el orden tooassign un nodo tooa de la configuración mediante el portal de Azure, abra hello **nodos** hoja, a continuación, seleccione un nodo y haga clic en **configuración de nodo de asignar** botón.  
  * En el orden tooassign un nodo tooa de la configuración mediante el cmdlet de PowerShell, use **AzureRmAutomationDscNode conjunto** cmdlet

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Escenario: no se produjeron configuraciones de nodo (archivos MOF) al compilarse una configuración
**Error:** suspende el trabajo de compilación DSC con error de hello: "la compilación se completó correctamente, pero no se generaron ninguna configuración de nodo. MOFs".

**Razón para el error de hello:** cuando Hola expresión que sigue hello **nodo** palabra clave en la configuración de hello DSC evalúa demasiado$ null, a continuación, no se producirá ninguna configuración de nodo.    

**Sugerencias de solución de problemas:**  
Cualquiera de hello siguiendo las soluciones solucionará el problema de hello:  

* Asegúrese de que ese toohello siguiente de expresión de hello **nodo** palabra clave en la definición de la configuración de hello no está evaluando demasiado null$.  
* Si se pasan ConfigurationData cuando se compila la configuración de hello, asegúrese de que está pasando valores esperados de hello requiere que la configuración de Hola desde [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>Escenario: Hola informes del nodo de DSC se quede bloqueado estado "en curso"
**Error:** el agente DSC genera el mensaje "No se encontró ninguna instancia con los valores de propiedad especificados".

**Razón para el error de hello:** ha actualizado la versión WMF y haber dañado WMI.  

**Sugerencias para solucionar problemas:** siga las instrucciones de Hola Hola [DSC problemas y limitaciones conocidos](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) problema de hello toofix.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>Escenario: No se puede toouse una credencial en una configuración de DSC
**Error:** se suspendió el trabajo de compilación DSC con error de hello: "error System.InvalidOperationException 'Credencial' del tipo de propiedad de procesamiento ``<some resource name>``: convertir y almacenar una contraseña cifrada que se permita sólo si el texto simple PSDscAllowPlainTextPassword se establece tootrue".

**Razón para el error de hello:** ya ha usado una credencial en una configuración pero no proporcionaba apropiado **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue para cada nodo configuración.  

**Sugerencias de solución de problemas:**  

* Realizar toopass seguro en hello apropiado **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue para cada configuración de nodo mencionado en la configuración de Hola. Para obtener más información, consulte demasiado[activos de DSC de automatización de Azure](automation-dsc-compile.md#assets).

## <a name="next-steps"></a>Pasos siguientes
Si ha seguido los pasos anteriores para solucionar problemas de hello y no se puede encontrar la respuesta de hello, puede revisar opciones de soporte adicionales de Hola a continuación.

* Obtener ayuda de expertos de Azure. Enviar su problema toohello [foros de Azure de MSDN o desbordamiento de la pila.](https://azure.microsoft.com/support/forums/).
* Registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **obtener asistencia** en **técnicas y soporte de facturación**.
* Si está buscando una solución de Runbook o un módulo de integración de Automatización de Azure, publique una solicitud de script en el [Centro de scripts](https://azure.microsoft.com/documentation/scripts/) .
* Si tiene comentarios o solicitudes de características para Automatización de Azure, publíquelos en [User Voice](https://feedback.azure.com/forums/34192--general-feedback).
