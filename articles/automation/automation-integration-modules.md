---
title: "aaaCreate un módulo de integración de la automatización de Azure | Documentos de Microsoft"
description: "Tutorial le guía a través del uso de creación, las pruebas y ejemplo de Hola de módulos de integración en automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a>Módulos de integración de Automatización de Azure
PowerShell es tecnología fundamental de hello detrás de automatización de Azure. Dado que la automatización de Azure se basa en PowerShell, los módulos de PowerShell son extensibilidad toohello clave de automatización de Azure. En este artículo, se le ayudará a obtener información específica de Hola de uso de automatización de Azure de módulos de PowerShell, denominada tooas "Módulos de integración" y las prácticas recomendadas para crear su propio toomake de módulos de PowerShell que funcionan como módulos de integración en Automatización de Azure. 

## <a name="what-is-a-powershell-module"></a>¿Qué son los módulos de PowerShell?
Un módulo de PowerShell es un grupo de cmdlets de PowerShell como **Get-Date** o **Copy-Item**que puede utilizarse desde la consola de PowerShell de hello, scripts, flujos de trabajo, runbooks y, al igual que los recursos de DSC de PowerShell WindowsFeature o archivo, que puede usarse desde configuraciones de DSC de PowerShell. Toda la funcionalidad de Hola de PowerShell se expone a través de los cmdlets y recursos de DSC y cada recurso de DSC de cmdlet/está respaldado por un módulo de PowerShell, muchos de los que se suministran con PowerShell. Por ejemplo, hello **Get-Date** cmdlet forma parte del programa Hola módulo Microsoft.PowerShell.Utility PowerShell, y **Copy-Item** cmdlet forma parte del módulo Microsoft.PowerShell.Management PowerShell hello y Hola recurso de DSC de paquete forma parte del módulo PSDesiredStateConfiguration PowerShell Hola. Estos módulos se suministran con PowerShell. Sin embargo, muchos módulos de PowerShell no se incluyen como parte de PowerShell y en su lugar se distribuyen con productos de primer o terceros como System Center 2012 Configuration Manager o amplia comunidad de PowerShell hello en lugares como galería de PowerShell.  módulos de Hello son útiles porque simplifican las tareas complejas más sencilla a través de la funcionalidad encapsulada.  Puede obtener más información sobre los [módulos de PowerShell en MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx). 

## <a name="what-is-an-azure-automation-integration-module"></a>¿Qué son los módulos de integración de Automatización de Azure?
Los módulos de integración se parecen mucho a los módulos de PowerShell. Su simplemente un módulo de PowerShell que contiene opcionalmente un archivo adicional: un archivo de metadatos especificando un toobe del tipo de conexión de automatización de Azure usado con los cmdlets del módulo de hello en runbooks. Opcional de archivos o no, estos módulos se importan en toomake de automatización de Azure sus cmdlets disponibles para usar en runbooks y sus recursos de DSC disponibles para su uso en las configuraciones de DSC de PowerShell. Entre bastidores de hello, automatización de Azure almacena estos módulos y en el trabajo del runbook y tiempo de ejecución de trabajo de compilación DSC, los carga en espacios aislados de automatización de Azure de Hola donde se ejecutan los runbooks y las configuraciones de DSC se compilan.  Los recursos de DSC en los módulos se colocan también automáticamente en el servidor de extracción de DSC de automatización de hello, para que pueden extraerse máquinas intentar tooapply las configuraciones de DSC.  

Enviamos un número de módulos de PowerShell de Azure fuera del cuadro hello en automatización de Azure para toouse, por lo que puede empezar a automatizar la administración de Azure inmediatamente, pero puede importar módulos de PowerShell para cualquier sistema, el servicio o la herramienta que desee toointegrate con. 

> [!NOTE]
> Algunos módulos se incluyen como "módulos globales" en el servicio de automatización de Hola. Estos módulos globales están disponible tooyou cuando se crea una cuenta de automatización, y se actualice a veces, que envía automáticamente tooyour cuenta de automatización. Si no desea toobe actualizadas de forma automática, siempre puede importar Hola mismo módulo usted mismo y que tendrá prioridad sobre la versión de módulo global Hola de ese módulo que se incluyen en el servicio de Hola. 

formato de Hello en el que importar un paquete de módulo de integración es un archivo comprimido con el mismo nombre que el módulo de hello y una extensión .zip de Hola. Que contiene el módulo de Windows PowerShell de Hola y los archivos auxiliares, incluido un archivo de manifiesto (. psd1) si el módulo de hello tiene uno.

Si el módulo de hello debe contener un tipo de conexión de automatización de Azure, también debe contener un archivo con nombre hello `<ModuleName>-Automation.json` que especifica las propiedades de tipo de conexión de Hola. Esto es un archivo json que se coloca dentro de la carpeta del módulo de hello del archivo .zip comprimido y contienen campos de Hola de una "conexión" que es necesario tooconnect toohello sistema o servicio Hola módulo representa. De este modo, se creará un tipo de conexión en Automatización de Azure. Uso de este archivo se puede establecer los nombres de campo de hello, tipos, y si deben ser campos Hola cifrados u opcional para el tipo de conexión de hello del módulo de Hola. Hola te mostramos una plantilla en formato de archivo de hello json:

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

Si ha implementado Service Management Automation y crear paquetes de módulos de integración para los runbooks de automatización, este debe tener un aspecto muy familiar tooyou. 

## <a name="authoring-best-practices"></a>Procedimientos recomendados sobre la creación de los módulos
Aunque módulos de integración son básicamente los módulos de PowerShell, hay varias cosas que se recomienda que considere la posibilidad de mientras se crea un módulo de PowerShell, toomake lo más utilizable en automatización de Azure. Algunos de ellos son específicos de automatización de Azure y algunas de ellas son útil toomake solo los módulos funcionan bien en el flujo de trabajo de PowerShell, independientemente de si usas la automatización. 

1. Incluir una sinopsis, descripción y ayudar a los URI para todos los cmdlets de módulo de Hola. En PowerShell, puede definir cierta información de ayuda para cmdlets tooallow Hola usuario tooreceive ayuda acerca de cómo utilizarlas con hello **Get-Help** cmdlet. Por ejemplo, a continuación le mostramos cómo puede definir una sinopsis y un identificador URI de ayuda para un módulo de PowerShell escrito en un archivo .psm1.<br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> Proporcionar esta información, no solo se mostrarán esta ayuda sobre el uso de hello **Get-Help** Hola de cmdlet en consola de PowerShell, también va a exponer esta funcionalidad ayuda en automatización de Azure.  Por ejemplo, al insertar actividades durante la creación de runbooks. Haga clic en "Ver ayuda detallada" se ayuda URI de hello abierto en otra ficha del programa Hola a web explorador está usando tooaccess automatización de Azure.<br>![Ayuda para los módulos de integración](media/automation-integration-modules/automation-integration-module-activitydesc.png)
2. Si el módulo de Hola se ejecuta en un sistema remoto,

    a. Debe contener un archivo de metadatos del módulo de integración que define Hola información necesaria tooconnect toothat sistema remoto, lo que significa que el tipo de conexión de Hola.  
    b. Cada cmdlet en el módulo de hello debe ser capaz de tootake en un objeto de conexión (una instancia de ese tipo de conexión) como un parámetro.  

    Cmdlets de módulo de Hola se convierten en toouse más fácil en automatización de Azure si permite pasar un objeto con campos de hello del tipo de conexión de Hola como un cmdlet de toohello de parámetro. Esta forma, los usuarios no tienen parámetros de toomap de los parámetros correspondientes del cmdlet de hello connection asset toohello cada vez que llame a un cmdlet. Tomando como ejemplo de Hola runbook anterior, utiliza un activo de conexión de Twilio denominado CorpTwilio tooaccess Twilio y devolver todos los números de teléfono de hello en la cuenta de hello.  ¿Tenga en cuenta cómo se trata de asignar campos de Hola Hola toohello de parámetros de conexión del cmdlet Hola?<br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    Una manera más fácil y mejor tooapproach directamente esto está pasando Hola conexión objeto toohello cmdlet-
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    Puede habilitar el comportamiento parecido a esto para sus cmdlets, permitiéndoles tooaccept un objeto de conexión directamente como un parámetro, en lugar de simplemente los campos de conexión para los parámetros. Por lo general debe tener un parámetro establecido para cada uno, por lo que un usuario no usar la automatización de Azure puede llamar a los cmdlets sin generar un tooact de tabla hash como objeto de conexión de Hola. Conjunto de parámetros **SpecifyConnectionFields** a continuación se muestra toopass usa propiedades de campo de conexión de hello uno por uno. **UseConnectionObject** permite pasar Hola directamente a través de la conexión. Como puede ver, Hola cmdlet envío TwilioSMS Hola [Twilio PowerShell módulo](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) permite pasar cualquier modo: 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. Defina el tipo de salida de todos los cmdlets en el módulo de Hola. Al definir un tipo de salida de un cmdlet permite IntelliSense en tiempo de diseño toohelp determinar Hola enviar propiedades del cmdlet de hello, para su uso durante la creación. Es especialmente útil durante la automatización gráfica creación de runbooks, donde conocimiento de tiempo de diseño es la experiencia de usuario sencilla tooan clave con el módulo.<br><br> ![Tipo de salida de runbooks gráficos](media/automation-integration-modules/runbook-graphical-module-output-type.png)<br> Esto es similar toohello "con antelación de tipo" funcionalidad de un cmdlet de salida de la en PowerShell ISE sin necesidad de toorun lo.<br><br> ![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)<br>
4. Cmdlets de módulo de hello no debería tardar tipos de objeto complejo para los parámetros. El flujo de trabajo de PowerShell se diferencia del propio PowerShell en que almacena tipos complejos con formato deserializado. Permanecerán tipos primitivos como tipos primitivos, pero los tipos complejos son versiones de tootheir convertido deserializada, que son esencialmente los contenedores de propiedades. Por ejemplo, si utiliza hello **Get-Process** cmdlet en un runbook (o un flujo de trabajo de PowerShell para este propósito), devuelven un objeto de tipo [Deserialized.System.Diagnostic.Process], no Hola [esperado Tipo de System.Diagnostic.Process]. Este tipo tiene todas Hola mismas propiedades como Hola no deserializar el tipo, pero ninguno de los métodos de Hola. Si intentas toopass este valor como un cmdlet de tooa parámetro, donde hello cmdlet espera un valor de [System.Diagnostic.Process] para este parámetro, recibirá Hola siguiente error: *no se puede procesar la transformación de argumento en el parámetro 'process' . Error: "no se puede convertir el valor de"System.Diagnostics.Process (CcmExec)"¡hello de tipo"Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process".*   Esto es porque no hay que una discordancia de tipos entre Hola espera hello dado tipo [Deserialized.System.Diagnostic.Process] y [System.Diagnostic.Process] tipo. forma de Hello alternativa a este problema es tooensure Hola cmdlets del módulo no tienen tipos complejos de parámetros. Aquí es toodo de manera incorrecta de Hola.
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    A continuación se Hola derecho a propósito, en un tipo primitivo que puede utilizarse internamente mediante el cmdlet hello toograb Hola objeto complejo y usarlo. Puesto que los cmdlets se ejecutan en el contexto de Hola de PowerShell, no PowerShell flujos de trabajo dentro de cmdlet de hello $process se convierte en tipo de [System.Diagnostic.Process] correcto de Hola.  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   Activos de conexión en los runbooks son tablas hash, que son un tipo complejo, y aún estas tablas hash parece toobe toobe puede pasado a cmdlets para sus: parámetro de conexión perfectamente, con ninguna excepción de conversión. Técnicamente, algunos tipos de PowerShell son toocast capaz de correctamente desde su forma de tootheir deserializada forma serializada y por lo tanto, pueden pasarse a cmdlets de para los parámetros que admite elección de tipo no deserializa de Hola. Las tablas hash son uno de ellos. Es posible que toobe de tipos definidos del autor de un módulo implementada de modo que puede deserializar correctamente así, pero hay algunos tooconsider ventajas e inconvenientes. Hola tipo necesidades toohave un constructor predeterminado, tiene todas sus propiedades públicas y tener un PSTypeConverter. Sin embargo, para tipos ya definidos por el autor del módulo de hello no posee, hay no demasiado "corregirlos", por lo tanto, Hola tipos complejos de recomendación tooavoid para parámetros todos juntos. Creación de runbooks Sugerencia: si por alguna razón su cmdlets necesita el parámetro de tipo de tootake complejo o que usa de otra persona módulo que requiere un parámetro de tipo complejo, la solución de hello en los runbooks de flujo de trabajo de PowerShell y flujos de trabajo de PowerShell local PowerShell, es toowrap Hola cmdlet que genera el tipo complejo de Hola y Hola cmdlet que consume el tipo complejo de Hola Hola misma actividad de InlineScript. Como InlineScript ejecuta su contenido como PowerShell en lugar de flujo de trabajo de PowerShell, cmdlet Hola generar tipo complejo de hello generaría ese tipo correcto, no Hola deserializa el tipo complejo.
5. Asegúrese de todos los cmdlets en el módulo de hello sin estado. Flujo de trabajo de PowerShell se ejecuta cada cmdlet denominado en el flujo de trabajo de hello en una sesión diferente. Esto significa que los cmdlets que dependen de estado de sesión creado o modificado por otros cmdlets Hola mismo módulo no funcionará en los runbooks de flujo de trabajo de PowerShell.  Este es un ejemplo de lo que no toodo.
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. módulo de Hello debe estar totalmente contenida en un paquete capaz de Xcopy. Dado que los módulos de automatización de Azure son espacios aislados de automatización distribuida toohello cuando runbooks necesario tooexecute, deben toowork independientemente de que se ejecutan en el host de Hola. Esto significa que debe ser capaz de tooZip paquete de módulo de hello, muévalo tooany otro host con Hola versión de PowerShell igual o más recientes, y para que funcione con normalidad cuando se importan en el entorno de PowerShell de ese host. En orden para que toohappen, módulo de hello no debe depender de los archivos fuera de la carpeta de módulo de hello (carpeta de Hola que obtiene comprimirán al importar en la automatización de Azure), o en cualquier configuración de registro único en un host, como las que se establecen por Hola la instalación de un producto. Si no se respeta esta práctica recomendada, módulo de hello no podrá utilizarse en automatización de Azure.  

## <a name="next-steps"></a>Pasos siguientes

* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)
* toolearn más información acerca de la creación de módulos de PowerShell, consulte [escribir un módulo de Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)

