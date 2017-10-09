En este paso, creará un puerto de sondeo firewall regla tooopen hello para el extremo de carga equilibrada de hello (59999, como se especificó anteriormente) y otro puerto de escucha de grupo de disponibilidad de tooopen Hola de regla. Dado que ha creado el extremo de carga equilibrada de hello en hello las máquinas virtuales que contienen réplicas del grupo de disponibilidad, debe tooopen puerto de sondeo de Hola y el puerto de agente de escucha de hello en hello respectivas máquinas virtuales.

1. Inicie el **Firewall de Windows con seguridad avanzada** en las máquinas virtuales que hospedan réplicas.

2. Haga clic con el botón derecho en **Reglas de entrada** y después en **Nueva regla**.

3. En hello **tipo de regla** página, seleccione **puerto**y, a continuación, haga clic en **siguiente**.

4. En hello **protocolo y puertos** página, seleccione **TCP**, tipo **59999** en hello **puertos locales específicos** cuadro y, a continuación, haga clic en **Siguiente**.

5. En hello **acción** página, mantenga **Permitir conexión hello** seleccionada y, a continuación, haga clic en **siguiente**.

6. En hello **perfil** página, acepte la configuración predeterminada de hello y, a continuación, haga clic en **siguiente**.

7. En hello **nombre** página Hola **nombre** texto, especifique un nombre de regla, como **siempre en sondeo de puerto de escucha**y, a continuación, haga clic en **finalizar**.

8. Repita Hola pasos para el puerto de escucha de grupo de disponibilidad de hello (como se especificó anteriormente en el parámetro hello $EndpointPort del script de Hola) anteriores y, a continuación, especifique un nombre de regla adecuado, como **siempre en el puerto de escucha**.

