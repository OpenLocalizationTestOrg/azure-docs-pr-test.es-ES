---
title: "aaaAzure los usuarios notificar a los centros de notificación con back-end de .NET"
description: "Obtenga información acerca de cómo toosend segura las notificaciones de inserción en Azure. Ejemplos de código escritos en C# mediante Hola .NET API."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>Los Centros de notificaciones de Azure notifican a los usuarios con back-end de .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Información general
Compatibilidad de la notificación de inserción en Azure permite tooaccess una fácil de usar, multiplataforma y la infraestructura de inserción de escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa para dispositivos móviles plataformas. Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push usuario de aplicación específica de tooa de notificaciones en un dispositivo específico. Un back-end de ASP.NET WebAPI es tooauthenticate usa clientes. Hola autenticadas usuario del cliente y etiqueta se agregará automáticamente al registro de hello back-end toonotification. Esta etiqueta será toosend usado por las notificaciones de toogenerate de hello back-end para un usuario específico. Para obtener más información sobre cómo registrar para notificaciones mediante un aplicación de back-end, vea el tema de la Guía de hello [registrar desde su aplicación de back-end](http://msdn.microsoft.com/library/dn743807.aspx). Este tutorial se basa en el centro de notificaciones de Hola y el proyecto que creó en hello [empezar a trabajar con los centros de notificaciones] tutorial.

Este tutorial también es toohello de requisitos previos de hello [seguros Push] tutorial. Después de haber completado los pasos de hello en este tutorial, puede continuar toohello [seguros Push] tutorial, que muestra cómo toomodify Hola código en este tutorial toosend una notificación de inserción de forma segura.

## <a name="before-you-begin"></a>Antes de empezar
Nos tomamos muy en serio sus comentarios. Si tiene dificultades completar este tema o recomendaciones para mejorar el contenido, le agradeceríamos sus comentarios en la parte inferior de Hola de página de Hola.

código de Hello completado para este tutorial se puede encontrar en GitHub [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). 

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe haber realizado los siguientes tutoriales de Servicios móviles:

* [empezar a trabajar con los centros de notificaciones]<br/>Crear el centro de notificaciones y reservar el nombre de la aplicación hello y registrar las notificaciones de tooreceive en este tutorial. En este tutorial se asume que ya ha completado estos pasos. Si no es así, siga los pasos de hello en [Introducción a centros de notificaciones (tienda Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); en concreto, Hola secciones [registrar la aplicación para la tienda Windows hello](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) y [configurar el centro de notificaciones](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). En concreto, asegúrese de que ha escrito hello **SID del paquete** y **secreto de cliente** valores en el portal de hello, Hola **configurar** pestaña para el centro de notificaciones. Este procedimiento de configuración se describe en la sección de hello [configurar el centro de notificaciones](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Se trata de un paso importante: si las credenciales de hello en el portal de hello no coinciden con los especificados para el nombre de la aplicación hello que elija, la notificación de inserción de hello no se realizará correctamente.

> [!NOTE]
> Si usas aplicaciones móviles en el servicio de aplicación de Azure como el servicio back-end, vea hello [versión de aplicaciones móviles](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) de este tutorial.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Actualizar código de hello para el proyecto de cliente de Hola
En esta sección, actualizar código de hello en proyecto de hello ha completado de hello [empezar a trabajar con los centros de notificaciones] tutorial. Hola ya debe ser asociado con el almacén de Hola y configurado para el centro de notificaciones. En esta sección, agregará código toocall hello WebAPI back-end y usarlo para registrar y enviar notificaciones.

1. En Visual Studio, abra la solución de Hola de Hola que creó para hello [empezar a trabajar con los centros de notificaciones] tutorial.
2. En el Explorador de soluciones, haga clic en hello **(Windows 8.1)** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.
3. En el lado izquierdo de hello, haga clic en **Online**.
4. Hola **búsqueda** , escriba **cliente Http**.
5. En la lista de resultados de hello, haga clic en **Microsoft HTTP Client Libraries**y, a continuación, haga clic en **instalar**. Completar la instalación de Hola.
6. Nuevo en hello NuGet **búsqueda** , escriba **Json.net**. Instalar hello **Json.NET** paquete y ventana de hello, a continuación, cierre el Administrador de paquetes de NuGet.
7. Repita los pasos de hello anteriormente para hello **(Windows Phone 8.1)** Hola de proyecto tooinstall **JSON.NET** paquete NuGet para el proyecto de Windows Phone Hola.
8. En el Explorador de soluciones, en hello **(Windows 8.1)** proyecto de equipo y haga doble clic en **MainPage.xaml** tooopen en el editor de Visual Studio Hola.
9. Hola **MainPage.xaml** código XML, reemplace hello `<Grid>` sección con el siguiente código de hello. Este código agrega un cuadro de texto Nombre de usuario y contraseña que Hola usuario se autenticará con. También agrega cuadros de texto de mensaje de notificación de Hola y la etiqueta de nombre de usuario de Hola que debe recibir una notificación de hello:
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. En el Explorador de soluciones, en hello **(Windows Phone 8.1)** proyecto abierto **MainPage.xaml** y reemplazar Hola Windows Phone 8.1 `<Grid>` sección con el mismo código anterior. interfaz de Hello debería ser similar toowhats que se muestra a continuación.
    
    ![][13]
11. En el Explorador de soluciones, abra hello **MainPage.xaml.cs** archivo para hello **(Windows 8.1)** y **(Windows Phone 8.1)** proyectos. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de ambos archivos:
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. En **MainPage.xaml.cs** para hello **(Windows 8.1)** y **(Windows Phone 8.1)** proyectos, agregar Hola siguiente miembro toohello `MainPage` clase. Ser seguro tooreplace `<Enter Your Backend Endpoint>` con hello obtenida anteriormente el punto de conexión real de back-end. Por ejemplo: `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Agregar código de hello debajo de la clase MainPage de toohello en **MainPage.xaml.cs** para hello **(Windows 8.1)** y **(Windows Phone 8.1)** proyectos.
    
    Hola `PushClick` método es hello haga clic en controlador de hello **enviar Push** botón. Llama a tootrigger de back-end de hello un tooall notificación dispositivos con una etiqueta de nombre de usuario que coincide con hello `to_tag` parámetro. mensaje de bienvenida de notificación se envía como contenido JSON en el cuerpo de la solicitud de saludo.
    
    Hola `LoginAndRegisterClick` método es hello haga clic en controlador de hello **iniciar sesión y registrar** botón. Almacena basic hello, a continuación, utiliza el token de autenticación en el almacenamiento local (tenga en cuenta que esto representa cualquier token que se utiliza el esquema de autenticación), `RegisterClient` tooregister para notificaciones mediante Hola back-end.

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. En el Explorador de soluciones, bajo hello **Shared** proyecto, abra hello **App.xaml.cs** archivo. Buscar llamada Hola demasiado`InitNotificationsAsync()` en hello `OnLaunched()` controlador de eventos. Convierta en comentario o eliminar llamada Hola demasiado`InitNotificationsAsync()`. controlador de botón de Hello agregada anteriormente inicializará en registros de notificación.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. En el Explorador de soluciones, haga clic en hello **Shared** proyecto, a continuación, haga clic en **agregar**y, a continuación, haga clic en **clase**. Nombre de la clase hello **RegisterClient.cs**, a continuación, haga clic en **Aceptar** clase de hello toogenerate.
   
   Esta clase ajustará Hola REST llamadas toocontact necesario Hola aplicación back-end, en orden tooregister las notificaciones de inserción. También localmente almacena hello *registrationIds* creado por hello centro de notificaciones como se detalla en [registrar desde su aplicación de back-end](http://msdn.microsoft.com/library/dn743807.aspx). Tenga en cuenta que usa un token de autorización almacenado en almacenamiento local al hacer clic en hello **iniciar sesión y registrar** botón.
2. Agregue los siguiente hello `using` instrucciones al principio de hello del archivo de RegisterClient.cs de hello:
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Agregar Hola siguiente código dentro de hello `RegisterClient` definición de clase.
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. Guarde todos los cambios.

## <a name="testing-hello-application"></a>Probar la aplicación hello
1. Inicie la aplicación hello en Windows 8.1 y Windows Phone 8.1. Para Windows Phone 8.1 puede ejecutar la instancia de hello en el emulador de Hola o un dispositivo real.
2. En la instancia de hello Windows 8.1 de la aplicación hello, escriba un **nombre de usuario** y **contraseña** tal y como se muestra en la siguiente pantalla de bienvenida. Debe diferir del nombre de usuario de Hola y la contraseña que se especifican en Windows Phone.
3. Haga clic en **Iniciar sesión y registrarse** y compruebe que el cuadro de diálogo se muestre que ha iniciado sesión. Esto también le permitirá hello **enviar Push** botón.
   
    ![][14]
4. En la instancia de hello Windows Phone 8.1, escriba una cadena de nombre de usuario con ambos hello **nombre de usuario** y **contraseña** campos, a continuación, haga clic en **inicio de sesión y registrar**.
5. A continuación, en hello **etiqueta de nombre de usuario de destinatario** , escriba el nombre de usuario de hello registrado en Windows 8.1. Escriba un mensaje de notificación y haga clic en **Enviar inserción**.
   
    ![][16]
6. Solo los dispositivos de Hola que han registrado con una etiqueta de nombre de usuario coincidente Hola reciban mensaje de notificación de Hola.
   
    ![][15]

## <a name="next-steps"></a>Pasos siguientes
* Si desea toosegment los usuarios por grupos de interés, vea [toosend de centros de notificaciones utilice noticias de última hora].
* toolearn más información acerca de cómo toouse centros de notificaciones, consulte [instrucciones de los centros de notificación].

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[empezar a trabajar con los centros de notificaciones]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[seguros Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[instrucciones de los centros de notificación]: http://msdn.microsoft.com/library/jj927170.aspx
