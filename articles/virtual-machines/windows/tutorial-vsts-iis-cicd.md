---
title: "aaaCreate una canalización de CI/CD en Azure con Team Services | Documentos de Microsoft"
description: "Obtenga información acerca de cómo de canalización toocreate un Visual Studio Team Services para la integración continua y entrega que implementa un tooIIS de aplicación web en una máquina virtual de Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a>Creación de una canalización de integración continua con Visual Studio Team Services e IIS
tooautomate Hola compilación, prueba y fases de implementación del desarrollo de aplicaciones, puede usar una integración continua y la canalización de implementación (CI/CD). En este tutorial se creará una canalización CI/CD utilizando Visual Studio Team Services y una máquina virtual Windows en Azure que ejecuta IIS. Aprenderá a:

> [!div class="checklist"]
> * Publicar un proyecto de Team Services de tooa de aplicación web ASP.NET
> * Crear una definición de compilación que se desencadena mediante confirmaciones de código
> * Instalar y configurar IIS en una máquina virtual de Azure
> * Agregar grupo de implementación de tooa de instancia IIS de hello en Team Services
> * Crear un nuevo web de versión definición toopublish implementar paquetes tooIIS
> * Probar Hola CI/CD canalización

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar `Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="create-project-in-team-services"></a>Crear el proyecto en Team Services
Visual Studio Team Services permite una colaboración y desarrollo sencillos sin mantener una solución de administración de código local. Team Services proporciona pruebas de código en la nube, compilación y visión de la aplicación. Puede elegir el repositorio de control de versiones y el IDE que mejor se adapten a su desarrollo de código. Para este tutorial, puede usar una cuenta gratuita toocreate una aplicación web ASP.NET básica y la canalización de CI/CD. Si no dispone de una cuenta de Team Services, [cree una](http://go.microsoft.com/fwlink/?LinkId=307137).

proceso de confirmación de código de hello toomanage, definiciones, de compilación y las definiciones de la versión, crear un proyecto en Team Services como se indica a continuación:

1. Abra el panel de Team Services en un explorador web y elija **Nuevo proyecto**.
2. Escriba *myWebApp* para hello **nombre del proyecto**. Dejar todos los demás toouse de valores predeterminado *Git* control de versiones y *Agile* proceso de elemento de trabajo.
3. Elija la opción de hello demasiado**compartir con** *los miembros del equipo*, a continuación, seleccione **crear**.
5. Una vez creado el proyecto, elija la opción de hello demasiado**inicializar con un archivo Léame o gitignore**, a continuación, **inicializar**.
6. En el proyecto nuevo, elija **paneles** a través de la parte superior de hello, a continuación, seleccione **abierta en Visual Studio**.


## <a name="create-aspnet-web-application"></a>Creación de una aplicación web ASP.NET
En el paso anterior de hello, creó un proyecto en Team Services. paso final de Hello abre el proyecto nuevo en Visual Studio. Administrar las confirmaciones de código de hello **Team Explorer** ventana. Cree una copia local del nuevo proyecto y, a continuación, cree una aplicación web ASP.NET a partir de una plantilla, como se indica a continuación:

1. Seleccione **clon** toocreate un repositorio de git local de su proyecto de Team Services.
    
    ![Clonación del repositorio del proyecto de Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. En **Soluciones**, seleccione **Nuevo**.

    ![Creación de la solución de aplicación web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. Seleccione **Web** plantillas y, a continuación, elija hello **aplicación Web ASP.NET** plantilla.
    1. Escriba un nombre para la aplicación, como *myWebApp*y desactive la casilla de Hola para **crear directorio para la solución**.
    2. Si está disponible la opción de hello, desactive la casilla cuadro Hola demasiado**tooproject agregar Application Insights**. Visión de la aplicación requiere tooauthorize su aplicación web con Azure Application Insights. tookeep que simple en este tutorial, omita este proceso.
    3. Seleccione **Aceptar**.
4. Elija **MVC** de lista de plantillas de Hola.
    1. Seleccione **Cambiar autenticación**, elija **Sin autenticación** y, a continuación, seleccione **Aceptar**.
    2. Seleccione **Aceptar** toocreate la solución.
5. Hola **Team Explorer** ventana, elija **cambios**.

    ![Confirmar el repositorio de git de servicios de tooTeam cambios locales](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. En el cuadro de texto de confirmación de hello, escriba un mensaje como *confirmación inicial*. Elija **confirmar todos y sincronización** desde el menú desplegable de Hola.


## <a name="create-build-definition"></a>Creación de la definición de compilación
En Team Services, use un toooutline de definición de compilación cómo debe crearse la aplicación. En este tutorial, creamos una definición básica que toma el código fuente, compila la solución de hello, a continuación, crea web implementa paquete podemos usar toorun hello web app en un servidor IIS.

1. En el proyecto de Team Services, elija **compilar & versión** a través de la parte superior de hello, a continuación, seleccione **genera**.
3. Seleccione **+ Nueva definición**.
4. Elija hello **ASP.NET (versión preliminar)** plantilla y seleccione **aplicar**.
5. Deje predeterminado de hello todos los valores de la tarea. En **obtener orígenes**, asegúrese de que hello *myWebApp* repositorio y *maestro* bifurcación está seleccionada.

    ![Creación de la definición de compilación en el proyecto de Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. En hello **desencadenadores** ficha, mueva el control deslizante de Hola para **habilitar este desencadenador** demasiado*habilitado*.
7. Guardar definición de compilación de Hola y cola una compilación nueva seleccionando **guardar y poner en cola** , a continuación, **Guardar & cola** nuevo. Deje los valores predeterminados de Hola y seleccione **cola**.

Inspección compilación Hola programada en un agente hospedado, a continuación, comienza toobuild. Hola de salida es similar toohello siguiente ejemplo:

![Compilación correcta del proyecto de Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a>Create virtual machine
tooprovide un toorun plataforma la aplicación web ASP.NET, necesita una máquina virtual de Windows que se ejecuta IIS. Team Services utiliza un toointeract de agente con la instancia de IIS de hello como Confirmar código y se activan compilaciones.

Cree una máquina virtual Windows Server 2016 mediante [este script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json). Se tarda unos minutos para toorun de script de Hola y crear hello VM. Una vez que se ha creado la VM de hello, abrir el puerto 80 para el tráfico web con [AzureRmNetworkSecurityRuleConfig agregar](/powershell/module/azurerm.resources/new-azurermresourcegroup) como se indica a continuación:

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

tooconnect tooyour VM, obtener dirección IP pública de hello con [AzureRmPublicIpAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress) como se indica a continuación:

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

Crear una máquina virtual de tooyour de sesión de escritorio remoto:

```cmd
mstsc /v:<publicIpAddress>
```

En hello VM, abra un **administrador PowerShell** símbolo del sistema. Instale IIS y las características de .NET necesarias como se indica a continuación:

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a>Creación de un grupo de implementación
toopush out web Hola implementar paquete toohello al servidor de IIS, defina un grupo de implementación de Team Services. Este grupo permite toospecify los servidores que son destino de Hola de nuevas compilaciones que confirma tooTeam código servicios y las compilaciones se completan.

1. En Team Services, elija **Compilación y versión** y, a continuación, seleccione **Grupos de implementación**.
2. Elija **Agregar grupo de implementación**.
3. Escriba un nombre para el grupo de hello, como *myIIS*, a continuación, seleccione **crear**.
4. Hola **registrar máquinas** sección, asegúrese de *Windows* está seleccionada, la casilla Hola demasiado**usar un token de acceso personal en el script de Hola para la autenticación**.
5. Seleccione **copiar script tooclipboard**.


### <a name="add-iis-vm-toohello-deployment-group"></a>Agregar grupo de implementación de IIS VM toohello
Con grupo de implementación de hello creado, agregue cada grupo de toohello de instancia IIS. Servicios de equipo genera un script que se descarga y se configura un agente en implementar la máquina virtual que recibe el nuevo sitio web de Hola paquetes, a continuación, se aplica tooIIS.

1. Nuevo en hello **administrador PowerShell** sesión en la máquina virtual, pegue y ejecute el script de Hola copiado desde Team Services.
2. Cuando se elige etiquetas tooconfigure solicitadas por el agente de hello, *Y* y escriba *web*.
3. Cuando se le solicite para cuenta de usuario de hello, presione *devolver* los valores predeterminados de tooaccept Hola.
4. Espere Hola script toofinish con un mensaje *vstsagent.account.computername de servicio se inició correctamente*.
5. Hola **grupos de implementación** página de hello **de compilación y la versión** menú, abra hello *myIIS* grupo de implementación. En hello **máquinas** , compruebe que aparece la máquina virtual.

    ![VM agregó correctamente el grupo de implementación de servicios de tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a>Creación de la definición de versión
toopublish las compilaciones, crear una definición de la versión de Team Services. Esta definición se desencadena automáticamente por una compilación correcta de la aplicación. Elija toopush de grupo de implementación de hello web implementa el paquete a y definir la configuración de IIS adecuados de Hola.

1. Elija **Compilación y versión** y, a continuación, seleccione **Compilaciones**. Elija la definición de compilación de hello creado en un paso anterior.
2. En **completado recientemente**, elija la compilación más reciente de Hola y luego seleccione **versión**.
3. Elija **Sí** toocreate una definición de la versión.
4. Elija hello **vacía** plantilla, a continuación, seleccione **siguiente**.
5. Compruebe la definición de compilación de proyecto y de origen Hola se rellenan con el proyecto.
6. Seleccione hello **implementación continua** casilla de verificación, a continuación, seleccione **crear**.
7. Seleccione cuadro de lista desplegable de hello siguiente demasiado**+ agregar tareas** y elija *agregar una fase de implementación de grupo*.
    
    ![Agregar definición de tarea toorelease en Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. Elija **agregar** siguiente demasiado**Deploy(Preview) de aplicación Web de IIS**, a continuación, seleccione **cerrar**.
9. Seleccione hello **ejecutar en el grupo de implementación** tarea primaria.
    1. Para **grupo de implementación**, seleccione el grupo de implementación de hello creado anteriormente, como *myIIS*.
    2. Hola **etiquetas de máquina** cuadro, seleccione **agregar** y elija hello *web* etiqueta.
    
    ![Tarea del grupo de implementación de la definición de versión en IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. Seleccione hello **implementar: implementación de aplicación Web IIS** tooconfigure tarea IIS instancia opciones del siguiente modo:
    1. En **Nombre del sitio web**, escriba *Sitio web predeterminado*.
    2. Deje Hola todas las otras configuraciones predeterminadas.
12. Elija **Guardar** y, a continuación, seleccione **Aceptar** dos veces.


## <a name="create-a-release-and-publish"></a>Creación de una versión y publicación
Ahora puede enviar el paquete de implementación web como una nueva versión. Este paso se comunica con el agente de hello en cada instancia que forma parte del grupo de implementación de hello, inserta web Hola implementar paquete, a continuación, configura la aplicación web IIS toorun Hola actualizado.

1. En la definición de versión, seleccione **+ Versión** y, a continuación, elija **Crear versión**.
2. Compruebe que la compilación más reciente de hello está seleccionado en la lista desplegable de hello, junto con **la implementación automatizada: después de la creación de la versión**. Seleccione **Crear**.
3. El encabezado pequeño aparece a través de la parte superior de saludo de la definición de la versión, como *versión 'Versión 1' se ha creado*. Vínculo de la versión de Hola seleccione.
4. Abra hello **registros** pestaña progreso de versión de hello toowatch.
    
    ![Versión e inserción del paquete de implementación web de Team Services correctas](media/tutorial-vsts-iis-cicd/successful_release.png)

5. Una vez completada la versión de hello, abra un explorador web y escriba Hola pública PII dirección de la máquina virtual. Se está ejecutando la aplicación web ASP.NET.

    ![Aplicación web ASP.NET en ejecución en la máquina virtual de IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a>Probar Hola todo CI/CD canalización
Con la aplicación web que se ejecuta en IIS, intente ahora canalización de hello todo CI/CD. Después de realizar un cambio en Visual Studio y la confirmación se desencadena el código, una compilación, lo que, a continuación, desencadena una versión del sitio web actualizado implementar tooIIS de paquete:

1. En Visual Studio, abra hello **el Explorador de soluciones** ventana.
2. Navegue tooand abrir *myWebApp | Vistas | Inicio | Index.cshtml*
3. Editar la línea 6 tooread:

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. Guarde el archivo hello.
5. Abra hello **Team Explorer** (ventana), seleccione hello *myWebApp* del proyecto, y luego elija **cambios**.
6. Escriba un mensaje de confirmación, como *pruebas CI/CD canalización*, a continuación, elija **todos de confirmación y sincronización** desde el menú desplegable de Hola.
7. En el área de trabajo de Team Services, se desencadena una nueva compilación de confirmación de código de hello. 
    - Elija **Compilación y versión** y, a continuación, seleccione **Compilaciones**. 
    - Elija la definición de compilación y vuelva a seleccionar hello **en cola & ejecución** toowatch de compilación como Hola compilación progresa.
9. Una vez Hola compilación es correcta, se desencadena una nueva versión.
    - Elija **compilar & versión**, a continuación, **versiones** toosee Hola WebDeploy paquete inserta tooyour IIS VM. 
    - Seleccione hello **actualizar** iconos de estado de hello tooupdate. Cuando Hola *entornos* columna muestra una marca de verificación verde, versión de Hola ha implementado correctamente tooIIS.
11. aplicar los cambios de toosee, actualice el sitio Web IIS en un explorador.

    ![Aplicación web ASP.NET en ejecución en una máquina virtual de IIS desde la canalización CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, creó una aplicación web ASP.NET en Team Services y compilación configurado y versión definiciones toodeploy nuevo web implementación paquetes tooIIS en cada confirmación de código. Ha aprendido a:

> [!div class="checklist"]
> * Publicar un proyecto de Team Services de tooa de aplicación web ASP.NET
> * Crear una definición de compilación que se desencadena mediante confirmaciones de código
> * Instalar y configurar IIS en una máquina virtual de Azure
> * Agregar grupo de implementación de tooa de instancia IIS de hello en Team Services
> * Crear un nuevo web de versión definición toopublish implementar paquetes tooIIS
> * Probar Hola CI/CD canalización

Avanzar toohello siguiente tutorial toolearn cómo toosecure un servidor web con certificados SSL.

> [!div class="nextstepaction"]
> [Protección de un servidor web con SSL](tutorial-secure-web-server.md)