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

     ><p>Contagem de Pedidos de compras entregues nos últimos anos, separar por  situações de entrega: Entrega Antecipada, Entregue no Prazo e Entrega Atrasada.</p> 
     ><p>Aplicado condição em DAX para criar uma nova coluna <strong>"Indicado_entrega"</strong>:</p>
     ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/372b2e25-a294-4707-9d57-b6f39920ce97)
     > Demonstrativo de Entrega por situação
     ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/7b10bfe0-e26d-4a58-8275-300d573ae212)

2.  Lead Time
   > <p>Indicador para medir o tempo em que a compra é requisitada, desde a solicitação de compra ao recebimento da mercadoria.</p>
   ><p>Aplicado Lead time considerando o tempo médio Pedido de compra x Recebimento.</p>
   ><p>Finalidade de medir o tempo que leva desde o momento em que um pedido é emitido até o momento em que os produtos são recebidos ajuda na gestão do estoque</p>
   > Criada medição DAX lead_time_Ped_rec:
   ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/aca7239e-789a-47a7-acc9-94f99482720b).

   ><p>Aplicado Lead time considerando o tempo médio Solicitação x Recebimento</p>
   ><p>Finalidade em para garantir o atendimento eficiente às solicitações internas de produtos ou materiais. Se um departamento solicita determinado item e leva muito tempo para recebê-lo, isso pode prejudicar suas operações e a produtividade.</p>
   >Criada medição DAX lead_time_Sol_rec:
   ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/9395260b-fc07-492f-85e0-748af2d8fe5d)
   >Demonstrativo Lead Time:</p>
   ![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/bfb6aca8-0cb6-4f75-8e40-2a5f9d028c13)


3.  Volumetria média Pedido Emergencial
   

  
- Volumetria média Pedido Emergencial
- Ranking Melhores fornecedores <b/>




