---
title: "implementación de aaaAutomating de una máquina virtual en Amazon Web Services | Documentos de Microsoft"
description: "Este artículo se demuestra cómo toouse creación de tooautomate de automatización de Azure de una VM de servicio Web de Amazon"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Escenario de Automatización de Azure: aprovisionamiento de una máquina virtual de AWS
En este artículo, demostraremos cómo puede aprovechar tooprovision de automatización de Azure en una máquina virtual en su suscripción de servicio Web de Amazon (AWS) y asigne un nombre específico: a esa máquina virtual que AWS hace referencia tooas "etiquetado" hello máquina virtual.

## <a name="prerequisites"></a>Requisitos previos
Para fines de Hola de este artículo, debe toohave una cuenta de automatización de Azure y una suscripción de AWS. Para más información sobre cómo configurar una cuenta de Azure Automation con las credenciales de una suscripción de AWS, consulte [Autenticación de Runbooks con Amazon Web Services](automation-configure-aws-account.md).  Esta cuenta debe creada o actualizada con sus credenciales de suscripción de AWS antes de continuar, tal y como se hará referencia a esta cuenta en estos pasos Hola.

## <a name="deploy-amazon-web-services-powershell-module"></a>Implementar un módulo Amazon Web Services de PowerShell 
Nuestro VM aprovisionamiento runbook aprovecharán toodo de módulo de PowerShell de AWS Hola su trabajo. Realizar Hola siguiendo los pasos tooadd Hola módulo tooyour cuenta de automatización que se configura con sus credenciales de suscripción AWS.  

1. Abra el explorador web y navegue toohello [Galería de PowerShell](http://www.powershellgallery.com/packages/AWSPowerShell/) y haga clic en hello **botón de automatización de implementar tooAzure**.<br><br> ![Importación del módulo AWS de PS](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. Se toman toohello página de inicio de sesión de Azure y tras la autenticación, será toohello enrutado Portal de Azure y se presenta con hello después de hoja.<br><br> ![Hoja de importación de módulo](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Hola seleccione grupo de recursos de hello **grupo de recursos** lista desplegable lista y en la hoja de parámetros de hello, proporcionar Hola siguiente información:
   
   * De hello **nuevo o cuenta de automatización existente (cadena)** lista desplegable, seleccione **existente**.  
   * Hola **nombre de la cuenta de automatización (cadena)** cuadro, escriba en el nombre exacto de Hola de hello cuenta de automatización que incluya credenciales de Hola para su suscripción de AWS.  Por ejemplo, si ha creado una cuenta dedicada denominada **AWSAutomation**, que es lo que escribe en el cuadro de Hola.
   * Seleccione Hola región adecuada de hello **ubicación de la cuenta de automatización** lista desplegable.
4. Cuando termines de escribir información de hello necesario, haga clic en **crear**.
   
   > [!NOTE]
   > Mientras importa un módulo de PowerShell en automatización de Azure, es también extraer cmdlets hello y estas actividades no aparecerá hasta que el módulo de Hola haya finalizado completamente importar y extraer Hola cmdlets. Este proceso puede tardar unos minutos.  
   > <br>
   > 
   > 
5. Hola Portal de Azure, abra su cuenta de automatización que se hace referencia en el paso 3.
6. Haga clic en hello **activos** icono y en hello **activos** hoja, seleccione hello **módulos** icono.
7. En hello **módulos** hoja verá hello **AWSPowerShell** módulo en la lista de Hola.

## <a name="create-aws-deploy-vm-runbook"></a>Implementar AWS y crear runbook de VM
Una vez Hola que se ha implementado el módulo de PowerShell de AWS, podemos ahora creamos un tooautomate runbook aprovisionar una máquina virtual en AWS mediante un script de PowerShell. pasos de Hello siguientes demuestran cómo tooleverage script de PowerShell nativo en automatización de Azure.  

> [!NOTE]
> Para obtener más opciones e información relacionada con esta secuencia de comandos, visite hello [Galería de PowerShell](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Descargar script de PowerShell New-AwsVM de Hola de hello Galería de PowerShell, abra una sesión de PowerShell y escriba Hola siguiente:<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. De hello Portal de Azure, abra su cuenta de automatización y haga clic en hello **Runbooks** icono.  
3. De hello **Runbooks** hoja, seleccione **agregar un runbook**.
4. En hello **agregar un runbook** hoja, seleccione **creación rápida** (crear un nuevo runbook).
5. En hello **Runbook** hoja de propiedades, escriba un nombre en el cuadro de nombre de hello para el runbook y de hello **tipo de Runbook** lista desplegable, seleccione **PowerShell**y, a continuación, haga clic en  **Crear**.<br><br> ![Hoja de importación de módulo](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Cuando aparezca la hoja de hello editar PowerShell Runbook, copie y pegue el script de PowerShell de hello en runbook Hola lienzo de creación.<br><br> ![Script de PowerShell de Runbook](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Tenga en cuenta los siguiente hello cuando se trabaja con el ejemplo de Hola script de PowerShell:
    > 
    > * Hola runbook contiene un número de valores de parámetros predeterminados. Evalúe todos los valores predeterminados y actualícelos cuando sea necesario.
    > * Si ha guardado sus credenciales AWS como un recurso de credencial con nombres diferentes que **AWScred**, necesitará tooupdate script de Hola en línea 57 toomatch en consecuencia.  
    > * Cuando se trabaja con hello comandos AWS CLI en PowerShell, especialmente con este runbook de ejemplo, debe especificar la región AWS Hola. En caso contrario, se producirá un error en los cmdlets de Hola.  Ver el tema AWS [especificar AWS región](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) Hola AWS herramientas para el documento de PowerShell para obtener más detalles.  
    >

7. tooretrieve una lista de nombres de imagen desde su suscripción AWS, iniciar PowerShell ISE e importar Hola AWS módulo de PowerShell.  Para realizar la autenticación con AWS, reemplace **Get-AutomationPSCredential** en su entorno ISE por **AWScred = Get-Credential**.  Se le solicitará las credenciales y puede proporcionar su **Id. de clave de acceso** para el nombre de usuario de Hola y **clave secreta de acceso** contraseña Hola.  Vea el ejemplo de Hola a continuación:  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Hello siguiente resultado se devuelve:<br><br>
   ![Obtener imágenes AWS](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Copie y pegue Hola uno de los nombres de imagen de hello en una variable de automatización como que se hace referencia en hello runbook como **$InstanceType**. Puesto que en este ejemplo, usamos Hola AWS libre en niveles de suscripción, vamos a usar **t2.micro** en nuestro ejemplo de runbook.  
9. Guardar runbook hello, a continuación, haga clic en **publicar** toopublish Hola runbook y, a continuación, **Sí** cuando se le solicite.

### <a name="testing-hello-aws-vm-runbook"></a>Hola AWS VM runbook de prueba
Antes de empezar a trabajar con pruebas runbook hello, necesitamos tooverify algunas cosas. Concretamente:  

* Se ha creado un recurso para autenticar con AWS llamado **AWScred** o script de Hola se ha actualizado tooreference nombre de Hola de su activo de credencial.    
* se ha importado el módulo de PowerShell de AWS Hello en automatización de Azure  
* Se ha creado un nuevo runbook y los valores de parámetro se han comprobado y actualizado donde ha sido necesario  
* **Registrar registros detallados** y, opcionalmente, **escribir registros de progreso** la configuración de runbook hello **registro y seguimiento** se han establecido demasiado**en**.<br><br> ![Seguimiento y registro de Runbook](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. Se desea toostart Hola runbook, haga clic en **iniciar** y, a continuación, haga clic en **Aceptar** cuando se abre la hoja de hello iniciar Runbook.
2. En la hoja de iniciar Runbook hello, proporcione un **VMname**.  Aceptar valores predeterminados de Hola para hello otros parámetros que ha configurado previamente en el script de Hola anteriormente.  Haga clic en **Aceptar** trabajo del runbook toostart Hola.<br><br> ![Iniciar nuevo runbook AWS VM](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. Se abre un panel de trabajo para el trabajo de runbook de Hola que acabamos de crear. Cierre este panel.
4. Podemos ver progreso de salida de trabajo y la vista de hello **secuencias** seleccionando hello **todos los registros de** icono de la hoja de trabajo de runbook de Hola.<br><br> ![Salida de transmisiones](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. Hola de tooconfirm se está aprovisionando la máquina virtual, inicie sesión en Hola consola de administración de AWS si no han iniciado sesión.<br><br> ![Máquinas virtual implementada en consola AWS](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks gráficos, consulte [mi primer runbook gráfico](automation-first-runbook-graphical.md)
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)
* tooknow más información acerca de los tipos de runbook, sus ventajas y limitaciones, consulte [tipos de runbook de automatización de Azure](automation-runbook-types.md)
* Para obtener más información sobre la característica de compatibilidad con scripts de PowerShell, consulte [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

