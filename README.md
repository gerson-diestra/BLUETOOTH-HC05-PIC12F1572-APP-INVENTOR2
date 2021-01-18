char dato;

void main() {
   C1ON_bit = 0x00;
   ADON_bit = 0x00;
   ANSELA   = 0x00;
   OSCCON   = 0x72;
   DACEN_bit = 0x00;

   TRISA   = 0x28;  // RA3 siempre es entrada "1", RA5 es Rx como entrada
   PORTA   = 0x00;
  // LATA    = 0x00;
   TXCKSEL_bit = 1;  // Trasmisor RA4 (Tx)
   RXDTSEL_bit = 1;  //Receptor   RA5 (Rx)

//------Configuración Tx (Transmisor) ------
   TX9_bit  = 0;  //tramision de 8 bits
   TXEN_bit = 1; //trasmision activa
   SYNC_bit = 0; //seleccion modo asíncrono

// ------configuración RXSTA(Receptor)------------------
   CREN_bit = 1;
   SYNC_bit = 0;
   SPEN_bit = 1; //habilitación RB1(Rx)/RB2(Tx)
   RX9_bit  = 0; //recepcion serial de 8 bits
//----- inicio de UART ---------------
    UART1_Init(9600);
    delay_ms(100);
   
   while(1){
        if(UART1_DATA_Ready()){
         dato = UART1_Read();
         UART1_Write(dato);
        }
       if(dato == 'A'){
         RA2_bit = 0x01;
         RA0_bit = 0x01;
       }
       if(dato == 'B'){
         RA2_bit = 0x00;
         RA0_bit = 0x00;
       }
   }
   
}
