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
Visualização Dashboard de Compras :wink: 
```
https://app.powerbi.com/view?r=eyJrIjoiYTA1ZTlmYWItMWVmNy00NGE5LTgwNTktNmJhMGIwODZmMjhlIiwidCI6IjFmZjZiYzdkLTU2ZmItNGY1Zi1hYmFlLTI4NjVhN2Q2YjlkMyJ9
```

## Funcionalidades
### 1. Indicador de Entrega

Contagem de Pedidos de compras entregues nos últimos anos, separado com as situações de entrega: Entrega Antecipada, Entregue no Prazo e Entrega Atrasada.</p> 
Aplicado condição em DAX para criar uma nova coluna <strong>"Indicado_entrega"</strong>.
```
Indicado_entrega = IF(
    mov_compras[Prazo de Entrega]> mov_compras[Data Recebimento],
    "Entrega Antecipada",
    IF(
        mov_compras[Prazo de Entrega] < mov_compras[Data Recebimento],
        "Entrega Atrasada",
        IF(
            mov_compras[Prazo de Entrega] == mov_compras[Data Recebimento],
            "Entregue no Prazo"
        )
    )
)
```

 $${\color{Orange}DEMONSTRATIVO \space DE \space ENTREGA}$$

![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/323014b5-9cc5-461e-bd09-0621f79c63d8)

### 2. Lead Time
Indicador para medir o tempo em que a compra é requisitada, desde a solicitação de compra ao recebimento da mercadoria.</p>
Aplicado Lead time considerando o tempo médio do Pedido de compra x Recebimento.</p>
Indicador importante para gestão de compra, auxiliando no planejamento do seu nívei de estoque de forma mais precisa, evitando excessos ou falta de produtos.</p>
Criada a medição DAX utilizando a função AVERAGEX. A função esta sendo usada para calcular a média de uma expressão calculada para cada linha de uma tabela. Neste caso, a expressão calculada é a diferença em dias entre a coluna Emissão do Pedido e a coluna Data Recebimento de cada linha. Considerando na estrutura da condição a função DATEDIFF, calculando a diferença em dias entre a data de emissão do pedido e a data de recebimento.
</p>
Aplicado Lead time considerando o tempo médio da Solicitação x Recebimento.</p>
Este indicador é crucial para garantir o atendimento eficiente das solicitações internas de produtos ou materiais. Se um departamento solicita determinado item e leva muito tempo para recebê-lo, isso pode prejudicar suas operações e a produtividade.</p>

```
lead_time_Ped_rec = AVERAGEX(
    mov_compras,
    DATEDIFF(mov_compras[Emissão do Pedido], mov_compras[Data Recebimento],DAY)
)
```
```
lead_time_Sol_rec = AVERAGEX(
    mov_compras,
    DATEDIFF(mov_compras[Data da Solicitação], mov_compras[Data Recebimento],DAY)
)
```
 $${\color{Orange}LEAD\space TIME}$$
 
![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/5d323570-315b-4493-a05c-b0d9e53f9e8f)

### 3. Ranking Melhores fornecedores
Ranking dos melhores fornecedores é essencial para a seleção estratégica de parceiros de negócios.</p>
Apresentando o ranking dos 3 melhores fornecedores. Os melhores fornecedores são aqueles onde a situação dos pedidos foram "Entregue no prazo" e "Entrega Antecipado".</p>
>[!IMPORTANT]
>Pedidos com o status Entrega Atrasada não está sendo considerado no ranking.

Criada a medida DAX para  __Contg_Entrega__ </p>
Fórmula usada para calcular a quantidade de entregas com a situação "Entrega Antecipada" ou "Entregue no Prazo". </p>
Portanto, resultado final da fórmula _CONTG_Entrega_ será a contagem total de entregas que foram "Entrega Antecipada" ou "Entregue no Prazo" na tabela "mov_compras". </p>
```
Contg_Entrega = 
 CALCULATE(
    SUMX(
        mov_compras,
        IF(
            mov_compras[Indicado_entrega] = "Entrega Antecipada" || mov_compras[Indicado_entrega] = "Entregue no Prazo",
            1,
            0
        )
    )
 )
```

Criada a medida DAX __Rankin_Entrega__ </p>
Fórmula usada para calcular o ranking dos fornecedores com base na contagem de entregas que foram __"Entrega Antecipada"__ ou __"Entregue no Prazo"__ em um conjunto de dados chamado "mov_compras". </p>
```
Rankin_Entrega = 
RANKX(
    FILTER(
        ALL(mov_compras[Fornecedor]),
        CALCULATE(
            SUMX(
                mov_compras,
                IF(
                    mov_compras[Indicado_entrega] = "Entrega Antecipada" || mov_compras[Indicado_entrega] = "Entregue no Prazo",
                    1,
                    0
                )
            )
        )
    ),
    [Contg_Entrega],
    ,
    DESC,
    Dense
)
```

Criada a medida DAX __Rank_entg_1__ </p>
Fórmula usada para calcular a quantidade de entregas que foram "Entrega Antecipada" ou "Entregue no Prazo" para o fornecedor que está em primeiro,segundo e terceiro lugar no ranking de fornecedores com base nas entregas.</p>
```
Rank_entg_1 = 
CALCULATE(
    [Contg_Entrega],
    FILTER(
        VALUES(mov_compras[Fornecedor]),
        [Rankin_Entrega] = 1
    )
)
```

Criada a medida __Rank_IMG_1__ </p>
Fórmula DAX usada para obter a imagem associada ao fornecedor que está em primeiro, segundo e terceiro lugar no ranking de fornecedores com base nas entregas "Entrega Antecipada" ou "Entregue no Prazo".</p>
Repositório de imagens dos fornecedores está na tabela __[FORNECEDOR]__ - coluna __[ImagemFornec]__ .
```
Rank_IMG_1 = 
CALCULATE(
    SELECTEDVALUE(Fornecedor[ImagemFornec]),
    FILTER(
        VALUES(mov_compras[Fornecedor]),
        [Rankin_Entrega] = 1
    )
)
```

****INCLUIR ANIMAÇÃO DO GRAFICO **** </p>

### 4. Volumetria Pedidos de compra
Apresentação da volumetria dos pedidos de compras classificados Urgentes e não urgentes.</p>
O indicador Pedidos Emergencial permite identificar as tendências ao longo do tempo. Se houver um aumento significativo no número de pedidos emergenciais, indicando problemas na cadeia de suprimentos, como falta de planejamento, falhas de fornecimento ou problemas de qualidade.</p>
Para mostar a demonstração foi criada a medida em DAX, utilizando a função COUNTROWS. Contagem de pedidos "comuns" e pedidos emergenciais</p>
```
Contagem_pedido = 
COUNTROWS(FILTER(mov_compras, mov_compras[Emergencial] = "0"))

```
```
Contagem_Pedidos_Emergenciais = 
COUNTROWS(FILTER(mov_compras, mov_compras[Emergencial] = "Pedido emergencial"))

```
 $${\color{Orange}DEMONSTRAÇÃO\space VOLUMETRIA \space DE \space PEDIDOS}$$
 
![image](https://github.com/joycecrds/Gestaocompra/assets/160512672/8a8d6bc3-ccf8-427d-aed9-8427c44b4ab0)

## Referências
> Lead Time: como calcular e guia prático para otimizar o indicador _ _ _ _ _ _  https://www.site.moki.com.br/post/lead-time#:~:text=C%C3%A1lculo%3A%20Lead%20Time%20%3D%20tempo%20de,produ%C3%A7%C3%A3o%20e%20entrega%20de%20produtos. </p>
> Gestão de pedidos e seus indicadores de desempenho _ _ _ _ _ __ _ _ _ _ __ _ _ https://moveideias.com.br/gestao-de-pedidos-e-seus-indicadores-de-desempenho/. </p>

