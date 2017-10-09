Una vez propagaron registros hello para el nombre de dominio, debe ser capaz de toouse su tooverify de explorador que el nombre de dominio personalizado puede ser tooaccess usa la aplicación web en el servicio de aplicaciones de Azure.

> [!NOTE]
> Puede tardar algún tiempo para su toopropagate CNAME a través de hello sistema DNS. Puede utilizar un servicio como <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify que Hola CNAME está disponible.
> 
> 

Si aún no ha agregado la aplicación web como un punto de conexión de Traffic Manager, debe hacerlo antes de que funcione la resolución de nombres, como nombre rutas tooTraffic Manager de hello dominio personalizado. El Administrador de tráfico, a continuación, enruta tooyour web app. Usar información de hello en [agregar o eliminar puntos de conexión](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd su aplicación web como un punto de conexión en el perfil de Traffic Manager.

> [!NOTE]
> Si s aplicación web no aparece en la lista al agregar un extremo, compruebe que está configurada para el modo de plan **estándar** del Servicio de aplicaciones. Debe usar **estándar** modo para la aplicación web en orden toowork con el Administrador de tráfico.
> 
> 

1. En el explorador, abra hello [Portal de Azure](https://portal.azure.com).
2. Hola **aplicaciones Web** , haga clic en nombre de saludo de la aplicación web, seleccione **configuración**y, a continuación, seleccione **los dominios personalizados**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Hola **los dominios personalizados** hoja, haga clic en **Agregar nombre de host**.
4. Hola de uso **Hostname** texto cuadros tooenter Hola Traffic Manager dominio nombre tooassociate con esta aplicación web.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. Haga clic en **validar** configuración de nombres de dominio de toosave Hola.
6. Al hacer clic en **Validar** , Azure iniciará el flujo de trabajo Verificación de dominio. Esto comprobará propiedad del dominio, así como correcto de disponibilidad y el informe de nombre de host o error detallado con orienteción preceptiva sobre cómo toofix Hola error.    
7. Después de validar correctamente **Agregar nombre de host** botón estará activo y será el nombre de host de toohello puede asignar. Ahora, explore tooyour nombre de dominio personalizado en un explorador. Ahora verá la aplicación en ejecución con su nombre de dominio personalizado. 
   
   Una vez completada la configuración, nombre de dominio personalizado de Hola se enumerarán en hello **nombres de dominio** sección de la aplicación web.

En este punto, debe ser nombre de nombre de dominio de Traffic Manager de tooenter capaz de hello en el explorador y comprobar que correctamente tarda tooyour web app.

