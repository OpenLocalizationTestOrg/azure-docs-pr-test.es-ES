Una vez propagaron registros hello para el nombre de dominio, debe asociarlos a su aplicación Web. Use Hola siguientes pasos le indican nombres de dominio de hello tooenable mediante el explorador web.

> [!NOTE]
> Puede tardar algún tiempo para los registros TXT creado en hello toopropagate de pasos anteriores a través de hello sistema DNS. No se puede agregar nombre de dominio de Hola de aplicación web de tooyour hasta que se ha propagado Hola registro TXT. Si usas un registro, no se puede agregar Hola una aplicación de web de tooyour de nombre de dominio registros hasta que se ha propagado registro TXT de hello creado en el paso anterior de Hola.
> 
> Puede utilizar un servicio como <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify que Hola registro TXT está disponible.
> 
> 

1. En el explorador, abra hello [Portal de Azure](https://portal.azure.com).
2. Hola **aplicaciones Web** pestaña, haga clic en nombre de saludo de la aplicación web y, a continuación, seleccione **los dominios personalizados**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Hola **los dominios personalizados** hoja, haga clic en **Agregar nombre de host**.
4. Hola de uso **Hostname** texto tooassociate de nombres de dominio cuadros tooenter Hola con esta aplicación web.
   
    ![](./media/custom-dns-web-site/add-custom-domain.png)
5. Haga clic en **Validar**.
6. Al hacer clic en **Validar** , Azure iniciará el flujo de trabajo Verificación de dominio. Esto comprobará propiedad del dominio, así como correcto de disponibilidad y el informe de nombre de host o error detallado con orienteción preceptiva sobre cómo toofix Hola error.    

En este punto, debe ser capaz de tooenter nombre de dominio personalizado de hello en el explorador y comprobar que correctamente tarda tooyour web app.

