# Tecnológico de Software
- **Arquitectura de Software**
- **Alumno:** Euruviel Marquez Martinez
- **Docente:** Jorge Javier Pedrozo Romero
- **Fecha:** 19/06/2026
- **Actividad:** Actividad #22 – Práctica .NET: API REST con ASP.NET Core Web API

---

## Descripción

**CitasMédicas** es una aplicación web desarrollada con **ASP.NET Core MVC** y extendida con una **API REST** construida sobre una arquitectura hexagonal (Ports & Adapters). Permite gestionar un sistema de citas médicas tanto desde una interfaz web (MVC) como desde cualquier cliente HTTP (Postman, PowerShell, aplicación móvil, navegador).

El proyecto demuestra cómo la arquitectura hexagonal permite **agregar un nuevo cliente** (la API REST) sin modificar el dominio ni la infraestructura existente, únicamente añadiendo una capa de servicios de aplicación y un nuevo proyecto de presentación.

---

## Arquitectura

El proyecto sigue una estructura **hexagonal multi-proyecto** con cinco capas:

```
CitasApp.sln
├── CitasApp.Domain/           
│   ├── Models/
│   │   ├── Paciente.cs
│   │   ├── Medico.cs
│   │   ├── Cita.cs
│   │   └── CitaJson.cs
│   └── Interfaces/
│       ├── IPacienteRepository.cs
│       ├── IMedicoRepository.cs
│       └── ICitaRepository.cs
│
├── CitasApp.Infrastructure/   
│   └── Repositories/
│       ├── JsonPacienteRepository.cs
│       ├── JsonMedicoRepository.cs
│       ├── JsonCitaRepository.cs
│       ├── CsvPacienteRepository.cs
│       ├── CsvMedicoRepository.cs
│       ├── CsvCitaRepository.cs
│       ├── SqlitePacienteRepository.cs
│       ├── SqliteMedicoRepository.cs
│       └── SqliteCitaRepository.cs
│
├── CitasApp.Application/      
│   └── Services/
│       ├── PacienteService.cs
│       ├── MedicoService.cs
│       └── CitaService.cs
│
├── CitasApp.Web/              
│   ├── Controllers/
│   ├── Views/
│   └── data/
│
└── CitasApp.Api/              
    ├── Controllers/
    │   ├── PacientesController.cs
    │   ├── MedicosController.cs
    │   ├── CitasController.cs
    │   └── CalculadoraController.cs
    ├── data/
    │   ├── pacientes.json
    │   ├── medicos.json
    │   └── citas.json
    └── Program.cs
```

## Endpoints disponibles

### Citas médicas

| Método | Ruta | Descripción |
|---|---|---|
| GET | `/api/pacientes` | Lista todos los pacientes |
| GET | `/api/pacientes/{id}` | Obtiene un paciente por ID |
| GET | `/api/medicos` | Lista todos los médicos |
| GET | `/api/medicos/{id}` | Obtiene un médico por ID |
| GET | `/api/citas` | Lista todas las citas |
| GET | `/api/citas/porpaciente/{pacienteId}` | Citas de un paciente específico |

### Calculadora

| Método | Ruta | Descripción |
|---|---|---|
| GET | `/api/calculadora/sumar?a={n}&b={n}` | Suma dos números |
| GET | `/api/calculadora/restar?a={n}&b={n}` | Resta dos números |
| GET | `/api/calculadora/multiplicar?a={n}&b={n}` | Multiplica dos números |
| GET | `/api/calculadora/dividir?a={n}&b={n}` | Divide dos números (valida división entre cero) |

---

## Tecnologías utilizadas

| Tecnología | Versión | Uso |
|---|---|---|
| C# | 13 | Lenguaje principal |
| ASP.NET Core MVC | .NET 10 | Cliente web (CitasApp.Web) |
| ASP.NET Core Web API | .NET 10 | Cliente REST (CitasApp.Api) |
| JSON | — | Adaptador de persistencia activo |
| CSV | — | Adaptador de persistencia alternativo |
| SQLite | 10.0.9 | Adaptador de persistencia alternativo |
| Git + GitHub | — | Control de versiones |
| HTML + JavaScript (fetch) | — | Cliente web externo para pruebas |

---

## Adaptadores de datos

El sistema soporta 3 fuentes de datos intercambiables desde `Program.cs` de cada proyecto cliente:

| Bloque | Adaptador | Archivos |
|---|---|---|
| Bloque A (activo) | JSON | `pacientes.json`, `medicos.json`, `citas.json` |
| Bloque B | CSV | `pacientes.csv`, `medicos.csv`, `citas.csv` |
| Bloque C | SQLite | `citasapp.db` |

Para cambiar de adaptador solo se descomenta el bloque correspondiente en `Program.cs`. **Los controllers, servicios y el dominio nunca cambian.**

---

## Patrones y principios aplicados

| Principio | Aplicación |
|---|---|
| **Arquitectura Hexagonal** | Domain, Application, Infrastructure, Web y Api separados en proyectos independientes |
| **Ports & Adapters** | Las interfaces son los puertos; los repositorios JSON/CSV/SQLite son los adaptadores |
| **Capa de Aplicación** | `PacienteService`, `MedicoService` y `CitaService` encapsulan la lógica de negocio entre los controllers y los repositorios |
| **Patrón Repositorio** | Interfaces desacoplan el acceso a datos del resto del sistema |
| **Inyección de dependencias** | Repositorios y servicios registrados en `Program.cs` como `AddScoped` |
| **SRP** | Cada controller maneja una sola entidad |
| **DIP** | Los controllers dependen de servicios/interfaces, nunca de implementaciones concretas |


---

## Cómo ejecutar

1. Clona el repositorio y cambia a la rama `Api`:
```bash
git checkout Api
```

2. Abre `CitasApp.sln` en Visual Studio 2022+.

3. Establece `CitasApp.Api` como proyecto de inicio (clic derecho → Establecer como proyecto de inicio).

4. Presiona **F5** para ejecutar. La API estará disponible en:
   - HTTP: `http://localhost:5067`
   - HTTPS: `https://localhost:7053`

5. Prueba los endpoints con PowerShell:
```powershell
(iwr "http://localhost:5067/api/pacientes").Content
(iwr "http://localhost:5067/api/calculadora/sumar?a=28&b=32").Content
```

---
