# Tabela dimensão calendário  

|Idioma/Culture|Doc|
|:--|:---|
|🇵🇹|README.md(atual)|
|🇺🇸|[README_en.md](./README_en.md)|
|🇪🇸|[README_es.md](./README_es.md)|

> [!IMPORTANT]  
Antes de tudo possua pelo menos a versão de janeiro de 2025 do Power BI Desktop instalado.  
Habilite a opção em Arquivo > Opções e configurações > Opções > Recursos de visualização > ✅ Exibição TMDL

## 1. Modo local diretamente no Power BI Desktop com TMDL  

> Este método é destinado àqueles que querem uma tabela dimensão calendário independente por modelo semântico.  
> Este é o único método que não exige nenhum licenciamento.  

Prós:
- Independência de outros itens como dataflows, lakehouses e warehouses.  

Contras:  
- Mais tempo de atualização.
- Mais volume de dados no Power BI Serviço.  
- Possível desencontro entre modelos.  

Intruções: 
- Crie ou importe qualquer tabela para o Power BI Desktop;  
- Clique em no botão `TMDL` na guia lateral esquerda;  
- Copie o código para o idioma desejado em [TMDLDesktop](./TMDLDesktop/) e cole na área do código.
- Clique em `Aplicar` e no alerta logo acima em `Atualizar agora`.  


## 2. Dataflow gen1 Import (PRO)

> Este método é indicado para àqueles que querem uma tabela dimensão calendário única para toda a organização utilizando os dataflows gen1.  
> Este é o método mais indicado para os usuários do licenciamento PRO.  

Prós: 
- Única fonte de datas para a organização;  
- Padronização;  
- Performance; 
- Reaproveitamento.  

Contras:  
- Mais passos para configuração inicial.  

Instruções:  
- Crie um novo dataflow gen1;  
- Crie uma consulta em branco;  
- Copie o código para o idioma desejado em [PowerQueryOrDataflow](./PowerQueryOrDataflow/) e cole no editor avançado da consulta em branco;  
- Renomeie sua tabela para DimCalendario;    
- Clique em `Salvar e fechar`;  
- Salve o dataflow e dê o nome de DfwCalendario;  
- Atualize o dataflow;  
- Configure a atualização automática diariamente às 00:00 de acordo com o fuso horário;
- Abra um arquivo em branco no Power BI Desktop;    
- Na guia `Página Inicial` Clique em `Obter dados` e depois em `Fluxos de dados`;  
- Caso solicitado faça o login com sua conta e senha;  
- Encontre o Workspace e o Dataflow `FlwCalendario`  e marque a tabela `dCalendario` e clique em `Carregar`;  
- Clique em no botão `TMDL` na guia lateral esquerda;  
- Arraste a tabela DimCalendario da guia Tabelas a direita para o campo do código do Script1;  
- Crie o Script2 clicando em `+` na guia inferior;  
- Copie o código do idioma correpondente em [TMDLAfterDataflow](./TMDLAfterDataflow/) e cole no Script2. Não aplique!;
- Retorne ao Script1, role até o final do código e copie desde 'partition' até o final;
- Vá até o Script2, role até o final e cole por cima do 'partition' até o final;
- Clique em `Aplicar`.  


### 3. Modo Direct Lake (Fabric Users)  

> Este modo é indicado para àqueles que utilizam modelos semânticos em Direct Lake do Fabric.  
> O código é atualizado através de Dataflows gen2 podendo ser alocados tanto em Lakehouses como em Warehouses.  
> Para a demonstração será utilizado a carga em um Warehouse simulando a camada gold de nosso projeto.  

Prós:  
- Única fonte de datas para a organização;  
- Padronização;  
- Performance; 
- Reaproveitamento.  

Contras:  
- Mais passos para configuração inicial.  

Instruções:  
- Crie um Workspace e configure para uma Capacidade da Malha (ou Trial);  
- Crie um novo Warehouse;  
- Dê o nome do Warehouse como DW_Gold;  
- Dê dentro do Warehouse clique em `Obter dados` e depois escolha `Novo Fluxo de Dados Gen2`;  
- Coloque o nome de DfwCalendario e marque a opção `Habilitar a integração do Git...` e clique em `Criar`;  
- Crie uma consulta em branco;  
- Copie o código para o idioma desejado em [PowerQueryOrDataflow](./PowerQueryOrDataflow/) e cole no editor avançado da consulta em branco;  
- Renomeie sua tabela para DimCalendario;    
- Salve o dataflow e feche;
- Aguarde a publicação e a atualização inicial. Caso não ocorra, force a atualização;    
- Configure a atualização automática diariamente às 00:00 de acordo com o fuso horário via agendamento ou Data Pipelines;
- Abra o warehouse, clique em `Relatórios`  depois em `Novo modelo semântico`;  
- Escolha a tabela `dCalendario` e outras tabelas do seu modelo desejado;
- Dê o nome de `SMGold` e salve;
- Abra o Power BI Desktop e na guia `Página inicial` clique em OneLake catalog e depois em `Power BI Semantic Models`;  
- Clique no modelo `SMGold` mas não clique no botão conectar e sim na seta ao lado e depois em `Editar`;  
- Clique em no botão `TMDL` na guia lateral esquerda;  
- Arraste a tabela DimCalendario da guia Tabelas a direita para o campo do código do Script1;  
- Crie o Script2 clicando em `+` na guia inferior;  
- Copie o código do idioma correpondente em [TMDLDirectLake](./TMDLDirectLake/) e cole no Script2. Não aplique!;
- Retorne ao Script1, role até o final do código e copie desde 'partition' até o final;
- Vá até o Script2, role até o final e cole por cima do 'partition' até o final;
- Aplique e atualize.  
- Clique em `Aplicar`.  

