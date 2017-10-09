

1. En el equipo Mac, inicie **Acceso a llaves**. En hello izquierda barra de navegación, en **categoría**, abra **mis certificados**. Encontrar el certificado SSL de Hola que descargó en la sección anterior de Hola y revelar su contenido. Seleccione solo Hola certificado (no seleccione clave privada de hello), y [exportarlo](https://support.apple.com/kb/PH20122?locale=en_US).
2. Hola [portal de Azure](https://portal.azure.com/), haga clic en **examinar todos los** > **servicios de aplicaciones**y haga clic en el back-end de aplicaciones móviles. En **Configuración**, haga clic en **App Service Push** y, después, en el nombre del centro de notificaciones. Vaya demasiado**servicios de notificación de inserción de Apple** > **cargar certificado**. Cargar archivo de Hola. p12, seleccionar Hola correcto **modo** (dependiendo de si un certificado de su cliente SSL desde versiones anteriores es de producción o de espacio aislado). Guarde los cambios.

El servicio ahora está configurado toowork con las notificaciones de inserción en iOS.

[1]: ./media/app-service-mobile-apns-configure-push/mobile-push-notification-hub.png
