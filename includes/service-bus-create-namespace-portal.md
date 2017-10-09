toobegin uso del Bus de servicio pone en cola en Azure, primero debe crear un espacio de nombres con un nombre que sea único a través de Azure. Un espacio de nombres proporciona un contenedor con un ámbito para el desvío de recursos del bus de servicio en la aplicación.

toocreate un espacio de nombres:

1. Inicie sesión en toohello [portal de Azure][Azure portal].
2. En el panel de navegación izquierdo de hello del portal de hello, haga clic en **New**, a continuación, haga clic en **integración empresarial**y, a continuación, haga clic en **Bus de servicio**.
3. Hola **crear espacio de nombres** cuadro de diálogo, escriba un nombre de espacio de nombres. sistema de Hello comprueba inmediatamente toosee si Hola nombre está disponible.
4. Después de realizar el nombre de espacio de nombres de hello seguro está disponible, elija Hola tarifa (Basic, Standard o Premium).
5. Hola **suscripción** , a continuación, elija una suscripción de Azure en qué espacio de nombres de hello toocreate.
6. Hola **grupo de recursos** , a continuación, elija un grupo de recursos existente en qué Hola live espacio de nombres o cree uno nuevo.      
7. En **ubicación**, elegir Hola país o una región en la que se debe hospedar el espacio de nombres.
   
    ![Crear un espacio de nombres][create-namespace]
8. Haga clic en **Crear**. sistema de Hello ahora crea el espacio de nombres y lo habilita. Es posible que tenga toowait unos minutos hasta que proporcione los recursos del sistema Hola para su cuenta.

### <a name="obtain-hello-management-credentials"></a>Obtener las credenciales de administración de Hola

1. Hola lista de espacios de nombres, haga clic en hello que acaba de crear espacio de nombres.
2. En la hoja de espacio de nombres de hello, haga clic en **directivas de acceso compartido**.
3. Hola **directivas de acceso compartido** hoja, haga clic en **RootManageSharedAccessKey**.
   
    ![información de conexión][connection-info]
4. Hola **directiva: RootManageSharedAccessKey** hoja, haga clic en botón de copiar Hola siguiente demasiado**clave principal: cadena de conexión**, Portapapeles toocopy Hola conexión cadena tooyour para su uso posterior. Pegue este valor en el Bloc de notas o cualquier otra ubicación temporal.
   
    ![connection-string][connection-string]

5. Paso anterior repetición hello, copiar y pegar el valor de Hola de **clave principal** tooa ubicación temporal para su uso posterior.

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
