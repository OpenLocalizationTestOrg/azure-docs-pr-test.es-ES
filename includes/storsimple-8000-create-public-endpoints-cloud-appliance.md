#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>toocreate extremos públicos en el dispositivo de hello en la nube

1. Inicie sesión en toohello portal de Azure.
2. Vaya demasiado**máquinas virtuales**y, a continuación, seleccione y haga clic en la máquina virtual de Hola que se usa como el dispositivo en la nube.
    
3. Debe toocreate red seguridad (NSG) del grupo regla toocontrol Hola flujo de tráfico dentro y fuera de la máquina virtual. Realizar Hola siguiendo los pasos toocreate una regla de NSG.
    1. Seleccione **Grupo de seguridad de red**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. Haga clic en el grupo de seguridad de red de forma predeterminada de Hola que se presenta.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. Seleccione **Reglas de seguridad de entrada**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. Haga clic en **+ agregar** toocreate una regla de seguridad de entrada.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        En la hoja de regla de seguridad de entrada de hello agregar:

        1. Para hello **nombre**, escriba lo siguiente Hola nombre para el punto de conexión de hello: WinRMHttps.
        
        2. Para hello **prioridad**, seleccione un número menor que 1000 (que es la prioridad de hello para la regla predeterminada de hello). Valor de hello mayor, menor prioridad Hola.

        3. Conjunto hello **origen** demasiado**cualquier**.

        4. Para hello **servicio**, seleccione **WinRM**. Hola **protocolo** automáticamente se establece demasiado**TCP** hello y **intervalo de puertos** se establece demasiado**5986**.

        5. Haga clic en **Aceptar** regla de toocreate Hola.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. El paso final es tooassociate grupo de seguridad de su red con una subred o una interfaz de red específica. Realizar Hola siguiendo los pasos tooassociate el grupo de seguridad de red con una subred.
    1. Vaya demasiado**subredes**.
    2. Haga clic en **+ Asociar**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. Seleccione la red virtual y, a continuación, seleccione subred adecuada de Hola.
    4. Haga clic en **Aceptar** regla de toocreate Hola.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

Después de crea la regla de hello, puede ver su dirección de IP Virtual pública (VIP) de detalles toodetermine Hola. Anote esta dirección.


