# 🛡️ CyberTrain v6 — SOC Training Lab

> Herramienta de estudio interactiva para **CompTIA Security+**, **Linux CLI** y **Networking**, con IA local via Ollama y modo examen cronometrado.

[![GitHub Pages](https://img.shields.io/badge/Live-GitHub%20Pages-00f5ff?style=flat-square&logo=github)](https://edwardvarelamariani-bit.github.io/cybersecurity-lab/)
[![Ollama](https://img.shields.io/badge/AI-Ollama%20Local-00ff88?style=flat-square)](https://ollama.com)
[![Security+](https://img.shields.io/badge/CompTIA-Security%2B-b44fff?style=flat-square)](https://www.comptia.org/certifications/security)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

---

## ✨ Características

### 🛡️ Módulo Security+
- **80+ preguntas locales** organizadas en 10 categorías: Fundamentals, Cryptography, Threats, Web Security, Network, IAM, Incident Response, Governance, Frameworks y Hardening
- **Cola pre-generada con Ollama** — mientras respondes una pregunta, la siguiente ya se está generando en background. Latencia cero percibida
- **Categorías rotatorias forzadas** — el cliente controla el tema en cada prompt, garantizando variedad real sin depender del modelo
- **Modo PRACTICE** — preguntas ilimitadas con explicación técnica detallada tras cada respuesta
- **Modo EXAM ⏱** — 20 preguntas / 45 minutos con cronómetro, barra de progreso y sin explicaciones intermedias (simula Pearson VUE)
- **Pantalla de resultados** — puntuación final, veredicto PASS/FAIL (umbral 75%), desglose por categoría con barras de color y detección automática de áreas de mejora
- **Shortcuts de teclado** — `A` `B` `C` `D` para responder, `Enter`/`Space` para siguiente

### 🐧 Módulo Linux CLI
- Simulador de terminal embebido con 100+ comandos
- Misiones progresivas con hints y reveal
- Contexto del entorno de laboratorio real

### 🌐 Módulo Networking
- Calculadora de subnetting interactiva con explicación paso a paso
- Quiz de puertos y protocolos
- Topologías de red con preguntas visuales

---

## 🚀 Uso

### Opción 1 — GitHub Pages (sin instalación)
Accede directamente en el navegador:
```
https://edwardvarelamariani-bit.github.io/cybersecurity-lab/
```
Funciona sin Ollama — usa el banco de preguntas local automáticamente.

### Opción 2 — Con Ollama (IA local, preguntas infinitas)

**Requisitos:**
- [Ollama](https://ollama.com) instalado
- Modelo descargado: `gemma3:1b` (rápido) o `qwen2.5-coder:7b` (más preciso)

**Arrancar Ollama con CORS habilitado:**
```bash
OLLAMA_ORIGINS="*" ollama serve
```

**Descargar modelo si no lo tienes:**
```bash
ollama pull gemma3:1b
```

Abre `index.html` en el navegador — el indicador cambiará a 🟢 **OLLAMA ONLINE** y aparecerá el selector de modelos disponibles.

---

## 🏗️ Arquitectura

```
index.html (single-file app)
│
├── CSS embebido          — diseño cyberpunk dark, Orbitron + Share Tech Mono
├── HTML                  — 3 paneles: Security+, Linux CLI, Networking
└── JavaScript embebido
    ├── Banco local        — 80 preguntas JSON hardcoded (sin dependencias)
    ├── Cola async         — pre-genera 5 preguntas en background via Ollama
    ├── callOllama()       — wrapper con deduplicación, seed aleatorio, reintentos
    ├── Modo Exam          — timer, tracking por categoría, pantalla de resultados
    └── Keyboard handler   — atajos A/B/C/D + Enter/Space
```

**Sin backend. Sin base de datos. Sin dependencias npm.** Un solo fichero HTML que funciona abriéndolo directamente o sirviendo desde cualquier servidor estático.

---

## 📊 Categorías Security+

| Categoría | Descripción |
|-----------|-------------|
| FUNDAMENTALS | CIA triad, MFA, controles, Zero Trust |
| CRYPTOGRAPHY | AES, RSA, PKI, TLS, hashing |
| THREATS | Malware, phishing, APT, supply chain |
| WEB SECURITY | OWASP Top 10, XSS, SQLi, CSRF |
| NETWORK | Firewalls, IDS/IPS, protocolos, ataques de red |
| IAM | RBAC, SAML, OAuth, PAM, Kerberos |
| IR | Fases IR, forense digital, cadena de custodia |
| GOVERNANCE | ISO 27001, GDPR, ENS, gestión de riesgos |
| FRAMEWORKS | MITRE ATT&CK, NIST CSF, Cyber Kill Chain |
| HARDENING | Patch management, CIS Benchmarks, bastionado |

---

## 🛠️ Stack técnico

- **Frontend**: HTML5 + CSS3 + JavaScript vanilla (sin frameworks)
- **Fuentes**: Google Fonts — Orbitron, Share Tech Mono, Rajdhani
- **IA local**: [Ollama](https://ollama.com) con modelos `gemma3:1b` / `qwen2.5-coder:7b`
- **Deploy**: GitHub Pages (estático, sin build step)

---

## 📁 Contexto del proyecto

Este proyecto forma parte del **laboratorio de ciberseguridad** desarrollado durante el **IFCT0109 — Certificado de Profesionalidad Nivel 3 (Seguridad Informática)**, orientado a preparación para rol de **SOC Analyst / Blue Team**.

Repositorio principal del lab: [cybersecurity-lab](https://github.com/edwardvarelamariani-bit/cybersecurity-lab)

---

## 📄 Licencia

MIT — libre para uso educativo y personal.

---

<div align="center">
  <sub>Built by <a href="https://github.com/edwardvarelamariani-bit">Edward Varela</a> · IFCT0109 · Alicante, España</sub>
</div>
