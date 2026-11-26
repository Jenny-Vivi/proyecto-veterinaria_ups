# Actividad 1: Definición del Negocio y Análisis Preliminar

## 1. Información General del Negocio (Datos Reales)
* **Nombre Comercial:** Vet San Francisco
* **Giro del Negocio:** Clínica veterinaria de especies mayores y menores, cirugía, diagnóstico por imagen y estética canina.
* **Zona Horaria Oficial:** `America/Guayaquil` (UTC-5).
* **Horario de Atención:** Lunes a sábado de 08:00 a 21:00 (domingos cerrado).
* **Recurso Reservable:** Cada **Médica Veterinaria en turno**,2 veterinarias disponibles; cada una atiende una única cita a la vez.

---

## 2. Catálogo de Servicios 
Para garantizar el cálculo exacto de disponibilidad sin cruces horarios, los servicios reales de *Vet San Francisco* se estructuran en bloques de tiempo fijos:

1. **Consulta Veterinaria (Especies Mayores y Menores)** — Duración: `15 minutos` | Precio base: `$15.00`
2. **Consulta de Especialidad** — Duración: `15 minutos` | Precio base: `$20.00`
3. **Ecografía Diagnóstica** — Duración: `10 minutos` | Precio base: `$40.00`
4. **Cirugía: Esterilización Macho** — Duración: `30 minutos` | Precio base: `$50.00` *(valor referencial sujeto a peso)*
5. **Cirugía: Esterilización Hembra** — Duración: `60 minutos` | Precio base: `$80.00` *(valor referencial sujeto a peso)*
6. **Grooming (Baño y Estética)** — Duración: `60 minutos` | Precio base: `$13.00` *(valor base sujeto a tamaño de mascota)*

*Nota de alcance: El servicio de hospitalización por noche ($20.00) queda fuera del módulo de agendamiento por bloques horarios.*

---

## 3. Recursos Reservables (Personal en Turno)
* **Dra. Nicol Gómez** — Médica Veterinaria (Habilitada para consultas, ecografías, cirugías y grooming).
* **Dra. Marcela Chuchuca** — Médica Veterinaria (Habilitada para consultas, ecografías, cirugías y grooming).

---

## 4. Roles de Usuario y Alcance Funcional

### Visitante (Sin sesión)
* Visualizar el catálogo de servicios activos de *Vet San Francisco* con su duración en minutos y costo base.
* Consultar los horarios disponibles filtrando por servicio, veterinaria en turno y fecha.
* Registrarse como cliente o iniciar sesión.

### Cliente (Autenticado)
* Agendar una reserva seleccionando servicio, veterinaria en turno y bloque horario libre futuro (nace en estado `CONFIRMADA`).
* Visualizar únicamente el historial y las citas próximas propias.
* Cancelar una reserva propia que esté en estado `CONFIRMADA` antes de su hora de inicio (cambia a estado `CANCELADA` y libera el espacio).

### Administrador (Autenticado)
* Gestionar el catálogo de servicios y las veterinarias en turno (crear, editar y activar/desactivar; no eliminar si existen reservas asociadas).
* Configurar los horarios de disponibilidad de cada veterinaria (impidiendo cambios que entren en conflicto con reservas futuras confirmadas).
* Visualizar todas las citas del sistema, cancelar citas confirmadas o marcarlas como `ATENDIDA` una vez cumplida su hora.

---

## 5. Reglas de Negocio y Disponibilidad
1. **Compatibilidad:** El servicio y la veterinaria deben estar activos (`activo = true`) y ser compatibles entre sí.
2. **Validación Temporal:** Toda reserva debe crearse para una fecha/hora futura y caber íntegramente dentro del horario laboral de la veterinaria (`08:00` a `21:00`).
3. **Regla de No Solapamiento:** Una misma veterinaria en turno no puede tener dos citas en estado `CONFIRMADA` que se crucen en el tiempo:
   $$\text{nuevoInicio} < \text{finExistente} \quad \land \quad \text{nuevoFin} > \text{inicioExistente}$$
4. **Inmutabilidad de Estados Finales:** Una cita marcada como `CANCELADA` o `ATENDIDA` no puede volver a modificarse.

---

## 6. Modelo Preliminar de Datos (Cloud Firestore)

| Colección | Atributos Principales |
| :--- | :--- |
| **`usuarios`** | `uid` (ID doc), `nombre`, `email`, `rol` (`'CLIENTE'` \| `'ADMIN'`) |
| **`servicios`** | `id`, `nombre`, `descripcion`, `duracionMinutos`, `precio`, `activo` |
| **`recursos`** | `id`, `nombre`, `especialidad`, `serviciosIds` (array), `activo` |
| **`disponibilidades`** | `id`, `recursoId`, `diaSemana` (1-6), `horaInicio`, `horaFin` |
| **`reservas`** | `id`, `clienteId`, `clienteNombre`, `servicioId`, `servicioNombre`, `recursoId`, `recursoNombre`, `fecha`, `inicio` (Timestamp), `fin` (Timestamp), `estado` (`'CONFIRMADA'` \| `'CANCELADA'` \| `'ATENDIDA'`) |