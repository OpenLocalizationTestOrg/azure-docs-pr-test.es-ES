Al generar un certificado de cliente, se instala automáticamente en el equipo que usó para generarlo. Si desea instalar el certificado de cliente en otro equipo cliente, debe exportar el certificado de cliente que ha generado.                              

1. Para exportar un certificado de cliente, abra **Administrar certificados de usuario**. De forma predeterminada, los certificados de cliente que ha generado se encuentran en "Certificates - Current User\Personal\Certificates". Haga clic con el botón derecho en el certificado de cliente que desee exportar y haga clic en **Todas las tareas** y en **Exportar** para abrir el **Asistente para exportar certificados**.
2. En el asistente, haga clic en **Siguiente**, seleccione **Exportar la clave privada** y, luego, haga clic en **Siguiente**.
3. En la página **Formato de archivo de exportación**, deje seleccionados los valores predeterminados. Asegúrese de que **Incluir todos los certificados en la ruta de certificación si es posible** esté seleccionada. Al seleccionar esta opción, también se exporta la información del certificado raíz que se requiere para una autenticación correcta. A continuación, haga clic en **Siguiente**.
4. En la página **Seguridad** , debe proteger la clave privada. Si decide usar una contraseña, asegúrese de anotarla o de recordar la contraseña que estableció para este certificado. A continuación, haga clic en **Siguiente**.
5. En **Archivo que se va a exportar**, haga clic en **Examinar** para ir a la ubicación a la que desea exportar el certificado. En **Nombre de archivo**, asígnele un nombre al archivo de certificado. A continuación, haga clic en **Siguiente**.
6. Haga clic en **Finalizar** para exportar el certificado.