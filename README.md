# 🛠️ Calculadora de Jornada de Trabalho

Esta é uma aplicação web simples, desenvolvida em HTML, CSS e JavaScript puro, projetada para calcular e verificar a jornada de trabalho diária de um colaborador, incluindo advertências baseadas em leis trabalhistas comuns no Brasil (CLT).

O código-fonte completo da calculadora é um arquivo HTML único, que contém o CSS e o JavaScript embarcados.

---

## 🚀 Funcionalidades Principais

| Funcionalidade | Descrição |
| :--- | :--- |
| **Cálculo Preciso** | Utiliza a conversão de todos os horários para **minutos** internamente, eliminando erros de precisão do JavaScript em operações com números decimais (`floating-point`). |
| **Controle de Jornada** | Calcula a duração exata dos dois períodos de trabalho, o tempo de intervalo e a diferença final (Hora Extra ou Atraso) em relação à jornada prevista. |
| **Advertências CLT** | Emite alertas visuais para: |
| | - Intervalo de Almoço menor que 1 hora ou maior que 2 horas. |
| | - Período de trabalho contínuo excedendo 6 horas. |
| | - Jornada total excedendo 10 horas. |
| **Persistência de Dados** | Um **Histórico de Cálculos** é mantido utilizando `localStorage`, permitindo a visualização e o carregamento de até 10 registros anteriores. |
| **Exportação** | Botão dedicado para **Imprimir Resultados**, formatando a saída de modo otimizado para papel ou PDF. |

---

## ⚙️ Estrutura e Tecnologia

### 1. Requisitos

* Navegador Web Moderno (Chrome, Firefox, Edge, etc.).
* Não requer instalação de servidor (funciona localmente).

### 2. Arquivos Necessários

Para rodar o projeto, você precisa de dois arquivos:

1.  **`calculadora.html`** (ou `index.html`): Contém todo o código da aplicação (formulário, estilos e lógica).
2.  **`README.md`** (Este arquivo): Documentação do projeto.

### 3. Detalhes da Implementação (JavaScript)

O arquivo JavaScript embarcado utiliza três funções auxiliares cruciais para a lógica:

| Função | Finalidade |
| :--- | :--- |
| `timeToMinutes(timeStr)` | Converte o formato `HH:MM` para um número inteiro de minutos. |
| `minutesToTime(totalMinutes)` | Converte o número total de minutos de volta para o formato `HH:MM`. |
| `calculateDurationInMinutes(start, end)` | Lida com a subtração de horários e com a **passagem da meia-noite** (usando 1440 minutos como referência para 24h). |

### 4. Usabilidade (UX)

Os rótulos foram ajustados para maior clareza:
* "Total de Horas Trabalhadas" foi alterado para **"Jornada Diária Prevista (HH:MM)"**.
* Os campos são numerados (1. Início, 4. Fim) para indicar a ordem correta de preenchimento.

---

## 📝 Como Iniciar

1.  Salve o código da calculadora no seu arquivo HTML.
2.  Abra o arquivo HTML no seu navegador.
3.  Preencha os campos (Jornada Prevista, Entrada, Saída p/ Almoço, Retorno, Saída).
4.  Clique em **"Calcular Jornada"** e verifique os resultados e as advertências no bloco inferior.
