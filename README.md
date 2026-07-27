# 🚀 Portfólio de Projetos - Alex Alves

Bem-vindo ao meu portfólio público! Este repositório centraliza a documentação, arquitetura e destaques técnicos dos principais projetos que desenvolvi e mantenho. Cada projeto representa um domínio diferente — desde ERPs fiscais complexos até sistemas de monitoramento de baixo nível em Go — demonstrando versatilidade em **Full Stack**, **DevOps**, **Arquitetura de Software** e **Segurança da Informação**.

---

## 📋 Índice
1. [Guard360](#-guard360---plataforma-de-gestão-de-segurança-patrimonial)
2. [MeuCondominio](#-meucondominio---sistema-de-gestão-inteligente-para-condomínios)
3. [WebVendas](#-webvendas---erp-pdv-com-fiscalização-nativa-brasileira)
4. [FazendeiroPRO](#-fazendeiropro---erp-saas-agropecuário-multi-tenant)
5. [OnlineMonitor](#-onlinemonitor---serviço-windows-em-go-para-sincronização-tjgo)

---

## 🛡️ Guard360 - Plataforma de Gestão de Segurança Patrimonial

Sistema completo para monitoramento de rondas, vigilantes, checkpoints (QR Code/NFC), incidentes e relatórios em tempo real. Arquitetura **Multi-Tenant** com isolamento de dados por empresa.

### � **Produção:** https://guard360security.com/

### �🏗️ Arquitetura
- **Backend:** Laravel 10 (PHP 8.2) + MySQL + JWT (Stateless Auth)
- **Frontend (Dashboard Admin):** PHP Puro (SSR) + Tailwind CSS (CDN) + Leaflet.js (Mapas) + ApexCharts
- **Mobile (Vigilantes):** React Native (Expo SDK 54) + Expo Router + NativeWind (Tailwind v4) + SQLite Local (Offline-First) + Firebase Push Notifications

### 🔑 Destaques Técnicos
- **Offline-First Mobile:** Persistência local via `expo-sqlite` com fila de sincronização bidirecional automática (background sync a cada 15 min).
- **Segurança:** Rate Limiting, Headers OWASP (CSP, HSTS, X-Frame-Options), Sanitização de inputs, Validação de Licença via Hardware ID.
- **Tempo Real:** Rastreamento GPS de patrulhas ativas no mapa (Leaflet) com WebSockets/Polling.
- **Multi-Tenancy:** Isolamento de dados por `company_id` em todas as queries (Shared Database, Shared Schema).

### 📸 Screenshots
| Dashboard | Mapa de Rondas | Mobile - Checkpoint |
| :---: | :---: | :---: |
| ![Dashboard](guard360/dashboard.png) | ![Mapa](guard360/map.png) | ![Mobile](guard360/mobile_checkpoint.png) |

> **Repositórios Privados:** `guard360-backend`, `guard360-dashboard-php`, `guard360-mobile`

---

## 🏢 MeuCondominio - Sistema de Gestão Inteligente para Condomínios

Plataforma robusta para gestão condominial com foco em **portaria inteligente** (leitura de QR Code/Code 128), multi-tenancy estrito, reservas, financeiro e comunicação.

### � **Produção:** https://meucondominio.app.br/

### �🏗️ Arquitetura
- **Backend:** FastAPI (Python 3.11+) + SQLModel (SQLAlchemy + Pydantic) + MySQL 8.0 / PostgreSQL
- **Frontend:** React 19 + Vite 7 + Tailwind CSS v4 + Lucide React + Recharts
- **Auth:** JWT (Access/Refresh Tokens) + Bcrypt + Rate Limiting (5 req/min login)

### 🔑 Destaques Técnicos
- **Portaria Avançada:** Scanner universal (HTML5-QRCode) com parsing inteligente de transportadoras (Amazon, Correios, Loggi, Mercado Livre) e preenchimento automático de Bloco/Unidade/Morador.
- **Multi-Tenancy Rigoroso:** Isolamento por `condominio_id` em **todas** as tabelas e queries (RLS-like via ORM).
- **IA Integrada:** Módulo `/api/ia` para classificação de comunicados, sugestão de respostas e análise de sentimento em assembleias.
- **Documentos & Exportação:** Geração de PDFs (Relatórios, Atas, Boletos) e Excel (Exportação LGPD).

### 📸 Screenshots
| Portaria - Scanner | Dashboard Financeiro | Gestão de Moradores |
| :---: | :---: | :---: |
| ![Portaria](meucondominio/portaria_scanner.png) | ![Financeiro](meucondominio/financeiro.png) | ![Moradores](meucondominio/moradores.png) |

> **Repositórios Privados:** `meucondominio-backend`, `meucondominio-frontend`

---

## 🛒 WebVendas - ERP/PDV com Fiscalização Nativa Brasileira

ERP completo para varejo/serviços com **PDV (Frente de Caixa)**, estoque, financeiro, compras, fiscal (NFe/NFCe/SAT/MDFe) e contabilidade. Projetado para legislação brasileira (SEFAZ).

### � **Produção:** https://www.webvendas.guard360security.com/

### �🏗️ Arquitetura
- **Backend:** FastAPI + SQLAlchemy 2.0 + PostgreSQL (Prod) / SQLite (Dev) + PyNFe (Assinatura XML)
- **Frontend:** Vue 3 + Vite + Tailwind CSS v4 + Axios + Vue Router + Vue Toastification
- **Infra:** HTTPS Local (Certificados autoassinados dinâmicos) + Uvicorn/Gunicorn + Docker Ready

### 🔑 Destaques Técnicos
- **Motor Fiscal Próprio:** Geração, assinatura (A1/A3), transmissão, contingência (SVC-AN/FS-DA) e impressão DANFE/NFCe/DAMDFE.
- **PDV Offline-First:** Operação contínua sem internet com sincronização posterior de vendas e NFCe em contingência.
- **Multi-Empresa/Estabelecimento:** Suporte a múltiplos CNPJs, séries, certificados e ambientes (Homologação/Produção) na mesma instância.
- **Conciliação Bancária:** Importação OFX/CSV, matching automático de lançamentos.
- **Segurança:** JWT duplo (Header + HttpOnly Cookie), CSP estrito, Rate Limit, Auditoria de Ações (Log estruturado).

### 📸 Screenshots
| PDV (Frente de Caixa) | Emissão NFe | Dashboard Gerencial |
| :---: | :---: | :---: |
| ![PDV](webvendas/pdv.png) | ![NFe](webvendas/nfe.png) | ![Dashboard](webvendas/dashboard.png) |

> **Repositórios Privados:** `webvendas-backend`, `webvendas-frontend`

---

## 🐄 FazendeiroPRO - ERP SaaS Agropecuário Multi-Tenant

Plataforma SaaS de alta performance para gestão operacional, financeira, sanitária e genética de fazendas (Bovinos, Equinos, Ovinos, Caprinos). **Zero-Trust**, **Offline-First (PWA)**, **IA Generativa (Text-to-SQL)**.

### � **Produção:** https://fazendeiro.guard360security.com/

### �🏗️ Arquitetura
- **Backend:** FastAPI (Async) + SQLAlchemy 2.0 (AsyncPG) + **PostgreSQL RLS (Row Level Security)** + Alembic + Celery/Redis
- **Frontend:** React 19 + Vite 8 + Tailwind CSS v4 + Framer Motion + TanStack Query + Leaflet (Mapas) + Recharts
- **IA:** LangChain + OpenAI/Gemini/Groq (Agente Text-to-SQL com RLS, Assistente Agro, OCR Notas Fiscais)
- **Mobile/PWA:** Vite PWA Plugin + Workbox + IndexedDB (idb) + Background Sync API

### 🔑 Destaques Técnicos
- **Segurança Nível Industrial (Zero-Trust):**
  - **PostgreSQL RLS Nativo:** Isolamento físico de dados no banco (`tenant_id` + Policies). Impossível vazar dados entre tenants mesmo com bug no backend.
  - **HttpOnly Cookies + SameSite=None + Secure:** Zero tokens no LocalStorage (Mitigação total de XSS).
  - **SlowAPI (Rate Limit), TrustedHost, CSP, HSTS, GZip.**
  - **LGPD Ready:** Soft Delete (`deleted_at`), Anonimização (Direito ao Esquecimento), Exportação JSON (Portabilidade).
- **Arquitetura Offline-First Real:** PWA instalável, IndexedDB para leitura/escrita offline, Fila de mutações (POST/PUT/DELETE) sincronizada automaticamente ao reconectar.
- **IA Generativa Integrada:**
  - **Text-to-SQL Seguro:** Gera SQL filtrado automaticamente pelo `tenant_id` da sessão.
  - **Assistente Agro:** Contexto de manejo, sanidade, nutrição, genética.
  - **OCR Fiscal:** Leitura de XML NFe/NFCe para lançamento automático de custos.
- **Design System "Agronomist Elite":** Glassmorphism, Tokens CSS (HSL), Dark/Light Mode nativo, Animações Framer Motion, Tipografia Space Grotesk/Inter.

### 📸 Screenshots
| Dashboard Executivo | Manejo de Pastos (Mapa) | IA - Text-to-SQL | PWA Mobile |
| :---: | :---: | :---: | :---: |
| ![Dashboard](fazendeiropro/dashboard.png) | ![Pastos](fazendeiropro/pastos_mapa.png) | ![IA](fazendeiropro/ia_sql.png) | ![PWA](fazendeiropro/pwa_mobile.png) |

> **Repositórios Privados:** `fazendeiropro-backend`, `fazendeiropro-frontend`

---

## ⚙️ OnlineMonitor - Serviço Windows em Go para Sincronização TJGO

Serviço híbrido (Background Service + GUI) nativo em **Go 1.22** para integração de Cartórios com o Portal Extrajudicial do TJGO (Selo Digital, Envio de Atos, Cancelamento de Lotes). Roda como **Windows Service** nativo (SCM).

### � **Produção:** Em operação em cartórios parceiros (on-premise)

### �🏗️ Arquitetura
- **Linguagem:** Go 1.22 (Compilação nativa, single binary ~15MB)
- **GUI:** `lxn/walk` (Win32 API Wrapper) - Interface nativa Windows com Common Controls v6 (Manifest).
- **Banco:** SQL Server (T-SQL) via `go-mssqldb` - Conexão via arquivo `Conexao.md` (INI).
- **Comunicação:** HTTP/REST + mTLS (Certificados A1/A3) com API TJGO.
- **Logs:** Arquivo rotativo (`Logs/MonitorLog.log`) + Event Viewer (Service).
- **Deploy:** `InstalarServico.bat` / `DesinstalarServico.bat` (Admin) + Assinatura de Código (Code Signing).

### 🔑 Destaques Técnicos
- **Modo Híbrido Inteligente:** Detecta automaticamente se roda como Serviço (SCM) ou Interativo (GUI/Console) via `golang.org/x/sys/windows/svc`.
- **Resiliência de Rede:** Retry exponencial, Timeout configurável, Validação de Certificado TLS customizada.
- **Cancelamento Inteligente de Lotes:** Lógica complexa para cancelar apenas lotes 100% não utilizados (unitário ou em massa `-cancel-all-unused`).
- **Configuração Dinâmica 100% Banco:** URL da API, Credenciais, Intervalo de Sync, SMTP, Hash de Acesso — tudo lido do SQL Server a cada ciclo (Zero Hardcode).
- **Observabilidade:** Logs estruturados, Health Check HTTP, Métricas de Sincronização (Sucesso/Falha/Latência).

### 📸 Screenshots
| GUI - Painel Principal | Logs em Tempo Real | Instalação como Serviço |
| :---: | :---: | :---: |
| ![GUI](onlinemonitor/gui_main.png) | ![Logs](onlinemonitor/gui_logs.png) | ![Service](onlinemonitor/service_install.png) |

> **Repositório Privado:** `onlinemonitor-go`

---

## 🛠️ Stack Tecnológica Consolidada

| Categoria | Tecnologias Dominantes |
| :--- | :--- |
| **Backend (API)** | **FastAPI (Python)**, **Laravel (PHP)**, **Go** |
| **Frontend (Web)** | **React 19**, **Vue 3**, **PHP (SSR)**, **Tailwind CSS v4** |
| **Mobile** | **React Native (Expo)**, **NativeWind (Tailwind)**, **SQLite Local** |
| **Banco de Dados** | **PostgreSQL (RLS)**, **MySQL**, **SQL Server**, **SQLite** |
| **ORM/ODM** | **SQLAlchemy 2.0 / SQLModel**, **Eloquent**, **GORM** |
| **Auth & Segurança** | **JWT (HttpOnly Cookies)**, **Bcrypt**, **OWASP Headers**, **Rate Limiting**, **RLS** |
| **IA / LLM** | **LangChain**, **OpenAI (GPT-4o)**, **Google Gemini**, **Groq**, **Text-to-SQL (RLS Safe)** |
| **DevOps / Infra** | **Docker**, **GitHub Actions**, **Nginx**, **Systemd/Windows Services**, **HTTPS Local (mkcert)** |
| **Qualidade** | **ESLint**, **PHPStan/Psalm**, **Go Vet**, **Pytest**, **PHPUnit**, **Conventional Commits** |

---

## 📫 Contato

- **GitHub:** [@AlexAlves100](https://github.com/AlexAlves100)
- **LinkedIn:** [Alex Alves](https://linkedin.com/in/alexalves100)
- **E-mail:** alex_alves100@hotmail.com

---

> *Este portfólio é um documento vivo. Projetos privados podem ter repositórios abertos mediante solicitação para avaliação técnica.*