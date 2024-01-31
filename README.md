# data-pipeline-dynamodb

O objetivo desse repositório é demonstrar um pipeline que ingere dados do DynamoDB em formato JSON, tratar os dados em diferentes camadas de um datalake e por fim escrever esses dados no Redshift.

Para a solução foi considerado que os dados precisam ser disponibilizados quase em tempo real.

<h2>Ingestão</h2>

A tabela *Order* no DynamoBD é a que possui os dados que queremos trabalhar. Inicialmente precisamos capturar as alterações que ocorrem nela e para isso precisamos configurar a exportação desses dados. Nas configurações da tabela, na AWS é possível configurar na opção "Exportação e Streams" e para que o Stream funcione basta ativar a opção desejada. Em nosso case, ativarei a opção Stream com Kinesis, mas note que há a possibilidade de ativar Stream com Trigger de uma função Lambda. A opção com Kinesis foi escolhida para o nosso contexto levando em consideração que o volume de dados pode crescer consideravelmente em pouco tempo, uma arquitetura que utilize o Amazon Kinesis pode ser mais adequada para garantir escalabilidade e flexibilidade a longo prazo. O Kinesis oferece uma plataforma robusta para processamento de streams em grande escala, permitindo que a gente lide com o aumento de volume de dados de forma mais eficaz do que se estivesse confiando apenas no DynamoDB Streams e em funções Lambda diretamente conectadas.

*Observação: o custo de utilização do Kinesis é maior em comparação a utilização de funções Lambda, este por sua vez tsambém funciona muito bem para volume de dados pequenos a moderados, então é importante verificar o contexto de volume de dados que realmente será utilizado para que não se tenha gastos desnecessários.*




