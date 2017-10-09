### <a name="noconnection"></a>prefijos de direcciones en la IP de la puerta de enlace de red local toomodify - no hay ninguna conexión de puerta de enlace

#### <a name="tooadd-additional-address-prefixes"></a>prefijos de dirección adicional tooadd:

1. En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **configuración**.
2. Agregar espacio de direcciones IP de Hola Hola *agregar otro intervalo de direcciones* cuadro.
3. Haga clic en **guardar** toosave la configuración.

#### <a name="tooremove-address-prefixes"></a>prefijos de direcciones de tooremove:

1. En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **configuración**.
2. Haga clic en hello **'...'** en la línea de Hola que contiene el prefijo de hello desea tooremove.
3. Haga clic en **Quitar**.
4. Haga clic en **guardar** toosave la configuración.

### <a name="withconnection"></a>toomodify red local puerta de enlace prefijos de direcciones IP: conexión de puerta de enlace existente

Si tiene una conexión de puerta de enlace y desea tooadd o quitar prefijos de direcciones IP de hello contenidos en la puerta de enlace de red local, deberá hello toodo siguiendo los pasos en orden. Esto tendrá como resultado un tiempo de inactividad para la conexión VPN. Cuando se modifica prefijos de direcciones IP, no es necesario puerta de enlace VPN toodelete Hola. Solo necesita conexión de hello tooremove.

#### <a name="1-remove-hello-connection"></a>1. Quitar conexión de Hola.

1. En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **conexiones**.
2. Haga clic en hello **...**  en línea hello para cada conexión, a continuación, haga clic en **eliminar**.
3. Haga clic en **guardar** toosave la configuración.

#### <a name="2-modify-hello-address-prefixes"></a>2. Modifique los prefijos de direcciones de Hola.

prefijos de dirección adicional tooadd:

1. En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **configuración**.
2. Agregar espacio de direcciones IP de Hola.
3. Haga clic en **guardar** toosave la configuración.

prefijos de direcciones de tooremove:

1. En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **configuración**.
2. Haga clic en hello **...**  en la línea de Hola que contiene el prefijo de hello desea tooremove.
3. Haga clic en **Quitar**.
4. Haga clic en **guardar** toosave la configuración.

#### <a name="3-recreate-hello-connection"></a>3. Vuelva a crear la conexión de Hola.

1. Navegue toohello puerta de enlace de red Virtual para la red virtual. (No Hola puerta de enlace de red Local.)
2. En hello puerta de enlace de red Virtual, en hello **configuración** sección, haga clic en **conexiones**.
3. Haga clic en hello **+ agregar** tooopen hello **Agregar conexión** hoja.
4. Vuelva a crear la conexión.
5. Haga clic en **Aceptar** conexión de hello toocreate.
