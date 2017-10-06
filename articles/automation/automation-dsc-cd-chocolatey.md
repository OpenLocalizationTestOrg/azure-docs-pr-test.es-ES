---
title: "aaaAzure implementación continua de DSC de automatización con Chocolatey | Documentos de Microsoft"
description: "Implementación continua de DevOps mediante DSC de Automatización de Azure y el administrador de paquetes Chocolatey.  Ejemplo con plantilla de ARM JSON completa y código fuente de PowerShell."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>Ejemplo de uso: La implementación continua tooVirtual máquinas con DSC de automatización y Chocolatey
En un mundo de DevOps hay muchos tooassist de herramientas con varios puntos de canalización de integración continua de Hola.  Configuración de estado deseado de automatización de Azure (DSC) es un asistente nuevas suma toohello opciones que pueden emplear los equipos de DevOps.  En este artículo, se muestra cómo configurar la implementación continua (CD) para un equipo de Windows.  Puede ampliar fácilmente Hola técnica tooinclude tantos equipos de Windows según sea necesario en función de hello (por ejemplo, un sitio web) y desde ahí tooadditional roles así.

![Implementación continua para máquinas virtuales IaaS](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>A nivel general
Aunque todo esto pueda parecer bastante complicado, afortunadamente puede dividirse en dos procesos principales: 

* Escribir código y probarlo, crear y publicar paquetes de instalación para las versiones principales y secundarias del sistema de Hola. 
* Crear y administrar las máquinas virtuales que se instale y ejecute código de hello en paquetes de saludo.  

Una vez que ambos de estos procesos principales están en vigor, es un paquete de Hola de actualización de paso corta tooautomatically con cualquier máquina virtual concreta según las nuevas versiones creadas e implementadas.

## <a name="component-overview"></a>Información general sobre los componentes
Administradores del paquete como [apt get](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) son muy conocidos en Linux Hola a todos, pero no tanto en el mundo de Windows hello.  [Chocolatey](https://chocolatey.org/) es una cosa, como y de Scott Hanselman [blog](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx) en hello tema es una introducción excelente.  En pocas palabras, Chocolatey permite tooinstall paquetes desde un repositorio central de los paquetes en un sistema de Windows mediante la línea de comandos de Hola.  Puede crear y administrar su propio repositorio y Chocolatey puede instalar paquetes desde cualquier número de repositorios que designe.

Estado de la configuración deseado (DSC) ([Introducción](https://technet.microsoft.com/library/dn249912.aspx)) es una herramienta de PowerShell que permite la configuración de hello toodeclare que desea para una máquina.  Por ejemplo, puede indicar "Quiero instalar Chocolatey, quiero instalar IIS, necesito abrir el puerto 80, quiero instalar la versión 1.0.0 de mi sitio web".  Administrador de configuración Hello DSC Local (LCM) implementa dicha configuración. Un servidor de extracción de DSC contiene un repositorio de configuraciones para los equipos. Hola LCM en cada equipo protege toosee periódicamente si su configuración coincide con la configuración almacenada Hola. Puede informar del estado o intente toobring máquina de hello en alineación con la configuración almacenada Hola. Puede editar Hola configuración almacenada en toocause de servidor de extracción de hello una máquina o un conjunto de máquinas toocome en alineación con la configuración de hello cambiado.

Automatización de Azure es un servicio administrado de Microsoft Azure que le permite tooautomate diversas tareas mediante runbooks, nodos, las credenciales, los recursos y activos como programaciones y las variables globales. DSC de automatización de Azure amplía esta automatización herramientas de capacidad tooinclude DSC de PowerShell.  Aquí hay una [introducción](automation-dsc-overview.md)muy buena.

Un recurso de DSC es un módulo de código con capacidades específicas, como la administración de redes, Active Directory o SQL Server.  Hola Chocolatey recurso de DSC sabe cómo tooaccess un servidor de NuGet (entre otras cosas), descargar los paquetes, instalar paquetes y así sucesivamente.  Hay muchos otros recursos de DSC en hello [Galería de PowerShell](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title).  Estos módulos se instalan en el servidor de extracción de DSC de Automatización de Azure (manualmente) para que se puedan usar con sus configuraciones.

Las plantillas de Resource Manager proporcionan una forma declarativa de generar la infraestructura: como las redes, las subredes, la seguridad de red y el enrutamiento, los equilibradores de carga, las NIC, las máquinas virtuales, etc.  Este es un [artículo](../azure-resource-manager/resource-manager-deployment-model.md) que compara Hola modelo de implementación del Administrador de recursos (declarativo) con hello administración de servicios de Azure (ASM o estándar) implementación modelo (imperativo) y se describen los recursos principales de hello proveedores, proceso, almacenamiento y red.

Una característica clave de una plantilla de administrador de recursos es su tooinstall capacidad una extensión de máquina virtual en hello VM tal y como se aprovisiona.  Una extensión de máquina virtual posee capacidades específicas, como ejecutar un script personalizado, instalar software antivirus o ejecutar un script de configuración de DSC.  Existen muchos otros tipos de extensiones de máquina virtual.

## <a name="quick-trip-around-hello-diagram"></a>Recorrido rápido por diagrama Hola
Comenzando por la parte superior de hello, escribir el código, compilar y probar, a continuación, crear un paquete de instalación.  Chocolatey admite diversos tipos de paquetes de instalación, como MSI, MSU o ZIP.  Y tiene toda la potencia de instalación real de PowerShell toodo Hola Hola si las capacidades nativas de Chocolatey no están bastante seguridad tooit.  Coloque el paquete de hello en un lugar accesible: un repositorio de paquetes.  En este ejemplo de uso se emplea una carpeta pública en una cuenta de almacenamiento de blobs de Azure, pero vale cualquier lugar.  Chocolatey funciona de forma nativa con los servidores NuGet y otros para administrar los metadatos de los paquetes.  [En este artículo](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed) se describen las opciones de Hola.  Este ejemplo de uso utiliza NuGet.  Nuspec son los metadatos de los paquetes.  Hello Nuspec es "compila" en del NuPkg y almacenado en un servidor de NuGet.  Cuando la configuración solicita un paquete por su nombre y haga referencia a un servidor de NuGet, hello Chocolatey recurso de DSC (ahora en Hola VM) toma paquete hello y lo instala automáticamente.  También se puede solicitar una versión específica de un paquete.

En hello parte inferior izquierda de la imagen de hello, hay una plantilla de Azure Resource Manager (ARM).  En este ejemplo de uso, Hola extensión de máquina virtual registra Hola VM con hello servidor de extracción de DSC de automatización de Azure (es decir, un servidor de extracción) como un nodo.  configuración de Hola se almacena en el servidor de extracción de Hola.  En realidad, se almacena dos veces: una vez como texto sin formato y otra como archivo MOF (para aquellos a quienes les interese).  En el portal de hello, Hola MOF es una configuración de nodo de"" (como toosimply lugar "configuración").  Su Hola artefacto que está asociado con un nodo para que el nodo de hello sepa su configuración.  Detalles a continuación muestran cómo tooassign Hola nodo toohello de configuración.

Supuestamente ya está realizando bit de hello en la parte superior de Hola o la mayoría de los datos.  Creación de hello nuspec, compilar y almacenar en un servidor de NuGet son algo pequeño.  además, ya está administrando máquinas virtuales.  Tomar Hola siguiente paso toocontinuous implementación requiere la configuración de servidor de extracción de hello (una vez), registrar los nodos con él (una vez) y crear y almacenar la configuración de Hola allí (inicialmente).  A continuación, tal y como se actualizan los paquetes e implementan toohello repositorio, actualice Hola configuración y la configuración de nodo en el servidor de extracción de hello (Repita según sea necesario).

No comenzar con una plantilla de ARM también es perfectamente válido.  Hay PowerShell cmdlets diseñados toohelp registrar las máquinas virtuales con servidor de extracción de Hola y todos de rest de Hola. Para obtener más detalles, vea este artículo: [Incorporación de máquinas para administrarlas con DSC de Automatización de Azure](automation-dsc-onboarding.md)

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>Paso 1: Configurar cuenta de servidor y la automatización de la extracción de Hola
En una línea de comandos de PowerShell (Add-AzureRmAccount) autenticada: (puede tardar unos minutos mientras se configura el servidor de extracción de hello)

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

Puede colocar su cuenta de automatización en cualquiera de hello después regiones (también conocido como ubicación): este de EE. 2, Ee.uu. Central sur, nos Gov Virginia, Europa occidental, sudeste de Asia, este de Japón, India Central y sudeste Australia, Canadá Central, Europa del Norte.

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>Paso 2: Plantilla de ARM toohello de ajustes de extensión de máquina virtual
Detalles de registro de máquina virtual (con la extensión de máquina virtual de DSC de PowerShell de Hola) de este [plantilla de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver).  Este paso registra su nueva máquina virtual con el servidor de extracción de hello en la lista de Hola de nodos de DSC.  Parte de este registro es especifica Hola nodo Configuración toobe aplica toohello.  Esta configuración de nodo aún no tiene tooexist en el servidor de extracción de hello, por lo que es aceptar que paso 4 es donde esto se lleva a cabo para hello primera vez.  Pero aquí en el paso 2 es necesario nombre de Hola decidido de toohave del nodo de Hola y Hola de configuración de Hola.  En este ejemplo de uso, nodo de hello es 'isvbox' y configuración de hello es 'ISVBoxConfig'.  Por lo que el nombre de configuración de nodo de hello (toobe especificado en DeploymentTemplate.json) es 'ISVBoxConfig.isvbox'.  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>Paso 3: Agregar servidor de extracción de toohello de recursos de DSC necesarios
Hola Galería de PowerShell es instrumentada tooinstall los recursos de DSC en su cuenta de automatización de Azure.  Navegar toohello recurso que desee y haga clic en el botón de "Implementar tooAzure automatización" Hola.

![Ejemplo de la Galería de PowerShell](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

Otra técnica agregado recientemente toohello Portal de Azure permite toopull en nuevos módulos o módulos de actualización existente. Desplazarse por los recursos de la cuenta de automatización de hello, mosaico de activos de hello y, finalmente, mosaico de módulos de Hola.  icono de examinar la Galería de Hello permite lista de hello toosee de módulos en la Galería de hello, profundizar en los detalles e importar en última instancia a la cuenta de automatización. Esto es una excelente manera tookeep los módulos de seguridad toodate de tootime de tiempo. Además, la característica de importación de hello comprueba las dependencias con otro tooensure módulos que nada obtiene no está sincronizado.

O bien, hay enfoque manual Hola.  estructura de carpetas de Hola de un módulo de integración de PowerShell para un equipo de Windows es un poco diferente de la estructura de carpetas de hello esperada Hola automatización de Azure.  Por tanto, es necesario hacer algunos ajustes.  Pero no es difícil, y se realiza una sola vez por recurso (a menos que desee tooupgrade que en el futuro.)  Para más información sobre la creación de módulos de integración de PowerShell, consulte este artículo: [Creación de módulos de integración para Azure Automation](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/).

* Instalar el módulo de Hola que necesita en la estación de trabajo, como se indica a continuación:
  * Instale [Windows Management Framework, v5](http://aka.ms/wmf5latest) (no es necesario para Windows 10).
  * `Install-Module –Name MODULE-NAME`<: grabs Hola módulo desde la Galería de PowerShell de Hola 
* Desde la carpeta de copia Hola módulo `c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME` carpeta temporal tooa 
* Retire la carpeta principal de Hola de documentación y ejemplos 
* Carpeta principal de ZIP hello, nombres de archivo ZIP de hello exactamente igual Hola como carpeta de Hola 
* Coloque el archivo ZIP de hello en una ubicación accesible de HTTP, como almacenamiento de blobs en una cuenta de almacenamiento de Azure.
* Ejecute este código de PowerShell:
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

ejemplo de Hola incluida realiza estos pasos para cChoco y xNetworking. Vea hello [notas](#notes) para un control especial para cChoco.

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>Paso 4: Agregar servidor de extracción de hello nodo Configuración toohello
No hay nada especial acerca de hello primera vez que importar la configuración en el servidor de extracción de Hola y de compilación.  Compilaciones de importación posteriores todos de hello mismo aspecto configuración Hola exactamente igual.  Cada vez que el paquete de actualización y necesita toopush horizontal tooproduction que realice este paso después de asegurarse de archivo de configuración de hello es correcta: incluidos Hola nueva versión del paquete.  Este es el archivo de configuración de Hola y PowerShell:

ISVBoxConfig.ps1:

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

New-ConfigurationScript.ps1:

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

Estos resultados de pasos en una nueva configuración de nodo denominan "ISVBoxConfig.isvbox" que se ubican en el servidor de extracción de Hola.  nombre de configuración de nodo de Hola se compila como "configurationName.nodeName".

## <a name="step-5-creating-and-maintaining-package-metadata"></a>Paso 5: Crear y mantener los metadatos del paquete
Para cada paquete que incluya en el repositorio de paquetes de saludo, necesita un nuspec que lo describe.  Ese nuspec se debe compilar y almacenar en el servidor NuGet. Este proceso se describe [aquí](http://docs.nuget.org/create/creating-and-publishing-a-package).  Puede usar MyGet.org como servidor NuGet.  Se vende este servicio, pero también se ofrece una SKU de inicio gratuita.  En NuGet.org encontrará instrucciones para instalar su propio servidor NuGet para los paquetes privados.

## <a name="step-6-tying-it-all-together"></a>Paso 6: Unión de todos los elementos
Cada vez que pasa el control de calidad de una versión y se aprueba para la implementación, se crea el paquete de hello, nuspec nupkg y actualizan había implementado toohello NuGet servidor.  Además, Hola configuración (paso 4 anterior) debe estar tooagree actualizada con nuevo número de versión de Hola.  Se debe enviar toohello servidor de extracción y compilado.  Desde ese momento, resulta las máquinas virtuales de toohello dependen de esa actualización de configuración toopull Hola e instalarlo.  Cada una de estas actualizaciones son sencillas: solo una línea o dos de PowerShell.  En caso de hello de Visual Studio Team Services, algunas de ellas se encapsulan en tareas de compilación que se pueden encadenar juntas en una compilación.  En [este artículo](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery) se ofrecen más detalles.  Esto [repositorio de GitHub](https://github.com/Microsoft/vso-agent-tasks) detalles Hola diversas tareas de compilación disponible.

## <a name="notes"></a>Notas
Este ejemplo de uso se inicia con una máquina virtual desde una imagen de Windows Server 2012 R2 genérica de hello Galería de Azure.  Puede iniciar desde cualquier imagen almacenada y, a continuación, ajustar desde ahí con la configuración de DSC Hola.  Sin embargo, el cambio de configuración que está preparado a una imagen es mucho más difícil que actualizar dinámicamente la configuración de hello mediante DSC.

No tienes toouse una plantilla de ARM y Hola VM extensión toouse esta técnica con sus máquinas virtuales.  Y las máquinas virtuales no tienen toobe en Azure toobe bajo la administración de CD.  Todo lo que es necesaria que Chocolatey se instalado y hello LCM configurada en hello VM para que sepa dónde hello servidor de extracción es.  

Por supuesto, cuando se actualiza un paquete en una máquina virtual que se encuentre en producción, debe tootake esa máquina virtual fuera de la rotación mientras se instala la actualización de Hola.  Existen métodos muy diversos de hacerlo.  Por ejemplo, con una máquina virtual tras un equilibrador de carga de Azure, puede agregar un sondeo personalizado.  Al actualizar Hola VM, tener extremo de sondeo de hello un código de estado 400.  Hola deformación necesarios toocause este cambio puede ser dentro de la configuración, como puede Hola tooswitch deformación nuevo tooreturning 200 una vez completada la actualización de Hola.

El código fuente completo de este ejemplo de uso se encuentra en [este proyecto de Visual Studio](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) en GitHub.

## <a name="related-articles"></a>Artículos relacionados
* [Información general de DSC de Automatización de Azure](automation-dsc-overview.md)
* [Cmdlets de DSC de Automatización de Azure](https://msdn.microsoft.com/library/mt244122.aspx)
* [Incorporación de máquinas para administrarlas con DSC de Automatización de Azure](automation-dsc-onboarding.md)

