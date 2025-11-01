# 🌍 KingCountry - Comparação Global de Custo de Vida

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-brightgreen.svg)
![Platform](https://img.shields.io/badge/platform-Android%20%7C%20iOS%20%7C%20Windows%20%7C%20Linux%20%7C%20KMP-green.svg)
![Status](https://img.shields.io/badge/status-Development-yellow.svg)

**Comparação de países/cidades com ~100 itens de custo de vida**  
*Simulações • Comparações • Análise Econômica • Relocação*

[📱 Download](#-download) • [📚 Docs](#-estrutura) • [🚀 Deploy](#-deploy)

</div>

---

## 🎯 ARQUITETURA DO ECOSSISTEMA KING

### Projeto GCP Único Compartilhado
```
Project: kinggroup-website-463104
Project #: 598115153491

✅ Login Único (Firebase Auth) para TODOS os 14 apps King
✅ 1 Cadastro → Acesso a qualquer app (após compra/assinatura)
✅ Dados isolados por app (SEM mistura)
```

### O Que É Compartilhado
- 🔐 **Firebase Auth**: Login único (SSO)
- 👤 **Collection `users`**: Perfil + `apps_access`
- 💳 **Collections `payments`, `subscriptions`**

### O Que É ISOLADO (KingCountry)
- 📊 **8 Firestore Collections**: `kingcountry_*`
- 📦 **Cloud Storage**: `gs://kinggroup-website-463104.appspot.com/kingcountry/` (✅ ESTRUTURA REAL VERIFICADA)
  ```
  gs://kinggroup-website-463104.appspot.com/
  └── kingcountry/                       # ✅ PASTA ISOLADA
      ├── android-native/                # APKs Android
      │   ├── kingcountry-latest.apk     # ← APK principal para download
      │   └── metadata.json              # Metadados das versões
      │
      ├── ios/                           # iOS builds (futuro)
      │
      ├── windows/                       # Windows desktop (futuro)
      │
      ├── linux/                         # Linux desktop (futuro)
      │
      ├── logs/                          # Logs de aplicação
      │
      └── assets/                        # Assets específicos do app
  ```
  **Download URL (quando disponível)**:
  ```
  https://storage.googleapis.com/kinggroup-website-463104.appspot.com/kingcountry/android-native/kingcountry-latest.apk
  ```
- 🚀 **App Engine Service**: `kingcountry`

---

## 🎯 GUIA RÁPIDO PARA DESENVOLVEDORES E IAs

> **📌 Estrutura baseada no template KingRoad GPS | Estrutura REAL verificada**

### 📂 Onde Criar/Modificar Arquivos

**REGRA DE OURO**: Cada pasta do GitHub tem um destino específico no GCP. Sempre crie código na pasta correta:

| Tipo de Código | Onde Criar no GitHub | Deploy Para | Status |
|---------------|---------------------|-------------|--------|
| 📱 **Mobile Android** | `/mobile/` | Cloud Storage (/kingcountry/) | 🚧 Pendente |
| 🍎 **Mobile iOS** | `/apps/ios/` | Cloud Storage (/kingcountry/) | 🚧 Pendente |
| 💻 **Desktop Windows** | `/apps/windows/` | Cloud Storage (/kingcountry/) | 🚧 Pendente |
| 🐧 **Desktop Linux** | `/apps/linux/` | Cloud Storage (/kingcountry/) | 🚧 Pendente |
| 🌐 **Backend API** | `/backend/` (Python/FastAPI) | App Engine (compartilhado) | ✅ Pronto |
| 💻 **Frontend Web** | `/frontend/src/` (React) | Firebase Hosting (compartilhado) | ✅ Pronto |

### 🏗️ Infraestrutura Compartilhada

**IMPORTANTE**: KingCountry compartilha infraestrutura com toda a família King:
- ✅ **Projeto GCP**: `kinggroup-website-463104` (compartilhado)
- ✅ **Backend**: Compartilhado com todos os apps King
- ✅ **Frontend**: Compartilhado com todos os apps King  
- ✅ **Firestore**: `kingroad-db` (database compartilhado)
- ✅ **Cloud Storage**: Pasta dedicada `/kingcountry/`

### 🚀 Fluxo de Deploy (Quando Configurado)

```
Developer: git push origin main
         ↓
GitHub Actions detecta mudanças
         ↓
    ┌────────┼────────┐
    ↓        ↓        ↓
/mobile/  /backend/ /frontend/
mudou?    mudou?    mudou?
    ↓        ↓        ↓
  Build    Deploy   Deploy
  APK      App      Firebase
          Engine    Hosting
    ↓        ↓        ↓
┌─────────────────────────────┐
│   GOOGLE CLOUD PLATFORM     │
│   kinggroup-website-463104  │
├─────────────────────────────┤
│ /kingcountry/ │ Backend │ Frontend │
│ 🚧 Pronto     │ ✅ Ativo │ ✅ Ativo │
└─────────────────────────────┘
```

### ✅ Checklist Antes de Criar Código

1. [ ] **Identificar tipo**: Mobile? Backend? Frontend?
2. [ ] **Verificar se existe**: `find /app/KingCountry -name "*nome*"`
3. [ ] **Criar na pasta CORRETA** (ver tabela acima)
4. [ ] **Lembrar**: Backend/Frontend são COMPARTILHADOS
5. [ ] **Commitar**: `git commit -m "feat: descrição clara"`
6. [ ] **Push**: `git push origin main`

---

## 💡 Sobre o KingCountry

**KingCountry** é um aplicativo gratuito da **Família King** criado para ajudar pessoas a entender onde o dinheiro realmente rende.

### 🎯 Objetivo

Oferecer uma visão **honesta, prática e comparativa** do custo de vida global, ajudando:
- 👥 Pessoas a decidir onde viver
- 💼 Profissionais a escolher onde trabalhar
- 💰 Famílias a economizar melhor

### ✨ Funcionalidades Principais

#### 💰 Comparação de Custo de Vida
- **Comparação entre países e cidades**
- Leva em conta:
  - 💵 Salários médios
  - 🏠 Moradia (aluguel, financiamento)
  - 🚗 Transporte (combustível, seguro, manutenção)
  - 🍔 Alimentação (supermercado, restaurantes)
  - 📊 Impostos (renda, propriedade, consumo)
  - 🏥 Saúde (planos, medicamentos)
  - 📚 Educação (escolas, universidades)

#### 👨‍👩‍👧‍👦 Perfil Familiar Personalizado
- **Configuração flexível**:
  - Solteiro, casal ou família com filhos
  - Profissão e salário
  - Idade dos membros
  - Tipo de moradia desejada
  - Veículo (modelo e ano)
  - Número de dependentes

#### 📊 Cálculo Automático
- **Quanto sobra no final do mês**
- Visualização clara e comparativa
- Diferença entre "ganhar bem" vs "viver melhor"
- Gráficos e tabelas intuitivos

#### 💼 Mercado de Trabalho
- **Vagas de emprego** por região
- **Salários médios** por profissão
- Tendências de mercado
- Oportunidades por cidade

#### 🚗 Custos de Veículos
- **Seguro** baseado em modelo e cidade
- **Manutenção** estimada
- **Combustível** por região
- Comparação de custos

#### 👶 Despesas com Dependentes
- **Creche** conforme idade
- **Escola** pública vs privada
- **Babá** e cuidadores
- **Atividades extracurriculares**

#### 💊 Custos de Saúde
- **Planos de saúde** por faixa etária
- **Medicamentos** essenciais
- **Consultas** e exames
- Sistema público vs privado

---

## 🏗️ Estrutura do Projeto

> **💡 ESTRUTURA REAL VERIFICADA** - Monorepo multiplataforma

```
KingCountry/
│
├── 📦 apps/                            # APLICATIVOS MULTIPLATAFORMA
│   │                                   # 🎯 CRIAR CÓDIGO MOBILE/DESKTOP AQUI
│   ├── android/                       # 🆕 Android app
│   ├── ios/                           # 🆕 iOS app  
│   ├── windows/                       # 🆕 Windows desktop
│   └── linux/                         # 🆕 Linux desktop
│
├── 📱 mobile/                          # MOBILE ANDROID (PRINCIPAL)
│   │                                   # 🎯 CRIAR APP ANDROID AQUI
│   ├── app/
│   │   ├── src/main/java/com/kinggroup/kingcountry/
│   │   │   ├── features/              # Features principais
│   │   │   │   ├── comparison/        # 🆕 Comparação países/cidades
│   │   │   │   ├── calculator/        # 🆕 Calculadora custo de vida
│   │   │   │   ├── profile/           # 🆕 Perfil familiar
│   │   │   │   ├── jobs/              # 🆕 Mercado de trabalho
│   │   │   │   └── costs/             # 🆕 Custos detalhados
│   │   │   ├── database/              # Room Database
│   │   │   └── MainActivity.kt
│   │   └── build.gradle
│   └── gradle/
│
├── 🌐 backend/                         # BACKEND API (Python/FastAPI)
│   │                                   # 🎯 CRIAR APIs AQUI
│   │                                   # ⚠️ COMPARTILHADO COM FAMÍLIA KING
│   ├── routes/                        # 🆕 Endpoints (quando criar)
│   │   ├── countries_routes.py        # APIs de países
│   │   ├── cities_routes.py           # APIs de cidades
│   │   ├── costs_routes.py            # APIs de custos
│   │   ├── jobs_routes.py             # APIs de empregos
│   │   └── comparison_routes.py       # APIs de comparação
│   ├── services/                      # Business logic
│   ├── models/                        # Pydantic models
│   └── main.py                        # FastAPI app principal
│
├── 💻 frontend/                        # WEBSITE (React)
│   │                                   # 🎯 CRIAR UI WEB AQUI
│   │                                   # ⚠️ COMPARTILHADO COM FAMÍLIA KING
│   ├── src/
│   │   ├── components/                # 🆕 Componentes (quando criar)
│   │   │   ├── CountryComparison/     # Comparador de países
│   │   │   ├── CostCalculator/        # Calculadora
│   │   │   ├── ProfileBuilder/        # Construtor de perfil
│   │   │   └── JobsExplorer/          # Explorador de empregos
│   │   └── App.js
│   └── package.json
│
├── 🗄️ database/                        # SCHEMAS
│   ├── firestore/                     # Firestore schemas
│   │   ├── countries.json             # Países
│   │   ├── cities.json                # Cidades
│   │   ├── costs.json                 # Custos por categoria
│   │   └── jobs.json                  # Vagas e salários
│   └── bigquery/                      # Analytics (opcional)
│
├── 📦 packages/                        # PACKAGES COMPARTILHADOS
│   ├── core/                          # Core functionality
│   └── ui/                            # UI components
│
├── 🚀 .github/workflows/               # CI/CD
│   ├── deploy-backend-manual.yml      # ✅ Deploy backend
│   └── deploy-frontend-manual.yml     # ✅ Deploy frontend
│
├── 🔧 scripts/                         # SCRIPTS UTILITÁRIOS
├── 📚 docs/                            # DOCUMENTAÇÃO
└── README.md                           # 📖 ESTE ARQUIVO
```

### 🎯 Onde Criar Código

| Funcionalidade | Criar em | Tecnologia |
|---------------|----------|------------|
| **App Mobile Android** | `/mobile/app/src/main/` | Kotlin + Jetpack Compose |
| **App Mobile iOS** | `/apps/ios/` | Swift + SwiftUI |
| **App Desktop Windows** | `/apps/windows/` | Python + PyQt6 |
| **App Desktop Linux** | `/apps/linux/` | Python + PyQt6 |
| **APIs Backend** | `/backend/routes/` | Python (FastAPI) - COMPARTILHADO |
| **Website** | `/frontend/src/` | React - COMPARTILHADO |

> **Nota**: Backend e Frontend são compartilhados com toda a família King.
> Apenas os apps mobile/desktop são específicos deste repositório.

---

## 🔄 ESPELHAMENTO GCP ↔ GITHUB

> **Para mapeamento completo**: Ver [MAPEAMENTO_COMPLETO_GCP_GITHUB.md](https://github.com/samuelgomes71/KingRoad-GPS/blob/main/MAPEAMENTO_COMPLETO_GCP_GITHUB.md) no repo KingRoad GPS

### 📊 Infraestrutura Compartilhada

**IMPORTANTE**: Todos os apps da família King compartilham a mesma infraestrutura:

| Componente | Compartilhado? | Localização GCP | Status |
|-----------|---------------|-----------------|--------|
| **Projeto GCP** | ✅ SIM | `kinggroup-website-463104` | ✅ Ativo |
| **Backend API** | ✅ SIM | App Engine (FastAPI/Python) | ✅ Ativo |
| **Frontend Web** | ✅ SIM | Firebase Hosting (React) | ✅ Ativo |
| **Firestore** | ✅ SIM | `kingroad-db` (42 collections) | ✅ Ativo |
| **Cloud Storage** | ⚠️ PARCIAL | Pasta por app `/kingcountry/` | ✅ Criada |
| **Builds Mobile** | ❌ NÃO | Específico de cada app | 🚧 Pendente |

### 🗄️ Firestore Compartilhado

**Database**: `kingroad-db` (42 collections compartilhadas)

Collections principais existentes:
- `users` - Usuários de todos os apps
- `sessions` - Sessões ativas
- `logs` - Logs de atividades

> **Quando KingCountry for desenvolvido**, poderá criar collections específicas:
> - `countries` - Dados de países
> - `cities` - Dados de cidades
> - `costs_data` - Custos por categoria e região
> - `jobs_data` - Vagas e salários
> - `user_profiles` - Perfis de usuários KingCountry
> - `comparisons` - Comparações salvas

### 🌐 URLs Compartilhadas

| Serviço | URL | Uso |
|---------|-----|-----|
| **Backend API** | https://kinggroup-website-463104.uc.r.appspot.com | Todos os apps |
| **Frontend Web** | https://www.kinggrouptech.com | Website King Group |
| **GCP Console** | https://console.cloud.google.com/home/dashboard?project=kinggroup-website-463104 | Gerenciamento |
| **Firebase Console** | https://console.firebase.google.com/project/kinggroup-website-463104 | Gerenciamento |

---

## ⚠️ Status de Infraestrutura

**Status Atual**: 🚧 Em Desenvolvimento

- ✅ **Repositório GitHub**: Criado e ativo
- ✅ **Estrutura de código**: Definida (`/mobile/`, `/backend/`, `/frontend/`)
- ✅ **Projeto GCP**: `kinggroup-website-463104` (compartilhado com família King)
- ✅ **Cloud Storage**: Pasta `/kingcountry/` criada e pronta para builds
- ✅ **Backend**: Compartilhado (App Engine - FastAPI/Python)
- ✅ **Frontend**: Compartilhado (Firebase Hosting - React)
- ✅ **Firestore**: `kingroad-db` (database compartilhado - 42 collections)
- ✅ **CI/CD Workflows**: Backend + Frontend configurados
- 🚧 **Deploy automático**: Configurado (aguardando código)
- 🚧 **Build mobile**: Ainda não disponível

**✅ Produção Completa**: Apenas **KingRoad GPS**  
**🚧 KingCountry**: Em desenvolvimento (infraestrutura 100% pronta)

> **Compartilhamento de Recursos**: Este app compartilha Backend, Frontend e Firestore com toda a família King. Apenas os builds mobile (APK/IPA) serão específicos.

---

## 🌍 Branches Multiplataforma

Este repositório suporta desenvolvimento para **5 plataformas** através de branches dedicados:

| Branch | Plataforma | Tecnologia | Status |
|--------|-----------|------------|--------|
| **main** | 🤖 Android | Kotlin Native + Jetpack Compose | 🚧 Em Desenvolvimento |
| **kmp** | 🤖🍎💻 Multi | Kotlin Multiplatform | 📦 Estrutura Pronta |
| **ios-native** | 🍎 iOS | Swift + SwiftUI | 📦 Estrutura Pronta |
| **windows** | 💻 Windows | Python + PyQt6 | 📦 Estrutura Pronta |
| **linux** | 🐧 Linux | Python + PyQt6 | 📦 Estrutura Pronta |

### Comandos Git para Trocar de Branch

```bash
# Android (branch principal)
git checkout main

# Kotlin Multiplatform
git checkout kmp

# iOS Nativo
git checkout ios-native

# Windows Desktop
git checkout windows

# Linux Desktop
git checkout linux
```

---

## 🏰 Família King - Ecossistema de Apps

KingCountry faz parte da **Família King** de aplicativos profissionais:

| App | Descrição | Status |
|-----|-----------|--------|
| **KingRoad GPS** | Navegação para caminhoneiros | ✅ Produção |
| **KingCountry** | Comparação global de custo de vida | 🚧 Desenvolvimento |
| **KingChat** | Mensagens profissionais | 🚧 Desenvolvimento |
| **KingLoc** | Rastreamento de localização | 🚧 Desenvolvimento |
| **KingMusic** | Streaming de música | 🚧 Desenvolvimento |
| ... e mais 10 apps | | 🚧 Desenvolvimento |

---

## 🎯 Casos de Uso

### 1. Profissional Considerando Mudança Internacional
"Ganho R$ 10.000 como desenvolvedor no Brasil. Quanto preciso ganhar no Canadá para manter o mesmo padrão de vida?"

### 2. Família Planejando Mudança
"Somos 4 pessoas (casal + 2 filhos). Quanto custa viver em Lisboa vs Porto?"

### 3. Freelancer Comparando Cidades
"Trabalho remoto. Onde meu salário de US$ 5.000 rende mais?"

### 4. Estudante Planejando Intercâmbio
"Quanto preciso por mês para estudar e viver em Sydney?"

---

## 📚 Documentação

### 📖 Guias Principais

- **[MAPEAMENTO_COMPLETO_GCP_GITHUB.md](https://github.com/samuelgomes71/KingRoad-GPS/blob/main/MAPEAMENTO_COMPLETO_GCP_GITHUB.md)** - 🌟 **GUIA ESSENCIAL** - Infraestrutura compartilhada
- **DATA_SOURCES.md** - Fontes de dados utilizadas (quando criar)
- **CALCULATION_LOGIC.md** - Lógica de cálculos (quando criar)

---

## 🔧 Tecnologias

### 📱 Mobile (Android)
- **Kotlin** - Linguagem principal
- **Jetpack Compose** - UI moderna
- **Room** - Database local
- **Retrofit** - HTTP Client

### 🌐 Backend (Compartilhado)
- **Python 3.11** - Linguagem
- **FastAPI** - Framework REST API
- **Firebase Admin SDK** - Autenticação
- **GCP App Engine** - Hosting

### 💻 Frontend (Compartilhado)
- **React 18** - UI Library
- **JavaScript ES6+** - Linguagem
- **Firebase Hosting** - Hosting

### 🗄️ Databases
- **Firestore** - NoSQL (compartilhado)
- **BigQuery** - Analytics (opcional)

---

## 📊 Fontes de Dados (Planejadas)

Os dados de custo de vida serão agregados de múltiplas fontes confiáveis:
- 🌍 Numbeo (custo de vida mundial)
- 💼 Glassdoor / LinkedIn (salários)
- 🏛️ Banco Mundial (dados econômicos)
- 📊 OCDE (estatísticas oficiais)
- 🏦 APIs de câmbio em tempo real

**Nota**: Dados serão atualizados periodicamente para precisão.

---

## 🤝 Contribuir

Este é um projeto da **King Group Tech**. Para contribuições:
1. Faça fork do repositório
2. Crie uma branch de feature
3. Commit suas mudanças
4. Push para a branch
5. Abra um Pull Request

---

## 📝 Status do Projeto

- [x] Repositório criado ✅
- [x] Estrutura definida ✅
- [x] Cloud Storage preparado ✅
- [x] Workflows CI/CD configurados ✅
- [ ] Desenvolvimento mobile iniciado
- [ ] APIs backend criadas
- [ ] Frontend web desenvolvido
- [ ] Integração de dados
- [ ] Testes
- [ ] Deploy produção

---

## 📄 Licença

Proprietary - King Group Tech © 2025

---

**KingCountry** - *Descubra onde seu dinheiro realmente rende* 🌍💰

**Última atualização**: 29 de Outubro, 2025  
**Versão**: 1.0.0 (Em Desenvolvimento)
