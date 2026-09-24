# mrngflow

A modern monorepo architecture for the **mrngflow** ecosystem, powered by [Turborepo](https://turbo.build/repo) and [pnpm](https://pnpm.io).

## Repository Structure

```
mrngflow/
├── apps/
│   ├── web/               # Next.js / Web Application
│   ├── desktop/           # Desktop Application (Electron / Tauri)
│   └── mobile/            # Mobile Application (React Native / Expo)
│
├── services/
│   └── api/               # Backend API services
│
├── packages/
│   ├── ui/                # Shared UI component library
│   ├── types/             # Shared TypeScript types & interfaces
│   ├── validation/        # Shared schemas (e.g., Zod / Valibot)
│   ├── config/            # Shared configs (ESLint, TSConfig, Tailwind)
│   └── utils/             # Shared utility functions and helpers
│
├── docs/
│   ├── product/           # Product specs, user stories & roadmaps
│   ├── architecture/      # System architecture & RFCs
│   └── decisions/         # Architecture Decision Records (ADRs)
│
├── infrastructure/        # Cloud, Docker, IaC, CI/CD pipelines
│
├── .gitignore
├── README.md
├── package.json
├── pnpm-workspace.yaml
└── turbo.json
```

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (>= 18.0.0)
- [pnpm](https://pnpm.io/) (`corepack enable` or `npm install -g pnpm`)

### Installation

```bash
pnpm install
```

### Development

To start all applications and services in development mode:

```bash
pnpm run dev
```

### Building

To build all apps and packages:

```bash
pnpm run build
```
