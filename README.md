# 📦 Automatização de Processamento de Arquivos e Backup

Este script automatiza o tratamento de arquivos extraídos do sistema GTPLAN para controle logístico e atualização dos dashboards gerenciais. Ele cuida da leitura, limpeza, concatenação, renomeação e organização dos dados, além de backups e versionamento automático.

---

## 🧩 O que esse script faz

### 📁 Parte B – Processamento dos arquivos `sku.csv` e `sku (1).csv`

- Lê os arquivos com encoding `utf-8-sig` (para evitar problemas com acentos);
- Remove cabeçalhos duplicados (caso existam);
- Concatena os dois arquivos;
- Exclui colunas irrelevantes;
- Renomeia colunas para nomes padronizados, inclusive previsões mensais (ex: `Apr/2025` → `M0`);
- Adiciona uma coluna com a data de extração;
- Salva o resultado como Excel: `sku DD.MM.xlsx`.

### 📁 Parte A – Consolidação dos arquivos `result*.csv`

- Lê todos os arquivos que comecem com `result` e terminem em `.csv`;
- Concatena todos em um único DataFrame;
- Salva o consolidado como `scm586g_followup.csv`.

### ⚙️ Extras

- Renomeia o arquivo `mrp8009g_ps_list.csv` para `scm420g_suggestions.csv`, se existir;
- Move os arquivos processados para uma pasta de histórico com base na data atual (ex: `historico_extracao/2025/Maio/03.06`);
- Copia os mesmos arquivos para uma pasta secundária usada em dashboards;
- Faz backup dos relatórios Power BI (`.pbix`) com data no nome;
- Remove backups de `.pbix` mais antigos que 7 dias.

---

## 📂 Entrada esperada

Coloque todos esses arquivos na pasta **Downloads** antes de rodar o script:

- `sku.csv`
- `sku (1).csv`
- Arquivos que começam com `result` (ex: `result_abc.csv`, `result_xyz.csv`)
- (Opcional) `mrp8009g_ps_list.csv`

---

## 🧾 Arquivos gerados

- `sku DD.MM.xlsx`
- `scm586g_followup.csv`
- `scm420g_suggestions.csv`

Esses arquivos são:

✅ **Movidos para:**
```
\\arqsv0\sl\PlanLogistica\INDICADORES\DASHBOARDs\PROJETO GERENCIAL\
└── Extracao GTPLAN
    ├── historico_extracao
    │   └── 2025
    │       └── NomeDoMês
    │           └── DD.MM
    └── [pasta principal para uso dos dashboards]
```

✅ **Backups `.pbix` salvos em:**
```
C:\Users\SeuUsuario\OneDrive\...\Backup\PowerBI\
```

---

## 🛠️ Tecnologias utilizadas

- Python 3.x
- Pandas
- Bibliotecas padrão (`os`, `glob`, `shutil`, `datetime`)

---

## 🚀 Como rodar

1. Certifique-se de que todos os arquivos mencionados estejam na pasta `Downloads`;
2. Execute o script com Python;
3. Acompanhe os prints no terminal para ver o status de cada etapa.

---

## 📌 Observações

- As renomeações de colunas foram pensadas para facilitar a leitura no Power BI;
- A organização por mês e dia ajuda no versionamento histórico;
- O código também cuida da limpeza automática dos backups antigos.

---

✅ **Feito para facilitar o dia a dia com os relatórios do GTPLAN.**
