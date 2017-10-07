---
title: "aaaSending tooiOS de notificaciones de inserción con centros de notificaciones de Azure | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toosend push aplicación de iOS de tooan de notificaciones."
services: notification-hubs
documentationcenter: ios
keywords: "notificación push,notificaciones push,notificaciones push de ios"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a>Enviar tooiOS de notificaciones de inserción con centros de notificaciones de Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Información general
> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).
> 
> 

Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push aplicación de iOS de tooan de notificaciones. Se creará una aplicación de iOS en blanco que recibe notificaciones de inserción mediante hello [servicio de notificaciones de inserción de Apple (APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html). 

Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación.

## <a name="before-you-begin"></a>Antes de empezar
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

código de Hello completado para este tutorial se puede encontrar [en GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere siguiente de hello:

* [servicios móviles iOS SDK versión 1.2.4]
* La versión más reciente de [Xcode]
* Un dispositivo compatible con iOS 8 (o una versión posterior)
* [programa para desarrolladores de Apple](https://developer.apple.com/programs/)
  
  > [!NOTE]
  > Debido a los requisitos de configuración para las notificaciones de inserción, debe implementar y probar las notificaciones de inserción en un dispositivo físico iOS (iPhone o iPad) en lugar de simulador de iOS de Hola.
  > 
  > 

La realización de este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>Configuración del Centro de notificaciones para notificaciones push de iOS
En esta sección le guía a través de la creación de un nuevo centro de notificaciones y configurar la autenticación con APNS mediante hello **. p12** certificado de inserción que creó. Si desea toouse un centro de notificaciones que ya haya creado, puede omitir toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p>Haga clic en hello <b>Notification Services</b> botón en hello <b>configuración</b> blade, a continuación, seleccione <b>Apple (APN)</b>. Haga clic en <b>cargar certificado</b> y seleccione hello <b>. p12</b> archivo que exportó anteriormente. Asegúrese de que también especificar contraseña correcta Hola.</p>

<p>Asegúrese de que tooselect <b>espacio aislado</b> modo ya que esto es para el desarrollo. Usar solo hello <b>producción</b> si desea toousers de notificaciones de inserción de toosend que han adquirido la aplicación desde el almacén de Hola.</p>
</li>
</ol>
&emsp;&emsp;&emsp;&emsp;![Configurar APN en Portal de Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)

&emsp;&emsp;&emsp;&emsp;![Configuración de certificados APNs en el Portal de Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

El centro de notificaciones está ahora configurado toowork con APNS, y tiene la aplicación de tooregister de cadenas de conexión de Hola y enviar notificaciones de inserción.

## <a name="connect-your-ios-app-toonotification-hubs"></a>Conectar su tooNotification de aplicación de iOS centros
1. En Xcode, cree un nuevo proyecto de iOS y seleccione hello **única aplicación de vista** plantilla.
   
    ![Xcode: aplicación de vista única][8]
    
2. Al configurar las opciones de hello para el proyecto nuevo, asegúrese de que toouse Hola mismo **Product Name** y **identificador de la organización** que ha usado al establecidos previamente Id. del lote de hello en hello para desarrolladores de Apple Portal.
   
    ![Xcode: opciones de proyecto][11]
    
3. En **destinos**, haga clic en el nombre del proyecto, haga clic en hello **configuración de generación** pestaña y expanda **identidad de firma de código**y, a continuación, en **depurar**, establecer la identidad de firma de código. Alternar **niveles** de **básica** demasiado**todos los**y establezca **perfil de aprovisionamiento de** toohello perfil que creó previamente de aprovisionamiento .
   
    Si no ve Hola nuevo perfil que creó en Xcode de aprovisionamiento, pruebe a actualizar los perfiles de hello para la identidad de firma. Haga clic en **Xcode** en la barra de menús de hello, haga clic en **preferencias**, haga clic en hello **cuenta** , haga clic en hello **ver detalles** botón, haga clic en el identidad de firma y, a continuación, haga clic en el botón de actualización de hello en la esquina inferior derecha de Hola.
   
    ![Xcode: perfil de aprovisionamiento][9]
4. Descargar hello [servicios móviles iOS SDK versión 1.2.4] y descomprima el archivo hello. En Xcode, haga clic en el proyecto y haga clic en hello **agregar archivos a** Hola de opción tooadd **WindowsAzureMessaging.framework** proyecto de Xcode tooyour de carpeta. Seleccione **Copy items if needed** (Copiar elementos si es necesario) y luego haga clic en **Add** (Agregar).
   
   > [!NOTE]
   > centros de notificaciones de Hello SDK no admite actualmente bitcode en Xcode 7.  Debe establecer **habilitar Bitcode** demasiado**No** en hello **opciones de compilación** para el proyecto.
   > 
   > 
   
    ![Descompresión del SDK de Azure][10]
5. Agregue un nuevo proyecto de tooyour de archivo de encabezado denominado `HubInfo.h`. Este archivo contendrá constantes de hello para el centro de notificaciones.  Agregar Hola siguiendo las definiciones y reemplace los marcadores de literal de cadena de hello con su *nombre del concentrador* hello y *DefaultListenSharedAccessSignature* que anotó anteriormente.
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. Abra su `AppDelegate.h` archivo agregar Hola siguiendo las directivas de importación:
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. En su `AppDelegate.m file`, agregar Hola después el código de hello `didFinishLaunchingWithOptions` método en función de su versión de iOS. Este código registra el identificador de dispositivo en APNS:
   
    Para iOS 8:
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    Para too8 anteriores versiones de iOS:
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. En Hola el mismo archivo, agregue Hola siguiendo métodos. Este código conecta toohello centro de notificaciones utilizando información de conexión de Hola que especificó en HubInfo.h. A continuación, ofrece centro de notificaciones de token toohello de dispositivo de Hola para que hello centro de notificaciones puede enviar notificaciones:
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. En Hola el mismo archivo, agregue Hola siguiendo el método toodisplay una **UIAlert** si se recibe la notificación de hello mientras está activa la aplicación hello:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. Compile y ejecute la aplicación hello en su tooverify de dispositivo que no hay ningún error.

## <a name="send-test-push-notifications"></a>Prueba de envío de las notificaciones push
Puede probar recibir notificaciones en la aplicación mediante el envío de notificaciones de inserción en hello [Portal de Azure] a través de hello **solución de problemas** sección en la hoja de la base de datos central de hello (usar hello *probar envío* opción).

![Portal de Azure: envío de prueba][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a>(Opcional) Enviar notificaciones de inserción de la aplicación hello
> [!IMPORTANT]
> Este ejemplo de envío de notificaciones de la aplicación de cliente de hello se proporciona con fines de aprendizaje. Puesto que esto requerirá hello `DefaultFullSharedAccessSignature` toobe presente en la aplicación de cliente de hello, expone el riesgo de toohello de concentrador de notificación que un usuario puede obtener acceso no autorizado de toosend notificaciones tooyour clientes.
> 
> 

Si desea que las notificaciones de inserción toosend desde dentro de una aplicación, esta sección proporciona un ejemplo de cómo toodo esta mediante Hola interfaz REST.

1. En Xcode, abra `Main.storyboard` y agregue Hola siguientes componentes de interfaz de usuario de hello objeto biblioteca tooallow Hola usuario toosend notificaciones de inserción en la aplicación hello:
   
   * Una etiqueta sin texto de etiqueta. Será usado tooreport errores en el envío de notificaciones. Hola **líneas** propiedad debe establecerse demasiado**0** para que ajustará automáticamente el tamaño toohello restringida derecha y los márgenes izquierdos y parte superior de Hola de vista de Hola.
   * Un campo de texto con **marcador de posición** texto se establece demasiado**escribir mensaje de notificación**. Restringir campo Hola justo debajo de la etiqueta de hello tal y como se muestra a continuación. Establecer Hola View Controller como delegado de toma de corriente de Hola.
   * Un botón denominado **enviar notificación** limitada justo debajo de campo de texto de Hola y en el centro de hello horizontal.
     
     vista de Hello debe ser similar al siguiente:
     
     ![Diseñador de Xcode][32]
2. [Agregar salidas](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) de campo de etiqueta y el texto hello conectado a la vista y actualizar su `interface` definición toosupport `UITextFieldDelegate` y `NSXMLParserDelegate`. Agregue tres declaraciones de propiedad Hola que se muestra por debajo del soporte de toohelp llamando a Hola API de REST y analizar la respuesta de Hola.
   
    El archivo ViewController.h debe tener el aspecto siguiente:
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. Abra `HubInfo.h` y agregue Hola después de constantes que se usará para el envío de concentrador de tooyour de notificaciones. Reemplace el literal de cadena de marcador de posición de Hola por su real *DefaultFullSharedAccessSignature* cadena de conexión.
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. Agregue los siguiente hello `#import` instrucciones tooyour `ViewController.h` archivo.
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. En `ViewController.m` agregue Hola después de la implementación de interfaz de toohello de código. Este código analizará la cadena de conexión *DefaultFullSharedAccessSignature* . Como se mencionó en hello [referencia de la API de REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), esta información analizada será toogenerate usa un token de SaS para hello **autorización** encabezado de solicitud.
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. En `ViewController.m`, actualización hello `viewDidLoad` cadena de conexión de Hola de método tooparse cuando se carga la vista de Hola. Agregar métodos de utilidad de hello, se muestra a continuación, implementación de la interfaz de toohello.  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. En `ViewController.m`, agregar Hola después código toohello interfaz implementación toogenerate Hola autorización token de SaS que se proporcionará en hello **autorización** encabezado, tal y como se mencionó en hello [API de REST Referencia](http://msdn.microsoft.com/library/azure/dn495627.aspx).
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. CTRL + arrastrar de Hola **enviar notificación** botón demasiado`ViewController.m` tooadd una acción denominada **SendNotificationMessage** para hello **Touch hacia abajo** eventos. Método de actualización con hello siguientes a la notificación de hello toosend de código mediante la API de REST de Hola.
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. En `ViewController.m`, agregar Hola después toosupport de método de delegado Cerrar teclado hello para el campo de texto hello. CTRL + arrastrar de icono View Controller toohello de campo de texto de Hola Hola Hola de diseñador tooset de interfaz ver controlador como delegado de toma de corriente de Hola.
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. En `ViewController.m`, agregar siguiente Hola delegar la respuesta de métodos toosupport análisis hello mediante `NSXMLParser`.
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. Compile el proyecto de Hola y compruebe que no hay ningún error.

> [!NOTE]
> Si se produce un error de compilación en Xcode7 sobre la compatibilidad de bitcode, debe cambiar hello **configuración de generación** > **Bitcode habilitar (ENABLE_BITCODE)** demasiado**n** en Xcode. Hola SDK de los centros de notificación no admite actualmente la bitcode. 
> 
> 

Puede encontrar todas las cargas de notificación posibles Hola Hola Apple [locales y Guía de programación de notificaciones de inserción].

## <a name="checking-if-your-app-can-receive-push-notifications"></a>Comprobación de si la aplicación puede recibir notificaciones push
notificaciones de inserción de tootest en iOS, debe implementar el dispositivo de E/s físicas de hello aplicación tooa. No se puede enviar notificaciones de inserción de Apple mediante el simulador de iOS de Hola.

1. Ejecute la aplicación hello y compruebe que el registro se realiza correctamente y, a continuación, presione **Aceptar**.
   
    ![Prueba de registro de notificación push de aplicación iOS][33]
2. Puede enviar una notificación de inserción de prueba de hello [Portal de Azure], tal y como se ha descrito anteriormente. Si agrega código para enviar notificaciones de inserción en la aplicación hello, toque tooenter de campo de texto hello dentro de un mensaje de notificación. A continuación, presione hello **enviar** botón de teclado de Hola o hello **enviar notificación** botón en el mensaje de notificación de hello vista toosend Hola.
   
    ![Prueba de envío de notificación push de aplicación iOS][34]
3. Hello notificación de inserción se envía tooall dispositivos registrado tooreceive notificaciones Hola Hola determinado centro de notificaciones.
   
    ![Prueba de recepción de notificación push de aplicación iOS][35]

## <a name="next-steps"></a>Pasos siguientes
En este sencillo ejemplo, difunden tooall de notificaciones de inserción los dispositivos iOS registrados. Se recomienda el siguiente paso en el aprendizaje que continúe toohello [Azure notificación centros de informar a los usuarios de iOS con back-end de .NET] tutorial, que le guiará por la creación de una inserción de toosend de back-end mediante etiquetas de notificaciones. 

Si desea toosegment los usuarios por grupos de interés, además puede mover en toohello [toosend de centros de notificaciones utilice noticias de última hora] tutorial. 

Para más información sobre los Centros de notificaciones, consulte [Introducción a los centros de notificaciones].

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[servicios móviles iOS SDK versión 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Introducción a los centros de notificaciones]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure notificación centros de informar a los usuarios de iOS con back-end de .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[locales y Guía de programación de notificaciones de inserción]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Portal de Azure]: https://portal.azure.com
