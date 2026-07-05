# Signal – Backend de Detecção de Eventos em Mercados Preditivos

> Trabalho de Conclusão de Curso (TCC)
> Bacharelado em Sistemas de Informação – Universidade Federal de Pernambuco (UFPE)

## Visão Geral

O **Signal** é um sistema desenvolvido para monitorar mercados preditivos, identificar alterações estatisticamente relevantes nas probabilidades negociadas e gerar automaticamente narrativas explicativas em linguagem natural.

O pipeline implementado neste notebook integra coleta de dados, detecção de eventos, deduplicação, geração de narrativas por modelos de linguagem e avaliação quantitativa e qualitativa dos resultados.

A versão disponibilizada neste repositório corresponde ao artefato utilizado nos experimentos descritos no Trabalho de Conclusão de Curso.

---

# Objetivos

O sistema foi desenvolvido para:

* monitorar contratos da plataforma Polymarket;
* detectar alterações relevantes nas probabilidades de mercado;
* eliminar eventos duplicados decorrentes do mesmo movimento;
* produzir narrativas econômicas automaticamente;
* avaliar a qualidade dos sinais gerados;
* medir a qualidade preditiva utilizando Brier Score;
* fornecer um pipeline reproduzível para pesquisas futuras.

---

# Pipeline do sistema

O notebook executa automaticamente as seguintes etapas:

```
Configuração
        │
        ▼
Coleta de mercados (Polymarket API)
        │
        ▼
Pré-processamento
        │
        ▼
Detector contextual (z-score)
        │
        ▼
Classificação da magnitude
        │
        ▼
Deduplicação por impacto
        │
        ▼
Geração das narrativas
        │
        ▼
Avaliação qualitativa
        │
        ▼
Brier Score
        │
        ▼
Exportação dos resultados
```

---

# Organização do notebook

O notebook está dividido em células independentes.

## Célula 0

Configuração das chaves de acesso e instalação das dependências.

Também contém o mecanismo para reprocessamento de eventos específicos.

---

## Célula 1

Implementa toda a comunicação com a API da Polymarket, incluindo:

* coleta dos mercados;
* download do histórico;
* tratamento de falhas;
* funções auxiliares;
* limpeza dos dados.

---

## Célula 1b

Realiza a tradução automática dos títulos dos contratos para português.

---

## Célula 2

Implementa o detector de eventos.

Principais funcionalidades:

* cálculo do z-score contextual;
* classificação da magnitude do evento;
* detecção de anomalias;
* filtragem inicial.

---

## Célula 3

Executa a análise de sensibilidade dos limiares do detector.

São comparados diferentes valores de (z^{*}), permitindo avaliar:

* quantidade de sinais detectados;
* cobertura líquida;
* distribuição de magnitude;
* robustez do detector.

---

## Célula 4

Pipeline responsável pela geração das narrativas.

Atualmente suporta múltiplos modelos de linguagem, incluindo:

* Gemini
* OpenRouter

As narrativas produzidas incluem:

* descrição do evento;
* interpretação econômica;
* possíveis impactos para o Brasil;
* controle de causalidade.

---

## Célula 5

Implementa a rubrica de avaliação qualitativa das narrativas.

As avaliações consideram quatro dimensões:

* Ancoragem factual;
* Integração do tema;
* Canal Brasil;
* Controle de causalidade.

Cada narrativa recebe uma pontuação máxima de 12 pontos.

---

## Célula 6

Pipeline principal.

Responsável por integrar todas as etapas do sistema:

* processamento completo;
* cálculo do Brier Score;
* consolidação dos resultados;
* exportação dos arquivos finais.

---

## Célula 7

Executa o sistema completo.

Após a execução são produzidos automaticamente os arquivos utilizados nas análises apresentadas no TCC.

---

# Dependências

O notebook utiliza principalmente:

* Python 3.10+
* pandas
* numpy
* requests
* google-genai

Caso necessário, instale manualmente:

```bash
pip install google-genai requests pandas numpy
```

---

# Configuração

Antes da execução configure as chaves de acesso.

Exemplo:

```python
GEMINI_KEY = "SUA_CHAVE"
OPENROUTER_KEY = "SUA_CHAVE"
```

---

# Como executar

1. Clone este repositório.

```bash
git clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
```

2. Abra o notebook.

```bash
jupyter notebook
```

ou

```bash
jupyter lab
```

3. Configure as chaves de API.

4. Execute as células em sequência.

---

# Resultados produzidos

Ao término da execução o sistema produz:

* eventos detectados;
* eventos deduplicados;
* narrativas geradas;
* avaliação qualitativa;
* Brier Score;
* arquivos JSON de saída.

Esses resultados correspondem aos experimentos apresentados no Trabalho de Conclusão de Curso.

---

# Reprodutibilidade

Os experimentos descritos no TCC foram executados utilizando esta versão do notebook.

Alterações em parâmetros como:

* limiar (z^{*});
* janela temporal;
* configuração do detector;
* modelos de linguagem;

podem produzir resultados diferentes daqueles apresentados na monografia.

---

# Autor

**Erick Daniel Alves de Lima**

Bacharelado em Sistemas de Informação

Centro de Informática – Universidade Federal de Pernambuco (UFPE)

---

# Licença

Este projeto foi desenvolvido para fins acadêmicos.

Os dados coletados pertencem às respectivas plataformas de mercados preditivos e permanecem sujeitos às suas políticas de uso.
