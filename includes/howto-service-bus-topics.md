## <a name="what-are-service-bus-topics-and-subscriptions"></a>Qué son los temas y las suscripciones del Bus de servicio
Las suscripciones y los temas del Bus de servicio son compatibles con el modelo de comunicación de mensajería de *publicación/suscripción* . Cuando se usan temas y suscripciones, los componentes de una aplicación distribuida no se comunican directamente entre sí, sino que intercambian mensajes a través de un tema, que actúa como un intermediario.

![TopicConcepts](./media/howto-service-bus-topics/sb-topics-01.png)

A diferencia de las colas del Bus de servicio, en las que un solo destinatario procesa cada mensaje, los temas y las suscripciones proporcionan una forma de comunicación de uno a varios mediante un patrón de publicación/suscripción. Es posible registrar varios temas de tooa de suscripciones. Cuando se envía un mensaje tooa tema, luego se convierte en disponible tooeach suscripción toohandle o proceso por separado.

Un tema de tooa de suscripción es similar a una cola virtual que recibe copias de mensajes de Hola que se enviaron toohello tema. Si lo desea puede registrar las reglas de filtro para un tema en una base por suscripción, lo que le permite toofilter o restringir qué tema tooa de mensajes son recibidos por qué suscripciones al tema.

Las suscripciones y los temas de Bus de servicio permiten tooscale y procesarán un gran número de mensajes a través de muchos usuarios y aplicaciones.

## <a name="create-a-namespace"></a>Creación de un espacio de nombres
toobegin con temas de Bus de servicio y las suscripciones de Azure, primero debe crear un *espacio de nombres de servicio*. Un espacio de nombres proporciona un contenedor con un ámbito para el desvío de recursos del bus de servicio en la aplicación.

toocreate un espacio de nombres:

1. Inicie sesión en toohello [portal de Azure][Azure portal].
2. En el panel de navegación izquierdo de hello del portal de hello, haga clic en **New**, a continuación, haga clic en **integración empresarial**y, a continuación, haga clic en **Bus de servicio**.
3. Hola **crear espacio de nombres** cuadro de diálogo, escriba un nombre de espacio de nombres. sistema de Hello comprueba inmediatamente toosee si Hola nombre está disponible.
4. Después de realizar el nombre de espacio de nombres de hello seguro está disponible, elija Hola tarifa (Basic, Standard o Premium).
5. Hola **suscripción** , a continuación, elija una suscripción de Azure en qué espacio de nombres de hello toocreate.
6. Hola **grupo de recursos** , a continuación, elija un grupo de recursos existente en qué Hola live espacio de nombres o cree uno nuevo.      
7. En **ubicación**, elegir Hola país o una región en la que se debe hospedar el espacio de nombres.
   
    ![Crear un espacio de nombres][create-namespace]
8. Haga clic en hello **crear** botón. sistema de Hello ahora crea el espacio de nombres y lo habilita. Es posible que tenga toowait unos minutos hasta que proporcione los recursos del sistema Hola para su cuenta.

### <a name="obtain-hello-credentials"></a>Obtener credenciales de Hola
1. Hola lista de espacios de nombres, haga clic en hello que acaba de crear espacio de nombres.
2. Hola **espacio de nombres de Bus de servicio** hoja, haga clic en **directivas de acceso compartido**.
3. Hola **directivas de acceso compartido** hoja, haga clic en **RootManageSharedAccessKey**.
   
    ![información de conexión][connection-info]
4. Hola **directiva: RootManageSharedAccessKey** hoja, haga clic en botón de copiar Hola siguiente demasiado**clave principal: cadena de conexión**, Portapapeles toocopy Hola conexión cadena tooyour para su uso posterior.
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


