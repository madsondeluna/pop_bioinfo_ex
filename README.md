# Procedimento Operacional Padrão (POP) – \EXEMPLO

**Código:** BIOINF-POP-XXX
**Versão:** v1.0
**Data de criação:** \[dd/mm/aaaa]
**Última revisão:** \[dd/mm/aaaa]
**Responsável:** \[Nome do responsável]
**Revisado por:** \[Nome do responsável]

---

## 1. Objetivo

Descrever de forma padronizada o procedimento para \[descrever a técnica/etapa bioinformática], garantindo reprodutibilidade, rastreabilidade e controle de qualidade da análise.

---

## 2. Escopo

Este POP aplica-se a \[instituição, laboratório ou equipe] e deve ser seguido por \[usuários, bolsistas, analistas, etc.] envolvidos em análises com \[tipo de dado, ferramenta, plataforma].

---

## 3. Definições e Abreviaturas

| Termo/Sigla | Definição                 |
| ----------- | ------------------------- |
| VCF         | Variant Call Format       |
| SNV         | Single Nucleotide Variant |
| CLI         | Command Line Interface    |
| \[outras]   | \[...]                    |

---

## 4. Materiais e Softwares Necessários

* **Sistema operacional:** \[ex: Ubuntu 22.04]
* **Gerenciador de pacotes:** \[ex: Conda v4.10, apt, brew]
* **Ferramentas utilizadas:**

  * \[ex: ANNOVAR (2020Jun08)]
  * \[ex: bcftools v1.17]
* **Scripts auxiliares:** \[ex: Python 3.11, Bash, R, etc.]

---

## 5. Requisitos de Entrada

* Arquivo(s) de entrada: `sample.vcf.gz`
* Formato: VCF v4.2, tabular, FASTA
* Pré-processamento necessário: compressão com bgzip, indexação com tabix

---

## 6. Procedimento Detalhado

Descrever passo a passo, com comandos, explicações e boas práticas.

```bash
# Exemplo 1 – conversão de VCF para formato ANNOVAR
convert2annovar.pl -format vcf4 sample.vcf > sample.avinput

# Exemplo 2 – anotação funcional
table_annovar.pl sample.avinput humandb/ -buildver hg19 -out sample_ann -remove \
  -protocol refGene,dbnsfp30a -operation g,f -nastring . -csvout
```

> **Observações:**
>
> * O banco `dbnsfp30a` precisa estar previamente baixado com `annotate_variation.pl`.
> * Utilize `-nastring .` para representar valores nulos de forma padronizada.

---

## 7. Saídas Esperadas

* `sample_ann.csv`: arquivo anotado com colunas funcionais e preditivas
* Arquivos intermediários: `.avinput`, logs, etc.
* Critérios para validação da execução: número de variantes ≈ ao do VCF original

---

## 8. Critérios de Aceitabilidade / Controle de Qualidade

* Conferência da integridade dos arquivos de saída
* Verificação de colunas-chave: `SIFT_pred`, `PolyPhen2_HDIV_pred`
* Logs sem erros e sem mensagens de truncamento
* Análise de variantes de exemplo para checar anotação correta

---

## 9. Problemas Conhecidos e Soluções

| Problema Comum              | Causa Possível                     | Solução Recomendada                   |
| --------------------------- | ---------------------------------- | ------------------------------------- |
| "Cannot locate humandb/..." | Banco não baixado                  | Baixar usando `annotate_variation.pl` |
| Arquivo `.csv` vazio        | Arquivo VCF com erro de formatação | Validar VCF com `vcf-validator`       |

---

## 10. Histórico de Revisões

| Data       | Versão | Alteração                    | Responsável   |
| ---------- | ------ | ---------------------------- | ------------- |
| dd/mm/aaaa | v1.0   | Criação inicial do documento | Madson Aragão |
| dd/mm/aaaa | v1.1   | Revisão de banco de dados    | \[Nome]       |

---

## 11. Referências Normativas ou Bibliográficas

* Wang, K., Li, M., & Hakonarson, H. (2010). ANNOVAR: functional annotation of genetic variants from high-throughput sequencing data. *Nucleic acids research*, 38(16), e164.
* [https://annovar.openbioinformatics.org](https://annovar.openbioinformatics.org)
* GATK Best Practices: [https://gatk.broadinstitute.org](https://gatk.broadinstitute.org)
* VCF Specification: [https://samtools.github.io/hts-specs/VCFv4.2.pdf](https://samtools.github.io/hts-specs/VCFv4.2.pdf)
