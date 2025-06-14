# Protocolo de Padronização da Nomenclatura de Peptídeos Antimicrobianos do LGBV

**Responsável:** Madson Aragão

**Versão:** 0.5.1

**Data:** 27 de maio de 2025

---

## 1. Objetivo

Estabelecer diretrizes claras e sistemáticas para a nomenclatura padronizada de peptídeos antimicrobianos (AMPs) identificados, preditos, modificados ou projetados *de novo* em projetos conduzidos pelo Laboratório de Genética e Biotecnologia Vegetal (LGBV). Este protocolo visa garantir consistência, rastreabilidade, facilidade de comunicação e organização eficiente dos dados, minimizando ambiguidades e facilitando a colaboração e a reprodutibilidade dos dados.

---

## 2. Estrutura do Identificador

O identificador único para cada AMP deverá seguir rigorosamente o padrão abaixo, composto por cinco componentes obrigatórios, justapostos (sem separadores):

`[Espécie][Classe][TipoAMP][Número][Versão]`

Cada componente é crucial para a correta identificação e categorização do peptídeo e será detalhado nas seções subsequentes.

---

## 3. [Espécie] - Abreviação do Nome Binomial da Origem

Este componente indica a origem taxonômica do AMP ou da fonte dos dados para predição.

* **Formato:** Um código de duas a quatro letras.
    * Para espécies conhecidas, utilizar as iniciais do gênero e da espécie (ex: *Arabidopsis thaliana* -> `At`).
    * Para metagenomas ou fontes não específicas, utilizar abreviações padronizadas (ex: Metagenoma -> `Meta`).
* **Lógica:**
    * Se o AMP for natural ou predito a partir de um organismo específico, usa-se a abreviação desse organismo.
    * Se for sintético (*de novo*), mas inspirado em sequências de uma espécie, pode-se usar a espécie de inspiração ou um código genérico como `Syn` (se não houver inspiração específica). No entanto, para manter a rastreabilidade da ideia original, se um AMP sintético foi desenhado com base em características de AMPs de *Arabidopsis thaliana*, `At` ainda poderia ser usado, com o `[TipoAMP]` `AMPsyn` sinalizando sua natureza sintética.
    * Para AMPs modificados (`AMPmod`), a espécie refere-se à do peptídeo original que sofreu a modificação.

| Nome Científico / Fonte | Abreviação Proposta | Observação |
| :--- | :--- | :--- |
| *Arabidopsis thaliana* | `At` | - |
| *Zea mays* | `Zm` | - |
| *Escherichia coli* | `Ec` | - |
| *Glycine max* | `Gm` | - |
| *Vigna unguiculata* | `Vu` | - |
| *Cajanus cajan* | `Cc` | - |
| *Phaseolus vulgaris* | `Pv` | - |
| *Medicago truncatula* | `Mt` | - |
| *Lotus japonicus* | `Lj` | - |
| *Arachis hypogaea* | `Ah` | - |
| Metagenoma Ambiental | `Meta` | Para amostras complexas sem organismo definido. |
| Fonte Sintética Genérica | `Syn` | Para AMPs sintéticos sem inspiração específica. |

*Observação:* Novas espécies devem seguir a lógica de abreviação (primeira letra do gênero + primeira letra da espécie). Em caso de ambiguidade (ex: *Bacillus subtilis* e *Bacillus sphaericus* ambos seriam `Bs`), adicionar uma terceira letra da espécie para desambiguar (ex: `Bsu` e `Bsp`).

---

## 4. [Classe] - Classificação Estrutural ou Funcional do AMP

Este componente categoriza o AMP com base em sua família estrutural, funcional ou mecanismo de ação conhecido ou predito.

* **Formato:** Código de **três letras**, com a primeira letra maiúscula (Title Case).
* **Lógica:** A classificação deve ser baseada em evidências de ferramentas de bioinformática (ex: InterProScan, Pfam, BLASTp contra bancos de dados de AMPs como APD, DBAASP), predições estruturais (ex: PEP-FOLD, AlphaFold) ou literatura descrevendo famílias homólogas.
* Se um AMP puder pertencer a múltiplas classes, escolher a mais específica ou relevante para o estudo. Se nenhuma classe conhecida se aplicar, utilizar `Unk` (Desconhecido).

| Classe Funcional/Estrutural | Abreviação | Descrição Sucinta |
| :--- | :---: | :--- |
| Defensina | `Def` | Pequenos peptídeos ricos em cisteína, com pontes dissulfeto características. |
| Tiorredoxina-like | `Thl` | Peptídeos com domínios ou estrutura similar à Tiorredoxina. |
| Ciclopeptídeo | `Cyc` | Peptídeos com estrutura em anel (ligação peptídica cabeça-cauda ou outras). |
| Cisteína-rich (Não-Defensina) | `Cys` | Peptídeos ricos em cisteína que não se enquadram na definição estrita de defensinas. |
| Lipopeptídeo | `Lip` | Peptídeos covalentemente ligados a uma porção lipídica. |
| Prolamina-like | `Prl` | Peptídeos com características similares às prolaminas (proteínas de reserva). |
| Peptídeo Linear Catiônico Alfa-Hélice | `Lca` | Peptídeos lineares que adotam estrutura alfa-helicoidal anfifílica. |
| Bacteriocina | `Bac` | Peptídeos produzidos por bactérias com atividade contra outras bactérias. |
| Lantibiótico | `Lan` | Peptídeos policíclicos contendo lantionina, produzidos por bactérias. |
| Beta-barrel (poro transmembrana) | `Bbl` | Peptídeos que formam estruturas beta-barril, frequentemente em membranas. |
| Desconhecido/Novel | `Unk` | Classe estrutural/funcional ainda não determinada ou não se encaixa nas demais. |

*Observação:* Esta lista pode ser expandida conforme novas classes surjam nos projetos do LGBV.

---

## 5. [TipoAMP] - Natureza da Origem ou Status Computacional/Experimental do Peptídeo

Este componente é crucial para entender como o peptídeo foi obtido ou identificado.

| Abreviação | Significado/Definição | Exemplo de Cenário de Origem |
| :--- | :--- | :--- |
| **AMPnat** | **Peptídeo Natural** <br> AMP isolado e identificado diretamente de uma fonte biológica (animal, planta, microrganismo), com sua sequência e atividade nativa determinadas e confirmadas experimentalmente *in vitro* ou *in vivo*. A descoberta primária é experimental. | Uma nova defensina é purificada do extrato de sementes de *Vigna unguiculata*. Sua sequência é determinada por espectrometria de massa, e sua atividade antifúngica é confirmada em bioensaios. <br> *Ex: `VuDefAMPnat001v1`* |
| **AMPcom** | **Peptídeo Computacional (Predito)** <br> Sequência peptídica candidata a AMP, identificada unicamente por ferramentas de bioinformática (*in silico*) a partir de bancos de dados genômicos, transcriptômicos ou proteômicos. Neste estágio, não há (ou não havia no momento da primeira catalogação) confirmação experimental de sua existência como peptídeo funcional ou de sua atividade. | Um pipeline de bioinformática analisa o genoma de *Arabidopsis thaliana* e prediz uma nova sequência com alta probabilidade de ser uma defensina, baseada em homologia e modelos de aprendizado de máquina. A sequência ainda não foi sintetizada ou testada. <br> *Ex: `AtDefAMPcom001v1`* |
| **AMPmod** | **Peptídeo Modificado** <br> Versão alterada de um AMP preexistente (seja um `AMPnat`, um `AMPcom` que foi sintetizado, ou um `AMPsyn` anterior). A modificação é intencional, visando, por exemplo, otimizar atividade, aumentar estabilidade, reduzir toxicidade, ou alterar especificidade. As modificações podem incluir substituições, deleções, adições de aminoácidos, ciclização, conjugação com outras moléculas, etc. | Um `AMPnat` conhecido (ex: `EcBacAMPnat005v1`) tem sua atividade aumentada após a substituição de dois resíduos de Leucina por Arginina. Esta nova sequência modificada seria catalogada como um `AMPmod`. <br> *Ex: `EcBacAMPmod001v1`* (onde `001` é o próximo número sequencial para `AMPmod` da classe `Bac` em `Ec`, e `v1` indica a primeira versão desta modificação específica). O metadado deve referenciar o peptídeo original. |
| **AMPsyn** | **Peptídeo Sintético (*de novo*)** <br> AMP desenhado e sintetizado artificialmente em laboratório, sem um molde direto de uma sequência natural ou computacionalmente predita preexistente e idêntica. O design é racional, podendo ser baseado em princípios físico-químicos, padrões estruturais de AMPs, algoritmos de inteligência artificial, ou combinação de fragmentos de diferentes peptídeos. | Uma equipe projeta uma nova sequência peptídica alfa-helicoidal anfifílica com 15 aminoácidos, combinando características ideais (carga positiva, hidrofobicidade controlada) para atividade contra bactérias Gram-negativas, sem que essa sequência exata exista em bancos de dados naturais. <br> *Ex: `SynLcaAMPsyn001v1`* (se design genérico) ou *`MetaLipAMPsyn003v1`* (se desenhado a partir de inspiração em lipopeptídeos de metagenoma). |

*Observação sobre `AMPcom` validado:* Se um `AMPcom` é posteriormente sintetizado e sua atividade é confirmada experimentalmente, ele **não** se torna `AMPnat`. Ele continua sendo `AMPcom` em sua origem, mas seu status de validação deve ser anotado nos metadados. Ex: `AtDefAMPcom001v1` (Metadados: Status = Validado experimentalmente, Data da validação = AA-MM-DD).

---

## 6. [Número] - Identificador Numérico Sequencial

Este componente é um número sequencial de três dígitos (com zeros à esquerda, ex: `001`, `023`, `104`) que individualiza o peptídeo dentro de sua categoria.

* **Lógica de Atribuição:**
    * O número é sequencial e único para cada nova entrada de peptídeo, considerando a combinação de `[Espécie][Classe][TipoAMP]`.
    * Por exemplo, `AtDefAMPnat001v1` é o primeiro AMP natural da classe Defensina em *Arabidopsis thaliana*. O próximo AMP natural da mesma classe e espécie seria `AtDefAMPnat002v1`.
    * Se um novo AMP predito (*AMPcom*) da classe Defensina em *Arabidopsis thaliana* for identificado, ele seria `AtDefAMPcom001v1` (se for o primeiro *AMPcom* dessa combinação).
* **Ordenação para Atribuição Inicial (sugestão para consistência):**
    * **A. Genomas Montados:** A primeira varredura para identificação/predição de AMPs pode seguir a ordem dos cromossomos ou scaffolds (ex: Chr1, Chr2,...). Peptídeos de organelas (mitocôndrias, cloroplastos) são numerados após os cromossômicos.
        * *Exemplo:* Ao analisar *Arabidopsis thaliana*:
            * Primeira defensina natural encontrada no Cromossomo 1: `AtDefAMPnat001v1`
            * Segunda defensina natural encontrada no Cromossomo 1: `AtDefAMPnat002v1`
            * Primeira defensina natural encontrada no Cromossomo 3: `AtDefAMPnat003v1`
    * **B. Genomas em Draft ou Metagenomas:** A numeração pode seguir a ordem dos contigs/scaffolds conforme aparecem no arquivo de montagem, ou por ordem de tamanho (do maior para o menor contig, ou vice-versa, desde que padronizado).
        * *Exemplo:* Ao analisar um metagenoma:
            * Primeiro lipopeptídeo predito (AMPcom) no Contig A: `MetaLipAMPcom001v1`
            * Segundo lipopeptídeo predito (AMPcom) no Contig A: `MetaLipAMPcom002v1`
            * Primeiro lipopeptídeo predito (AMPcom) no Contig B: `MetaLipAMPcom003v1`

*Importante:* Uma vez que um número é atribuído a um peptídeo específico (ex: `AtDefAMPnat001v1`), esse número (`001` para esta combinação `AtDefAMPnat`) não deve ser reutilizado para um peptídeo diferente dentro da mesma combinação `[Espécie][Classe][TipoAMP]`.

---

## 7. [Versão] - Controle de Iterações e Modificações Específicas

Este componente indica a versão da sequência peptídica específica.

* **Formato:** Inicia com `v` seguido de um número (ex: `v1`, `v2`, `v10`).
* **Lógica:**
    * **`v1`**: Sempre representa a primeira versão da sequência catalogada para um determinado identificador `[Espécie][Classe][TipoAMP][Número]`.
        * Ex: `AtDefAMPnat001v1` é a sequência original da defensina natural 001 de *A. thaliana*.
        * Ex: `ZmCysAMPcom003v1` é a sequência original do AMPcom rico em cisteína 003 de *Z. mays*.
        * Ex: `EcBacAMPmod001v1` é a primeira sequência resultante de um processo de modificação que gerou o AMPmod número 001 da classe Bacteriocina em *E. coli*. (O metadado deste `AMPmod` deve indicar qual peptídeo original deu origem a ele, ex: "Modificado a partir de `EcBacAMPnat005v1`").
    * **`v2`, `v3`, ...**: Indicam iterações subsequentes ou otimizações realizadas **sobre a mesma entrada base** `[Espécie][Classe][TipoAMP][Número]`.
        * Isto é particularmente relevante para `AMPmod` e `AMPsyn`. Se `EcBacAMPmod001v1` é submetido a uma nova rodada de modificações (ex: mais uma substituição de aminoácido para tentar melhorar ainda mais sua atividade), a nova sequência resultante será `EcBacAMPmod001v2`. O peptídeo "pai" desta `v2` é o `EcBacAMPmod001v1`.
        * Da mesma forma, se um `AMPsyn001v1` é refinado, a nova versão é `AMPsyn001v2`.
    * Um `AMPnat` ou `AMPcom` geralmente permanecerá como `v1`, pois sua sequência é, por definição, a natural ou a predita originalmente. Se uma variante natural de um `AMPnat` for descoberta (ex: um alelo com uma pequena diferença), ela deveria ser catalogada como um novo `AMPnat` com um novo número (ex: `AtDefAMPnat002v1`) e os metadados devem indicar a relação de homologia ou alelismo. A modificação intencional de um `AMPnat` o transforma em um `AMPmod`.

**Exemplos de uso de Versão:**

* `ZmDefAMPmod005v1`: A primeira versão de um peptídeo de Zea mays, classe Defensina, que foi modificado (AMPmod) e recebeu o número sequencial 005 para esta categoria.
* `ZmDefAMPmod005v2`: Uma segunda modificação ou otimização aplicada sobre a sequência de `ZmDefAMPmod005v1`.

---

## 8. Exemplos Completos de Nomenclatura e Interpretação

| Identificador Completo | Interpretação Detalhada |
| :--- | :--- |
| `AtDefAMPcom001v1` | *Arabidopsis thaliana*, classe Defensina, tipo Peptídeo Computacional (predito *in silico*), número sequencial 001 para esta categoria, versão original da sequência predita. |
| `ZmCysAMPnat010v1` | *Zea mays*, classe Cisteína-rich, tipo Peptídeo Natural (isolado e validado experimentalmente), número sequencial 010 para esta categoria, versão original da sequência natural. |
| `GmThlAMPcom007v1` | *Glycine max*, classe Tiorredoxina-like, tipo Peptídeo Computacional, número sequencial 007, versão original da sequência predita. |
| `VuCycAMPnat012v1` | *Vigna unguiculata*, classe Ciclopeptídeo, tipo Peptídeo Natural, número sequencial 012, versão original da sequência natural. |
| `MetaLipAMPsyn003v1` | Metagenoma (ou inspirado em dados de metagenoma), classe Lipopeptídeo, tipo Peptídeo Sintético (*de novo*), número sequencial 003, primeira versão do design sintético. |
| `MetaLipAMPsyn003v2` | Metagenoma, classe Lipopeptídeo, tipo Peptídeo Sintético (*de novo*), número sequencial 003, segunda versão (otimizada ou alterada) do design sintético `MetaLipAMPsyn003`. |
| `EcBblAMPnat002v1` | *Escherichia coli*, classe Beta-barrel, tipo Peptídeo Natural, número sequencial 002, versão original. |
| `EcBblAMPmod001v1` | *Escherichia coli*, classe Beta-barrel, tipo Peptídeo Modificado, número sequencial 001 para AMPmods desta classe/espécie. Esta é a primeira versão desta modificação específica. (Metadados devem indicar qual peptídeo original, ex: `EcBblAMPnat002v1`, foi modificado). |
| `EcBblAMPmod001v2` | *Escherichia coli*, classe Beta-barrel, tipo Peptídeo Modificado, número sequencial 001. Esta é a segunda versão (uma nova modificação/otimização) da linhagem de modificação `EcBblAMPmod001`, derivada de `EcBblAMPmod001v1`. |

---

## 9. Recomendações Adicionais para Gerenciamento de Dados

* **Nomenclatura de Arquivos:** Utilizar o identificador padronizado como base para nomear arquivos de sequência (FASTA), estruturas (PDB), planilhas de resultados, etc.
    * Ex: `AtDefAMPcom001v1.fasta`, `MetaLipAMPsyn003v2_results.xlsx`.
* **Metadados Detalhados:** Manter uma planilha ou banco de dados centralizado com metadados ricos para cada peptídeo. Campos sugeridos:
    * `ID_LGBV` (o identificador completo)
    * `Nome_Comum` (se houver)
    * `Sequencia_AA` (baseado apenas em AAs canônicos)
    * `Origem_Peptideo_Pai` (para `AMPmod`, referenciar o ID do peptídeo original)
    * `Descricao_Modificacao` (para `AMPmod` e versões > v1)
    * `Fonte_Dados_Original` (ex: ID do genoma no NCBI, Phytozome ou in house, ID do artigo...)
    * `Localizacao_Genomica` (Cromossomo/Contig, coordenadas, gene ID)
    * `Ferramentas_Predicao_Classe` (ex: InterProScan ID, HMMER e-value)
    * `Ferramentas_Predicao_AMP` (ex: CAMPr, AMPScanner score, DeepAMP resultado)
    * `Status_Experimental` (ex: Não testado, Sintetizado, Atividade confirmada contra X, valores de MIC)
    * `Data_Registro` (DD/MM/AA)
    * `Pesquisador_Responsavel` (nome e sobrenome)
    * `Projeto_Associado` (título do proj. de IC, mestrado ou doutorado)
    * `Publicacoes_Associadas` (DOIs)
    * `Notas` (observações gerais)
* **Controle de Versão de Metadados:** Registrar alterações na planilha de metadados ou no banco de dados utilizando um sistema de versionamento ou changelogs.
* **Ferramentas:** Considerar o uso de bancos de dados relacionais (CSV gerenciado com Git, SQLite) conforme a escala da base. Scripts (Python ou Bash) podem auxiliar na geração de IDs e na manutenção da consistência.

---

## 10. Recursos Futuros

* Modelo de planilha padrão para metadados de AMPs.
* Script interativo para auxiliar na geração de identificadores padronizados, também incluídos na nova plataforma de consulta do LGBV.
* Integração da lógica de nomenclatura em workflows de bioinformática existentes para atribuição automática de IDs a novos AMPs preditos.
* Repositório centralizado para sequências e metadados (em fase final de desenvolvimento por Rafael).

---

**LGBV - 2025.**
