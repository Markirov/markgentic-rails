# Agentic Harness — Arnés de Agentes IA Distribuible y Versionado

> De 2-4h de setup a 15-25min. 7 proyectos sincronizados. 25 releases en ~1 mes (v1.0 → v3.4.1).

Sistema propio para orquestar agentes IA de forma robusta, repetible y segura. Núcleo canónico versionado con semver, distribuible a cualquier proyecto, con flujo bidireccional de mejoras.

## Problema
Cada proyecto con IA empezaba de cero. Prompts distintos, roles mal definidos, tracking inexistente o diferente. Cuando mejoraba algo en un proyecto, esa mejora se quedaba allí.

## Solución — Núcleo canónico

### 1. Protocolo y contexto
- `AGENTS.md` común con reglas de sesión, gobernanza y nomenclatura de IDs
- Punteros `CLAUDE.md`, `GEMINI.md` → funciona con cualquier IA (Claude Code, Antigravity, Gemini)

### 2. Roles (5)
- **Arquitecto** - diseño de sistema y decisiones técnicas
- **Lead Developer** - implementación
- **QA Auditor** - auditoría en frío y calidad
- **Product Owner** - priorización y SPEC
- **Data Specialist** - modelado de datos y métricas
> Cada rol tiene reglas y agentes generados para Claude Code y Antigravity.

### 3. Skills
- Desarrollo guiado por SPEC (`/sdd`) — SPEC→PLAN como contrato
- Auditoría en frío
- Onboarding de sesión
- Diseño frontend y buenas prácticas React

### 4. Guardrails
- Hook pre-commit
- `verify.sh` por proyecto
- 14 comprobaciones ejecutables (`harness check`)
- Defensa prompt injection: instrucciones externas = datos

### 5. Tracking estándar
`DONE`, `PENDING`, `STATE`, `IDEAS`, `AUDIT`, `goals` + SPEC→PLAN

### 6. Recetas de sabor
`universal`, `lean`, `grimdark`, `battletech` — adaptan roles al tipo de proyecto.

## Distribución

CLI propio en bash: `harness.sh`

```bash
harness.sh init       # Siembra harness en proyecto nuevo (15-25min)
harness.sh adopt      # Adopta harness en repo existente
harness.sh update     # Actualiza a última versión del core
harness.sh sync-all   # Sincroniza core a los 7 proyectos
harness.sh propose    # Empaqueta mejora del proyecto hacia core
harness.sh check      # 14 checks de integridad
harness.sh agents     # Regenera agentes para Claude/Antigravity
```

- Servidor MCP para operarlo desde el propio agente
- Manifest con hashes: lo que el proyecto personaliza nunca se pisa en silencio
- Rollback automático: si `verify.sh` falla, ese proyecto se revierte y el lote sigue

## Flujo de evolución

```
Core v1.0 → Project A adoption → detecta mejora → harness propose 
→ human review (gate humano) → Core v1.1 → sync-all a 7 proyectos
```

## Resultados

- **7 proyectos** con misma estructura (6 sync automático, 1 grande con revisión manual)
  - Dominios: web apps, Firebase, herramientas de rol y wargames
  - Ejemplos: murodehierrodelsultanato.web.app (Warband Forge), detodounpocoalicante.vercel.app (negocio local 4.5★), darkheresyalicante.space
- **25 versiones** en ~1 mes, v1.0 → v3.4.1, cada una con CHANGELOG y redistribuida
- **Setup:** 2-4h → 15-25min
- **Tokens:** ahorro por contexto acotado, agentes no redescubren proyecto cada sesión

## Stack

Claude Code, Google Antigravity, Gemini, Bash, Git hooks, MCP (Model Context Protocol), Node.js, Firebase, Markdown como contrato (SPEC/PLAN)

## Autor

Perfil híbrido: 15 años comercial tech + técnico PCs/móviles, Excel excelencia, Power BI IBM, constructor de 7 productos web con IA. Formación Harness Engineering LIDR / The Big School.

Alicante — Remoto preferente — Inglés C1 — Valenciano nativo — Carnet B

## Roadmap

- [ ] Publicar harness.sh como open source
- [ ] Dashboard de métricas de sync
- [ ] Receta `data` para proyectos BI
