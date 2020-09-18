Master:
Glavni:
 banksel SSPCON
 movlw 0x20
 movwf SSPCON
 banksel SSPSTAT
 clrf SSPSTAT
 banksel TRISC
 bcf TRISC,3
 bcf TRISC,5
L0
 banksel SSPBUF
 movlw 0xFF
 movwf SSPBUF
call delay
 clrf SSPBUF
 call delay
 goto L0

delay
 movlw 0x01 ; brojac A=1
 movwf brojaca ;
L1
 movlw 0x0A ; brojac B=10
 movwf brojacb ;
L2
 movlw 0x0A ; brojac C=10
 movwf brojacc ;
L3
 movlw 0x0A ; brojac D=10
 movwf brojacd ;
L4
 decfsz brojacd,1
 goto L4
 decfsz brojacc,1
 goto L3
 decfsz brojacb,1
 goto L2
 decfsz brojaca,1
 goto L1
 return
end
Slave:
Glavni
 banksel SSPCON
 movlw 0x24
 movwf SSPCON
 banksel SSPSTAT
 clrf SSPSTAT
 banksel TRISD
 bcf TRISD,0
 banksel TRISC
 bsf TRISC,3
 bcf TRISC,5
 banksel ADCON1
 movlw 0x07
 movwf ADCON1
 banksel TRISA
 bsf TRISA,5
L0
 banksel SSPSTAT
 btfss SSPSTAT,0
 goto L0
 banksel SSPBUF
 movf SSPBUF,0
 banksel LATD
 movwf LATD
 call delay
 goto L0

delay
 movlw 0x01 ; brojac A=1
 movwf brojaca ;
L1
 movlw 0x0A ; brojac B=10
 movwf brojacb ;
L2
movlw 0x0A ; brojac C=10
 movwf brojacc ;
L3
 movlw 0x0A ; brojac D=10
 movwf brojacd ;
L4
 decfsz brojacd,1
 goto L4
 decfsz brojacc,1
 goto L3
 decfsz brojacb,1
 goto L2
 decfsz brojaca,1
 goto L1
return
end

