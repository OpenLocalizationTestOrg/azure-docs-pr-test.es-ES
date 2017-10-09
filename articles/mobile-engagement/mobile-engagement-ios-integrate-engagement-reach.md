---
title: "aaaAzure integración con alcanzar el SDK de Mobile Engagement iOS | Documentos de Microsoft"
description: "Actualizaciones y procedimientos más recientes para el SDK de iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a>Cómo tooIntegrate interacción a en iOS
Debe seguir el procedimiento de integración de hello descrito en hello [cómo tooIntegrate interacción en el documento de iOS](mobile-engagement-ios-integrate-engagement.md) antes de seguir esta guía.

Esta documentación requiere XCode 8. Si realmente dependen XCode 7, a continuación, puede usar hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Existe un problema conocido en esta versión anterior cuando se ejecuta en dispositivos iOS 10: las notificaciones del sistema no se ejecutan. toofix esto tendrá tooimplement hello en desuso API `application:didReceiveRemoteNotification:` en la aplicación el delegado como sigue:

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **No se recomienda esta solución** ya que este comportamiento puede cambiar en la próxima actualización de la versión de iOS (por menor que sea) porque esta API de iOS está en desuso. Debería pasar tooXCode 8 tan pronto como sea posible.
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Habilitar la tooreceive aplicación silenciosa de las notificaciones de inserción
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>Pasos de integración
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>Incrustar Hola interacción Reach SDK en el proyecto de iOS
* Agregar sdk de alcance de hello en el proyecto de Xcode. En Xcode, vaya demasiado**proyecto \> agregar tooproject** y elija hello `EngagementReach` carpeta.

### <a name="modify-your-application-delegate"></a>Modifique su delegado de la aplicación
* Hola parte superior de su archivo de implementación, importe el módulo de llegar a la interacción de hello:

      [...]
      #import "AEReachModule.h"
* Método `applicationDidFinishLaunching:` o `application:didFinishLaunchingWithOptions:`, cree un módulo de reach y páselo tooyour línea de inicialización de contratación existente:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* Modificar **'icon.png'** cadena con el nombre de la imagen de Hola que desee utilizar como icono de la notificación.
* Si desea que la opción de hello toouse *valor del distintivo actualización* en las campañas de cobertura o si desea que la inserción nativa toouse \<nativa y formato de SaaS/alcance API/campaña de inserción\> campañas, debe dejar que módulo de Reach Hola administre Hola distintivo propio icono (se borrará automáticamente distintivo de la aplicación de Hola y también restablece el valor de hello almacenado interacción cada vez aplicación hello se inició o foregrounded). Esto se realiza mediante la adición de hello después de línea después de la inicialización del módulo de Reach:

      [reach setAutoBadgeEnabled:YES];
* Si desea que la inserción de datos de cobertura de toohandle, debe permitir que el delegado de la aplicación se ajustan toohello `AEReachDataPushDelegate` protocolo. Agregue Hola después de línea después de la inicialización del módulo de alcance:

      [reach setDataPushDelegate:self];
* A continuación, puede implementar métodos de hello `onDataPushStringReceived:` y `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` en el delegado de aplicación:

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a>Categoría
parámetro de categoría de Hello es opcional cuando se crea una campaña de inserción de datos y permite que los datos de toofilter inserta. Esto es útil si desea que toopush diferentes tipos de `Base64` tooidentify de datos y quiere que su tipo antes del análisis de ellos.

**La aplicación es ahora la presentación y listo tooreceive alcanzar el contenido.**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>¿Cómo tooreceive sondeos en cualquier momento y anuncios
Interacción puede enviar notificaciones de alcance a los usuarios finales de tooyour en cualquier momento mediante Hola servicio de notificaciones Push de Apple.

tooenable esta funcionalidad, deberá tener tooprepare la aplicación para notificaciones de inserción de Apple y modificar el delegado de la aplicación.

### <a name="prepare-your-application-for-apple-push-notifications"></a>Preparar la aplicación para notificaciones de inserción de Apple
Siga la Guía de hello: [cómo tooPrepare la aplicación para notificaciones Push de Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>Agregar código de cliente necesario Hola
*En este momento la aplicación debe tener un certificado de inserción de Apple registrado en el front-end de hello interacción.*

Si ya no es así, deberá tooregister las notificaciones de inserción de tooreceive de aplicación.

* Hola de importación `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>
* Agregar Hola siguientes línea cuando se inicia la aplicación (normalmente, en `application:didFinishLaunchingWithOptions:`):

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

A continuación, deberá token del dispositivo tooprovide tooEngagement Hola devuelta por servidores de Apple. Esto se hace en el método hello denominado `application:didRegisterForRemoteNotificationsWithDeviceToken:` en el delegado de aplicación:

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

Por último, tendrá tooinform Hola Engagement SDK cuando la aplicación recibe una notificación remota. Hola a toodo que llame al método `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` en el delegado de aplicación:

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> De forma predeterminada, interacción alcanzar controla completionHandler Hola. Si desea que toomanually responden toohello `handler` un bloqueo en el código, puede pasar nulo para hello `handler` bloquear el argumento y el control de finalización de hello usted mismo. Vea hello `UIBackgroundFetchResult` tipo para obtener una lista de valores posibles.
>
>

### <a name="full-example"></a>Ejemplo completo
Este es un ejemplo completo de integración:

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Resolución de conflictos de delegado de UNUserNotificationCenter

*Si ni la aplicación ni una de las bibliotecas de terceros implementa `UNUserNotificationCenterDelegate`, puede pasar por alto esta parte.*

Un `UNUserNotificationCenter` delegado es utilizado por el ciclo de vida de hello SDK toomonitor Hola de notificaciones de interacción en dispositivos que ejecutan en iOS 10 o superior. Hola SDK tiene su propia implementación de hello `UNUserNotificationCenterDelegate` de protocolo, pero puede haber solo un `UNUserNotificationCenter` delegar por aplicación. Cualquier otro delegado agrega toohello `UNUserNotificationCenter` objeto entrarán en conflicto con hello interacción uno. Si Hola SDK detecta a delegado su o cualquier otro de terceros no usará su propio toogive de implementación, una posibilidad tooresolve Hola conflictos. Tendrá tooadd Hola interacción lógica tooyour posee conflictos de hello tooresolve de delegado en orden.

Hay dos tooachieve formas esto.

Propuesta 1, enviando el delegado llama toohello SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

O propuesta 2, heredando de hello `AEUserNotificationHandler` (clase)

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> Puede determinar si una notificación pueden proceder de contratación o no pasando su `userInfo` diccionario toohello agente `isEngagementPushPayload:` método de la clase.

Asegúrese de que ese hello `UNUserNotificationCenter` delegado del objeto se establece el delegado tooyour dentro de cualquier hello `application:willFinishLaunchingWithOptions:` o hello `application:didFinishLaunchingWithOptions:` método de delegado de la aplicación.
Por ejemplo, si implementa Hola anteriormente propuesta 1:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a>Cómo las campañas de toocustomize
### <a name="notifications"></a>Notificaciones
Hay dos tipos de notificaciones: las notificaciones del sistema y de aplicaciones.

Las notificaciones del sistema se controlan con iOS y no se pueden personalizar.

Se realizan en la aplicación notificaciones de una vista que se agrega dinámicamente toohello ventana actual de la aplicación. Esto se denomina superposición de notificaciones. Superposiciones de notificación son excelentes para una integración rápida porque no requieren toomodify cualquier vista de la aplicación.

#### <a name="layout"></a>Diseño
visión de hello toomodify de las notificaciones de la aplicación, simplemente puede modificar archivo hello `AENotificationView.xib` tooyour necesita, como conservar los valores de etiqueta de Hola y tipos de subvistas existente Hola.

De forma predeterminada, las notificaciones de la aplicación se muestran en la parte inferior de Hola de pantalla de bienvenida. Si prefiere toodisplay proporcionan estos en la parte superior de Hola de pantalla, editar hello `AENotificationView.xib` y cambiar hello `AutoSizing` propiedad de la vista principal de Hola por lo que se pueden guardar en parte superior de Hola de su supervista.

#### <a name="categories"></a>Categorías
Cuando se modifica Hola proporcionada diseño, modificar aspecto de Hola de todas las notificaciones. Las categorías permiten toodefine que distintos destino busca (posiblemente comportamientos) para las notificaciones. Las categorías pueden especificarse cuando se crea una campaña de cobertura. Tenga en cuenta que las categorías también permiten personalizar anuncios y sondeos, aspectos que se describen más adelante en este documento.

tooregister un controlador de categoría para las notificaciones, debe tooadd una llamada una vez Hola llegan módulo se inicializa.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`debe ser una instancia de un objeto que se ajusta toohello protocolo `AENotifier`.

Puede implementar métodos de protocolo de Hola por usted mismo o puede elegir la clase existente de hello tooreimplement `AEDefaultNotifier` ya que realiza la mayor parte del trabajo de Hola.

Por ejemplo, si desea vista de notificaciones de hello tooredefine para una categoría específica, puede seguir este ejemplo:

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

En este ejemplo simple de categoría, se supone que tiene un archivo denominado `MyNotificationView.xib` en el paquete de aplicación principal. Si el método hello no es capaz de toofind correspondiente `.xib`, no se mostrará la notificación de Hola y contratación dará como resultado un mensaje en la consola de Hola.

archivo nib de Hello proporcionado debe respetar Hola siguiendo las reglas:

* Solo debe contener una vista.
* Deben ser subvistas de hello mismo tipos como Hola aquellos dentro de hello proporciona nib archivo denominado`AENotificationView.xib`
* Subvistas deben tener Hola mismo etiquetas como Hola aquellos dentro de hello proporciona nib archivo denominado`AENotificationView.xib`

> [!TIP]
> Simplemente copie el archivo nib de hello proporcionado, denominado `AENotificationView.xib`y empezar a trabajar desde allí. Pero tenga cuidado, Hola vista toohello clase asociada, dentro de este archivo nib es `AENotificationView`. Esta clase se volvió a definir método hello `layoutSubViews` toomove y cambiar el tamaño de sus subvistas según toocontext. Puede que desee tooreplace con un `UIView` o una clase de vista personalizada.
>
>

Si necesita personalización más profunda de las notificaciones (si se desea para la instancia tooload la vista directamente desde el código de hello), se recomienda tootake un vistazo a Hola proporciona documentación de código y la clase de origen de `Protocol ReferencesDefaultNotifier` y `AENotifier`.

Tenga en cuenta que puede usar Hola notificador mismo para varias categorías.

Puede notificador de hello también redefinido predeterminado similar al siguiente:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>Manejo de notificaciones
Cuando se usa la categoría predeterminada de hello, se llaman a algunos métodos de ciclo de vida en hello `AEReachContent` tooreport estadísticas y actualización Hola campaña el estado del objeto:

* Cuando se muestra la notificación de hello en aplicaciones, Hola `displayNotification` se llama al método (que notifica estadísticas) por `AEReachModule` si `handleNotification:` devuelve `YES`.
* Si se descarta la notificación de hello, Hola `exitNotification` método se llama, se notifica la estadística y ahora se pueden procesar las campañas siguientes.
* Si se hace clic en la notificación de hello, `actionNotification` es llama, se notifican estadísticas y se realiza la acción de hello asociado.

Si la implementación de `AENotifier` omisiones Hola comportamiento predeterminado, tendrá toocall estos métodos de ciclo de vida por usted mismo. Hello en los ejemplos siguientes muestra algunos casos donde se omite el comportamiento predeterminado de hello:

* No se extienden `AEDefaultNotifier`, por ejemplo, se implementa el control de categoría desde cero.
* Reemplazó `prepareNotificationView:forContent:`, ser al menos seguro toomap `onNotificationActioned` o `onNotificationExited` tooone de los controles de I.U.

> [!WARNING]
> Si `handleNotification:` inicia una excepción, Hola contenido se elimina y `drop` es llama, se notifica en las estadísticas y ahora se pueden procesar las campañas siguientes.
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>Incluir notificaciones como parte de una vista existente
Las superposiciones son ideales para una integración rápida, pero a veces pueden no ser convenientes o pueden tener efectos secundarios no deseados.

Si no está satisfecho con el sistema de superposición de hello en algunas de las vistas, puede personalizarlo para estas vistas.

Puede decidir tooinclude nuestro diseño de notificación en las vistas existentes. toodo por lo tanto, hay dos estilos de implementación:

1. Agregar vista de notificaciones de hello mediante el generador de interfaz

   * Abrir el *generador de la interfaz*
   * Coloque un 320 x 60 (o 60 x 768 si se encuentra en iPad) `UIView` donde desea Hola notificación tooappear
   * Establezca el valor de etiqueta de Hola para esta vista demasiado: **36822491**
2. Agregar vista de notificaciones de hello mediante programación. Basta con agregar Hola después de código cuando se ha inicializado la vista:

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

La macro `NOTIFICATION_AREA_VIEW_TAG` puede encontrarse en `AEDefaultNotifier.h`.

> [!NOTE]
> notificador de Hello predeterminado detecta automáticamente ese diseño de notificación de Hola se incluye en esta vista y no agregará una superposición para él.
>
>

### <a name="announcements-and-polls"></a>Anuncios y sondeos
#### <a name="layouts"></a>Diseños
Puede modificar archivos de hello `AEDefaultAnnouncementView.xib` y `AEDefaultPollView.xib` como mantener valores de etiqueta de Hola y tipos de subvistas existente Hola.

#### <a name="categories"></a>Categorías
##### <a name="alternate-layouts"></a>Diseños alternativos
Al igual que las notificaciones, categoría de la campaña de hello puede ser toohave usado diseños alternativos para los sondeos y anuncios.

toocreate una categoría de un anuncio, debe extender **AEAnnouncementViewController** y registrarlo una vez que se ha inicializado el módulo de reach hello:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> Cada vez que un usuario ha hecho clic en una notificación para un anuncio con la categoría de Hola "Mi\_categoría", el controlador de vista registrados (en ese caso `MyCustomAnnouncementViewController`) se inicializará mediante una llamada a método hello `initWithAnnouncement:` y ver Hola será ventana de la aplicación de actual de toohello agregada.
>
>

En la implementación de hello `AEAnnouncementViewController` clase tendrá la propiedad de hello tooread `announcement` tooinitialize sus subvistas. Considere la posibilidad de ejemplo de Hola siguiente, donde dos etiquetas se inicializan mediante `title` y `body` propiedades de hello `AEReachAnnouncement` clase:

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

Si no desea tooload sus vistas por sí mismo, pero solo desea que el diseño de la vista de anuncio de manera predeterminada tooreuse hello, simplemente hacer que el controlador de vista personalizada extiende la clase hello proporciona `AEDefaultAnnouncementViewController`. En ese caso, duplicar archivo nib de hello `AEDefaultAnnouncementView.xib` y cambie su nombre por lo que se puede cargar el controlador de vista personalizada (para un controlador denominado `CustomAnnouncementViewController`, debe llamar a su archivo nib `CustomAnnouncementView.xib`).

categoría de tooreplace Hola predeterminada de los anuncios, simplemente registrar el controlador de vista personalizada para la categoría de hello definida en `kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

Sondeos pueden ser personalizada hello igual:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

Esta vez, Hola proporciona `MyCustomPollViewController` debe extender `AEPollViewController`. O bien puede tooextend controlador predeterminado de hello: `AEDefaultPollViewController`.

> [!IMPORTANT]
> No olvide toocall o `action` (`submitAnswers:` para controladores de la vista de sondeo personalizado) o `exit` método antes de que se cierra el controlador de vista de Hola. En caso contrario, no se envían las estadísticas (es decir, ningún análisis en campaña Hola) y más las campañas siguiente lo importante es que no se notificará hasta que se reinicie el proceso de la aplicación hello.
>
>

##### <a name="implementation-example"></a>Ejemplo de implementación
En esta implementación vista de anuncio personalizado Hola se carga desde un archivo externo xib.

Al igual que para la personalización avanzada de notificación, se recomienda toolook en el código fuente de Hola de implementación estándar de Hola.

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
