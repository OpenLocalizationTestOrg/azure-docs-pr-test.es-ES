---
title: "aplicación de ejemplo aaaAzure para su uso con DMZ | Documentos de Microsoft"
description: "Implemente esta aplicación web simple después de crear una red Perimetral tootest escenarios de flujo de tráfico"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: e0d9cf14590f75b50c64b677efce2c5425b83ec6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-application-for-use-with-dmzs"></a>Aplicación de ejemplo para su uso con DMZ
[Devolver toohello página de prácticas recomendadas de seguridad límite][HOME]

Estas secuencias de comandos de PowerShell se pueden ejecutar localmente en hello IIS01 y AppVM01 tooinstall de servidores y configurar una aplicación web simple que muestra una página html del servidor front-end de IIS01 de hello con contenido de servidor AppVM01 de hello back-end.

Esta aplicación proporciona un entorno de prueba sencillo para muchos de los ejemplos de la red Perimetral de Hola y cómo Hola a cambios en los puntos de conexión, los NSG, UDR y las reglas de Firewall pueden afectar a los flujos de tráfico.

## <a name="firewall-rule-tooallow-icmp"></a>Regla de Firewall tooallow ICMP
Esta instrucción simple de PowerShell se puede ejecutar en cualquier tráfico ICMP (Ping) de tooallow de máquina virtual de Windows. Esta actualización de firewall permite más fácil de probar y solucionar problemas proporcionando Hola ping protocolo toopass a través de firewall de windows hello (para la mayoría distribuciones de Linux que ICMP está activada de forma predeterminada).

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

Si usas Hola siguientes secuencias de comandos, esta adición de reglas de firewall es Hola primera instrucción.

## <a name="iis01---web-application-installation-script"></a>IIS01: script de instalación de aplicación web
Este script le permitirá hacer lo siguiente:

1. Abra IMCPv4 (Ping) en firewall de windows de servidor local de Hola para probar más fácil
2. Instalar IIS y Hola .net Framework v4.5
3. Crear una página web ASP.NET y un archivo Web.config
4. Cambiar Hola predeterminada grupo toomake archivo acceso a la aplicación sea más fácil
5. Establecer la cuenta de administrador de tooyour de usuario anónimo de Hola y la contraseña

Este script de PowerShell debe ejecutarse localmente mientras el RDP tiene lugar en IIS01.

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter hello admin account information used toocreate this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "hello Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "hello Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from hello inside (a web server on a private network),<br />
          and it is making its way toohello outside! (If you are viewing this from hello internet)<br />
          <br />
          hello following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that hello web server is reaching AppVM01 on hello backend subnet and successfully returning content</li>
            <li> Image from hello Internet - Doesnt really show anything, but it made me happy toosee this when hello app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from hello Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool tooClasic Pipeline tooremote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure hello IIS settings take
    Write-Host "Restarting hello W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a>AppVM01: script instalación de servidor de archivos
Este script configura Hola back-end de esta aplicación simple. Este script le permitirá hacer lo siguiente:

1. Abra IMCPv4 (Ping) en firewall de Hola para probar más fácil
2. Cree un directorio para el sitio web de Hola
3. Crear un toobe de archivo de texto de forma remota tener acceso a la página web de Hola
4. Establecer permisos en tooAnonymous de archivos y directorios de hello tooallow acceso
5. Desactive la opción tooallow de seguridad mejorada de Internet Explorer sea más fácil examinar desde este servidor 

> [!IMPORTANT]
> **Procedimiento recomendado**: nunca desactivar la seguridad mejorada de Internet Explorer en un servidor de producción, además de suele ser un sitio web de Hola de mala idea toosurf desde un servidor de producción. Asimismo, la apertura de recursos compartidos de archivos para el acceso anónimo no es la mejor opción, pero aquí se realiza para simplificar el proceso.
> 
> 

Este script de PowerShell debe ejecutarse localmente mientras RDP tiene lugar en AppVM01. PowerShell es necesario toobe de identificación de la ejecución correcta de administrador tooensure.

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands toowork

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm hello contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a>DNS01: script de instalación del servidor DNS
No hay ningún script incluido en este tooset de aplicación de ejemplo de servidor de DNS de Hola. Si las pruebas de las reglas de firewall de hello, NSG o UDR necesita tooinclude el tráfico DNS, servidor hello DNS01 toobe es necesario configurar manualmente. archivo xml de configuración de red de Hola y plantilla de administrador de recursos de ambos ejemplos incluye DNS01 como servidor DNS principal de Hola y servidor DNS público Hola hospedado por nivel 3 como servidor DNS de la copia de seguridad Hola. servidor de DNS de nivel 3 de Hello podría ser servidor DNS real Hola que se usa para el tráfico no locales y con DNS01 no configura, no hay ninguna red local DNS se produciría.

## <a name="next-steps"></a>Pasos siguientes
* Ejecutar script de Hola IIS01 en un servidor IIS
* Ejecutar el script de servidor de archivos en AppVM01
* Examinar toohello IP pública en IIS01 toovalidate la compilación

<!--Link References-->
[HOME]: ../best-practices-network-security.md
