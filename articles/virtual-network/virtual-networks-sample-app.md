---
title: "Aplicación de ejemplo de Azure para su uso con DMZ | Microsoft Docs"
description: "Implemente esta sencilla aplicación web después de crear una red perimetral para probar los escenarios de flujo de tráfico."
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
ms.openlocfilehash: 8506238e41c5d9dac8d76d729d4919b30a0528b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sample-application-for-use-with-dmzs"></a><span data-ttu-id="40623-103">Aplicación de ejemplo para su uso con DMZ</span><span class="sxs-lookup"><span data-stu-id="40623-103">Sample application for use with DMZs</span></span>
<span data-ttu-id="40623-104">[Volver a la página de procedimientos recomendados de límites de seguridad][HOME]</span><span class="sxs-lookup"><span data-stu-id="40623-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="40623-105">Estos scripts de PowerShell se pueden ejecutar localmente en los servidores IIS01 y AppVM01 para instalar y configurar una aplicación web sencilla que muestra una página html del servidor front-end IIS01 con el contenido del servidor back-end AppVM01.</span><span class="sxs-lookup"><span data-stu-id="40623-105">These PowerShell scripts can be run locally on the IIS01 and AppVM01 servers to install and set up a simple web application that displays an html page from the front-end IIS01 server with content from the back-end AppVM01 server.</span></span>

<span data-ttu-id="40623-106">Esta aplicación proporciona un entorno de prueba sencillo para muchos de los ejemplos de la red perimetral y muestra el modo en que los cambios en las reglas de puntos de conexión, grupos de seguridad de red, UDR y firewall pueden afectar a los flujos de tráfico.</span><span class="sxs-lookup"><span data-stu-id="40623-106">This application provides a simple testing environment for many of the DMZ Examples and how changes on the Endpoints, NSGs, UDR, and Firewall rules can affect traffic flows.</span></span>

## <a name="firewall-rule-to-allow-icmp"></a><span data-ttu-id="40623-107">Regla de firewall para habilitar ICMP</span><span class="sxs-lookup"><span data-stu-id="40623-107">Firewall rule to allow ICMP</span></span>
<span data-ttu-id="40623-108">Esta instrucción simple de PowerShell se puede ejecutar en cualquier máquina virtual de Windows para permitir el tráfico ICMP (Ping).</span><span class="sxs-lookup"><span data-stu-id="40623-108">This simple PowerShell statement can be run on any Windows VM to allow ICMP (Ping) traffic.</span></span> <span data-ttu-id="40623-109">Esta actualización de firewall hace posible un proceso de prueba y solución de problemas más sencillo al permitir al protocolo ping que pase a través del Firewall de windows (en la mayoría de las distribuciones de Linux, la característica ICMP está activada de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="40623-109">This firewall update allows for easier testing and troubleshooting by allowing the ping protocol to pass through the windows firewall (for most Linux distros ICMP is on by default).</span></span>

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

<span data-ttu-id="40623-110">Si usa los siguientes scripts, esta adición de regla de firewall es la primera instrucción.</span><span class="sxs-lookup"><span data-stu-id="40623-110">If you use the following scripts, this firewall rule addition is the first statement.</span></span>

## <a name="iis01---web-application-installation-script"></a><span data-ttu-id="40623-111">IIS01: script de instalación de aplicación web</span><span class="sxs-lookup"><span data-stu-id="40623-111">IIS01 - Web application installation script</span></span>
<span data-ttu-id="40623-112">Este script le permitirá hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="40623-112">This script will:</span></span>

1. <span data-ttu-id="40623-113">Abrir IMCPv4 (Ping) en el Firewall de Windows del servidor local para facilitar el proceso de pruebas.</span><span class="sxs-lookup"><span data-stu-id="40623-113">Open IMCPv4 (Ping) on the local server windows firewall for easier testing</span></span>
2. <span data-ttu-id="40623-114">Instalar IIS y .Net Framework v4.5</span><span class="sxs-lookup"><span data-stu-id="40623-114">Install IIS and the .Net Framework v4.5</span></span>
3. <span data-ttu-id="40623-115">Crear una página web ASP.NET y un archivo Web.config</span><span class="sxs-lookup"><span data-stu-id="40623-115">Create an ASP.NET web page and a Web.config file</span></span>
4. <span data-ttu-id="40623-116">Cambiar el grupo de aplicaciones predeterminado para facilitar el acceso a archivos</span><span class="sxs-lookup"><span data-stu-id="40623-116">Change the Default application pool to make file access easier</span></span>
5. <span data-ttu-id="40623-117">Establecer el usuario anónimo para la cuenta de administrador y la contraseña</span><span class="sxs-lookup"><span data-stu-id="40623-117">Set the Anonymous user to your admin account and password</span></span>

<span data-ttu-id="40623-118">Este script de PowerShell debe ejecutarse localmente mientras el RDP tiene lugar en IIS01.</span><span class="sxs-lookup"><span data-stu-id="40623-118">This PowerShell script should be run locally while RDP’d into IIS01.</span></span>

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter the admin account information used to create this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "The Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "The Admin Password"

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
          This is a page from the inside (a web server on a private network),<br />
          and it is making its way to the outside! (If you are viewing this from the internet)<br />
          <br />
          The following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that the web server is reaching AppVM01 on the backend subnet and successfully returning content</li>
            <li> Image from the Internet - Doesnt really show anything, but it made me happy to see this when the app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from the Internet</b>:<br />
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

# Set App Pool to Clasic Pipeline to remote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure the IIS settings take
    Write-Host "Restarting the W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a><span data-ttu-id="40623-119">AppVM01: script instalación de servidor de archivos</span><span class="sxs-lookup"><span data-stu-id="40623-119">AppVM01 - File server installation script</span></span>
<span data-ttu-id="40623-120">Este script configura el back-end para esta aplicación simple.</span><span class="sxs-lookup"><span data-stu-id="40623-120">This script sets up the back-end for this simple application.</span></span> <span data-ttu-id="40623-121">Este script le permitirá hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="40623-121">This script will:</span></span>

1. <span data-ttu-id="40623-122">Abrir IMCPv4 (Ping) en el firewall para facilitar el proceso de pruebas.</span><span class="sxs-lookup"><span data-stu-id="40623-122">Open IMCPv4 (Ping) on the firewall for easier testing</span></span>
2. <span data-ttu-id="40623-123">Crear un directorio para el sitio web</span><span class="sxs-lookup"><span data-stu-id="40623-123">Create a directory for the web site</span></span>
3. <span data-ttu-id="40623-124">Crear un archivo de texto al que se acceda de forma remota por la página web</span><span class="sxs-lookup"><span data-stu-id="40623-124">Create a text file to be remotely access by the web page</span></span>
4. <span data-ttu-id="40623-125">Establecer permisos en los directorios y el archivo en Anónimo para permitir el acceso</span><span class="sxs-lookup"><span data-stu-id="40623-125">Set permissions on the directory and file to Anonymous to allow access</span></span>
5. <span data-ttu-id="40623-126">Desactivar la seguridad mejorada de Internet Explorer para permitir una exploración más fácil desde este servidor</span><span class="sxs-lookup"><span data-stu-id="40623-126">Turn off IE Enhanced Security to allow easier browsing from this server</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="40623-127">**Procedimiento recomendado**: no desactive nunca la seguridad mejorada de Internet Explorer en un servidor de producción; además, no es aconsejable explorar la Web desde un servidor de producción.</span><span class="sxs-lookup"><span data-stu-id="40623-127">**Best Practice**: Never turn off IE Enhanced Security on a production server, plus it's generally a bad idea to surf the web from a production server.</span></span> <span data-ttu-id="40623-128">Asimismo, la apertura de recursos compartidos de archivos para el acceso anónimo no es la mejor opción, pero aquí se realiza para simplificar el proceso.</span><span class="sxs-lookup"><span data-stu-id="40623-128">Also, opening up file shares for anonymous access is a bad idea, but done here for simplicity.</span></span>
> 
> 

<span data-ttu-id="40623-129">Este script de PowerShell debe ejecutarse localmente mientras RDP tiene lugar en AppVM01.</span><span class="sxs-lookup"><span data-stu-id="40623-129">This PowerShell script should be run locally while RDP’d into AppVM01.</span></span> <span data-ttu-id="40623-130">Es necesario que PowerShell se ejecute como administrador para garantizar la correcta ejecución.</span><span class="sxs-lookup"><span data-stu-id="40623-130">PowerShell is required to be run as Administrator to ensure successful execution.</span></span>

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands to work

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm the contents of a remote file on AppVM01."
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

## <a name="dns01---dns-server-installation-script"></a><span data-ttu-id="40623-131">DNS01: script de instalación del servidor DNS</span><span class="sxs-lookup"><span data-stu-id="40623-131">DNS01 - DNS server installation script</span></span>
<span data-ttu-id="40623-132">No hay ningún script incluido en esta aplicación de ejemplo para configurar el servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="40623-132">There is no script included in this sample application to set up the DNS server.</span></span> <span data-ttu-id="40623-133">Si las pruebas de las reglas de firewall, el grupo de seguridad de red o UDR deben incluir el tráfico DNS, el servidor DNS01 debe configurarse manualmente.</span><span class="sxs-lookup"><span data-stu-id="40623-133">If testing of the firewall rules, NSG, or UDR needs to include DNS traffic, the DNS01 server needs to be set up manually.</span></span> <span data-ttu-id="40623-134">El archivo xml de configuración de red y la plantilla de Resource Manager para ambos ejemplos incluye DNS01 como el servidor DNS principal y el servidor DNS público hospedado por el nivel 3 como el servidor DNS de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="40623-134">The Network Configuration xml file and Resource Manager Template for both examples includes DNS01 as the primary DNS server and the public DNS server hosted by Level 3 as the backup DNS server.</span></span> <span data-ttu-id="40623-135">El servidor DNS de nivel 3 podría ser el servidor DNS real utilizado para el tráfico no local, y si DNS01 no está configurado, no se produciría ningún DNS de red local.</span><span class="sxs-lookup"><span data-stu-id="40623-135">The Level 3 DNS server would be the actual DNS server used for non-local traffic, and with DNS01 not setup, no local network DNS would occur.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40623-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="40623-136">Next steps</span></span>
* <span data-ttu-id="40623-137">Ejecutar el script IIS01 en un servidor IIS</span><span class="sxs-lookup"><span data-stu-id="40623-137">Run the IIS01 script on an IIS server</span></span>
* <span data-ttu-id="40623-138">Ejecutar el script de servidor de archivos en AppVM01</span><span class="sxs-lookup"><span data-stu-id="40623-138">Run File Server script on AppVM01</span></span>
* <span data-ttu-id="40623-139">Ir a la dirección IP pública en IIS01 para validar la compilación</span><span class="sxs-lookup"><span data-stu-id="40623-139">Browse to the Public IP on IIS01 to validate your build</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
