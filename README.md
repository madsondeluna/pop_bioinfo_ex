# Procedimento Operacional Padrão (POP) – Identificação de Padrões Proteicos com HMM

**Código:** BIOINF-POP-HMM-001 / Ex.: SETOR-POP-TECNICA-VERSAO

**Versão:** v1.0  

**Data de criação:** \[dd/mm/aaaa]  

**Última revisão:** \[dd/mm/aaaa]  

**Responsável:** \[Nome do responsável]  

**Aprovado por:** \[Nome do responsável]

---

## 1. Objetivo

Padronizar o procedimento para buscar e identificar padrões ou famílias de proteínas em um proteoma em formato FASTA utilizando perfis de Hidden Markov Models (HMM) por meio da suíte HMMER no ambiente Linux.

---

## 2. Escopo

Este POP aplica-se a laboratórios e equipes de bioinformática que necessitam detectar domínios ou motivos proteicos específicos em grandes conjuntos de sequências (proteomas). Aplica-se ao uso de HMMER v3.x em distribuições Linux (ex.: Ubuntu, CentOS).

---

## 3. Definições e Abreviaturas

| Termo/Sigla | Definição                                      |
| ----------- | ---------------------------------------------- |
| HMM         | Hidden Markov Model                            |
| HMMER       | Suíte de programas para análise com HMM (v3.x) |
| FASTA       | Formato padrão de sequências biológicas        |
| CPU         | Unidade de processamento central               |
| E-value     | Estatística de probabilidade para alinhamento  |

---

## 4. Materiais e Softwares Necessários

* **Sistema operacional:** Linux (Ubuntu 20.04 ou superior)
* **Pacotes obrigatórios:**

  * HMMER v3.3 (hmmpress, hmmbuild, hmmsearch)
  * gzip, tar (para compactação e descompactação)
* **Hardware recomendado:** CPU multicore (4 cores ou mais), ≥8 GB de RAM

---

## 5. Requisitos de Entrada

1. **Perfil HMM:** arquivo `perfil.hmm` gerado a partir de múltiplos alinhamentos (ex.: via hmmbuild).
2. **Proteoma em FASTA:** arquivo `proteome.fasta` contendo todas as sequências proteicas a serem pesquisadas.
3. **Parâmetros de busca:** valor de corte de E-value (ex.: `1e-5`).

---

## 6. Procedimento Detalhado

1. **Preparar ambiente e diretório de trabalho:**

   ```bash
   mkdir -p ~/hmm_search && cd ~/hmm_search
   cp /caminho/para/perfil.hmm .
   cp /caminho/para/proteome.fasta .
   ```

2. **Indexar o perfil HMM:**

   ```bash
   hmmpress perfil.hmm
   ```

3. **Executar busca com HMMER (hmmsearch):**

   ```bash
   hmmsearch --cpu 4 \                   # número de threads
             --tblout resultados.tbl \   # formato tabular resumido
             --domtblout dominios.tbl \  # saída de domínios alinhados
             -E 1e-5 \                   # E-value de corte
             perfil.hmm proteome.fasta > log_hmmsearch.out
   ```

4. **Verificar integridade dos arquivos de saída:**

   ```bash
   ls -lh resultados.tbl dominios.tbl log_hmmsearch.out
   ```

5. **Filtrar resultados principais (opcional):**

   ```bash
   awk '$5 < 1e-5' resultados.tbl > hits_filtrados.tbl
   ```

6. **Analisar cobertura e qualidade dos domínios:**

   * Conferir colunas `seq-fraction` e `domain c-Evalue` em `dominios.tbl`.
   * Plotar estatísticas ou importar em script Python/R para análise aprofundada.

7. **Documentar achados:**

   * Resumo de hits e domínios presentes.
   * Taxonomia ou anotação funcional associada às sequências identificadas.

---

## 7. Saídas Esperadas

| Arquivo             | Descrição                                      |
| ------------------- | ---------------------------------------------- |
| resultados.tbl      | Lista de sequências com hits (formato tabular) |
| dominios.tbl        | Detalhes de domínios encontrados               |
| hits\_filtrados.tbl | Hits filtrados por E-value                     |
| log\_hmmsearch.out  | Log completo da execução                       |

---

## 8. Critérios de Aceitabilidade / Controle de Qualidade

* Pelo menos 80% dos domínios conhecidos do perfil devem ser detectados em sequências de referência.
* E-value ≤ 1e-5 para considerável significância.
* Cobertura de domínio (`hmmalign coverage`) ≥ 50%.
* Ausência de erros de execução no `log_hmmsearch.out`.

---

## 9. Problemas Conhecidos e Soluções

| Problema Comum                          | Causa Possível                                         | Solução Recomendada                                                    |
| --------------------------------------- | ------------------------------------------------------ | ---------------------------------------------------------------------- |
| `hmmpress: HMM file has no binary file` | Perfil não foi indexado corretamente                   | Executar `hmmpress perfil.hmm` de novo                                 |
| Memória insuficiente durante busca      | Arquivo FASTA muito grande ou múltiplas threads ativas | Reduzir número de CPUs (`--cpu`) ou dividir proteoma em partes menores |
| `Segmentation fault`                    | Versão incompatível do HMMER ou arquivo corrompido     | Reinstalar HMMER e validar integridade do arquivo HMM                  |

---

## 10. Histórico de Revisões

| Data       | Versão | Alteração                                  | Responsável |
| ---------- | ------ | ------------------------------------------ | ----------- |
| dd/mm/aaaa | v1.0   | Criação do POP para busca HMM em proteomas | \[Nome]     |

---

## 11. Referências Normativas ou Bibliográficas

* Eddy, S. R. (2011). Accelerated Profile HMM Searches. *PLoS Computational Biology*, 7(10), e1002195.
* HMMER User Guide v3.3: [http://hmmer.org/documentation.html](http://hmmer.org/documentation.html)
* Finn, R. D., et al. (2014). Pfam: the protein families database. *Nucleic Acids Research*, 42(D1), D222–D230.
