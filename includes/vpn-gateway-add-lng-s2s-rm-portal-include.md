1. En el portal de hello, de **todos los recursos**, haga clic en **+ agregar**. 
2. Hola **todo** cuadro de búsqueda de hoja, escriba **puerta de enlace de red Local**, a continuación, haga clic en toosearch. Esto devolverá una lista. Haga clic en **puerta de enlace de red Local** tooopen Hola blade, a continuación, haga clic en **crear** tooopen hello **crear puerta de enlace de red local** hoja.

  ![crear una puerta de enlace de red local](./media/vpn-gateway-add-lng-s2s-rm-portal-include/createlng.png)

3. En hello **hoja de puerta de enlace de red local crear**, especificar valores de hello para la puerta de enlace de red local.

  - **Nombre:** especifique el nombre del objeto de puerta de enlace de red local.
  - **Dirección IP:** es Hola de dirección IP pública del dispositivo VPN de Hola que desee tooconnect Azure para. Especifique una dirección IP pública válida. dirección IP de Hello no puede estar detrás de NAT y tiene toobe accesible por Azure. Si no tiene dirección IP de hello ahora mismo, puede utilizar valores de hello se muestra en la captura de pantalla de hello, pero podrá necesita toogo nuevo y reemplace la dirección IP de marcador de posición por dirección IP pública de hello de dispositivo VPN. En caso contrario, Azure no será capaz de tooconnect.
  - **Espacio de direcciones** hace referencia toohello los intervalos de direcciones de red de Hola que representa esta red local. Puede agregar varios intervalos de espacios de direcciones. Asegúrese de que los intervalos de Hola que especifique aquí no se superponen con intervalos de otras redes que desea tooconnect a. Azure distribuirá el intervalo de direcciones de Hola que especifique la dirección IP de dispositivo VPN de toohello local. *Usar sus propios valores aquí, no Hola valores que se muestran en la captura de pantalla de hello*.
  - **Suscripción:** comprobar ese Hola correcto de suscripción que se muestra.
  - **Grupo de recursos:** grupo de recursos de hello Select que desea toouse. Puede crear un grupo de recursos nuevo o seleccionar uno ya creado.
  - **Ubicación:** Seleccionar ubicación de Hola que se creará en este objeto. Puede que desee tooselect Hola la misma ubicación que la red virtual reside en pero no es necesario toodo así.

4. Cuando haya terminado de especificar valores de hello, haga clic en **crear** final Hola de puerta de enlace de hello hoja toocreate Hola red local.
