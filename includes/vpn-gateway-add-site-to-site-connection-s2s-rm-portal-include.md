1. Navegue tooand hoja de hello abierto para la puerta de enlace de red virtual. No hay toonavigate de varias maneras. En nuestro ejemplo, se abrirá la puerta de enlace de toohello 'VNet1GW' yendo demasiado**TestVNet1 -> Introducción -> conectado dispositivos -> VNet1GW**.
2. En la hoja de Hola para VNet1GW, haga clic en **conexiones**. En la parte superior de Hola de hoja de las conexiones de hello, haga clic en **+ agregar** tooopen hello **Agregar conexión** hoja.

    ![Creación de una conexión de sitio a sitio](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. En hello **Agregar conexión** hoja, hello, rellene los valores de toocreate la conexión.

  - **Nombre**: asigne un nombre a la conexión. En nuestro ejemplo usamos **VNet1toSite2**.
  - **Tipo de conexión:** seleccione **Sitio a sitio (IPSec)**.
  - **Puerta de enlace de red virtual:** Hola valor es fijo porque se conecta desde esta puerta de enlace.
  - **Puerta de enlace de red local:** haga clic en **elegir una puerta de enlace de red local** y seleccione Hola de puerta de enlace de red local que desea toouse. En el ejemplo, se usa **Site2**.
  - **Clave compartida:** Hola valor aquí debe coincidir con hello que está usando para el dispositivo VPN de instalaciones locales. En el ejemplo de Hola, hemos usado "abc123", pero puede (y debe) usar algo más complejo. Hola importante que es ese valor de Hola que especifique aquí debe ser Hola que mismo valor que especificó al configurar el dispositivo VPN.
  - Hola los valores restantes de **suscripción**, **grupo de recursos**, y **ubicación** son fijos.

4. Haga clic en **Aceptar** toocreate la conexión. Verá *crear conexión* flash en pantalla de bienvenida.
5. Puede ver conexiones de Hola Hola **conexiones** hoja de puerta de enlace de red virtual de Hola. Hello estado pasará de *desconocido* demasiado*conexión*y, a continuación, demasiado*correcto*.
