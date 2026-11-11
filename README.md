# VIDA SAUDÁVEL

Assistente pessoal de hidratação, refeições e hábitos. 100% gratuito, sem servidor, dados salvos no próprio aparelho.

## Perfil já configurado

| Item | Valor |
|---|---|
| Peso / altura | 70 kg / 175 cm |
| Atividade física | Leve |
| Rotina | Trabalho e estudo |
| Acorda / dorme | 06:00 / 23:00 (você dorme entre 23:00 e 00:00; o app usa 23:00 para não lembrar perto do sono) |
| Meta de água | 2.100 ml (experimental, editável) |
| Lembretes de água | 8, entre 06:30 e 21:30 (≈260 ml cada) |
| Refeições | 06:30 café · 10:00 lanche · 12:00 almoço · 15:00 lanche · 19:30 jantar · 21:00 ceia opcional |
| Objetivo | Organizar hidratação e refeições — **sem dietas restritivas e sem metas de peso** |

Na primeira abertura o app mostra o perfil preenchido para você conferir (falta só a idade) e tocar em **Salvar e começar**. Depois disso tudo é usado automaticamente nos dias seguintes.

## Funcionalidades

- **Início**: saudação, data e hora ao vivo, água do dia × meta, próximo horário de água, próxima refeição, % do dia e resumo dos hábitos.
- **Água**: botões +150/+250/+350/+500 ml e valor livre, barra de progresso, histórico (com remoção), horários programados com status, nº de lembretes ajustável, pausar (1h, 3h, até amanhã), meta manual ou referência calculada (peso × 30 ml + atividade + clima + rotina). Opção de restrição de líquidos por orientação médica.
- **Alimentação**: 6 refeições com horário editável, 3 cardápios econômicos por refeição (alternam por dia), quantidades aproximadas, **trocar alimento** (só hoje ou sempre) dentro do mesmo grupo, filtros de alergia/intolerância/vegetariano/alimentos que não gosta/orçamento, dicas para levar ao trabalho/faculdade, lembrete X min antes e botão de concluída.
- **Histórico**: gráficos de água e refeições, média, dias com meta atingida, dias com rotina cumprida, sequência e tabela diária — apenas com dados reais registrados.
- **Perfil**: todos os dados editáveis, notificações, backup/restauração e apagar dados.

## Notificações — como funcionam

| Forma de uso | Lembretes |
|---|---|
| **APK (Capacitor)** — recomendado | Agendados no próprio Android com `@capacitor/local-notifications`. Tocam **com o app fechado**, todos os dias, nunca no horário de sono. |
| **PWA instalado pelo Chrome** | Aparecem como notificação do Android **enquanto o app estiver aberto ou em segundo plano recente**. O Android encerra páginas em segundo plano, então para lembretes confiáveis com o app fechado use o APK. |

Regras: cada lembrete aparece no máximo 1x por dia; lembrete de água é pulado se você já bebeu o planejado até aquele horário; nada entre a hora de dormir e a de acordar.

## Opção 1 — APK Android (notificações completas)

Requisitos gratuitos: [Node.js LTS](https://nodejs.org) e [Android Studio](https://developer.android.com/studio).

```bash
cd vida-saudavel
npm install
npx cap add android
npx cap sync android
npx cap open android
```

No Android Studio:
1. Ative no celular **Opções do desenvolvedor → Depuração USB** e conecte o cabo.
2. Clique em **Run ▶** — o app é instalado no celular.
3. Ou gere o arquivo: **Build → Build App Bundle(s)/APK(s) → Build APK(s)** e copie o `.apk` para o celular.

Ao abrir: toque em **Ativar** (topo) → permita notificações. No Android 12+ se pedir, permita também **Alarmes e lembretes** para os horários exatos.

Depois de alterar algo em `www/`, rode `npx cap sync android` e execute de novo.

## Opção 2 — PWA (sem instalar nada no PC)

1. Crie um repositório no GitHub e envie o conteúdo da pasta `www/`.
2. Em **Settings → Pages**, publique a branch `main` (pasta raiz).
3. Abra o link `https://SEU-USUARIO.github.io/REPO/` no **Chrome do Android** → menu ⋮ → **Instalar app / Adicionar à tela inicial**.
4. Abra pelo ícone, toque em **Ativar** e permita notificações.

Para testar no computador: `npx serve www` e abra o endereço mostrado.

## Estrutura

```
vida-saudavel/
├── www/
│   ├── index.html            # app completo (HTML + CSS + JS, sem dependências)
│   ├── manifest.webmanifest  # instalação como app
│   ├── sw.js                 # offline + notificações PWA
│   └── icon.svg / icon-192.png / icon-512.png
├── capacitor.config.json     # empacotamento Android
├── package.json
└── README.md
```

Dados: `localStorage` (chave `vidaSaudavel.v1`). Histórico guardado por 180 dias. Use **Perfil → Copiar backup** para levar os dados a outro aparelho.

> As metas e sugestões são para organização pessoal e não substituem orientação de médico ou nutricionista.
