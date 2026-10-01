# Bitacora de tecnicas avanzadas
Laboratorio 07: Tecnicas Avanzadas de Prompting.
Herramienta de IA usada: (escribe aqui cual usaste)
## Ejercicio 2: Zero-shot, one-shot y few-shot
Tipo | Aciertos (de 5) | Formato de la respuesta | Todas con el mismo formato  (Si/No) |
|------|-----------------|-------------------------|-----------------------------------|
| Zero-shot |SI|NO|NO|
| One-shot |SI|SI|SI|
| Few-shot |SI|SI|SI|

## Ejercicio 3: Chain of Thought
| Pedido | Respuesta de la IA | Muestra los pasos (Si/No) | Correcta (Si/No) |
|--------|--------------------|---------------------------|------------------|
| Directo |SI |NO |SI |
| Paso a paso |SI |SI |SI |

## Ejercicio 4: Role prompting
| Version | Vocabulario (sencillo/tecnico) | Usa ejemplos o codigo | A quien les irve mas |
|---------|-------------------------------|-----------------------|----------------------|
| A. Sin rol |TECNICO |CODIGO | NO|
| B. Rol docente |SENCILLO |EJEMPLOS |SI |
| C. Rol senior |SENCILLO |CODIGO |NO |

## Ejercicio 5: Descomposicion
- Paso 1 (requisitos): (que te entrego la IA)
- Paso 2 (diseno de clases): (que te entrego la IA)
- Paso 3 (codigo de Producto): (que te entrego la IA; si compilaste con `javac Producto.java`, anota si compilo)
- Paso 4 (3 mejoras): (que te entrego la IA)
- Comparacion con el pedido de una sola vez: (ej: el pedido unico fue generico/muy largo; por pasos fue coherente y pude revisar cada parte)
## Ejercicio 6: Prompt estructurado y autocritica
¡Excelente observación! Como analista de pruebas, tienes toda la razón. Es fundamental validar las reglas de negocio preliminares y los datos de frontera (Boundary Value Analysis / Equivalence Partitioning) antes de procesar el intento de inicio de sesión en el servidor. Esto evita llamadas innecesarias a la base de datos y asegura que el sistema maneje correctamente los errores de formato.
A continuación, presento la tabla actualizada. He agregado 4 nuevos casos de prueba (del CP-07 al CP-10) para cubrir estos escenarios límite y de formato.
Tabla de Casos de Prueba (Actualizada)
ID	Escenario	Datos de Entrada	Resultado Esperado
CP-01	Login exitoso con credenciales válidas.	Correo: usuario@test.com
Contraseña: Pass123!	El sistema permite el ingreso y redirige al Dashboard principal.
CP-02	Primer intento fallido (Contraseña incorrecta).	Correo: usuario@test.com
Contraseña: Incorrecta1	Mensaje de error: "Credenciales incorrectas". Permite reintentar. El contador de intentos sube a 1.
CP-03	Segundo intento fallido consecutivo.	Correo: usuario@test.com
Contraseña: Incorrecta2	Mensaje de error: "Credenciales incorrectas". El contador de intentos sube a 2.
CP-04	Tercer intento fallido (Bloqueo de cuenta).	Correo: usuario@test.com
Contraseña: Incorrecta3	Mensaje de error: "Cuenta bloqueada tras 3 intentos fallidos. Contacte a soporte o restablezca su contraseña".
CP-05	Intento de login en cuenta ya bloqueada.	Correo: usuario@test.com
Contraseña: Pass123! (Válida)	No permite el ingreso. Mensaje: "Esta cuenta se encuentra bloqueada".
CP-06	Reset de contador tras éxito al segundo intento.	Intento 1: Contraseña incorrecta
Intento 2: Pass123! (Válida)	El sistema permite el ingreso. El contador de intentos fallidos se restablece a 0.
CP-07	[Nuevo] Intento de inicio de sesión con campos vacíos.	Correo: (Vacío)
Contraseña: (Vacío)	El sistema no envía la solicitud. Muestra alertas visuales inline: "El correo es requerido" y "La contraseña es requerida".
CP-08	[Nuevo] Formato de correo inválido (sin arroba o sin dominio).	Correo: usuariotest.com
Contraseña: Pass123!	Bloqueo en el cliente o error de validación: "Por favor, introduce una dirección de correo válida".
CP-09	[Nuevo] Contraseña que contiene espacios en blanco.	Correo: usuario@test.com
Contraseña: "Pass 123 !"	El sistema debe procesar los espacios como caracteres válidos (o recortar espacios al inicio/final según la política de la empresa). Si no coincide con la guardada, cuenta como intento fallido.
CP-10	[Nuevo] Sensibilidad a mayúsculas en la contraseña.	Correo: usuario@test.com
Contraseña: PASS123! (Original es Pass123!)	El sistema la reconoce como incorrecta. Muestra error de credenciales y suma 1 intento fallido (la contraseña debe ser case-sensitive).
🔍 Casos específicos que se agregaron:
1. CP-07 (Campos vacíos): Valida que el sistema detenga la ejecución y no consuma recursos del servidor si el usuario no interactúa con los campos obligatorios.
2. CP-08 (Correo sin @ o formato inválido): Asegura que la validación de sintaxis (Regex) del lado del cliente funcione correctamente antes de disparar el evento de autenticación.
3. CP-09 (Contraseña con espacios): Es una vulnerabilidad común. Se prueba para verificar si el sistema "recorta" (trim) los espacios por error, lo cual alteraría la contraseña real del usuario, o si los acepta correctamente como caracteres especiales.
4. CP-10 (Sensibilidad a mayúsculas): Una validación crítica de seguridad para confirmar que Pass123! y PASS123! se manejen como cadenas de texto distintas.
¿Qué te parece esta cobertura para la fase de pruebas unitarias o de integración? Si lo deseas, podemos:
1. Definir la estrategia de desbloqueo (por ejemplo, si la cuenta se desbloquea automáticamente después de 15 minutos o mediante un enlace de correo).
2. Diseñar casos de prueba enfocados en la seguridad, como inyección SQL en los campos de entrada.
3. Escribir los pasos de ejecución detallados (Test Steps) para uno de estos escenarios.
Dime el número de la opción que prefieras para continuar.

|   REVISAR | CUMPLE (SI/NO) |
|-----------|----------------|
|¿Tiene las 4 columnas pedidas?|SI|
|¿Incluye el bloqueo después de 3 intentos?|SI|
|¿Indica qué casos agregó en la autocrítica?|SI|
|¿Hay algún caso repetido o que no tenga sentido?|SI|