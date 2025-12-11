# 🔧 Sistema de Gerenciamento de Oficina Mecânica

![Status do Projeto](https://img.shields.io/badge/Status-Concluído-green) ![Database](https://img.shields.io/badge/Database-MySQL-blue) ![Tools](https://img.shields.io/badge/Tools-MySQL%20Workbench-orange)

Projeto de modelagem de banco de dados relacional para um cenário de oficina mecânica, desenvolvido como parte do desafio de projeto [DIO/Bootcamp]. O objetivo foi transformar requisitos de negócio em um modelo lógico robusto e funcional.

## 📖 Descrição do Desafio

O projeto consiste na criação de um esquema conceitual e lógico para gerenciar o fluxo de trabalho de uma oficina, cobrindo desde a recepção do veículo até a entrega do serviço.

**A narrativa do sistema inclui:**
* Cadastro de clientes e veículos.
* Gerenciamento de mecânicos e formação de equipes.
* Criação de Ordens de Serviço (OS) contendo serviços (mão-de-obra) e peças.
* Controle de status da OS e cálculo de valores totais.

## 📊 Diagrama Entidade-Relacionamento (EER)

Abaixo está a representação gráfica do modelo desenvolvido no MySQL Workbench.

![Diagrama EER da Oficina](diagrama_oficina.png)
*(Certifique-se de que o arquivo 'diagrama_oficina.png' esteja na raiz do seu repositório)*

## 🧠 Solução e Decisões de Modelagem

Para atender aos requisitos e garantir a integridade dos dados, foram aplicadas as seguintes estratégias:

### 1. Equipes de Mecânicos
Foi estabelecido que um serviço é executado por uma **Equipe**, não por um mecânico isolado.
* Tabela `Equipes`: Entidade que agrupa os profissionais.
* Tabela `Mecanicos`: Possui chave estrangeira ligando à equipe. Isso permite saber quem trabalhou em qual OS indiretamente.

### 2. Composição da Ordem de Serviço (OS)
Uma OS não tem um valor fixo único, ela é a soma de vários itens. Para isso, utilizei relacionamentos **Muitos-para-Muitos (N:M)**:
* **OS + Serviços:** Tabela pivo `OS_Servicos`. Permite que uma OS tenha, por exemplo, "Troca de Óleo" e "Alinhamento".
* **OS + Peças:** Tabela pivo `OS_Pecas`. Permite listar todos os componentes usados (ex: "4 Litros de Óleo", "1 Filtro").

### 3. Controle de Status
Foi criado um campo `ENUM` na tabela de OS para controlar o ciclo de vida do serviço, garantindo que o fluxo lógico seja respeitado (ex: O serviço não pode ser 'Finalizado' se não foi 'Autorizado').
> **Status:** Aberta ➡️ Em Análise ➡️ Aguardando Autorização ➡️ Em Execução ➡️ Finalizada.

## 🗂️ Estrutura do Banco de Dados

As principais entidades criadas foram:

| Tabela | Descrição |
| :--- | :--- |
| **Clientes** | Dados pessoais e contato. |
| **Veiculos** | Carros/Motos associados a um cliente (Placa, Modelo). |
| **OrdensServico** | Tabela central que une Veículo, Equipe e Data. |
| **Mecanicos** | Profissionais com especialidade e endereço. |
| **Pecas** | Catálogo de peças com valor unitário e controle de estoque. |
| **Servicos_Referencia** | Tabela de preços tabelados para mão-de-obra. |

## 🚀 Como Utilizar

Se você deseja replicar este banco de dados em sua máquina:

1.  **Pré-requisitos:** Tenha o MySQL e o MySQL Workbench instalados.
2.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git](https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git)
    ```
3.  **Importe o Script:**
    * Abra o MySQL Workbench.
    * Vá em `File > Open SQL Script`.
    * Selecione o arquivo `script_oficina.sql` (ou o nome que você salvou).
    * Execute todo o script (Raio ⚡).

## 🤝 Contribuições

Sinta-se à vontade para sugerir melhorias, como novas tabelas para "Agendamento" ou "Pagamentos Parcelados". Abra uma *issue* ou envie um *Pull Request*!

---
Desenvolvido por **[Seu Nome]**
