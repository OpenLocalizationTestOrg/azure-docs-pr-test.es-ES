toocreate una red virtual en modelo de implementación de administrador de recursos de hello mediante el uso de hello portal de Azure, siga estos pasos Hola. Hola de uso [valores de ejemplo](#values) si va a usar estos pasos como un tutorial. Si no está realizando estos pasos como un tutorial, ser seguro de valores de hello tooreplace por los suyos propios. Para obtener más información sobre cómo trabajar con redes virtuales, vea hello [información general de red Virtual](../articles/virtual-network/virtual-networks-overview.md).

1. Desde un explorador, navegue toohello [portal de Azure](http://portal.azure.com) e inicie sesión con su cuenta de Azure.
2. Haga clic en **Nuevo**. Hola **busque en marketplace hello** , escriba 'Red Virtual'. Busque **red Virtual** de hello devuelve lista y haga clic en hello tooopen **red Virtual** hoja.
3. En parte inferior de Hola de hoja de la red Virtual de hello, de hello **seleccionar un modelo de implementación** seleccione **el Administrador de recursos**y, a continuación, haga clic en **crear**. Esto abre una hoja de hello 'Crear red virtual'.

    ![Hoja Crear red virtual](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/createvnet.png "Hoja Crear red virtual")
4. En hello **crear red virtual** hoja, configurar opciones de red virtual de Hola. Cuando se rellena en campos de hello, hello marca de exclamación rojo se convierte en una marca de verificación verde cuando caracteres Hola especificados en el campo de hello son válidos.

  - **Nombre**: escriba el nombre de hello para la red virtual. En este ejemplo, se usa TestVNet1.
  - **Espacio de direcciones**: escriba el espacio de direcciones de Hola. Si tiene varios tooadd de espacios de direcciones, agregue el primer espacio de direcciones. Posteriormente, puede agregar espacios de direcciones adicionales después de crear Hola red virtual. Asegúrese de que ese espacio de direcciones de Hola que especifique no se superpone con el espacio de direcciones de hello para la ubicación local.
  - **Nombre de subred**: agregar Hola primera subred nombre y la subred intervalo de direcciones. Puede agregar subredes adicionales y la subred de puerta de enlace de hello más adelante, después de crear esta red virtual. 
  - **Suscripción**: Compruebe que suscripción Hola enumerado se Hola correcto. Puede cambiar las suscripciones mediante Hola de lista desplegable.
  - **Grupo de recursos**: seleccione un grupo de recursos existente, o bien cree uno nuevo y escriba su nombre. Si está creando un nuevo grupo, el grupo de recursos de nombre hello según tooyour había planeada valores de configuración. Para obtener más información sobre los grupos de recursos, visite [Información general del Administrador de recursos de Azure](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
  - **Ubicación**: Seleccionar ubicación de hello para la red virtual. ubicación de Hello determina dónde se ubicación recursos Hola que implemente toothis red virtual.

5. Seleccione **Pin toodashboard** si desea toobe pueda toofind la red virtual fácilmente en el panel de hello y, a continuación, haga clic en **crear**. Después de hacer clic **crear**, verá un icono en el panel que reflejará el progreso de saludo de la red virtual. Hola de iconos cambia cuando Hola red virtual se está creando.
