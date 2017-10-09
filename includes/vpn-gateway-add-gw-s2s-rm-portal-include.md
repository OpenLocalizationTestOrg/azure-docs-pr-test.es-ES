1. En la parte izquierda de la página del portal Hola Hola haga clic en  **+**  y escriba 'Puerta de enlace de red Virtual' en la búsqueda. En **Resultados**, busque y haga clic en **Puerta de enlace de red virtual**.
2. En la parte inferior de Hola de hoja de "Puerta de enlace de red Virtual" Hola, haga clic en **crear**. Se abrirá hello **crear puerta de enlace de red virtual** hoja.

    ![Campos de la hoja Crear puerta de enlace de red virtual](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "Nueva puerta de enlace")

3. En hello **crear puerta de enlace de red virtual** hoja, especificar valores de hello para la puerta de enlace de red virtual.

  - **Nombre**: asigne un nombre a la puerta de enlace. Esto es no Hola igual que una subred de puerta de enlace. Nombre de Hola de objeto de la puerta de enlace de Hola que está creando del.
  - **Tipo de puerta de enlace**: seleccione **VPN**. Puertas de enlace VPN utilice el tipo de puerta de enlace de red virtual de hello **VPN**. 
  - **Tipo de VPN**: Seleccionar tipo VPN de Hola que se especifica para la configuración. La mayoría de las configuraciones requieren un tipo de VPN basada en enrutamiento.
  - **SKU**: puerta de enlace de hello seleccione SKU de la lista desplegable de Hola. SKU de Hello enumeradas en la lista desplegable de hello dependen de hello seleccione el tipo de VPN. Para más información acerca de las SKU de puerta de enlace, consulte [SKU de puerta de enlace](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).
  - **Ubicación**: puede que necesite tooscroll toosee ubicación. Ajustar hello **ubicación** campo toopoint toohello ubicación donde se encuentra la red virtual. Si la ubicación de hello no señala región toohello donde reside la red virtual, red virtual de hello no aparecerá en el paso siguiente de Hola desplegable 'Elegir una red virtual'.
  - **Red virtual**: elija hello toowhich de red virtual que desee tooadd esta puerta de enlace. Haga clic en **red Virtual** hoja de tooopen hello 'Elegir una red virtual'. Seleccione Hola red virtual. Si no ve la red virtual, asegúrese de que el campo de ubicación de hello señala región toohello en el que se encuentra la red virtual.
  - **Dirección IP pública**: hoja de hello 'Crear dirección IP pública' crea un objeto de dirección IP público. la dirección IP pública Hola se asigna dinámicamente cuando se crea la puerta de enlace VPN de Hola. Actualmente, VPN Gateway solo admite la asignación de direcciones IP públicas *dinámicas*. Sin embargo, esto no significa que se cambia la dirección IP de hello después de que se le ha asignado tooyour puerta de enlace VPN. cambios en la dirección IP pública hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear. No cambia cuando se cambia el tamaño, se restablece o se realizan actualizaciones u otras operaciones de mantenimiento interno de una puerta de enlace VPN.

    - En primer lugar, haga clic en **dirección IP pública** tooopen Hola 'Elegir la dirección IP pública' blade, a continuación, haga clic en **+ crear nuevos** hoja de tooopen hello 'Crear dirección IP pública'.
    - A continuación, de entrada una **nombre** para la dirección IP pública, a continuación, haga clic en **Aceptar** en Hola parte inferior de esta hoja toosave los cambios.

      ![Crear dirección IP pública](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "Crear PIP")

4. Compruebe la configuración de Hola. Puede seleccionar **toodashboard Pin** final Hola de hoja de hello si desea que su tooappear de puerta de enlace en el panel de Hola. 
5. Haga clic en **crear** toobegin crear puerta de enlace VPN de Hola. configuraciones de Hola se validarán y verá Hola icono Panel de Hola "Puerta de enlace de red Virtual de implementación". Crear una puerta de enlace puede tardar minutos too45. Puede que necesite toorefresh el estado de página del portal toosee Hola completado.

Después de crea la puerta de enlace de hello, ver la dirección IP de Hola que se ha asignado tooit examinando la red virtual de hello en el portal de Hola. puerta de enlace de Hello aparecerá como un dispositivo conectado. Puede hacer clic en hello conectado (la puerta de enlace de red virtual) de dispositivo tooview obtener más información.
