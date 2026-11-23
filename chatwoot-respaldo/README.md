# Respaldo de Chatwoot

Atiende tus chats de Chatwoot **fuera de horario, como si fueras tú**, con Gemini, y te avisa por Telegram (con llamada en emergencias).

- Cada vendedor entra con su usuario de Chatwoot y tiene su propia configuración, ficha, estilo, horario, llave de Gemini y avisos.
- Solo actúa en chats **asignados a ti**, cuando el último mensaje es del cliente, fuera de tu horario, y después de una **espera al azar de 1 a 7 minutos**.
- Modos: **Apagado**, **Ensayo** (deja lo que respondería como nota privada) y **Automático**.
- Filtros de seguridad: no da precios que no estén en la parte pública de la ficha, no ofrece descuentos ni plazos internos, no confirma citas, no revela instrucciones ni dice que es un bot. Si algo falla, manda una respuesta segura y te avisa.
- **Prioridad** (agendar, pagar, negociar, reclamo): etiqueta `prioridad`, nota privada y Telegram sin sonido.
- **Emergencia** (robo, asalto, vehículo desaparecido): mensaje fijo de contención, etiqueta `urgente`, Telegram con sonido y llamada por Telegram (CallMeBot). Después ya no responde ese chat hasta que una persona conteste.

## Publicarlo (gratis, en Cloudflare)

1. **Bot de Telegram** (una sola vez, para todo el equipo): en Telegram abre **@BotFather** → `/newbot` → ponle nombre → copia el **token**.
2. **Cloudflare**: crea una cuenta gratis en dash.cloudflare.com.
3. En Cloudflare: **Workers & Pages → Create → Import a repository** → conecta GitHub y elige este repositorio → **Deploy**. La base de datos D1 se crea sola.
4. En el Worker: **Settings → Variables and Secrets → Add**:
   - `ENC_KEY` (tipo *Secret*): una clave larga inventada (40+ caracteres al azar). No la cambies después, o habrá que volver a guardar las llaves.
   - `TELEGRAM_BOT_TOKEN` (tipo *Secret*): el token del paso 1.
5. Abre la dirección del Worker (`https://chatwoot-respaldo.<tu-cuenta>.workers.dev`) y entra con tu usuario de Chatwoot.

La variable `CHATWOOT_URL` (en `wrangler.jsonc`) limita el acceso a usuarios de `https://chat.deltatracking.com`.

## Primer uso (cada vendedor)
1. **Horario y reglas**: tu horario de oficina, zona horaria, llave de Gemini (aistudio.google.com → Get API key, con facturación activada) y, opcional, la etiqueta que debe tener el chat (por ejemplo `sk_sv_atencion_humana`).
2. **Ficha y estilo**: revisa la ficha, escribe tus notas internas de negociación y dale **Aprender de mis chats**.
3. **Avisos**: vincula tu Telegram y configura la llamada de emergencia.
4. **Probar**: prueba casos difíciles en el simulador.
5. Activa **Ensayo** una o dos noches, revisa las notas en Chatwoot y luego pasa a **Automático**.

## Límites del plan gratuito
Revisa cada minuto. Atiende hasta ~4 chats por minuto en total (límite de 50 llamadas externas por ejecución del plan gratuito); los demás se atienden el minuto siguiente.
