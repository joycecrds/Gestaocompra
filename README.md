# Dashboard de Compras
### Sobre o Projeto

[License](https://github.com/joycecrds/Gestaocompra?tab=MIT-1-ov-file#readme
)

Este é um projeto de Dashboard de Compras desenvolvido como parte de um estudo sobre visualização de dados e análise de compras. O objetivo deste projeto é fornecer uma interface interativa e informativa para análise de dados relacionados a compras, permitindo aos usuários uma visão detalhada e fácil de entender sobre os gastos e tendências.

### Tecnologias Utilizadas
<p>Frontend: (DAX - Data Analysis Expressions) e (M - M Query)<p/>
<p>Backend: Não se aplica. <p/>
<p>Banco de Dados: Microsoft Excel <p/><br/>

### Instalação e Uso
Git clone
```
[https://github.com/joycecrds/Gestaocompra.git]>
```
Entre no diretório do projeto
```
CD Gestaocompra\bi
```
Requisitos
```
https://github.com/users/joycecrds/projects/3/views/1
```

### Funcionalidades
1.  Indicador de Entrega

     ><p>Contagem de Pedidos de compras entregues nos últimos anos, separado por situação de entrega: Entrega Antecipada, Entregue no Prazo e Entrega Atrasada.</p> 
     ><p>Aplicado condição em DAX para criar uma nova coluna <strong>"Indicado_entrega"</strong>:</p>
     ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/372b2e25-a294-4707-9d57-b6f39920ce97)
     > Demonstrativo de Entrega por situação
     ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/7b10bfe0-e26d-4a58-8275-300d573ae212)

2.  Lead Time
   > <p>Indicador para medir o tempo em que a compra é requisitada, desde a solicitação de compra ao recebimento da mercadoria.</p>
   ><p>Aplicado Lead time considerando o tempo médio Pedido de compra x Recebimento.</p>
   ><p>Indicador importante para gestão de compra, auxiliando no planejamento do seu nívei de estoque de forma mais precisa, evitando excessos ou falta de produtos.</p>
   > Criada medição DAX lead_time_Ped_rec:
   ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/aca7239e-789a-47a7-acc9-94f99482720b).

   ><p>Aplicado Lead time considerando o tempo médio Solicitação x Recebimento</p>
   ><p>Este indicador é crucial para garantir o atendimento eficiente das solicitações internas de produtos ou materiais. Se um departamento solicita determinado item e leva muito tempo para recebê-lo, isso pode prejudicar suas operações e a produtividade.</p>
   >Criada medição DAX lead_time_Sol_rec:
   ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/9395260b-fc07-492f-85e0-748af2d8fe5d)
   >Demonstrativo Lead Time:</p>
   ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/bfb6aca8-0cb6-4f75-8e40-2a5f9d028c13)


3.  Ranking Melhores fornecedores
   <p>Ranking dos melhores fornecedores é essencial para a seleção estratégica de parceiros de negócios.</p>
   <p>Apresentado o ranking dos 4 melhores fornecedores. Os melhores fornecedores são aqueles onde a situação dos pedidos foram "Entregue no prazo" e "Entrega Antecipado".</p>
<p>Pedidos com o status Entrega Atrasada não serão considerados no ranking</p>
<p>Criada a medida DAX para >Contg_Entrega< </p>
   <p>Esta fórmula será usada para calcular a quantidade de entregas que foram "Entrega Antecipada" ou "Entregue no Prazo" em um conjunto de dados chamado "mov_compras".</p>
   <p>Portanto, o resultado final da fórmula CONTG_Entrega será a contagem total de entregas que foram "Entrega Antecipada" ou "Entregue no Prazo" na tabela "mov_compras". </p>
   <p>Criada a medida DAX >Rankin_Entrega<</p>
<p> fórmula está sendo usada para calcular o ranking dos fornecedores com base na contagem de entregas que foram "Entrega Antecipada" ou "Entregue no Prazo" em um conjunto de dados chamado "mov_compras".</p>
<p>Criada a medida >DAX >Rank_entg_1< </p>
<p>fórmula está sendo usada para calcular a quantidade de entregas que foram "Entrega Antecipada" ou "Entregue no Prazo" para o fornecedor que está em primeiro lugar no ranking de fornecedores com base nas entregas.</p>
<p>Criado a mesma condições para os Ranking 2, 3 e 4 </p>
<p>Criada a medida >Rank_IMG_1< </p>
<p>fórmula DAX está sendo usada para obter a imagem associada ao fornecedor que está em primeiro lugar no ranking de fornecedores com base nas entregas "Entrega Antecipada" ou "Entregue no Prazo".</p>
<p> Associado na medida Rank_entg_1, mostrar a imagem do fornecedor associado ao ranking</p>

   *****CRIAR UM VIDEO DE ANIMAÇÃO DO ranking****
   ****INCLUIR O FONTE DO DAX DE CADA MEDIDA****


4.  Volumetria média Pedido Emergencial
<p>O indicador de Volumetria de Pedidos Emergenciais permite identificar tendências ao longo do tempo. Se houver um aumento significativo no número de pedidos emergenciais, isso pode indicar problemas na cadeia de suprimentos, como falta de planejamento, falhas de fornecimento ou problemas de qualidade.</p>





