---
title: "aaaUse PowerShell tooCreate una máquina virtual con unas Native Mode Report Server | Documentos de Microsoft"
description: "Este tema describe y le guía a través de la implementación de Hola y configuración de un servidor de informes de modo nativo de SQL Server Reporting Services en una máquina Virtual de Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>Usar PowerShell tooCreate un Azure VM con un modo de servidor de informes nativo
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Este tema describe y le guía a través de la implementación de Hola y configuración de un servidor de informes de modo nativo de SQL Server Reporting Services en una máquina Virtual de Azure. Hola pasos de este documento, use una combinación de máquina virtual de pasos manuales toocreate hello y una secuencia de comandos de Windows PowerShell tooconfigure Reporting Services en hello máquina virtual. script de configuración de Hello incluye abrir un puerto de firewall para HTTP o HTTPs.

> [!NOTE]
> Si no es necesario que **HTTPS** en el servidor de informes de hello, **omita el paso 2**.
> 
> Después de crear Hola VM en el paso 1, vaya toohello sección usar script tooconfigure Hola servidor de informes y HTTP. Después de ejecutar script de Hola, servidor de informes de hello es toouse listo.

## <a name="prerequisites-and-assumptions"></a>Requisitos previos y suposiciones
* **Suscripción de Azure**: Compruebe el número de Hola de núcleos disponibles en su suscripción de Azure. Si creas Hola recomendada tamaño de memoria virtual **A3**, necesita **4** núcleos disponibles. Si usa un tamaño de máquina virtual de **A2**, necesita **2** núcleos disponibles.
  
  * límite de núcleos de hello tooverify de su suscripción, Hola portal de Azure clásico, haga clic en configuración en el panel izquierdo de hello y, a continuación, haga clic en uso en el menú superior Hola.
  * cuota de núcleos de hello tooincrease, póngase en contacto con [soporte técnico de Azure](https://azure.microsoft.com/support/options/). Para obtener más información sobre el tamaño de la máquina virtual, consulte [Tamaños de máquinas virtuales para Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* **Script de Windows PowerShell**: tema Hola se da por supuesto que tiene conocimientos prácticos básicos de Windows PowerShell. Para obtener más información sobre cómo usar Windows PowerShell, vea Hola siguiente:
  
  * [Inicio de Windows PowerShell en Windows Server](https://technet.microsoft.com/library/hh847814.aspx)
  * [Introducción a Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>Paso 1: Aprovisionar una máquina virtual de Azure
1. Examinar toohello portal de Azure clásico.
2. Haga clic en **máquinas virtuales** en el panel izquierdo de Hola.
   
    ![máquinas virtuales de microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. Haga clic en **Nuevo**.
   
    ![botón nuevo](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. Haga clic en **De la galería**.
   
    ![nueva máquina virtual de la galería](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. Haga clic en **SQL Server 2014 RTM Standard: Windows Server 2012 R2** y, a continuación, haga clic en hello flecha toocontinue.
   
    ![Siguiente](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    Si necesita datos de Reporting Services de hello controlada por la característica de suscripciones, elija **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**. Para obtener más información sobre las ediciones de SQL Server y compatibilidad con las características, vea [características compatibles con las ediciones de SQL Server 2012 hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).
6. En hello **configuración de máquina Virtual** página, edite Hola siguientes campos:
   
   * Si hay más de un **versión fecha**, seleccione Hola versión más reciente.
   * **Nombre de máquina virtual**: nombre de la máquina de hello también se utiliza en la siguiente página de configuración de hello como nombre DNS del servicio de nube de hello predeterminado. nombre DNS de Hello debe ser único en hello servicio de Azure. Considere la posibilidad de configurar Hola VM con un nombre de equipo que describe qué Hola máquina virtual se utiliza para. Por ejemplo, ssrsnativecloud.
   * **Nivel**: estándar
   * **Tamaño: A3** recomienda Hola tamaño de máquina virtual para las cargas de trabajo de SQL Server. Si una máquina virtual solo se utiliza como un servidor de informes, un tamaño A2 es suficiente a menos que el servidor de informes de hello experimente una carga de trabajo grande. Para más información sobre precios de máquinas virtuales, consulte [Precios de Máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/).
   * **Nuevo nombre de usuario**: nombre de Hola que proporcione se crea como un administrador en hello VM.
   * **Nueva contraseña** y **Confirmar**. Esta contraseña se usa para la nueva cuenta de administrador de Hola y se recomienda que utilice una contraseña segura.
   * Haga clic en **Siguiente**. ![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. En la página siguiente de hello, edite Hola siguientes campos:
   
   * **Servicio en la nube**: seleccione **Crear un nuevo servicio en la nube**.
   * **Nombre DNS del servicio de nube**: se trata de nombre DNS público de Hola de hello servicio de nube que está asociado con hello VM. Hola predeterminado es nombre hello que escribió para el nombre de la máquina virtual de Hola. Si en pasos posteriores del tema de hello, crear un certificado SSL de confianza y, a continuación, se utiliza el nombre DNS de Hola valor Hola Hola "**emitido para**" del certificado de Hola.
   * **Afinidad de la región/grupo/red Virtual**: elija Hola región más cercana tooyour a los usuarios finales.
   * **Cuenta de almacenamiento**: use una cuenta de almacenamiento generada automáticamente
   * **Conjunto de disponibilidad**: ninguno.
   * **Los puntos de conexión** mantener hello **escritorio remoto** y **PowerShell** puntos de conexión y, a continuación, agregue el extremo HTTP o HTTPS, dependiendo de su entorno.
     
     * **HTTP**: Hola predeterminadas son puertos públicos y privados **80**. Tenga en cuenta que si utiliza un puerto privado distinto de 80, modifique **$HTTPport = 80** en secuencia de comandos de hello http.
     * **HTTPS**: Hola predeterminadas son puertos públicos y privados **443**. Una práctica recomendada de seguridad es el puerto privado de toochange hello y configurar su hello y firewall informes servidor toouse Hola privado puerto. Para obtener más información sobre los puntos de conexión, vea [cómo tooSet la comunicación con una máquina Virtual](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Tenga en cuenta que si utiliza un puerto distinto de 443, cambie el parámetro hello **$HTTPsport = 443** Hola script HTTPS.
   * Haga clic en Siguiente. ![Siguiente](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. En hello última página del Asistente de hello, mantenga el valor predeterminado de hello **instalar agente de máquina virtual de hello** seleccionado. Hello pasos de este tema no utilizar agente de máquina virtual de hello pero si piensa tookeep esta máquina virtual, agente de VM de Hola y las extensiones le permitirá tooenhance visitará CM.  Para obtener más información sobre el agente de máquina virtual de hello, consulte [agente de máquina virtual y extensiones – parte 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/). Uno de anuncio de Hola predeterminado extensiones instaladas ejecutando es extensión "BGINFO" de Hola que se muestra en el escritorio de la máquina virtual de hello, espacio de la unidad de información del sistema, como la dirección IP interna y free.
9. Haga clic en Completo. ![Aceptar](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. Hola **estado** de hello VM se muestra como **iniciando (aprovisionamiento)** durante el proceso de aprovisionamiento de hello y, a continuación, se muestra como **ejecuta** cuando Hola máquina virtual se ha aprovisionado y listo toouse.

## <a name="step-2-create-a-server-certificate"></a>Paso 2: Crear un certificado de servidor
> [!NOTE]
> Si no se requiere HTTPS en el servidor de informes de hello, puede **omita el paso 2** y vaya sección toohello **usar HTTP y el servidor de informes de script tooconfigure hello**. Use Hola HTTP script tooquickly configurar servidor de informes de Hola y el informe de hello servidor será toouse listo.

En orden toouse HTTPS en hello VM, necesita un certificado SSL de confianza. Según el escenario, puede usar uno de hello siguiendo dos métodos:

* Un certificado SSL válido emitido por una entidad de certificación (CA) y de confianza de Microsoft. los certificados de CA raíz de Hello son necesario toobe distribuida a través de hello programa de certificados raíz de Microsoft. Para obtener más información acerca de este programa, consulte [Windows y el programa de certificados de Windows Phone 8 SSL raíz (miembro de CA)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) y [Introducción toohello programa de certificados raíz de Microsoft](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).
* Un certificado autofirmado. No se recomiendan los certificados autofirmados para entornos de producción.

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse un certificado creado por una entidad de confianza de certificados (CA)
1. **Solicitar un certificado de servidor para el sitio Web de Hola de una entidad de certificación**. 
   
    Hola Asistente para certificados de servidor Web puede usar cualquier toogenerate un archivo de solicitud de certificado (Certreq.txt) que envía tooa entidad emisora de certificados, o toogenerate una solicitud para una entidad de certificación en línea. Por ejemplo, los Servicios de certificados de Microsoft en Windows Server 2012. Según el nivel de Hola de garantía de identificación proporcionado por el certificado de servidor, es la solicitud de varios días, meses tooseveral para tooapprove de entidad de certificación de Hola y envíe un archivo de certificado. 
   
    Para obtener más información sobre las solicitudes de certificados de servidor, vea Hola siguiente: 
   
   * Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).
   * TooAdminister de herramientas de seguridad Windows Server 2012.
     
     [Herramientas de seguridad tooAdminister Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > Hola **emitido para** campo de hello confianza certificado SSL debe ser Hola igual como hello **nombre de DNS del servicio de nube** que usó para Hola nueva máquina virtual.

2. **Instalar certificado de servidor de hello en el servidor Web de hello**. servidor Web de Hello en este caso es hello VM que Hola de hosts de servidor de informes y se crea el sitio Web de Hola en pasos posteriores cuando se configura Reporting Services. Para obtener más información acerca de cómo instalar certificado de servidor hello en el servidor Web de hello utilizando el complemento MMC de certificados de hello, consulte [instalar un certificado de servidor](https://technet.microsoft.com/library/cc740068).
   
    Si desea que el script de Hola toouse incluido con este tema, el servidor de informes de tooconfigure hello, Hola valor de certificados de hello **huella digital** es necesario que un parámetro de script de Hola. Vea Hola próxima sección para obtener más información sobre cómo tooobtain Hola huella digital del certificado de Hola.
3. Asignar al servidor de informes de hello server certificado toohello. asignación de Hola se completa en la sección siguiente de hello cuando se configura el servidor de informes de Hola.

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>Hola toouse certificado autofirmado de máquinas virtuales
Un certificado autofirmado se creó en hello VM cuando Hola VM se haya proporcionado. certificado de Hello tiene Hola mismo nombre como nombre DNS de VM de Hola. En errores de certificado de orden tooavoid, es necesario dicho certificado hello es de confianza en hello propia máquina virtual y también para todos los usuarios del sitio de Hola.

1. tootrust Hola CA raíz del certificado de hello en hello VM Local, agregue Hola certificado toohello **entidades de certificación raíz de confianza**. Hola aquí te mostramos un resumen de pasos de hello necesarios. Para obtener instrucciones detalladas sobre cómo tootrust Hola entidad emisora de certificados, consulte [instalar un certificado de servidor](https://technet.microsoft.com/library/cc740068).
   
   1. En hello portal de Azure clásico, seleccione Hola máquina virtual y haga clic en conectar. Según la configuración del explorador, es posible que toosave solicitada un archivo .rdp para la conexión toohello máquina virtual.
      
       ![conectar máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Usar el nombre de VM de hello usuario, nombre de usuario y contraseña que configuró cuando creaste Hola máquina virtual. 
      
       Por ejemplo, en Hola después de la imagen, nombre de la máquina virtual de hello es **ssrsnativecloud** y es el nombre de usuario de hello **testuser**.
      
       ![el inicio de sesión incluye la máquina virtual](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. Ejecute mmc.exe. Para obtener más información, consulte [Cómo: ver certificados con hello complemento MMC](https://msdn.microsoft.com/library/ms788967.aspx).
   3. En la aplicación de consola de hello **archivo** menú, agregar hello **certificados** complemento, seleccione **cuenta de equipo** cuando se le pida y, a continuación, haga clic en **siguiente**.
   4. Seleccione **equipo Local** toomanage y, a continuación, haga clic en **finalizar**.
   5. Haga clic en **Aceptar** y, a continuación, expanda hello **certificados - Personal** nodos y, a continuación, haga clic en **certificados**. se denomina nombre de DNS de Hola de hello VM Hello certificado y termina con **cloudapp.net**. Haga clic en el nombre del certificado de Hola y haga clic en **copia**.
   6. Expanda hello **entidades de certificación raíz de confianza** nodo y, a continuación, haga **certificados** y, a continuación, haga clic en **pegar**.
   7. toovalidate, doble haga clic en el nombre del certificado Hola bajo **entidades de certificación raíz de confianza** y compruebe que no hay ningún error y puede ver el certificado. Si desea que toouse Hola HTTPS script incluido con este tema, el servidor de informes de tooconfigure hello, Hola valor de certificados de hello **huella digital** es necesario que un parámetro de script de Hola. **valor de huella digital de hello tooget**, complete Hola siguiente. También hay una huella digital de PowerShell ejemplo tooretrieve hello en sección [usar HTTPS y servidor de informes de script tooconfigure Hola](#use-script-to-configure-the-report-server-and-HTTPS).
      
      1. Haga doble clic en el nombre de Hola Hola del certificado de, por ejemplo ssrsnativecloud.cloudapp.net.
      2. Haga clic en hello **detalles** ficha.
      3. Haga clic en **Huella digital**. valor de Hola de huella digital de Hola se muestra en el campo de detalles de hello, por ejemplo a6 08 3C df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9C 2c fb 2f.
      4. Copie la huella digital de Hola y guardar el valor de Hola para más tarde o editar script de Hola ahora.
      5. (*) Antes de ejecutar script de Hola, quite los espacios de hello entre pares de Hola de valores. Por ejemplo la huella digital de Hola que se indicó antes ahora sería a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.
      6. Asignar al servidor de informes de hello server certificado toohello. asignación de Hola se completa en la sección siguiente de hello cuando se configura el servidor de informes de Hola.

Si usas un certificado SSL autofirmado, nombre de hello en el certificado de Hola ya coincide con hostname Hola de hello VM. Por lo tanto, Hola DNS de la máquina de hello ya está registrado globalmente y puede tener acceso desde cualquier cliente.

## <a name="step-3-configure-hello-report-server"></a>Paso 3: Configurar el servidor de informes de Hola
En esta sección se explica cómo configurar Hola VM como un servidor de informes de modo nativo de Reporting Services. Puede usar uno de hello después el servidor de informes de métodos tooconfigure hello:

* Servidor de informes de uso Hola script tooconfigure Hola
* Hola tooConfigure use el Administrador de configuración del servidor de informes.

Para obtener pasos más detallada, vea la sección de hello [toohello conectar Máquina Virtual e inicie Hola Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).

**Nota sobre la autenticación:** Hola método de autenticación recomendado no es autenticación de Windows y autenticación de Reporting Services de hello predeterminada. Solo los usuarios que se configuran en hello VM pueden tener acceso a Reporting Services y asignan tooReporting roles de servicios.

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>Servidor de informes de uso script tooconfigure hello y HTTP
toouse Hola Windows PowerShell script tooconfigure Hola servidor de informes, Hola completa pasos. configuración de Hello incluye HTTP y HTTPS no:

1. En hello portal de Azure clásico, seleccione Hola máquina virtual y haga clic en conectar. Según la configuración del explorador, es posible que toosave solicitada un archivo .rdp para la conexión toohello máquina virtual.
   
    ![conectar máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Usar el nombre de VM de hello usuario, nombre de usuario y contraseña que configuró cuando creaste Hola máquina virtual. 
   
    Por ejemplo, en Hola después de la imagen, nombre de la máquina virtual de hello es **ssrsnativecloud** y es el nombre de usuario de hello **testuser**.
   
    ![el inicio de sesión incluye la máquina virtual](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. En hello VM, abra **Windows PowerShell ISE** con privilegios administrativos. Hola PowerShell ISE se instala de forma predeterminada en Windows server 2012. Se recomienda que usar hello ISE en lugar de una ventana estándar de Windows PowerShell, por lo que puede pegar el script de Hola en hello ISE, modificar el script de Hola y, a continuación, ejecute el script de Hola.
3. En Windows PowerShell ISE, haga clic en hello **vista** menú y, a continuación, haga clic en **Mostrar panel de scripts**.
4. Hola siguiente secuencia de comandos de copiar y pegar el script de Hola en panel de scripts de Windows PowerShell ISE Hola.
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. Si ha creado Hola VM con un puerto HTTP distinto de 80, modifique el parámetro de hello $HTTPport = 80.
6. script de Hola está configurado actualmente para Reporting Services. Si desea que toorun Hola script para Reporting Services, modificar parte de la versión de Hola del espacio de nombres de toohello de ruta de acceso de hello demasiado "v11", en la instrucción de hello Get-WmiObject.
7. Ejecutar script de Hola.

**Validación**: tooverify que Hola funcionalidad del servidor de informes básica funciona, vea hello [Compruebe la configuración de hello](#verify-the-configuration) sección más adelante en este tema.

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>Servidor de informes de uso script tooconfigure hello y HTTPS
toouse Windows PowerShell tooconfigure Hola servidor de informes, Hola completa pasos. configuración de Hello incluye HTTPS y no HTTP.

1. En hello portal de Azure clásico, seleccione Hola máquina virtual y haga clic en conectar. Según la configuración del explorador, es posible que toosave solicitada un archivo .rdp para la conexión toohello máquina virtual.
   
    ![conectar máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Usar el nombre de VM de hello usuario, nombre de usuario y contraseña que configuró cuando creaste Hola máquina virtual. 
   
    Por ejemplo, en Hola después de la imagen, nombre de la máquina virtual de hello es **ssrsnativecloud** y es el nombre de usuario de hello **testuser**.
   
    ![el inicio de sesión incluye la máquina virtual](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. En hello VM, abra **Windows PowerShell ISE** con privilegios administrativos. Hola PowerShell ISE se instala de forma predeterminada en Windows server 2012. Se recomienda que usar hello ISE en lugar de una ventana estándar de Windows PowerShell, por lo que puede pegar el script de Hola en hello ISE, modificar el script de Hola y, a continuación, ejecute el script de Hola.
3. tooenable ejecutar secuencias de comandos, ejecute hello siguiente comando de Windows PowerShell:
   
        Set-ExecutionPolicy RemoteSigned
   
    A continuación, puede ejecutar Hola después de la directiva de Hola tooverify:
   
        Get-ExecutionPolicy
4. En **Windows PowerShell ISE**, haga clic en hello **vista** menú y, a continuación, haga clic en **Mostrar panel de scripts**.
5. Copie Hola siguiente script y péguelo en el panel de scripts de Windows PowerShell ISE Hola.
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. Modificar hello **$certificatehash** parámetro hello script:
   
   * Se trata de un parámetro **obligatorio** . Si no ha guardado el valor de certificado de Hola de los pasos anteriores de hello, use uno de hello siguiendo el valor de hash del certificado de métodos toocopy Hola de huella digital de certificados de Hola.:
     
       En hello VM, abra Windows PowerShell ISE y ejecute hello siguiente comando:
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       salida de Hello tendrá un aspecto similar a continuación toohello. Si el script de Hola devuelve una línea en blanco, Hola VM no tiene un certificado configurado por ejemplo, vea la sección de hello [toouse Hola certificado autofirmado de máquinas virtuales](#to-use-the-virtual-machines-self-signed-certificate).
     
     OR
   * Hola máquina virtual, ejecute mmc.exe y, a continuación, agregar Hola **certificados** complemento.
   * En hello **entidades emisoras de certificados raíz de confianza** haga doble clic en el nombre del certificado. Si utilizas un certificado autofirmado de Hola de hello VM, el certificado de Hola se denomina nombre de DNS de Hola de hello VM y termina con **cloudapp.net**.
   * Haga clic en hello **detalles** ficha.
   * Haga clic en **Huella digital**. valor de Hola de huella digital de Hola se muestra en el campo de detalles de hello, por ejemplo af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48
   * **Antes de ejecutar script de Hola**, quitar Hola espacios entre los pares de Hola de valores. Por ejemplo, af1160b64b288d890a8212ff6ba9c3664f319048.
7. Modificar hello **$httpsport** parámetro: 
   
   * Si utiliza el puerto 443 para el punto de conexión de hello HTTPS, no deberá tooupdate este parámetro en el script de Hola. En caso contrario, use valor del puerto Hola seleccionado al configurar extremo privado HTTPS de hello en hello VM.
8. Modificar hello **$DNSName** parámetro: 
   
   * script de Hola está configurado para un certificado comodín $DNSName = "+". Si lo no hace ningún tooconfigure desee para un enlace de certificado comodín, comente $DNSName = "+"y habilitar Hola después de la línea, la referencia de $DNSNAme completa de hello, ## $DNSName="$server.cloudapp.net".
     
       Cambie el valor de hello $DNSName si no desea que nombre DNS de la máquina virtual de toouse Hola para Reporting Services. Si usa el parámetro hello, certificado hello también debe usar este nombre y registrar nombre hello globalmente en un servidor DNS.
9. script de Hola está configurado actualmente para Reporting Services. Si desea que toorun Hola script para Reporting Services, modificar parte de la versión de Hola del espacio de nombres de toohello de ruta de acceso de hello demasiado "v11", en la instrucción de hello Get-WmiObject.
10. Ejecutar script de Hola.

**Validación**: tooverify que Hola funcionalidad del servidor de informes básica funciona, vea hello [Compruebe la configuración de hello](#verify-the-connection) sección más adelante en este tema. enlace de certificado de hello tooverify abra un símbolo del sistema con privilegios administrativos y, a continuación, ejecute el siguiente comando de Hola:

    netsh http show sslcert

resultado de Hello incluirá siguiente hello:

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>Hola tooConfigure use el Administrador de configuración del servidor de informes
Si no desea toorun tooconfigure de secuencia de comandos de PowerShell Hola Forms Hola el servidor de informes, siga los pasos de hello en esta sección toouse Hola modo nativo configuration manager tooconfigure Hola servidor de Reporting Services.

1. En hello portal de Azure clásico, seleccione Hola máquina virtual y haga clic en conectar. Usar el nombre de usuario de Hola y la contraseña que configuró al crear Hola máquina virtual.
   
    ![conectar máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. Ejecute Windows update e instale las actualizaciones toohello máquina virtual. Si se requiere un reinicio de hello VM, reiniciar Hola VM y vuelva a conectar toohello VM de hello portal de Azure clásico.
3. En el menú de inicio de hello en hello VM, escriba **Reporting Services** y abra **Reporting Services Configuration Manager**.
4. Deje los valores predeterminados de Hola para **nombre del servidor** y **instancia del servidor de informes**. Haga clic en **Conectar**.
5. En el panel izquierdo de hello, haga clic en **dirección URL del servicio Web**.
6. De forma predeterminada, RS está configurado para el puerto 80 HTTP con la IP "Todas asignadas". tooadd HTTPS:
   
   1. En **certificado SSL**: certificado Hola seleccione desee toouse, por ejemplo [nombre de VM]. cloudapp.net. Si no aparece ningún certificado, vea la sección de hello **paso 2: crear un certificado de servidor** para obtener información sobre cómo tooinstall y confianza Hola certificado en hello máquina virtual.
   2. En **Puerto SSL**: elija 443. Si configuró el extremo privado HTTPS de Hola Hola VM con otro puerto privado, usar ese valor aquí.
   3. Haga clic en **aplicar** y espere Hola operación toocomplete.
7. En el panel izquierdo de hello, haga clic en **base de datos**.
   
   1. Haga clic en **Cambiar base de datos**.
   2. Haga clic en **Crear una nueva base de datos del servidor de informes** y luego en **Siguiente**.
   3. Deje Hola predeterminado **nombre del servidor**: Hola VM puede llamar y dejar predeterminado hello **tipo de autenticación** como **usuario actual** : **laseguridadintegrada**. Haga clic en **Siguiente**.
   4. Deje Hola predeterminado **nombre de base de datos** como **ReportServer** y haga clic en **siguiente**.
   5. Deje Hola predeterminado **tipo de autenticación** como **credenciales del servicio** y haga clic en **siguiente**.
   6. Haga clic en **siguiente** en hello **resumen** página.
   7. Una vez completada la configuración de hello, haga clic en **finalizar**.
8. En el panel izquierdo de hello, haga clic en **Report Manager URL**. Deje Hola predeterminado **directorio Virtual** como **informes** y haga clic en **aplicar**.
9. Haga clic en **Exit** tooclose Hola Reporting Services Configuration Manager.

## <a name="step-4-open-windows-firewall-port"></a>Paso 4: abrir el puerto de Firewall de Windows
> [!NOTE]
> Si ha usado uno Hola scripts tooconfigure Hola servidor de informes, puede omitir esta sección. script de Hola incluye un puerto de firewall de paso tooopen Hola. valor predeterminado de Hello era el puerto 80 para HTTP y el puerto 443 para HTTPS.
> 
> 

tooconnect remotamente tooReport Manager u Hola de informes es necesario Server en la máquina virtual de hello, un extremo TCP en hello máquina virtual. Es hello tooopen necesario mismo número de puerto en firewall de la máquina virtual de Hola. Hola extremo se creó cuando se aprovisionó Hola máquina virtual.

Esta sección proporciona información básica sobre cómo tooopen Hola puerto de firewall. Para más información, consulte [Configurar un firewall para el acceso del Servidor de informes](https://technet.microsoft.com/library/bb934283.aspx)

> [!NOTE]
> Si utiliza el servidor de informes de hello script tooconfigure hello, puede omitir esta sección. script de Hola incluye un puerto de firewall de paso tooopen Hola.
> 
> 

Si configura un puerto privado para HTTPS distinto de 443, modifique Hola siguiente secuencia de comandos de forma adecuada. puerto de tooopen **443** en hello Firewall de Windows, realice el siguiente hello:

1. Abra la ventana de Windows PowerShell con privilegios administrativos.
2. Si usa un puerto distinto de 443 al configurar el punto de conexión de hello HTTPS en hello VM, actualizar el puerto de Hola Hola siguiente comando y, a continuación, ejecute el comando de hello:
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. Una vez completado el comando de hello, **Aceptar** se muestra en el símbolo del sistema Hola.

tooverify que se abre el puerto de hello, abra una ventana de Windows PowerShell y ejecución Hola siguiente comando:

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>Comprobar la configuración de Hola
tooverify que la funcionalidad del servidor de informes básica hello ahora funciona, abra el explorador con privilegios administrativos y, a continuación, examinar toohello siguiente URL del Administrador de informes de ad de servidor de informes:

* En hello VM, busque toohello dirección URL del servidor de informes:
  
        http://localhost/reportserver
* En hello VM, busque toohello dirección URL del Administrador de informes:
  
        http://localhost/Reports
* Desde el equipo local, busque toohello **remoto** Administrador de informes en hello máquina virtual. Actualice el nombre DNS de Hola Hola siguiente ejemplo según corresponda. Cuando se le pida una contraseña, utilice credenciales de administrador de Hola que creó cuando se aprovisionó Hola máquina virtual. nombre de usuario de Hello es Hola [dominio]\[nombre de usuario] formato, donde dominio hello es el nombre de equipo para la máquina virtual de hello, por ejemplo ssrsnativecloud\testuser. Si no usa HTTP**S**, quitar hello **s** en dirección URL de Hola. Vea Hola próxima sección para obtener información sobre cómo crear usuarios adicionales en la máquina virtual.
  
        https://ssrsnativecloud.cloudapp.net/Reports
* Desde el equipo local, busque toohello dirección URL del servidor de informes remoto. Actualice el nombre DNS de Hola Hola siguiente ejemplo según corresponda. Si no usa HTTP, quite Hola s en la dirección URL de Hola.
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>Crear usuarios y asignar roles
Después de configurar y verificar Hola el servidor de informes, una tarea administrativa común es toocreate uno o más usuarios y asignar usuarios tooReporting las funciones de servicios. Para obtener más información, vea Hola siguiente:

* [Crear una cuenta de usuarios local](https://technet.microsoft.com/library/cc770642.aspx)
* [Conceder acceso de usuario tooa el servidor de informes (Administrador de informes)](https://msdn.microsoft.com/library/ms156034.aspx))
* [Crear y administrar asignaciones de roles](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate y publicar informes toohello Máquina Virtual de Azure
Hello tabla siguiente resume algunas de hello opciones toopublish disponibles los informes existentes desde un servidor de informes de toohello de equipo local hospedado en hello Máquina Virtual de Microsoft Azure:

* **Script RS.exe**: utilice RS.exe script toocopy elementos del informe y tooyour de servidor de informes existente Máquina Virtual de Microsoft Azure. Para obtener más información, vea la sección Hola "tooNative de modo nativo: modo de máquina Virtual de Microsoft Azure" en [Sample Reporting Services rs.exe Script tooMigrate contenido entre servidores de informes](https://msdn.microsoft.com/library/dn531017.aspx).
* **Generador de informes**: máquina virtual de hello incluye Hola click-una vez versión del generador de informes de Microsoft SQL Server. Hola de generador de informes de toostart primera vez en la máquina virtual de hello:
  
  1. Inicie el explorador con privilegios administrativos.
  2. Busque el Administrador de tooreport en la máquina virtual de Hola y haga clic en **Report Builder** en cinta de opciones de Hola.
     
     Para más información, consulte [Instalar, desinstalar y asistencia del Generador de informes](https://technet.microsoft.com/library/dd207038.aspx).
* **SQL Server Data Tools: Máquina virtual**: si creaste Hola VM con SQL Server 2012, SQL Server Data Tools se instala en la máquina virtual de Hola y puede ser usado toocreate **proyectos de servidor de informes** e informes acerca de hello virtual máquina. Herramientas de datos de SQL Server puede publicar el servidor de informes de toohello Hola informes en la máquina virtual de Hola.
  
    Si ha creado Hola VM con SQL server 2014, puede instalar a SQL Server Data Tools - BI para visual Studio. Para obtener más información, vea Hola siguiente:
  
  * [Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SQL Server Data Tools y SQL Server Business Intelligence (SSDT-BI)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **SQL Server Data Tools: remoto**: en el equipo local, cree un proyecto de Reporting Services en SQL Server Data Tools que contenga informes de Reporting Services. Configurar URL de servicio web de hello proyecto tooconnect toohello.
  
    ![propiedades del proyecto de ssdt para proyecto SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **Usar script**: usar el contenido del servidor de informes de toocopy de secuencia de comandos. Para obtener más información, consulte [Sample Reporting Services rs.exe Script tooMigrate contenido entre servidores de informes](https://msdn.microsoft.com/library/dn531017.aspx).

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>Minimizar el costo si no usas Hola VM
> [!NOTE]
> toominimize cargos para las máquinas virtuales de Azure cuando no esté en uso, apague Hola VM desde el portal de Azure clásico Hola. Si utiliza opciones de energía de Windows hello dentro de un tooshut VM hacia abajo Hola VM, se sigue cobrando Hola mismo importe para hello máquina virtual. tooreduce se aplicarán cargos, necesita tooshut hacia abajo Hola VM Hola portal de Azure clásico. Si ya no necesita Hola VM, recuerde toodelete Hola VM y Hola cargos de almacenamiento de tooavoid de archivos .vhd asociado. Para obtener más información, vea la sección de preguntas más frecuentes de hello en [detalles de precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="more-information"></a>Más información
### <a name="resources"></a>Recursos
* Para consultar contenido similar relacionados con la implementación de servidor único de tooa de SQL Server Business Intelligence y SharePoint 2013, vea [tooCreate de usar Windows PowerShell una máquina virtual de Azure con SQL Server BI y SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).
* Para tooa relacionado de contenido similar consulte implementación de varios servidores de SQL Server Business Intelligence y SharePoint 2013, [implementar SQL Server Business Intelligence en máquinas virtuales Azure](https://msdn.microsoft.com/library/dn321998.aspx).
* Para obtener información General relacionadas toodeployments de SQL Server Business Intelligence en máquinas de virtuales de Azure, consulte [SQL Server Business Intelligence en máquinas virtuales Azure](virtual-machines-windows-classic-ps-sql-bi.md).
* Para obtener más información sobre el costo de hello del proceso de Azure, consulte la ficha de máquinas virtuales de Hola de [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).

### <a name="community-content"></a>Contenido de la Comunidad
* Para obtener instrucciones paso a paso sobre cómo toocreate un modo nativo de Reporting Services servidor de informes sin utilizar script, consulte [hospedar SQL Reporting Service en la máquina Virtual Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>Recursos de tooother de vínculos para SQL Server en máquinas virtuales de Azure
[Información general sobre SQL Server en máquinas virtuales de Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

