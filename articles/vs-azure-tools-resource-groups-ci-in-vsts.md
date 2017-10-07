---
title: "integración de aaaContinuous en VS Team Services mediante proyectos de grupo de recursos de Azure | Documentos de Microsoft"
description: "Describe cómo se proyecta tooset la integración continua en Visual Studio Team Services mediante la implementación de grupo de recursos de Azure en Visual Studio."
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Integración continua en Visual Studio Team Services mediante proyectos de implementación del Grupo de recursos de Azure
toodeploy una plantilla de Azure, realizar tareas en varias fases: compilación, prueba, tooAzure copia (también denominada "Staging") o una plantilla de implementación. Hay dos maneras diferentes toodeploy plantillas tooVisual Studio Team Services (VS Team Services). Ambos métodos proporcionan Hola mismos resultados, elija Hola que mejor se adapte a su flujo de trabajo.

1. Agregar una definición de compilación de tooyour paso a paso que se ejecuta el script de PowerShell de Hola que se incluye en el proyecto de implementación de grupo de recursos de Azure de hello (Deploy-AzureResourceGroup.ps1). script de Hola copia artefactos y, a continuación, implementa la plantilla de Hola.
2. Agregue varios pasos de compilación de VS Team Services, cada uno de los cuales realiza una tarea de fase.

En este artículo se muestran ambas opciones. primera opción de Hello tiene la ventaja de Hola de con hello usa la misma secuencia de comandos por los desarrolladores de Visual Studio y se proporciona coherencia a lo largo del ciclo de vida de Hola. segunda opción de Hello ofrece una secuencia de comandos integrada toohello alternativa adecuada. Ambos procedimientos suponen que ya tiene un proyecto de implementación de Visual Studio activado en VS Team Services.

## <a name="copy-artifacts-tooazure"></a>Copie los artefactos tooAzure
Cualquiera que sea el escenario de hello, si dispone de los artefactos que son necesarios para la implementación de plantilla, debe dar toothem de acceso de administrador de recursos de Azure. Estos artefactos pueden incluir archivos como:

* Plantillas anidadas
* Scripts de configuración y de DSC
* Archivos binarios de aplicación

### <a name="nested-templates-and-configuration-scripts"></a>Plantillas anidadas y scripts de configuración
Cuando usa plantillas de hello proporcionadas por Visual Studio (o se crea con fragmentos de código de Visual Studio), Hola script de PowerShell no solo crea etapas en artefactos de hello, también parametriza Hola URI de los recursos de Hola para las distintas implementaciones. script de Hola copia tooa un contenedor seguro Hola artefactos de Azure, crea un token de SaS para ese contenedor y, a continuación, pasa esa información en la implementación de la plantilla de toohello. Vea [crear una implementación de plantilla](https://msdn.microsoft.com/library/azure/dn790564.aspx) toolearn más información sobre plantillas anidadas.  Al utilizar las tareas en VS Team Services, debe seleccionar tareas apropiadas de hello para la implementación de plantilla y si es necesario, pasar valores de parámetro de hello paso toohello plantilla implementación de ensayo.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>Configuración de la implementación continua en VS Team Services
script de PowerShell de hello toocall en VS Team Services, necesita tooupdate la definición de compilación. En resumen, pasos de hello son: 

1. Editar definición de compilación de Hola.
2. Configuración de la autorización de Azure en VS Team Services.
3. Agregue un paso de compilación de PowerShell de Azure que hace referencia el script de PowerShell de hello en el proyecto de implementación de grupo de recursos de Azure Hola.
4. Establecer valor de Hola de hello *- ArtifactsStagingDirectory* toowork de parámetro con un proyecto compilado en VS Team Services.

### <a name="detailed-walkthrough-for-option-1"></a>Tutorial detallado para la opción 1
Hello procedimientos siguientes le guiarán por hello pasos necesarios tooconfigure la implementación continua de VS Team Services mediante una única tarea que se ejecuta el script de PowerShell de hello en el proyecto. 

1. Edite la definición de compilación de VS Team Services y agregue un paso de compilación de Azure PowerShell. Elija la definición de compilación de hello en hello **las definiciones de compilación** categoría y, a continuación, elija hello **editar** vínculo.
   
   ![Edición de la definición de compilación][0]
2. Agregue un nuevo **Azure PowerShell** definición de compilación de toohello de paso de compilación y, a continuación, elija hello **agregar el paso de compilación...** .
   
   ![Incorporación de un paso "Compilar"][1]
3. Elija hello **implementar tarea** categoría, seleccione hello **Azure PowerShell** de tareas y, a continuación, elija su **agregar** botón.
   
   ![Adición de tareas][2]
4. Elija hello **Azure PowerShell** paso de compilación y, a continuación, rellene sus valores.
   
   1. Si ya tiene un punto de conexión de servicio de Azure agrega tooVS Team Services, elija la suscripción de Hola Hola **suscripción de Azure** cuadro de lista desplegable y, a continuación, omitir toohello próxima sección. 
      
      Si no tiene un punto de conexión de servicio de Azure en VS Team Services, deberá tooadd uno. En esta subsección le guiará por el proceso de Hola. Si su cuenta de Azure usa una cuenta de Microsoft (por ejemplo, Hotmail), debe tomar Hola siguiendo los pasos tooget una autenticación de entidad de servicio.
   2. Elija hello **administrar** vínculo siguiente toohello **suscripción de Azure** cuadro de lista desplegable.
      
      ![Administración de suscripciones de Azure][3]
   3. Elija **Azure** en hello **nuevo extremo de servicio** cuadro de lista desplegable.
      
      ![Nuevo punto de conexión de servicio][4]
   4. Hola **Agregar suscripción de Azure** cuadro de diálogo, seleccione hello **entidad de servicio** opción.
      
      ![Opción de entidad de servicio][5]
   5. Agregue su toohello de información de suscripción de Azure **Agregar suscripción de Azure** cuadro de diálogo. Necesita hello tooprovide siguientes elementos:
      
      * Id. de suscripción
      * Subscription Name
      * Id. de entidad del servicio
      * Clave de entidad del servicio 
      * Identificador de inquilino
   6. Agregar un nombre de su elección toohello **suscripción** cuadro Nombre. Este valor aparece más adelante en hello **suscripción de Azure** la lista desplegable de VS Team Services. 
   7. Si no conoce el identificador de la suscripción de Azure, puede usar uno de hello después tooretrieve de comandos.
      
      Para scripts de PowerShell, use:
      
      `Get-AzureRmSubscription`
      
      Para la CLI de Azure, utilice:
      
      `azure account show`
   8. tooget un identificador de entidad de servicio, clave de entidad de servicio y el Id. de inquilino, siga el procedimiento de hello en [aplicación crear Active Directory y la entidad de seguridad de servicio mediante el portal de](resource-group-create-service-principal-portal.md) o [con una entidad de servicio de autenticación El Administrador de recursos Azure](resource-group-authenticate-service-principal.md).
   9. Agregar hello toohello de valores de Id. de entidad de servicio y clave de entidad de servicio, Id. de inquilino **Agregar suscripción de Azure** diálogo cuadro y, a continuación, elija hello **Aceptar** botón.
      
      Ahora tiene un Hola de toorun toouse de entidad de servicio válido script de PowerShell de Azure.
5. Editar definición de compilación de Hola y elija hello **Azure PowerShell** paso de compilación. Seleccione la suscripción de Hola Hola **suscripción de Azure** cuadro de lista desplegable. (Si no aparece la suscripción de hello, elija hello **actualizar** Hola siguiente botón **administrar** vínculo.) 
   
   ![Configure la tarea de compilación de Azure PowerShell][8]
6. Proporcione un script de PowerShell Deploy-AzureResourceGroup.ps1 toohello de ruta de acceso. toodo, elija el botón de puntos suspensivos (...) hello toohello siguiente **ruta de acceso de secuencia de comandos** , navegue toohello script de PowerShell Deploy-AzureResourceGroup.ps1 en hello **Scripts** carpeta del proyecto, seleccione, y, a continuación, elija hello **Aceptar** botón.    
   
   ![Seleccione la ruta de acceso tooscript][9]
7. Después de seleccionar el script de Hola, actualiza la secuencia de comandos de toohello de ruta de acceso de Hola para que se ejecuta desde hello Build.StagingDirectory (Hola el mismo directorio que *ArtifactsLocation* se establece en). Puede hacerlo mediante la adición de "$(Build.StagingDirectory)/" toohello a partir de la ruta de acceso de script de Hola.
   
    ![Editar tooscript de ruta de acceso][10]
8. Hola **argumentos de secuencia de comandos** cuadro, escriba Hola parámetros (en una sola línea) siguientes. Al ejecutar el script de Hola en Visual Studio, puede ver cómo usa VS Hola parámetros Hola **salida** ventana. Puede usar como punto de partida para establecer valores de parámetro de hello en el paso de compilación.
   
   | Parámetro | Descripción |
   | --- | --- |
   | -ResourceGroupLocation |Hola valor de ubicación geográfica donde se encuentra, como grupo de recursos de hello **eastus** o **'UU'**. (Agregar comillas simples si hay un espacio de nombre de hello). Para más información, consulte [Regiones de Azure](https://azure.microsoft.com/en-us/regions/). |
   | -ResourceGroupName |nombre de Hola Hola del grupo de recursos utilizado en esta implementación. |
   | -UploadArtifacts |Este parámetro, cuando está presente, especifica que los artefactos que deben toobe tooAzure de sistema local de Hola. Solo necesita tooset este modificador si la implementación de plantilla requiere artefactos adicionales que desea que toostage mediante script de PowerShell de hello (por ejemplo, los scripts de configuración o las plantillas anidadas). |
   | -StorageAccountName |nombre de Hola de cuenta de almacenamiento de hello usa toostage artefactos para esta implementación. Este parámetro solo se usa si almacena provisionalmente los artefactos para la implementación. Si se proporciona este parámetro, se crea una nueva cuenta de almacenamiento si no ha creado el script de Hola durante una implementación anterior. Si se especifica el parámetro hello, debe existir la cuenta de almacenamiento de Hola. |
   | -StorageAccountResourceGroupName |nombre de Hola Hola del grupo de recursos asociado a la cuenta de almacenamiento de Hola. Este parámetro es necesario únicamente si proporciona un valor para el parámetro de StorageAccountName Hola. |
   | -TemplateFile |archivo de plantilla de Hello ruta de acceso toohello en el proyecto de implementación de grupo de recursos de Azure de Hola. flexibilidad de tooenhance, use una ruta de acceso para este parámetro que es la ubicación relativa toohello de hello secuencia de comandos de PowerShell en lugar de una ruta de acceso absoluta. |
   | -TemplateParametersFile |archivo de parámetros de Hello ruta de acceso toohello en el proyecto de implementación de grupo de recursos de Azure Hola. flexibilidad de tooenhance, use una ruta de acceso para este parámetro que es la ubicación relativa toohello de hello secuencia de comandos de PowerShell en lugar de una ruta de acceso absoluta. |
   | -ArtifactStagingDirectory |Este parámetro permite script de PowerShell de hello saber carpeta Hola desde donde deben copiarse los archivos binarios del proyecto Hola. Este valor invalida el valor predeterminado de hello usado por hello script de PowerShell. Para usar VS Team Services, establezca el valor de hello en: $(Build.StagingDirectory) - ArtifactStagingDirectory |
   
   A continuación se muestra un ejemplo de argumentos de script (línea dividida para mejorar la legibilidad):
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   Cuando haya terminado, Hola **argumentos de secuencia de comandos** cuadro debe ser similar a Hola lista siguiente:
   
   ![Argumentos de script][11]
9. Después de agregar todos Hola toohello elementos necesarios paso de compilación de PowerShell de Azure, elija hello **cola** compilar el proyecto de botón toobuild Hola. Hola **generar** pantalla muestra la salida Hola Hola script de PowerShell.

### <a name="detailed-walkthrough-for-option-2"></a>Tutorial detallado para la opción 2
Hello procedimientos siguientes le guiarán por hello pasos necesarios tooconfigure la implementación continua de VS Team Services mediante tareas integradas Hola.

1. Edite sus VS Team Services compilación definición tooadd dos nuevos pasos de compilación. Elija la definición de compilación de hello en hello **las definiciones de compilación** categoría y, a continuación, elija hello **editar** vínculo.
   
   ![Edición de la definición de compilación][12]
2. Agregar Hola de nuevo los toohello definición de compilación mediante Hola de pasos de compilación **agregar el paso de compilación...** .
   
   ![Incorporación de un paso "Compilar"][13]
3. Elija hello **implementar** categoría de tarea, seleccione hello **Azure File Copy** de tareas y, a continuación, elija su **agregar** botón.
   
   ![Incorporación de la tarea Copia de archivos de Azure][14]
4. Elija hello **implementación de grupo de recursos de Azure** de tareas, a continuación, elija su **agregar** botón y, a continuación, **cerrar** hello **tarea catálogo**.
   
   ![Incorporación de la tarea Implementación de un grupo de recursos de Azure][15]
5. Elija hello **Azure File Copy** rellenar sus valores y de la tarea.
   
   Si ya tiene un punto de conexión de servicio de Azure agrega tooVS Team Services, elija la suscripción de Hola Hola **suscripción de Azure** cuadro de lista desplegable. Si no tiene suscripción, vea la [opción 1](#detailed-walkthrough-for-option-1) para obtener las instrucciones sobre cómo configurar una en VS Team Services.
   
   * Origen: escriba **$(Build.StagingDirectory)**
   * Tipo de conexión de Azure: seleccione **Azure Resource Manager**
   * Suscripción de Azure RM - suscripción seleccione Hola Hola cuenta de almacenamiento que desee toouse Hola **suscripción de Azure** cuadro de lista desplegable. Si no aparece la suscripción de hello, elija hello **actualizar** Hola siguiente botón **administrar** vínculo.
   * Tipo de destino: seleccione **Blob de Azure**
   * RM cuenta de almacenamiento - Seleccionar cuenta de almacenamiento de Hola desearía toouse de artefactos de almacenamiento provisional
   * Nombre de contenedor - escriba Hola nombre del contenedor de hello le gustaría toouse para el almacenamiento provisional; puede ser cualquier nombre de contenedor válido, pero usar una definición de compilación toothis dedicado
   
   Para los valores de salida de hello:
   
   * URI de contenedor de almacenamiento: escriba **artifactsLocation**
   * Token SAS de contenedor de almacenamiento: escriba **artifactsLocationSasToken**
   
   ![Configuración de la tarea Copia de archivos de Azure][16]
6. Elija hello **implementación de grupo de recursos de Azure** paso de compilación y, a continuación, rellene sus valores.
   
   * Tipo de conexión de Azure: seleccione **Azure Resource Manager**
   * Suscripción de Azure RM - suscripción Hola select para la implementación en hello **suscripción de Azure** cuadro de lista desplegable. Esto suele ser hello usa la misma suscripción en el paso anterior de Hola
   * Acción: seleccione **Creación o actualización del grupo de recursos**
   * Grupo de recursos: seleccione un grupo de recursos o escribir nombre de Hola de un nuevo grupo de recursos para la implementación de Hola
   * Ubicación - seleccione Hola Hola para grupo de recursos
   * Plantilla - escriba Hola ruta y nombre de hello plantilla toobe implementado anteponiendo **$(Build.StagingDirectory)**, por ejemplo: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Parámetros de plantilla: escriba la ruta de acceso de Hola y nombre de hello parámetros toobe utiliza, anteponiéndole **$(Build.StagingDirectory)**, por ejemplo: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Reemplazar parámetros de plantilla: escriba o copie y pegue el siguiente código de hello:
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Configuración de la tarea Implementación de un grupo de recursos de Azure][17]
7. Una vez que haya agregado todos los elementos de hello necesario, guarde la definición de compilación de Hola y elija **poner nueva compilación en cola** en la parte superior de Hola.

## <a name="next-steps"></a>Pasos siguientes
Lectura [Introducción al administrador de recursos de Azure](azure-resource-manager/resource-group-overview.md) toolearn más información acerca de los grupos de recursos de Azure y Azure Resource Manager.

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
