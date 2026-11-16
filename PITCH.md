# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: Un agente de atención al cliente por chat para vuelos interrumpidos, sobre la API de Mensajes de Claude, con las nueve herramientas de Larkspur más dos añadidas, next_available_day y fare_rules, servidas por MCP desde un servidor independiente (support/mcp_server.py).
Does: Busca la reserva, comprueba el estado real del vuelo, determina lo que Larkspur debe al cliente según la política, busca opciones de reubicación y emite un vale de comida cuando corresponde; responde a "¿cuándo puedo volar?" con el primer día con asiento libre; y deriva una reserva de grupo (G2HL9V) al Group Desk en lugar de gestionarla.
Number: Los tokens que Claude leyó en los cinco tickets pasaron de 70.138 (Build 1) a 86.574 (Build 2, con las dos herramientas por MCP), es decir, de unos 14.028 a 17.315 tokens por ticket. Es un solo run por build, así que parte de la subida es variación entre ejecuciones. Solo la lista de herramientas pasó de 2.749 a 2.844 tokens por turno (contado en el cable).
Safety check: confirm_rebooking no se llamó en ninguno de los cinco runs, y su descripción dice que exige un token que solo produce el clic de Confirmar del propio cliente. Lo vimos en los trace (las llamadas a herramientas de cada ticket), no intentando forzarlo.
Next: Hacer que next_available_day funcione para un grupo entero: hoy responde solo para un pasajero, así que con un grupo puede dar una fecha con asientos insuficientes.
Still broken: El ticket del cliente abusivo con amenaza legal (R8KD3F) se responde como cualquier otro, con un vale de comida, sin escalar y sin cambiar el tono. Todavía nada comprueba cómo trata el agente el enfado.
Lever: <cost | speed | intelligence>

## Priya asked

Costs:
Wrong:
Runs it:
Left out:
