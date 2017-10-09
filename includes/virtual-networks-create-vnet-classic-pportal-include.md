## <a name="how-toocreate-a-classic-vnet-in-hello-azure-portal"></a>¿Cómo toocreate una red virtual clásica Hola portal de Azure
toocreate una red virtual clásica en función de hello escenario anterior, siga estos pasos Hola.

1. Desde un explorador, navegue toohttp://portal.azure.com y, si es necesario, inicie sesión con su cuenta de Azure.
2. Haga clic en **NEW** > **red** > **red Virtual**, tenga en cuenta que hello **seleccionar un modelo de implementación** lista ya se muestran **clásico**y, a continuación, haga clic en **crear**, como se muestra en la siguiente ilustración de Hola.
   
    ![Creación de una red virtual en el Portal de Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. En hello **red Virtual** hoja, Hola de tipo **nombre** de hello red virtual y, a continuación, haga clic en **espacio de direcciones**. Configurar la configuración del espacio de direcciones de red virtual de Hola y de su primera subred, a continuación, haga clic en **Aceptar**. Hola siguiente ilustración muestra la configuración de bloque CIDR de hello en nuestro caso.
   
    ![Hoja de espacio de direcciones](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. Haga clic en **grupo de recursos** y seleccione Hola red virtual a un tooadd de grupo de recursos, o haga clic en **crear nuevo grupo de recursos** tooadd Hola red virtual tooa nuevo grupo de recursos. Hello siguiente figura muestra recursos Hola configuración de grupo para un grupo de recursos nuevo llamado **TestRG**. Para obtener más información sobre los grupos de recursos, visite [Información general del Administrador de recursos de Azure](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
   
    ![Crear hoja de grupo de recursos](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. Si es necesario, cambie hello **suscripción** y **ubicación** configuración de la red virtual. 
6. Si no desea toosee Hola red virtual como un icono en hello **panel de inicio**, deshabilitar **tooStartboard Pin**. 
7. Haga clic en **crear** y el icono de anuncio Hola denominado **red crear Virtual** tal y como se muestra en la siguiente ilustración de Hola.
   
    ![Crear red virtual en el portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. Espere hello toobe de red virtual que creó y, cuando vea Hola mosaico a continuación, haga clic en él tooadd más subredes.
   
    ![Crear red virtual en el portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. Debería ver Hola **configuración** para la red virtual, tal y como se muestra a continuación. 
   
    ![Crear red virtual en el portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. Haga clic en **Subredes** > **Agregar**, escriba un **nombre**, especifique un **intervalo de direcciones (bloque CIDR)** para la subred y haga clic en **Aceptar**. ilustración de Hello siguiente muestra valores de hello para nuestro escenario actual.
    
    ![Creación de una red virtual en el Portal de Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)

