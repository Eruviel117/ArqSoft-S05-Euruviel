# Code Smells identificados — CitaService

## Smell 1: God Class (tendencia)

**Qué es:** `CitaService` (en `CitasApp.Application/Services/CitaService.cs`) no solo
maneja citas — también expone `ValidarPaciente()` y `ValidarMedico()`, que son
responsabilidades de `PacienteService` y `MedicoService` (ya existen en el proyecto).

**Por qué existe:** decisión accidental — cuando se agregó el Observer para
notificar citas confirmadas, fue más rápido inyectar los repositorios directo
que reutilizar los servicios ya creados.

**Costo de no pagarla:** cada nueva regla de negocio de Paciente o Medico
tendría que duplicarse en CitaService para mantenerlo "autosuficiente",
haciendo que la clase crezca sin límite.

**Propuesta de solución:** Dependency Injection — inyectar `PacienteService`
y `MedicoService` en `CitaService` en vez de `IPacienteRepository` e
`IMedicoRepository` directos.

## Smell 2: Tight Coupling

**Qué es:** `CitaService` depende directamente de `IPacienteRepository` e
`IMedicoRepository` — dos repositorios completos — solo para llamar un método
(`ObtenerPorId`) que ya está resuelto por los servicios de aplicación
correspondientes.

**Por qué existe:** mismo origen que el smell 1 — acoplarse al repositorio
fue el camino corto en el momento.

**Costo de no pagarla:** si mañana cambia la forma de validar un paciente
(ej. se agrega una regla de negocio en `PacienteService`), `CitaService`
seguiría usando la validación vieja porque no pasa por ese servicio.

**Propuesta de solución:** misma técnica — Dependency Injection de los
servicios de aplicación en vez de los repositorios.