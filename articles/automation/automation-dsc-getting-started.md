---
title: "aaaGetting a trabajar con DSC de automatización de Azure | Documentos de Microsoft"
description: "Explicación y ejemplos de las tareas más comunes de hello en Azure Automation estado configuración deseado (DSC)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>Introducción al DSC de Automatización de Azure:
Este tema explica cómo toodo Hola tareas más comunes con Azure Automation estado configuración deseado (DSC), como crear, importar y compilación de configuraciones, incorporación demasiado administración máquinas y ver informes. Para obtener información general sobre qué es DSC de Automatización de Azure es, consulte [Información general de DSC de Automatización de Azure](automation-dsc-overview.md). Para obtener documentación de DSC, consulte [Información general sobre la configuración de estado deseado de Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).

En este tema se proporciona un toousing guía paso a paso DSC de automatización de Azure. Si desea que un entorno de ejemplo que ya está configurado sin seguir los pasos de hello descritos en este tema, puede usar [Hola después de la plantilla de ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup). Esta plantilla configura un entorno de DSC de Automatización de Azure completado, incluida una máquina virtual de Azure administrada por DSC de Automatización de Azure.

## <a name="prerequisites"></a>Requisitos previos
ejemplos de hello toocomplete en este tema, se necesita siguiente de hello:

* Una cuenta de Automatización de Azure Para obtener instrucciones sobre cómo crear una cuenta de ejecución de Azure Automation, consulte el artículo sobre las [cuentas de ejecución de Azure](automation-sec-configure-azure-runas-account.md).
* Una máquina virtual de Azure Resource Manager (no clásico) ejecuta Windows Server 2008 R2, o cualquier versión posterior. Para obtener instrucciones sobre cómo crear una máquina virtual, consulte [crear la primera máquina virtual de Windows en hello portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>Creación de una configuración de DSC
Crearemos una sencilla [configuración de DSC](https://msdn.microsoft.com/powershell/dsc/configurations) que garantiza la presencia de Hola o ausencia de hello **Web-Server** Windows característica (IIS), dependiendo de cómo asignar nodos.

1. Iniciar Windows PowerShell ISE hello (o cualquier editor de texto).
2. Escriba Hola siguiente texto:
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. Guardar archivo de hello como `TestConfig.ps1`.

Esta configuración llama a un recurso en cada bloque del nodo, hello [recurso WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), que garantiza la presencia de Hola o ausencia de hello **Web-Server** característica.

## <a name="importing-a-configuration-into-azure-automation"></a>Importación de una configuración en Automatización de Azure
A continuación, se podrá importar configuración de Hola Hola cuenta de automatización.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **las configuraciones de DSC**.
4. En hello **las configuraciones de DSC** hoja, haga clic en **agregar una configuración**.
5. En hello **importar configuración** hoja, examinar toohello `TestConfig.ps1` archivo en el equipo.
   
    ![Captura de pantalla de Hola ** importar configuración ** hoja](./media/automation-dsc-getting-started/AddConfig.png)
6. Haga clic en **Aceptar**.

## <a name="viewing-a-configuration-in-azure-automation"></a>Visualización de una configuración en Automatización de Azure
Después de importar una configuración, puede verlo en hello portal de Azure.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **las configuraciones de DSC**
4. En hello **las configuraciones de DSC** hoja, haga clic en **TestConfig** (Esto es nombre de Hola de configuración de hello ha importado en el procedimiento anterior de hello).
5. En hello **TestConfig configuración** hoja, haga clic en **origen de la configuración de vista**.
   
    ![Captura de pantalla de hoja de configuración de hello TestConfig](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    A **origen de configuración de TestConfig** se abre la hoja, muestre código de PowerShell de Hola de configuración de Hola.

## <a name="compiling-a-configuration-in-azure-automation"></a>Compilación de una configuración en Automatización de Azure
Antes de aplicar un nodo de estado deseado tooa, una configuración de DSC definir ese estado debe compilar en una o varias configuraciones de nodo (documento MOF) y coloca en Hola servidor de extracción de DSC de automatización. Para obtener una descripción más detallada de la compilación de configuraciones en DSC de Automatización de Azure, consulte [Compilación de configuraciones en DSC de Automatización de Azure](automation-dsc-compile.md). Para más información sobre la compilación de configuraciones, consulte [Configuraciones DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **las configuraciones de DSC**
4. En hello **las configuraciones de DSC** hoja, haga clic en **TestConfig** (nombre de Hola de hello configuración importado previamente).
5. En hello **TestConfig configuración** hoja, haga clic en **compilar**y, a continuación, haga clic en **Sí**. Así se inicia un trabajo de compilación.
   
    ![Captura de pantalla de hoja de configuración de hello TestConfig resaltado de botón de compilación](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> Cuando se compila una configuración en la automatización de Azure, implementa automáticamente cualquier servidor de extracción nodo creado toohello de MOF de configuración.
> 
> 

## <a name="viewing-a-compilation-job"></a>Visualización de un trabajo de compilación
Después de iniciar una compilación, puede verlo en hello **trabajos de compilación** el icono Servicios hello **configuración** hoja. Hola **trabajos de compilación** mosaico muestra se están ejecutando, ha completado y trabajos con errores. Cuando se abre una hoja de trabajo de compilación, muestra información acerca del trabajo incluidos los errores o advertencias, usan parámetros de entrada en la configuración de Hola y compilación de registros.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **las configuraciones de DSC**.
4. En hello **las configuraciones de DSC** hoja, haga clic en **TestConfig** (nombre de Hola de hello configuración importado previamente).
5. En hello **trabajos de compilación** icono de hello **TestConfig configuración** hoja, haga clic en cualquiera de los trabajos de hello enumerados. A **trabajo de compilación** se abre la hoja, una etiqueta con fecha de Hola Hola trabajo de compilación se inició.
   
    ![Captura de pantalla de hoja de trabajo de compilación de Hola](./media/automation-dsc-getting-started/CompilationJob.png)
6. Haga clic en cualquier icono de hello **trabajo de compilación** hoja toosee más detalles sobre el trabajo de Hola.

## <a name="viewing-node-configurations"></a>Visualización de configuraciones de nodo
La finalización correcta de un trabajo de compilación crea una o varias configuraciones de nodo nuevas. Una configuración de nodo es un documento MOF de servidor de extracción de toohello implementado y listo toobe extrae y aplicada por uno o más nodos. Puede ver las configuraciones de nodo de hello en su cuenta de automatización en hello **configuraciones del nodo DSC** hoja. Una configuración de nodo tiene un nombre con formato de hello *ConfigurationName*. *NodeName*.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **configuraciones del nodo DSC**.
   
    ![Captura de pantalla de hoja de hello las configuraciones de nodo de DSC](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>Incorporación de una máquina virtual de Azure para la administración con DSC de Automatización de Azure
Puede usar DSC de automatización de Azure VM de Azure toomanage (clásico y Administrador de recursos), máquinas virtuales locales, máquinas de Linux, AWS las máquinas virtuales y máquinas físicas locales. En este tema se explica cómo tooonboard solo máquinas virtuales de administrador de recursos de Azure. Para más información sobre la incorporación de otros tipos de máquinas, consulte [Incorporación de máquinas para administrarlas con DSC de Automatización de Azure](automation-dsc-onboarding.md).

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>tooonboard una VM de administrador de recursos de Azure para la administración mediante el DSC de automatización de Azure
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **nodos**.
4. Hola **nodos** hoja, haga clic en **agregar Azure VM**.
   
    ![Captura de pantalla de hoja de nodos de hello resaltado de botón de agregar máquinas virtuales de Azure Hola](./media/automation-dsc-getting-started/OnboardVM.png)
5. Hola **agregar máquinas virtuales de Azure** hoja, haga clic en **seleccionar máquinas virtuales tooonboard**.
6. Hola **seleccionar máquinas virtuales** hoja, seleccione Hola máquina virtual que desee tooonboard y haga clic en **Aceptar**.
   
   > [!IMPORTANT]
   > Debe ser una máquina virtual de Azure Resource Manager que ejecute Windows Server 2008 R2, o cualquier versión posterior.
   > 
   > 
7. Hola **agregar máquinas virtuales de Azure** hoja, haga clic en **configurar datos de registro**.
8. Hola **registro** hoja, escriba Hola nombre de configuración de nodos de hello desea tooapply toohello VM en hello **nombre de la configuración de nodo** cuadro. Esto debe coincidir exactamente con nombre de Hola de una configuración de nodo en hello cuenta de automatización. Especificar un nombre en este momento es opcional. Puede cambiar configuración de nodo de hello asigna después del nodo de Hola de incorporación.
   Marque **Reiniciar el nodo si es necesario** y haga clic en **Aceptar**.
   
    ![Captura de pantalla de hoja de registro de hello](./media/automation-dsc-getting-started/RegisterVM.png)
   
    configuración de nodo de Hello especificada será aplicado toohello VM en los intervalos especificados por hello **frecuencia del modo de configuración**, y configuración de nodo toohello de actualizaciones en los intervalos especificados por hello comprobaráHolaVM **Frecuencia de actualización**. Para obtener más información sobre cómo se utilizan estos valores, consulte [Hola de configuración Administrador de configuración Local](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).
9. Hola **agregar máquinas virtuales de Azure** hoja, haga clic en **crear**.

Azure iniciará el proceso de Hola de incorporación hello máquina virtual. Cuando se complete, Hola VM aparecerán en hello **nodos** hoja Hola cuenta de automatización.

## <a name="viewing-hello-list-of-dsc-nodes"></a>Ver la lista de Hola de nodos de DSC
Puede ver Hola lista de todas las máquinas que se han incorporado para la administración de su cuenta de automatización en hello **nodos** hoja.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **nodos**.

## <a name="viewing-reports-for-dsc-nodes"></a>Visualización de informes de los nodos DSC
Cada vez que DSC de automatización de Azure realiza una comprobación de coherencia en un nodo administrado nodo Hola envía un servidor de extracción de toohello atrás de informes de estado. Puede ver estos informes en la hoja de Hola para ese nodo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **nodos**.
4. En hello **informes** icono, haga clic en cualquiera de los informes de hello en lista de Hola.
   
    ![Captura de pantalla de hoja de informe de Hola](./media/automation-dsc-getting-started/NodeReport.png)

En la hoja de Hola para un informe individual, puede ver Hola siguiendo la información de estado para mantener la coherencia correspondiente Hola comprobar:

* Hola informar del estado, si nodo hello es "Compatible", "Error", configuración de Hola o "nodo de hello no es compatible con" (cuando se encuentra el nodo de hello en **applyandmonitor** hello y modo de máquina no está en estado de hello deseado).
* hora de inicio de Hola de comprobación de coherencia de Hola.
* Compruebe el tiempo de ejecución total de Hola para mantener la coherencia Hola.
* Compruebe el tipo de Hola de coherencia.
* Los errores, incluidos los mensajes de error y de código de error de Hola. 
* Los recursos de DSC utilizados en configuración de Hola y estado de Hola de cada recurso (si el nodo de Hola se encuentra en estado de hello deseado para ese recurso), puede hacer clic en cada recurso tooget información más detallada sobre dicho recurso.
* nombre de Hello, dirección IP y el modo de configuración del nodo de Hola.

También puede hacer clic en **ver el informe sin formato** toosee Hola los datos reales que Hola nodo envía toohello server. Para más información sobre el uso de esos datos, consulte [Uso de un servidor de informes de DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).

Puede tardar algún tiempo después de que un nodo está incorporado antes de hello primer informe está disponible. Tendrá que toowait una too30 minutos Hola informe por primera vez después de incorporar un nodo.

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>Reasignación de una configuración de nodo tooa nodo diferente
Puede asignar un nodo toouse una configuración de otro nodo de Hola uno que asigna inicialmente.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **nodos**.
4. En hello **nodos** hoja, haga clic en el nombre de hello del nodo de hello desea tooreassign.
5. En la hoja de Hola para ese nodo, haga clic en **asignar nodo**.
   
    ![Captura de pantalla de hoja de nodo de hello resaltado de botón de nodo asignar Hola](./media/automation-dsc-getting-started/AssignNode.png)
6. En hello **asignar configuración del nodo** hoja, seleccione Hola nodo Configuración toowhich desea tooassign Hola nodo y, a continuación, haga clic en **Aceptar**.
   
    ![Captura de pantalla de hoja de configuración del nodo asignar Hola](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>Anulación del registro de un nodo
Si ya no desea un toobe nodo administrado mediante el DSC de automatización de Azure, puede anular el registro.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **todos los recursos** y, a continuación, el Hola nombre de la cuenta de automatización.
3. En hello **cuenta de automatización** hoja, haga clic en **nodos**.
4. En hello **nodos** hoja, haga clic en el nombre de hello del nodo de hello desea toounregister.
5. En la hoja de Hola para ese nodo, haga clic en **Unregister**.
   
    ![Captura de pantalla de hoja de nodo de hello resaltado de botón de anular el registro de hello](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>Artículos relacionados
* [Información general de DSC de Automatización de Azure](automation-dsc-overview.md)
* [Incorporación de máquinas para administrarlas con DSC de Automatización de Azure](automation-dsc-onboarding.md)
* [Windows PowerShell Desired State Configuration Overview (Información general de la configuración de estado deseado de Windows Powershell)](https://msdn.microsoft.com/powershell/dsc/overview)
* [Cmdlets de DSC de Automatización de Azure](/powershell/module/azurerm.automation/#automation)
* [Precios de DSC de Automatización de Azure](https://azure.microsoft.com/pricing/details/automation/)

