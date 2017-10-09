
De forma predeterminada, se pueden invocar las API en un back-end de Mobile Apps de forma anónima. A continuación, necesita a los clientes de toorestrict acceso tooonly autenticado.  

* **Terminar Node.js nuevo (a través de Hola portal de Azure)** :  

    En la configuración de Mobile Apps, haga clic en **Tablas fáciles** y seleccione la tabla. Haga clic en **Cambiar permisos**, seleccione **Solo acceso autenticado** para todos los permisos y luego haga clic en **Guardar**.
* **Back-end de .NET (C#)**:  

    En el proyecto de servidor hello, navegue demasiado**controladores** > **TodoItemController.cs**. Agregar hello `[Authorize]` atributo toohello **TodoItemController** de la clase, como se indica a continuación. toorestrict acceso únicos toospecific métodos, también puede aplicar este método simplemente toothose de atributo en lugar de la clase hello. Volver a publicar el proyecto de servidor de Hola.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Back-end de Node.js (a través del código de Node.js)** :  

    toorequire autenticación para el acceso a la tabla, agregue Hola siguiente secuencia de comandos de línea toohello Node.js server:

        table.access = 'authenticated';

    Para obtener más información, consulte [Cómo: requerir la autenticación para acceso tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth). toolearn cómo ver el proyecto de código de inicio rápido de toodownload Hola desde su sitio, [Cómo: Descargar proyecto de código de la inicio rápido de hello Node.js back-end mediante Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).
