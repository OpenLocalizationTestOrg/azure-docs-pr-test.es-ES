---
title: "aaaAzure AD v2 Windows Desktop introducción - el programa de instalación | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones .NET de escritorio de Windows (XAML) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configurar su proyecto

En esta sección proporciona instrucciones paso a paso sobre cómo toocreate un nuevo toodemonstrate proyecto cómo toointegrate .NET de escritorio de Windows (XAML) de la aplicación con *inicie sesión con Microsoft* para que pueden consultar las API Web que requiere un token.

aplicación Hello creado por esta guía muestra un botón toograph y mostrar los resultados en pantalla y un botón de cierre de sesión.

> ¿Prefiere toodownload proyecto de Visual Studio de este ejemplo en su lugar? [Descargar un proyecto](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) y omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutar.


### <a name="create-your-application"></a>Creación de la aplicación
1. En Visual Studio: `File` > `New` > `Project`<br/>
2. En *Plantillas*, seleccione `Visual C#`.
3. Seleccione `WPF App` (o *aplicación WPF* según la versión de Hola de su Visual Studio)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Agregar proyecto de hello biblioteca de autenticación de Microsoft (MSAL) tooyour
1. En Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Copiar y pegar siguiente Hola Hola ventana de la consola de administrador de paquetes:

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> paquete de Hello anterior instala Hola biblioteca de autenticación de Microsoft (MSAL). MSAL controla la adquisición, almacenamiento en caché y actualizar usuario toskens utiliza tooaccess API protegidas por Azure Active Directory v2.

## <a name="add-hello-code-tooinitialize-msal"></a>Agregar código de hello tooinitialize MSAL
Este paso le ayudará a crear una interacción de toohandle de clase con la biblioteca de MSAL, como el control de tokens.

1. Abra hello `App.xaml.cs` de archivos y agregar referencia de hello para la clase MSAL biblioteca toohello:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Actualizar Hola aplicación clase toohello a continuación:
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a>Creación de la IU de la aplicación
sección de Hello siguiente muestra cómo una aplicación puede consultar un servidor protegido de back-end como Microsoft Graph. Debe crearse un archivo MainWindow.xaml automáticamente como parte de la plantilla de proyecto. Abra este archivo de este archivo y, a continuación, siga estas instrucciones hello:

Reemplace la aplicación `<Grid>` con ser siguiente hello:

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
