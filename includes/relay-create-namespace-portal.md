1. Inicie sesión en toohello [portal de Azure][Azure portal].
2. En el panel de navegación izquierdo de hello del portal de hello, haga clic en **New**, a continuación, haga clic en **integración empresarial**y, a continuación, haga clic en **retransmisión**.
3. Hola **crear espacio de nombres** cuadro de diálogo, escriba un nombre de espacio de nombres. sistema de Hello comprueba inmediatamente toosee si Hola nombre está disponible.
4. Hola **suscripción** , a continuación, elija una suscripción de Azure en qué espacio de nombres de hello toocreate.
5. Hola  **[grupo de recursos](../articles/azure-resource-manager/resource-group-portal.md)**  , a continuación, elija un grupo de recursos existente en qué Hola live espacio de nombres o cree uno nuevo.      
6. En **ubicación**, elegir Hola país o una región en la que se debe hospedar el espacio de nombres.
   
    ![Crear un espacio de nombres][create-namespace]
7. Haga clic en **Crear**. sistema de Hello ahora crea el espacio de nombres y lo habilita. Después de unos minutos, Hola sistema proporcione los recursos de su cuenta.

### <a name="obtain-hello-management-credentials"></a>Obtener las credenciales de administración de Hola
1. Hola lista de espacios de nombres, haga clic en hello que acaba de crear espacio de nombres.
2. En la hoja de espacio de nombres de hello, haga clic en **directivas de acceso compartido**.
3. Hola **directivas de acceso compartido** hoja, haga clic en **RootManageSharedAccessKey**.
   
    ![información de conexión][connection-info]
4. Hola **directiva: RootManageSharedAccessKey** hoja, haga clic en botón de copiar Hola siguiente demasiado**clave principal: cadena de conexión**, Portapapeles toocopy Hola conexión cadena tooyour para su uso posterior. Pegue este valor en el Bloc de notas o cualquier otra ubicación temporal.
   
    ![connection-string][connection-string]

5. Paso anterior repetición hello, copiar y pegar el valor de Hola de **clave principal** tooa ubicación temporal para su uso posterior.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
