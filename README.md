# 🛡️ CyberTrain v6
> Herramienta de estudio para SOC analyst junior — CompTIA Security+ · Linux CLI · Networking  
> Edward Varela · Abril 2026

---

## ¿Qué es?

CyberTrain es una aplicación web standalone de estudio para ciberseguridad. No requiere instalación ni servidor — se abre directamente en el navegador. Usa Ollama como motor de IA local para generar preguntas infinitas, con fallback automático a banco de preguntas integrado si Ollama no está disponible.

---

## Uso rápido

```
Abrir index.html en el navegador
```

Sin dependencias. Sin servidor. Sin instalación.

---

## Motor de IA — Ollama

CyberTrain usa **Ollama** corriendo localmente para generar preguntas dinámicas. Si Ollama no está disponible, la app cambia automáticamente al banco de preguntas local integrado (todos los módulos siguen funcionando).

**Modelo:** `qwen2.5-coder:7b`  
**Puerto:** `11434`

### CASO 1 — Abrir el HTML en el mismo equipo donde corre Ollama

Arrancar Ollama con CORS habilitado:

```bash
killall ollama 2>/dev/null; sleep 2
OLLAMA_ORIGINS="*" ollama serve
```

Abrir `index.html` en el navegador del mismo equipo. El indicador mostrará **OLLAMA ONLINE** en verde.

---

### CASO 2 — Abrir el HTML desde otro dispositivo (móvil, otro PC, VM)

El HTML apunta por defecto a `localhost`, que no es accesible desde otros equipos. Hay que hacer dos cosas:

**1. Editar index.html** — al inicio del `<script>`, cambiar:

```javascript
// Antes
const OLLAMA_URL = 'http://localhost:11434';

// Después — poner la IP del equipo donde corre Ollama
const OLLAMA_URL = 'http://192.168.1.XXX:11434';
```

**2. Arrancar Ollama escuchando en red:**

```bash
killall ollama 2>/dev/null; sleep 2
OLLAMA_HOST=0.0.0.0 OLLAMA_ORIGINS="*" ollama serve
```

> `OLLAMA_HOST=0.0.0.0` → escucha en todas las interfaces, no solo localhost  
> `OLLAMA_ORIGINS="*"` → permite las peticiones fetch del navegador (CORS)

Abrir `index.html` desde el dispositivo remoto. ✅

**Verificar que Ollama responde desde red:**
```bash
curl http://192.168.1.XXX:11434/api/tags
```

---

### CASO 3 — GitHub Pages / internet

Cuando el HTML está alojado en GitHub Pages, Ollama **no es accesible** desde internet (es un servicio local). La app usará el fallback automático con el banco de preguntas integrado. Los módulos sin IA (Subnetting, Ports, Topology) funcionan al 100%.

---

### Fallback automático

Si Ollama no responde, el indicador muestra **OLLAMA OFFLINE — usando banco local** en rojo y la app continúa usando preguntas predefinidas. El badge en cada pregunta indica si viene de `🤖 OLLAMA` o `📦 LOCAL`.

---

## Módulos

### 🛡️ SECURITY+
Quiz de CompTIA Security+ con generación infinita de preguntas via Ollama.  
Temas: Threats/Attacks, Cryptography, IAM, Network Security, IR, Governance, MITRE ATT&CK, NIST, ISO 27001, OWASP.

### 🐧 LINUX CLI
10 misiones SOC con terminal simulado integrado. No usa Ollama.  
Cada misión incluye descripción, tarea concreta, pista y solución revelable.

### 🌐 NETWORKING
4 submodos:

| Submodo | Descripción | Motor |
|---|---|---|
| 📡 SUBNETTING | Ejercicios aleatorios: calcula network, mask, broadcast, first/last host, hosts útiles. Incluye guía de cálculo paso a paso para cada red. | Local |
| 🔌 PORTS | Flashcards de puertos conocidos — identifica protocolo o servicio (21, 22, 25, 53, 80, 443, 3389…) | Local |
| 🗺 TOPOLOGY | Diagramas SVG de topologías de red (bus, estrella, anillo, malla, árbol, híbrida). Preguntas sobre tipo de topología y características. | Local |
| ❓ Q&A | Quiz infinito de redes via Ollama — OSI, TCP/IP, routing, VLANs, ACLs, QoS, troubleshooting, seguridad. | Ollama |

---

## Dificultades

| Nivel | Perfil |
|---|---|
| RECRUIT | Conceptos básicos — para empezar |
| ANALYST | Escenarios reales — nivel SOC junior |
| EXPERT | Arquitecturas avanzadas — threat hunting, forense, MITRE |

---

## Gamificación

- Contador Total / Correct / Errors por módulo
- Streak tracker 🔥 (activa desde 3 respuestas correctas seguidas)
- Flash visual ✓ / ✗ al responder

---

> En GitHub Pages Ollama no estará disponible (servicio local), pero todos los módulos sin IA funcionan perfectamente y los módulos con IA usan el banco de preguntas integrado.

---

## Stack técnico

- HTML + CSS + JS vanilla — sin frameworks, sin dependencias externas
- Fuentes: Orbitron, Rajdhani, Share Tech Mono (Google Fonts)
- IA: Ollama API (`/api/generate`) con modelo `qwen2.5-coder:7b`

