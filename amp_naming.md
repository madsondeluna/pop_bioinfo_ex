# Protocolo de Padronização da Nomenclatura de Peptídeos Antimicrobianos do LGBV

**Responsável:** Madson Aragão 

**Versão:** 0.1

**Data:** 20 de maio de 2025

---

## 1. Objetivo

Estabelecer diretrizes para a nomenclatura padronizada de peptídeos antimicrobianos (AMPs) identificados, preditos ou projetados em projetos conduzidos pelo LGBV. Este protocolo visa garantir consistência, reprodutibilidade e clareza na organização na anotações dos dados.

---

## 2. Estrutura do Identificador

O identificador de cada AMP deve seguir o seguinte padrão:

```
[Espécie]_[Classe]_[TipoAMP]_[Número]_[Versão]
```

Cada componente é descrito em detalhe a seguir.

---

## 3. \[Espécie] - Abreviação do nome binomial

A espécie de origem deve ser representada por um código de duas letras, derivado das iniciais do gênero e da espécie:

| Nome Científico        | Abreviação |
| ---------------------- | ---------- |
| *Arabidopsis thaliana* | At         |
| *Zea mays*             | Zm         |
| *Escherichia coli*     | Ec         |
| *Glycine max*          | Gm         |
| *Vigna unguiculata*    | Vu         |
| *Cajanus cajan*        | Cc         |
| *Phaseolus vulgaris*   | Pv         |
| *Medicago truncatula*  | Mt         |
| *Lotus japonicus*      | Lj         |
| *Arachis hypogaea*     | Ah         |
| Metagenoma ambiental   | Meta       |

*Observação:* Outras espécies devem seguir a mesma lógica de abreviação (duas letras representando gênero e espécie).

---

## 4. \[Classe] - Tipo estrutural ou funcional do AMP

A classe representa a estrutura ou família funcional do peptídeo. As principais categorias incluem:

| Classe Funcional/Estrutural | Abreviação |
| --------------------------- | ---------- |
| Defensina                   | Def        |
| Tiorredoxina-like           | Thio       |
| Ciclopeptídeo               | Cycl       |
| Cisteína-rich               | Cys        |
| Lipopetídeo                 | Lipo       |
| Prolamina-like              | Prol       |
| Beta-barrel bacteriano      | BBar       |
| Desconhecido                | Unk        |

*Critérios de classificação incluem análises por ferramentas como InterProScan, PEP-FOLD ou base em famílias descritas.*

---

## 5. \[TipoAMP] - Status computacional ou origem do peptídeo

| Abreviação | Significado                            |
| ---------- | -------------------------------------- |
| AMP        | Genérico ou validado experimentalmente |
| AMPc       | Predito in silico                      |
| AMPmod     | Versão modificada ou otimizada         |
| AMPsyn     | AMP projetado sinteticamente (de novo) |

---

## 6. \[Número] - Identificador numérico ordenado

O número é um identificador sequencial de três dígitos, definido com base na origem genômica do peptídeo.

### A. Genomas montados

* A ordenação segue a ordem dos cromossomos (ex: cromossomo 1, 2, ...).
* Para genes oriundos de plastídeos, mitocôndrias ou outros elementos extragênicos, numerar após os cromossomos nucleares.

**Exemplo:**

* `At_Def_AMPc_001` (Origem no cromossomo 1)
* `At_Def_AMPc_045` (Origem no cromossomo 3)

### B. Genomas em draft ou metagenomas

* A numeração segue a ordem de tamanho da sequência, do menor para o maior.

**Exemplo:**

* `Meta_Cys_AMPc_001` (Menor AMP encontrado)
* `Meta_Cys_AMPc_002` (Maior AMP encontrado)

---

## 7. \[Versão] - Controle de versão (opcional)

**Importante:** para separar a sequência numérica da versão, sempre utilize um underscore (`_`) antes do identificador de versão. Exemplos:

* `_v1` - Versão original
* `_v2` - Versão modificada (mutada, otimizada, etc.)

**Tabela de abreviações de versão:**

| Abreviação | Significado                                |
| ---------- | ------------------------------------------ |
| v1         | Versão original                            |
| v2         | Segunda versão (com modificações)          |
| v3         | Terceira versão (otimizações subsequentes) |

**Exemplos de uso correto:**

* `Zm_Def_AMPmod_005_v1` (Versão original do AMPmod 005)
* `Zm_Def_AMPmod_005_v2` (Versão otimizada do AMPmod 005)

---

## 8. Exemplos completos de nomenclatura

| Identificador             | Interpretação                                                                |
| ------------------------- | ---------------------------------------------------------------------------- |
| `At_Def_AMPc_001_v1`      | Defensina predita no cromossomo 1 de *Arabidopsis thaliana*, versão original |
| `Zm_Cys_AMP_010`          | AMP cisteína-rich validado experimentalmente em *Zea mays*                   |
| `Gm_Thio_AMPc_007_v1`     | Tiorredoxina-like predita em *Glycine max*, versão original                  |
| `Vu_Cycl_AMPc_012`        | Ciclopeptídeo encontrado em *Vigna unguiculata*                              |
| `Meta_Lipo_AMPsyn_003_v2` | Peptídeo lipídico sintético de metagenoma, versão otimizada                  |
| `Ec_BBar_AMPmod_002_v3`   | Beta-barrel modificado de *Escherichia coli*, versão 3                       |

---

## 9. Recomendações adicionais

* Nomear arquivos e sequências (FASTA, planilhas) com base no identificador padronizado.
* Manter metadados organizados com campos como: espécie, classe, origem, sequência, ferramentas utilizadas, localização genômica, versão e descrição funcional.
* Registrar alterações em changelogs (preferencialmente em formato Markdown ou CSV).
* Recomenda-se utilizar banco de dados interno (CSV ou SQLite) e automatização via scripts.

---

## 10. Recursos futuros (em desenvolvimento)

* Modelo de planilha para metadados
* Script em Python para gerar identificadores automaticamente
* Workflow Snakemake para integração com pipelines de predição de AMPs

---

**LGBV - 2025.**
