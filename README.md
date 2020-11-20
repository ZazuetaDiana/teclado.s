
@ greet.s - un pequeño saludo asm.
@ programa corto que obtiene la entrada del teclado y luego lo imprime de nuevo en la pantalla.


.sección 	.bss
.comm búfer, 48 	     @ reserva búfer de 48 bytes

.section 	.data
msg:
	.ascii 	"** Greeter ** \ nPor favor ingrese su nombre:"
msgLen = . - msg
msg2:
	.ascii 	"Hola"
msg2Len = . - msg2

.sección 	.texto
.globl 	_start
_comienzo:

mov r0, $ 1 		    @ mensaje de apertura del programa de impresión	
ldr r1, = mensaje
ldr r2, = msgLen
mov r7, $ 4
svc $ 0

mov r7, $ 3 		    @ read syscall
mov r0, $ 1		
ldr r1, = búfer
mov r2, $ 0x30
svc $ 0

mov r0, $ 1 		    @ imprimir msg2
ldr r1, = msg2
ldr r2, = msg2Len
mov r7, $ 4
svc $ 0

mov r0, $ 1 		    @ ahora imprime la entrada del usuario
ldr r1, = búfer
mov r2, $ 0x30
mov r7, $ 4
svc $ 0

mov r7, $ 1 	            @ salir de syscall
svc $ 0 		            @ wake kernel
.fin
