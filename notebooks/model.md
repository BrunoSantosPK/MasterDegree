# Modelo Matemático Integração Lavoura e Pecuária

Este modelo tem como objetivo descrever os relacionamentos entre o cultivo na lavoura e a criação de animais, dentro da lógica da Integração Lavoura-Pecuária demonstrada pela EMBRAPA.

## Variáveis de decisão

AC_{ij} = área em m^{2} plantada do cultivo j no mês i

VC_{ij} = quantidade em kg do cultivo produzido j vendida no mês i

EC_{ij} = quantidade em kg do cultivo produzido j estocado no mês i

CC_{ij} = quantidade em kg do cultivo j comprado no mês i

PC_{ij} = quantidade em kg do cultivo produzido j que é utilizado para consumo dos moradores no mês i

RC_{ijk} = quantidade em kg do cultivo produzido j que é utilizado para alimentação do animal k no mês i

FC_{i} = quantidade em kg de fertilizante comprado no mês i

CA_{ik} = quantidade de lotes do animal k comprados para criação no mês i

VA_{ik} = quantidade de lotes do animal k vendidos no mês i

AA_{ik} = quantidade de lotes do animal k abatidos no mês i

PA_{ik} = quantidade de carne do animal k comprada para cosumo no mês i

RA_{ik} = quantidade em kg de ração comprada para o animal k no mês i

VP_{ik} = quantidade (unidade específica) de produto gerado pelo animal k vendido no mês i

AP_{ik} = quantidade (unidade específica) de produto gerado pelo animal k consumido no mês i

CP_{ik} = quantidade (unidade específica) de produto do animal k comprado no mês i


## Entradas

I = conjunto de meses que serão avaliados no planejamento

J = conjunto de culturas disponíveis para plantação

K = conjunto de animais disponíveis para criação

L = área total da propriedade (m^{2}) disponível para plantio e criação de animais

P = quantidade de pessoas que vivem na propriedade

NAC_{j} = necessidade alimentar da cultura j em kg / (mês . pessoa)

NAA_{k} = necessidade alimentar da carne do animal k em kg / (mês . pessoa)

NAP_{k} = necessidade alimentar do produto gerado pelo animal k em kg / (mês . pessoa)

## Parâmetros

PAC = valor em R\$ / kg do adubo utilizado nas plantações

TCC_{j} = tempo em meses que a cultura j leva para estar pronta para colheita

PYC_{j} = quantidade colhida em kg / m^{2} da cultura j

VCC_{j} = valor em R\$ / kg de compra da cultura j

VVC_{j} = valor em R\$ / kg de venda da cultura j

CCC_{j} = custo em R\$ / m^{2} para plantar a cultura j

CEC_{j} = custo em R\$ / (kg . mês) para armazenar a cultura j

RAC_{j} = requisito em kg / (m^{2} . mês) de adubo que a cultura j necessita

AAC_{jk} = valor binário que indica que a plantação j pode alimentar o animal k

TCA_{k} = tempo em meses que um animal k precisa para estar pronto para abate

CCA_{k} = custo em R\$ / (lote animal) de compra do animal k para crescimento

PRA_{k} = valor em R\$ / kg da ração do animal k

VCA_{k} = valor em R\$ / kg de compra da carne do animal k

VVA_{k} = valor em R\$ / (lote animal) de venda de um lote do animal k

RRA_{k} = requisito em kg / (lote animal . mês) de ração necessária para o animal k

PYA_{k} = massa em kg de um lote de animal k crescido

RAA_{k} = requisito de área em m^{2} para criar um lote de animal k

TCP_{k} = tempo em meses que um animal k precisa para começar a gerar produtos

PYP_{k} = quantidade de produto em (unidade específica) / mês gerada pelo animal k

VCP_{k} = valor em R\$ / (unidade específica) de compra do produto gerado pelo animal k

AGA_{k} = quantidade em kg / (lote animal . mês) de esterco para adubação gerado pelo animal k

VVP_{k} = valor em R\$ / (unidade específica) de venda do produto do animal k

## Função Objetivo

Para atingir uma maior sustentabilidade, a função objetivo será a quantidade de excedente de produção, que pode ser destinada para a geração de lucro. Para isso, as quantidades das variáveis de decisão são transformadas em valores mometários. São parcelas que compõe o excedente:

1. (+) Valor das plantações vendidas;
2. (+) Valor dos animais vendidos;
3. (+) Valor dos produtos animais vendidos;
4. (-) Custo dos animais comprados;
5. (-) Custo das plantações realizadas;
6. (-) Custo das compras de fertilizante;
7. (-) Custo das compras de ração;
8. (-) Custo das compras de plantações para consumo;
9. (-) Custo do armazenamento de plantações colhidas.



\begin{align}
    FO_1 = \sum_{j=0}^{J} \sum_{i=0}^{I} VC_{ij} \cdot VVC_j \\

    FO_2 = \sum_{k=0}^{K} \sum_{i=0}^{I} VA_{ik} \cdot VVA_k \\

    FO_3 = \sum_{k=0}^{K} \sum_{i=0}^{I} VP_{ik} \cdot VVP_k \\

    FO_4 = \sum_{k=0}^{K} \sum_{i=0}^{I} CA_{ik} \cdot PYA_k \cdot VCA_k \\

    FO_5 = \sum_{j=0}^{J} \sum_{i=0}^{I} AC_{ij} \cdot CCC_j \\

    FO_6 = \sum_{i=0}^{I} FC_i \cdot PAC  \\

    FO_7 = \sum_{k=0}^{K} \sum_{i=0}^{I} RA_{ik} \cdot PRA_k  \\

    FO_8 = \sum_{j=0}^{J} \sum_{i=0}^{I} CC_{ij} \cdot VCC_j  \\

    FO_9 = \sum_{j=0}^{J} \sum_{i=0}^{I} EC_{ij} \cdot CEC_j  \\

    max FO = FO_1 + FO_2 + FO_3 - FO_4 - FO_5 - FO_6 - FO_7 - FO_8 - FO_9 
\end{align}

## Restrições

As restrições estão relacionadas com a disponibilidade de área para cultivo e criação de animais, requisitos de alimentação de animais e de adubação de cultivos, segurança alimentar dos membros da propriedade, tempo de colheita das culturas, tempo de crescimento de animais para abate e tempo para geração de produtos animais.

### Balanço de massa

A propriedade é um sistema que precisa ter seu fluxo de massa controlado. Isto significa definir como as variáveis de decisão podem ser tomadas, garantindo que nenhuma massa é criada ou destruída ao se encontrar uma resolução. As seguintes restrições são responsáveis por manter:

1. Todas as plantações colhidas em um mês são vendidas ou estocadas;
2. Todos os produtos animais produzidos em um mês são vendidos ou consumidos;
3. Os animais abatidos ou vendidos em um mês é resultado dos animais que cresceram na propriedade;
4. Em um mês o estoque de plantações é consumido pelos moradores ou utilizado para a alimentação de animais.

\begin{align}
    A_{(i-TCC_j)j} \cdot PYC_j = EC_{ij} + VC_{ij}, \ \forall i \in I \ e \ \forall j \in J \\
    AP_{ik} + VP_{ik} = \sum_{a=0}^{i-TCP_k} (CA_{ak} - VA_{ak} - AA_{ak}) PYP_k, \ \forall i \in I \ e \ \forall k \in K \\
    AA_{ik} + VA_{ik} \leq \sum_{a=0}^{i-TCA_k} (CA_{ak} - VA_{ak} - AA_{ak}), \ \forall i \in I \ e \ \forall k \in K \\
    PC_{ij} + \sum_{k=0}^{K} RC_{ijk} \leq \sum_{a=0}^{i} EC_{ij} - \sum_{a=0}^{i-1} (PC_{aj} + \sum_{k=0}^{K} RC_{ajk}), \ \forall i \in I \ e \ \forall j \in J
\end{align}

### Área

Cada plantação ocupa uma determinada área, assim como os animais necessitam de espaço para a criação. Neste sentido, as áreas ocupadas pelas plantações e animais devem obedecer ao limite de área da propriedade. Como plantações são colhidas no após um tempo TCC_{j}, este caso deve ser considerado ao se avaliar a área gasta. Por outro lado, como compra, venda e abate de animais são variáveis de decisão, a verificação do gasto de área é mais direto, de modo que:

\begin{equation}
    \sum_{j=0}^{J} (\sum_{a=0}^{i} AC_{aj} - \sum_{a=0}^{i-TCC_j} AC_{aj}) + \sum_{k=0}^{K} \sum_{a=0}^{i} (CA_{ak} - VA_{ak} - AA_{ak}) RAA_k \leq L , \ \forall i \in I
\end{equation}

### Adubação e alimentação

Para que ocorra desenvolvimento das plantações é preciso que seja feita a adubação, o que garante também a saúde das plantas para suportar pragas e doenças. A adubação pode ser feita por meio da compra de fertilizantes ou utilizando o esterco gerado pelos animais. Em modo análogo, os animais precisam de ração, que pode ser obtida por meio da compra ou da colheita das plantações. Este conjunto de restrições são as responsáveis por garantir a integração do sistema, sendo elas:

\begin{align}
    FA_i + \sum_{a=0}^{i} (CA_{ak} - VA_{ak} - AA_{ak}) AGA_k \geq RAC_j, \ \forall j \in J \ e \ \forall i \in I \\
    RA_{ik} + \sum_{j=0}^{J} RC_{ijk} \cdot AAC_{jk} \geq RRA_k, \ \forall k \in K \ e \ \forall i \in I \\
\end{align}

### Segurança alimentar

O grande diferencial da agricultura familiar é o objetivo primordial de garantir subsistência para a família. Neste sentido, é necessário incluir esta sequência de restrições no intuito de garantir que a propriedade seja capaz de produzir os recursos necessários (plantações e animais). Existe um <i>trade-off</i> entre a produção na interna ou a compra externa, já que a área para produção de comida pode ser alocada para produtos mais lucrativas. Esta decisão será o resultado do processo de otimização, que responderá o que gera mais excedente.

\begin{align}
    PC_{ij} + CC_{ij} \geq P \cdot NAC_j, \ \forall i \in I \ e \ \forall j \in J \\
    AA_{ik} \cdot PYA_k + PA_{ik} \geq P \cdot NAA_k, \ \forall i \in I \ e \ \forall k \in K \\
    AP_{ik} + CP_{ik} \geq P \cdot NAP_k, \ \forall i \in I \ e \ \forall k \in K
\end{align}