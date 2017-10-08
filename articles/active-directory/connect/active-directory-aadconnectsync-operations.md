---
title: "Sincronización de Azure AD Connect: tareas y consideraciones operativas | Microsoft Docs"
description: "En este tema se describe las tareas operativas para la sincronización de Azure AD Connect y cómo tooprepare para el funcionamiento de este componente."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Sincronización de Azure AD Connect: tareas y consideraciones operativas
objetivo de Hola de este tema es toodescribe tareas operativas para la sincronización de Azure AD Connect.

## <a name="staging-mode"></a>Modo provisional
Se puede usar el modo provisional para distintos escenarios como:

* Alta disponibilidad.
* Prueba e implementación de nuevos cambios de configuración.
* Introducir a un nuevo servidor y retirar Hola anterior.

Con un servidor en modo de almacenamiento provisional, puede realizar cambios toohello vista previa y configuración Hola cambios antes de realizar active server Hola. También permite importación completa toorun y tooverify de sincronización completa que se esperan que todos los cambios antes de realizar estos cambios en el entorno de producción.

Durante la instalación, puede seleccionar Hola server toobe en **modo de almacenamiento provisional**. Esta acción hace que el servidor hello activo para importación y sincronización, pero no ejecuta las exportaciones. Un servidor en modo provisional no ejecutará la sincronización de contraseñas ni habilitará la escritura diferida de contraseñas, aunque se seleccionen estas características durante la instalación. Cuando se deshabilita el modo de almacenamiento provisional, servidor hello inicia la exportación, habilita la sincronización de contraseña y permite la escritura diferida de contraseñas.

Todavía puede forzar una exportación mediante el Administrador de servicio de sincronización de Hola.

Un servidor en modo de almacenamiento provisional continuará tooreceive cambios de Active Directory y Azure AD. Siempre tiene una copia de los cambios más recientes de Hola y que pueden tomar muy rápido a través de las responsabilidades de Hola de otro servidor. Si realiza el servidor principal de tooyour de cambios de configuración, es su responsabilidad toomake Hola el mismo servidor de toohello de cambios en el modo de almacenamiento provisional.

Para los usuarios que tienen conocimientos de tecnologías de sincronización anteriores, Hola modo de almacenamiento provisional es diferente puesto que servidor hello tiene su propia base de datos SQL. Esta arquitectura permite Hola modo servidor toobe ubicado en otro centro de datos de almacenamiento provisional.

### <a name="verify-hello-configuration-of-a-server"></a>Comprobar la configuración de Hola de un servidor
tooapply este método, siga estos pasos:

1. [Preparación](#prepare)
2. [Configuración](#configuration)
3. [Importación y sincronización](#import-and-synchronize)
4. [Verify](#verify)
5. [Cambio de servidor activo](#switch-active-server)

#### <a name="prepare"></a>Preparación
1. Instalar Azure AD Connect, seleccione **modo de almacenamiento provisional**y anule la selección de **iniciar la sincronización de** en la última página del Asistente para instalación Hola de Hola. Este modo le permite motor de sincronización de hello toorun manualmente.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. Inicio de sesión desactivado/inicio de sesión y de hello iniciar menú, seleccione **servicio de sincronización**.

#### <a name="configuration"></a>Configuración
Si ha realizado cambios personalizados toohello principal configuración del servidor y desea toocompare Hola con hello servidor de ensayo, a continuación, utilice [Documentador de configuración de Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

#### <a name="import-and-synchronize"></a>Importación y sincronización
1. Seleccione **conectores**, y seleccione Hola primer conector con el tipo de hello **los servicios de dominio de Active Directory**. Haga clic en **Ejecutar** y seleccione **Importación completa** y **Aceptar**. Realice estos pasos para todos los conectores de este tipo.
2. Seleccione Hola conector con el tipo de **Azure Active Directory (Microsoft)**. Haga clic en **Ejecutar** y seleccione **Importación completa** y **Aceptar**.
3. Asegúrese de que todavía se selecciona la ficha de hello conectores. Para cada conector de tipo **Active Directory Domain Services**, haga clic en **Ejecutar**, y seleccione **Sincronización diferencial** y **Aceptar**.
4. Seleccione Hola conector con el tipo de **Azure Active Directory (Microsoft)**. Haga clic en **Ejecutar**, seleccione **Sincronización diferencial** y, después, **Aceptar**.

Tiene ahora la exportación preconfigurada cambia tooAzure AD y AD local (si está utilizando la implementación híbrida de Exchange). pasos siguientes Hola permiten tooinspect novedades sobre toochange antes de empezar realmente directorios de toohello de exportación de Hola.

#### <a name="verify"></a>Verify
1. Inicie un símbolo del sistema y vaya demasiado`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. Para ejecutar: `csexport "Name of Connector" %temp%\export.xml /f:x` nombre Hola de hello conector puede encontrarse en el servicio de sincronización. Tiene un too"contoso.com similar nombre – AAD" para Azure AD.
3. Copie el script de PowerShell de Hola de sección de hello [CSAnalyzer](#appendix-csanalyzer) archivo tooa denominado `csanalyzer.ps1`.
4. Abra una ventana de PowerShell y busque la carpeta toohello donde se creó la secuencia de comandos de PowerShell de Hola.
5. Ejecute `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.
6. Ahora tiene un archivo denominado "**processedusers1.csv**" que se puede examinar en Microsoft Excel. Todos los cambios almacenados provisionalmente toobe exportar tooAzure AD se encuentran en este archivo.
7. Realice los cambios necesarios toohello datos o la configuración y ejecute estos pasos nuevo (importación y sincronización y comprobar) hasta Hola se esperan que los cambios que tienen aproximadamente toobe exportado.

#### <a name="switch-active-server"></a>Cambio de servidor activo
1. En servidor actualmente activo de hello, desactive la opción servidor hello (DirSync/FIM/Azure AD Sync) por lo que no está exportando tooAzure AD o establecerla en el modo (Azure AD Connect) de almacenamiento provisional.
2. Ejecutar el Asistente para la instalación de hello en servidor de hello en **modo de almacenamiento provisional** y deshabilitar **modo de almacenamiento provisional**.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>Recuperación ante desastres
Parte del diseño de la implementación de hello es tooplan para qué toodo en caso de que hay un desastre que pierde el servidor de sincronización de Hola. Existen distintos modelos toouse y qué uno toouse depende de varios factores como:

* ¿Qué es la tolerancia para que no se puede hacer cambios tooobjects en Azure AD durante el tiempo de inactividad de hello?
* ¿Si utiliza la sincronización de contraseña, los usuarios de hello acepta que tienen contraseña antigua de toouse hello en Azure AD en caso de cambian local?
* ¿Tiene una dependencia en operaciones en tiempo real, como la escritura diferida de contraseñas?

Función hello respuestas toothese preguntas y directiva de su organización, se puede implementar uno Hola siguientes estrategias:

* Recompilación si es necesario.
* Servidor en espera de reserva, conocido como **modo provisional**.
* Uso de máquinas virtuales.

Si no utiliza la base de datos SQL Express integrado hello, también debe revisar hello [alta disponibilidad de SQL](#sql-high-availability) sección.

### <a name="rebuild-when-needed"></a>Recompilación si es necesario
Una estrategia viable es tooplan para una regeneración del servidor cuando sea necesario. Por lo general, instalar motor de sincronización de Hola y Hola importación inicial y sincronización puede realizarse dentro de unas pocas horas. Si no hay un servidor de repuesto disponibles, es posible tootemporarily utilice un motor de sincronización de dominio controlador toohost Hola.

servidor de motor de sincronización de Hello no almacenan cualquier estado acerca de los objetos de hello, por lo que se puede volver a generar base de datos de Hola de datos de hello en Active Directory y Azure AD. Hola **sourceAnchor** atributo es toojoin usado Hola objetos desde el entorno local y hello en la nube. Si se vuelve a generar Hola servidor con objetos locales existentes y hello en la nube, a continuación, el motor de sincronización de hello coincide con esos objetos conjuntamente nuevo de reinstalación. las cosas de Hello necesite toodocument y guarde son cambios de configuración de hello realizados toohello server, como las reglas de filtrado y la sincronización. Estas configuraciones personalizadas deben volver a aplicarse antes de iniciar la sincronización.

### <a name="have-a-spare-standby-server---staging-mode"></a>Servidor en espera de reserva - modo provisional
Si tiene un entorno más complejo, se recomienda tener uno o más servidores en espera. Durante la instalación, puede habilitar un toobe server en **modo de almacenamiento provisional**.

Para obtener más información, consulte [Modo provisional](#staging-mode).

### <a name="use-virtual-machines"></a>Uso de máquinas virtuales
Un método común y se admite es el motor de sincronización de hello toorun en una máquina virtual. En caso de que el host de hello tiene un problema, imagen de hello con servidor de motor de sincronización de hello puede ser servidor tooanother migrados.

### <a name="sql-high-availability"></a>alta disponibilidad de SQL
Si no utilizas Hola SQL Server Express que viene con Azure AD Connect, alta disponibilidad para SQL Server también debe considerarse. soluciones de alta disponibilidad de Hello admitidas incluyen la agrupación en clústeres de SQL y AOA (grupos de disponibilidad AlwaysOn). Entre las soluciones no admitidas se incluye la creación de reflejo.

Se agregó compatibilidad con SQL AOA tooAzure AD Connect en la versión 1.1.524.0. Debe habilitar AOA de SQL antes de instalar Azure AD Connect. Durante la instalación, Azure AD Connect detecta si la instancia SQL Hola proporcionada está habilitada para SQL AOA o no. Si está habilitado SQL AOA, Azure AD Connect más averigua si SQL AOA es toouse configurada la replicación sincrónica o replicación asincrónica. Al configurar el agente de escucha del grupo de disponibilidad de hello, se recomienda que establezca hello RegisterAllProvidersIP propiedad too0. Esto es porque Azure AD Connect utiliza actualmente SQL Native Client tooconnect tooSQL y SQL Native Client no admite el uso de Hola de propiedad MultiSubNetFailover.

## <a name="appendix-csanalyzer"></a>Apéndice: CSAnalyzer
Consulte la sección de hello [comprobar](#verify) acerca de cómo toouse esta secuencia de comandos.

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>Pasos siguientes
**Temas de introducción**  

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)  
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)  
