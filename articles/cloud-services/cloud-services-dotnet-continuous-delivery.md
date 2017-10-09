---
title: Servicios de entrega de aaaContinuous para la nube con TFS en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de nube tooset la entrega continua de Azure. Ejemplos de código para las instrucciones de línea de comandos de MSBuild y scripts PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Entrega continua para Servicios en la nube de Azure
Hello proceso descrito en este artículo muestra cómo tooset la entrega continua para aplicaciones de nube de Azure. Este proceso le permite crear automáticamente paquetes e implementar Hola paquete tooAzure después de cada comprobación de código. proceso de compilación del paquete se describe en este artículo Hello es equivalente toohello **paquete** comandos en Visual Studio y los pasos de publicación son equivalente toohello **publicar** en Visual Studio.
Hola artículo abarca Hola métodos que usaría toocreate un servidor de compilación con instrucciones de línea de comandos de MSBuild y scripts de Windows PowerShell y también se muestra cómo toooptionally configurar Visual Studio Team Foundation Server - definiciones de Team Build comandos de MSBuild hello toouse y scripts de PowerShell. proceso de Hello es personalizable para su entorno de compilación y los entornos de destino de Azure.

También puede usar Visual Studio Team Services, una versión de TFS que está hospedado en Azure, toodo esto más fácilmente. 

Antes de comenzar, debe publicar su aplicación desde Visual Studio.
Así se asegurará de que todos los recursos de hello están disponibles y se inicializa al intentar el proceso de publicación de tooautomate Hola.

## <a name="1-configure-hello-build-server"></a>1: configurar Hola Build Server
Para poder crear un paquete de Azure mediante el uso de MSBuild, debe instalar Hola requerido software y las herramientas en el servidor de compilación Hola.

Visual Studio no es necesario toobe instalado en el servidor de compilación Hola. Si desea que el servidor de compilación toouse toomanage de servicio de Team Foundation Build, siga las instrucciones de Hola Hola [servicio de Team Foundation Build] [ Team Foundation Build Service] documentación.

1. En el servidor de compilación de hello, instale hello [.NET Framework 4.5.2][.NET Framework 4.5.2], que incluye MSBuild.
2. Instalar más reciente hello [herramientas de creación de Azure para .NET](https://azure.microsoft.com/develop/net/).
3. Instalar hello [bibliotecas de Azure para .NET](http://go.microsoft.com/fwlink/?LinkId=623519).
4. Servidor de compilación del archivo de copia hello Microsoft.WebApplication.targets de una toohello de instalación de Visual Studio.

   En un equipo con Visual Studio instalado, este archivo se encuentra en el directorio de hello C:\\Program Files(x86)%\\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications. Debe copiar toohello mismo directorio en el servidor de compilación Hola.
5. Instalar hello [Azure Tools para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).

## <a name="2-build-a-package-using-msbuild-commands"></a>2 Compilación de un paquete con comandos de MSBuild
Esta sección describe cómo tooconstruct un MSBuild comando que crea un paquete de Azure. Ejecutar este paso en tooverify de servidor de compilación de Hola que todo está configurado correctamente y encargada de comandos de MSBuild Hola lo que le gustaría toodo. Puede agregar esta tooexisting de línea de comandos generar secuencias de comandos en el servidor de compilación de hello, o puede usar la línea de comandos de hello en una definición de compilación de TFS, tal y como se describe en la sección siguiente Hola. Para obtener más información acerca de los parámetros de línea de comandos y MSBuild, consulte [Referencia de la línea de comandos de MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).

1. Si Visual Studio está instalado en el servidor de compilación de hello, busque y seleccione **Visual Studio Command Prompt** en hello **Visual Studio Tools** carpeta de Windows.

   Si Visual Studio no está instalado en el servidor de compilación de hello, abra un símbolo del sistema y asegúrese de que MSBuild.exe es accesible en la ruta de acceso. MSBuild se instala con .NET Framework de hello en hello ruta de acceso % WINDIR %\\Microsoft.NET\\Framework\\*versión*. Por ejemplo, para agregar la variable de entorno PATH de MSBuild.exe toohello si tiene instalado .NET Framework 4, escriba Hola siguiente comando en el símbolo del sistema de hello:

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. En el símbolo de hello, desplazarse por las carpetas de toohello que contiene el archivo de proyecto de Azure que desea toobuild.
3. Ejecute MSBuild con/target hello: opción como en el siguiente ejemplo de Hola de publicación:

       MSBuild /target:Publish

   Esta opción se puede abreviar como /t:Publish. opción de /t:Publish Hello en MSBuild no debe confundirse con los comandos de publicación de hello disponibles en Visual Studio cuando tienes hello que Azure SDK instalado. Hola /t: opción de publicación solo compilaciones Hola paquetes de Azure. No implementa paquetes de saludo como Hola publicar comandos en Visual Studio tienen.

   Si lo desea, puede especificar el nombre del proyecto de Hola como un parámetro de MSBuild. Si no se especifica, se utiliza el directorio actual de Hola. Para más información acerca de las opciones de línea de comandos de MSBuild, consulte [Referencia de la línea de comandos de MSBuild1](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).
4. Busque la salida de hello. De forma predeterminada, este comando crea un directorio en carpeta de raíz de toohello de relación para el proyecto de hello, como *ProjectDir*\\bin\\*configuración* \\ App.Publish\\. Al compilar un proyecto de Azure, se generan dos archivos, el propio archivo de paquete Hola y Hola que acompaña a archivo de configuración:

   * Project.cspkg
   * ServiceConfiguration.*TargetProfile*.cscfg

   De manera predeterminada, cada proyecto de Azure incluye un archivo de configuración del servicio (archivo .cscfg) para las compilaciones locales (depuración) y otro para las compilaciones en la nube (ensayo o producción), pero puede agregar o quitar archivos de configuración del servicio según sea necesario. Al compilar un paquete de Visual Studio, se le pedirá que tooinclude de archivo de configuración de servicio junto con el paquete de saludo.
5. Especifique el archivo de configuración de servicio de Hola. Al compilar un paquete con MSBuild, archivo de configuración de servicio local de Hola se incluye de forma predeterminada. tooinclude un archivo de configuración de servicio diferente, establezca la propiedad de TargetProfile de comandos de MSBuild hello, como en el siguiente ejemplo de Hola:

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. Especifique la ubicación de hello para la salida de hello. Ruta de acceso del conjunto Hola utilizando el/p: PublishDir =*directorio* \\ opción, incluidos los Hola separador de barra diagonal inversa, como en el siguiente ejemplo de Hola final:

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   Una vez que haya construido y probar un MSBuild adecuado toobuild de línea de comandos de los proyectos y combinarlos en un paquete de Azure, puede agregar esta línea de comandos tooyour los scripts de compilación. Si su servidor de compilación usa scripts personalizados, este proceso dependerá de los detalles de su proceso personalizado de compilación. Si usa TFS como un entorno de compilación, a continuación, puede seguir las instrucciones de Hola Hola siguiente paso tooadd hello Azure paquete compilación tooyour proceso de compilación.

## <a name="3-build-a-package-using-tfs-team-build"></a>3: Compilación de un paquete con TFS Team Build
Si tiene configurado como servidor de compilación de un controlador de compilación y Hola Team Foundation Server (TFS) configurado como una máquina de compilación TFS, a continuación, opcionalmente, puede configurar una compilación automatizada para el paquete de Azure. Para obtener información sobre cómo tooset una y usar Team Foundation server como un sistema de compilación, consulte [escalar horizontalmente un sistema de compilación][Scale out your build system]. En concreto, el siguiente procedimiento se supone que ha configurado el servidor de compilación tal y como se describe en [implementar y configurar un servidor de compilación][Deploy and configure a build server], y que ha creado un proyecto de equipo creado una nube proyecto de servicio en el proyecto de equipo de Hola.

tooconfigure TFS toobuild Azure realizado por paquetes, Hola pasos:

1. En Visual Studio en el equipo de desarrollo, en el menú de vista de hello, elija **Team Explorer**, o elija Ctrl +\\, Ctrl + M. En la ventana de Team Explorer, expanda hello **compilaciones** nodo o elija hello **compilaciones** página y elija **nueva definición de compilación**.

   ![Opción Nueva definición de compilación][0]
2. Elija hello **desencadenador** pestaña y especificar Hola deseada condiciones para cuando desee Hola toobe paquete creado. Por ejemplo, especificar **integración continua** paquete de hello toobuild siempre que sea un origen de control en el repositorio se produce.
3. Elija hello **configuración del origen de** y a asegurarse de que la carpeta del proyecto aparece en hello **carpeta de Control de código fuente** columna, y el estado de hello es **Active**.
4. Elija hello **valores predeterminados de compilación** pestaña y en el controlador de compilación, compruebe el nombre de hello del servidor de compilación de Hola.  Además, elija la opción hello **siguiente de toohello de salida de compilación copia la carpeta de entrega** y especifique la ubicación de destino de hello deseado.
5. Elija hello **proceso** ficha. En la ficha proceso de hello, elija plantilla predeterminada de hello, en **generar**, elija el proyecto de hello si aún no está seleccionado y expanda hello **avanzadas** sección Hola **compilar**sección de la cuadrícula de Hola.
6. Elija **argumentos de MSBuild**y establezca los argumentos de línea de comandos de MSBuild apropiados Hola tal como se describe en el paso 2 anterior. Por ejemplo, escriba **/t: publicar/p: PublishDir =\\\\myserver\\quita\\**  toobuild un paquete de hello empaquetar y copiar archivos de ubicación toohello \\ \\myserver\\quita\\:

   ![Argumentos de MSBuild][2]

   > [!NOTE]
   > Copiar Hola archivos tooa recurso compartido público facilita toomanually más fácil de implementar paquetes de saludo desde el equipo de desarrollo.
7. Hola se ha comprobado correctamente el paso de compilación de prueba mediante la comprobación en un proyecto de tooyour de cambio o una nueva compilación en cola. tooqueue de una nueva compilación de Team Explorer, haga clic en **todas las definiciones de compilación,** y, a continuación, elija **poner nueva compilación en cola**.

## <a name="4-publish-a-package-using-a-powershell-script"></a>4: Publicación de un paquete con un script de PowerShell
Esta sección describe cómo tooconstruct una secuencia de comandos de Windows PowerShell que se publicará el paquete de aplicación de nube de hello había salida tooAzure con parámetros opcionales. Este script se puede llamar después del paso de compilación de hello en la automatización de compilación personalizada. También puede llamarse desde las actividades de flujo de trabajo de la Plantilla de procesos en Visual Studio TFS Team Build.

1. Instalar hello [cmdlets de PowerShell de Azure] [ Azure PowerShell cmdlets] (v0.6.1 o superior).
   Durante la fase de la instalación de cmdlet de hello, elija tooinstall como un complemento. Tenga en cuenta que esta versión compatible oficialmente reemplaza la versión anterior de hello ofrecida a través de CodePlex, aunque las versiones anteriores de Hola se numeran 2.x.x.
2. Inicie PowerShell de Azure mediante el menú de inicio de Hola o página de inicio. Si se inicia en este modo, se cargará Hola cmdlets de PowerShell de Azure.
3. En el símbolo del sistema de PowerShell hello, verifique que los cmdlets de PowerShell de Hola estén cargados escribiendo el comando parcial de hello `Get-Azure` y, a continuación, presione la tecla Tab para finalización de instrucciones de Hola.

   Si presiona la tecla de la pestaña de hello varias veces, verá varios comandos de PowerShell de Azure.
4. Compruebe que puede conectarse tooyour suscripción de Azure importando la información de suscripción de archivo .publishsettings de Hola.

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   A continuación, escriba el comando de Hola

   `Get-AzureSubscription`

   Se muestra información sobre su suscripción. Verifique que todo esté correcto.
5. Guarde la plantilla de script de Hola Hola final de este artículo a la carpeta de scripts como c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.
6. Revise la sección de parámetros de Hola de script de Hola. Agregue o modifique cualquiera de los valores predeterminados. Estos valores siempre pueden omitirse al pasar parámetros explícitos.
7. Asegúrese de no hay servicios de nube válido y script de publicación de las cuentas de almacenamiento creadas en la suscripción que puede tener como destino Hola. La cuenta de almacenamiento (almacenamiento de blobs) se pueden tooupload usado y almacenar temporalmente el archivo de paquete y la configuración de implementación de hello mientras se está creando la implementación.

   * toocreate un nuevo servicio de nube, puede llamar a esta secuencia de comandos o utilice hello [portal de Azure](https://portal.azure.com). nombre del servicio de nube de Hola se usará como prefijo un nombre de dominio completo y, por tanto, deben ser único.

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * toocreate una cuenta de almacenamiento, puede llamar a esta secuencia de comandos o utilice hello [portal de Azure](https://portal.azure.com). nombre de cuenta de almacenamiento de Hola se usará como prefijo un nombre de dominio completo y, por tanto, deben ser único. También puede intentar usar Hola mismo nombre como servicio en la nube.

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. Llame al script de Hola directamente desde PowerShell de Azure, o conecte este toooccur de automatización de compilación de script tooyour host después de la compilación del paquete Hola.

   > [!IMPORTANT]
   > script de Hola siempre eliminará o reemplazar las implementaciones existentes de forma predeterminada si se detectan. Esto es necesario para habilitar la entrega continua desde la automatización donde no es posible una solicitud del usuario.
   >
   >

   **Escenario de ejemplo 1:** toohello de implementación continua de un servicio de almacenamiento provisional:

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   A esto le sigue generalmente una verificación de ejecución de prueba y un intercambio de VIP. intercambio de VIP de Hello puede hacerse a través de hello [portal de Azure](https://portal.azure.com) o mediante el cmdlet de hello Move-Deployment.

   **Escenario de ejemplo 2:** entorno de producción de toohello de implementación continua de un servicio de prueba dedicados

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **Escritorio remoto:**

   Si está habilitado Escritorio remoto en su proyecto de Azure necesitará tooperform los pasos de un solo uso adicionales hello tooensure que correcta certificado del servicio de nube está cargado servicios en la nube tooall objetivo de esta secuencia de comandos.

   Buscar valores de huella digital de certificado de hello esperados por sus roles. Los valores de huella digital son visibles en la sección certificados de hello del archivo de configuración de nube (es decir, ServiceConfiguration.Cloud.cscfg). También es visible en el cuadro de diálogo de configuración de escritorio remoto de hello en Visual Studio cuando Mostrar opciones y ver Hola seleccionado certificado.

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   Cargar certificados de escritorio remoto como un paso de instalación única mediante Hola siguiente secuencia de comandos de cmdlet:

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   Por ejemplo:

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   O bien puede exportar el archivo de certificado de hello PFX con clave privada y cargar certificados tooeach servicio de destino en la nube utilizando la [portal de Azure](https://portal.azure.com).

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **Actualizar implementación frente a Eliminar implementación -\> Nueva implementación**

   script de Hola predeterminada realizará una implementación de actualización ($enableDeploymentUpgrade = 1) cuando no se pasa ningún parámetro o el valor 1 se pasa explícitamente. Para las instancias simples, esto tiene la ventaja de tardar menos tiempo que una implementación completa. Para instancias que necesitan una alta disponibilidad, que este enfoque también tiene la ventaja de Hola de dejar algunas instancias que se ejecutan mientras que otros están actualizadas (recorrido de su dominio de actualización), además de la dirección VIP no se eliminará.

   La implementación de actualización puede deshabilitarse en el script de Hola ($enableDeploymentUpgrade = 0) o pasando *- enableDeploymentUpgrade 0* como un parámetro, que modifica la eliminación de toofirst del comportamiento de script cualquier implementación existente y, a continuación, creará una nueva implementación.

   > [!IMPORTANT]
   > script de Hola siempre eliminará o reemplazar las implementaciones existentes de forma predeterminada si se detectan. Esto es necesario para habilitar la entrega continua desde la automatización donde no es posible una solicitud del usuario/operador.
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5: Publicación de un paquete con TFS Team Build
Este paso opcional conecta a TFS Team Build toohello secuencia de comandos creada en el paso 4, que controla la publicación de tooAzure de compilación del paquete de saludo. Esto implica Hola Modificar plantilla de proceso utilizada por la definición de compilación para que se ejecute una actividad de publicación final Hola de flujo de trabajo de Hola. Hola publicar actividad ejecutará el comando de PowerShell pasar parámetros de compilación de Hola. Salida de hello tiene como destino de MSBuild y script de publicación se canalizará a la salida de compilación estándar de hello.

1. Editar definición de compilación responsables de hello continua implementar.
2. Seleccione hello **proceso** ficha.
3. Siga [estas instrucciones](http://msdn.microsoft.com/library/dd647551.aspx) tooadd un proyecto de actividad para hello plantilla de proceso de compilación, descargar la plantilla predeterminada de hello, agregarlo al proyecto de Hola y lo proteja. Asigne un nombre nuevo, como AzureBuildProcessTemplate a plantilla de proceso de compilación de Hola.
4. Devolver toohello **proceso** y a usar **mostrar detalles** tooshow una lista de plantillas de proceso de compilación disponible. Elija hello **nuevo...**  botón y navegue toohello proyecto que acaba de agrega y protegido. Busque la plantilla de Hola que acaba de crear y elija **Aceptar**.
5. Hola abierto había seleccionado la plantilla de proceso para su edición. Puede abrir directamente en el Diseñador de flujo de trabajo de Hola o en hello toowork de editor de XML con hello XAML.
6. Agregar Hola siguiendo la lista de argumentos nuevos como partidas separadas en la ficha de argumentos de hello del Diseñador de flujo de trabajo de Hola. Todos los argumentos deben tener la dirección=In y el tipo=String. Estos serán tooflow usa parámetros de definición de compilación de hello en flujo de trabajo de hello, qué Hola de toocall usa get, a continuación, el script de publicación.

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lista de argumentos][3]

   Hola que XAML correspondiente tiene el siguiente aspecto:

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. Agregue una nueva secuencia final Hola de ejecutar en el agente:

   1. Empiece agregando un toocheck de actividad de instrucción If para un archivo de script válido. Establecer el valor de toothis de hello condición:

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. Hola, a continuación, caso de hello instrucción If, agregue una nueva actividad de secuencia. Publicar conjunto Hola Mostrar nombre too'Start'
   3. Con hello inicio publicar secuencia aún seleccionado, agregue la siguiente lista de nuevas variables como elementos de línea independientes en la pestaña variables de diseñador de flujo de trabajo de Hola. Todas las variables deben tener el tipo de variable =Cadena y el ámbito =Iniciar publicación. Estos serán tooflow usa parámetros de definición de compilación de hello en el flujo de trabajo, que, a continuación, hello toocall usado de get script de publicación.

      * SubscriptionDataFilePath, de tipo Cadena
      * PublishScriptFilePath, de tipo Cadena

        ![Nuevas variables][4]
   4. Si usa TFS 2012 o versiones anteriores, agregar una actividad ConvertWorkspaceItem Hola principio de Hola nueva secuencia. Si usa TFS 2013 o versiones posteriores, agregar una actividad GetLocalPath Hola principio de la nueva secuencia de Hola. Para una ConvertWorkspaceItem, establecer las propiedades de hello como sigue: dirección = ServerToLocal, DisplayName = 'Convert publicar nombre de archivo de script,' entrada = 'PublishScriptLocation', resultado = 'PublishScriptFilePath', el área de trabajo = 'Área de trabajo'. Para una actividad GetLocalPath, establecer Hola propiedad IncomingPath too'PublishScriptLocation', y Hola resultado too'PublishScriptFilePath'. Esta toohello de ruta de acceso de actividad convierte Hola script desde ubicaciones de servidor TFS de publicación (si procede) tooa ruta de acceso del disco local estándar.
   5. Si usa TFS 2012 o versiones anteriores, agregue otra actividad ConvertWorkspaceItem final Hola de Hola nueva secuencia. Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'. Si está utilizando TFS 2013 o posterior, agregue otro GetLocalPath. IncomingPath='SubscriptionDataFileLocation' y Result='SubscriptionDataFilePath.'
   6. Agregue una actividad InvokeProcess final Hola de hello nueva secuencia.
      Esta llamadas de actividad PowerShell.exe con hello argumentos pasan por Hola definición de compilación.

      + Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)
      + DisplayName =Ejecutar script de publicación
      + FileName = "PowerShell" (incluya comillas hello)
      + OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)
   7. Hola **controlar la salida estándar** sección cuadro de texto de la InvokeProcess, establezca Hola cuadro de texto valor too'data'. Se trata de una salida estándar de hello toostore variable datos.
   8. Agregar una actividad WriteBuildMessage justo debajo de hello **controlar la salida estándar** sección. Establecer la importancia de hello = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' y Hola mensaje = 'data'. Esto garantiza que la salida estándar de hello de la secuencia de comandos obtener escribirán toohello resultados de la compilación.
   9. Hola **controlar la salida de Error** sección cuadro de texto de la InvokeProcess, establezca Hola cuadro de texto valor too'data'. Se trata de un datos de error estándar de hello toostore variable.
   10. Agregar una actividad WriteBuildError justo debajo de hello **controlar la salida de Error** sección. Establecer Hola mensaje = 'data'. Esto garantiza la salida de error de compilación toohello obtener escribirán Hola estándar errores de script de Hola.
   11. Corrija los errores, que se indican por signos de exclamación azules. Mantenga el mouse sobre el tooget signos de exclamación una sugerencia sobre el error de Hola. Guardar el flujo de trabajo de Hola para borrar los errores.

   resultado final de Hola de hello publicar actividades tendrá un aspecto similar al siguiente en el Diseñador de Hola de flujo de trabajo:

   ![Actividades de flujo de trabajo][5]

   resultado final de Hola de hello publicar actividades tendrá un aspecto similar al siguiente en XAML de flujo de trabajo:

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. Guarde el flujo de trabajo de plantilla de proceso de compilación de Hola y proteger este archivo.
9. Editar definición de compilación de hello (cerrarla si ya está abierto), seleccione hello y **New** botón si aún no ve nueva plantilla de hello en lista de Hola de plantillas de proceso.
10. Establecer valores de propiedad de parámetro de Hola Hola sección adicional de la manera siguiente:

    1. CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Este valor se obtiene de: ($PublishDir)ServiceConfiguration.Cloud.cscfg*
    2. PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Este valor se obtiene de:($PublishDir)($ProjectName).cspkg*
    3. PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'
    4. ServiceName = 'mycloudservicename' *usar Hola nube adecuada servicio el nombre aquí*
    5. Entorno = 'Staging'
    6. StorageAccountName = 'mystorageaccountname' *usar Hola almacenamiento adecuado cuenta el nombre aquí*
    7. SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'
    8. SubscriptionName = 'default'

    ![Valores de propiedad de parámetro][6]
11. Guardar cambios de hello toohello definición de compilación.
12. Poner en cola un tooexecute compilación ambos Hola compilación del paquete y publicación. Si tiene un desencadenador establecer tooContinuous integración, se ejecutará este comportamiento en cada protección.

### <a name="publishcloudserviceps1-script-template"></a>Plantilla de script PublishCloudService.ps1
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>Pasos siguientes
depuración remota de tooenable cuando se utiliza la entrega continua, vea [habilitar la depuración remota al utilizar la entrega continua toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
