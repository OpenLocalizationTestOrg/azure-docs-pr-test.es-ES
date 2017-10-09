### <a name="gwipnoconnection"></a>dirección IP en la puerta de enlace de la red local de hello toomodify - no hay ninguna conexión de puerta de enlace

Utilice toomodify de ejemplo de Hola una puerta de enlace de red local que no tiene una conexión de puerta de enlace. Cuando se modifica este valor, también puede modificar los prefijos de direcciones de hello en hello mismo tiempo.

1. En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **configuración**.
2. Hola **dirección IP** cuadro, modifique la dirección IP de Hola.
3. Haga clic en **guardar** configuración de toosave Hola.

### <a name="gwipwithconnection"></a>dirección IP de puerta de enlace puerta de enlace de toomodify Hola red local - conexión de puerta de enlace existente

toomodify una puerta de enlace de red local que tiene una conexión, debe quitar de la conexión hello toofirst. Después de quita la conexión de hello, puede modificar la dirección IP de puerta de enlace de Hola y volver a crear una nueva conexión. También puede modificar los prefijos de direcciones de hello en hello mismo tiempo. Esto tendrá como resultado un tiempo de inactividad para la conexión VPN. Cuando se modifica la dirección IP de puerta de enlace de hello, no necesita la puerta de enlace VPN toodelete Hola. Solo necesita conexión de hello tooremove.
 
#### <a name="1-remove-hello-connection"></a>1. Quitar conexión de Hola.

1. En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **conexiones**.
2. Haga clic en hello **...**  en línea hello para la conexión de hello, a continuación, haga clic en **eliminar**.
3. Haga clic en **guardar** toosave la configuración.

#### <a name="2-modify-hello-ip-address"></a>2. Modificar la dirección IP de Hola.

También puede modificar los prefijos de direcciones de hello en hello mismo tiempo.

1. Hola **dirección IP** cuadro, modifique la dirección IP de Hola.
2. Haga clic en **guardar** configuración de toosave Hola.

#### <a name="3-recreate-hello-connection"></a>3. Vuelva a crear la conexión de Hola.

1. Navegue toohello puerta de enlace de red Virtual para la red virtual. (No Hola puerta de enlace de red Local.)
2. En hello puerta de enlace de red Virtual, en hello **configuración** sección, haga clic en **conexiones**.
3. Haga clic en hello **+ agregar** tooopen hello **Agregar conexión** hoja.
4. Vuelva a crear la conexión.
5. Haga clic en **Aceptar** conexión de hello toocreate.
