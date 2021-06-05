# Kit de termos: alguns conceitos para construir objetos

Todos os termos que serão definidos neste texto são parte do vocábulário usado para construir objetos e seus relacionamentos. Cada um deles serão abordados para que estejam bem contextualizados ao longo da leitura.

### Refatoração 

Refatoração é o processo de modificar um código para melhorá-lo sem modificar o seu funcionamento. Refatorar é uma prática que deve ser constante para se manter um bom código, essa prática envolve várias técnicas que podem ser aplicadas em diversas situações. Para se obter um código de mais qualidade, refatorar deve ser uma tarefa constante.

### Granularidade 

Granularidade é o termo utilizado para definir o quanto um software é separado em partes pequenas, quanto maior a granularidade maior a separação e quanto menor a granularidade, menor é a separação do código em partes menores. Quando mais granularidade ter o código, mais separado serão as suas responsabilidades, consequentemente mais coesão é obtidas.

### Acoplamento

O acoplamento é o grau de ligação que uma classe tem com outra, o acoplamento acontece quando classes são engessadas de uma forma que prejudica a flexibilidade do software e limita muito as mudanças. Basicamente, o acoplamento é o termo utilizado para definir o quanto um componente de um software está preso ao outro.

Manter o acoplamento baixo é essencial para um software orientado a objetos, pois isso possibilita flexibilidade nas mudanças e melhora a manutenção do software. Justamente pelo acoplamento limitar as coisas, uma das ideias mais difundidas dentro da orientação a objetos é ter um baixo acoplamento.

### Coesão

Quando se trata de objetos, o conceito de coesão é utilizado para definir o quanto as operações presentes em um objeto estão relacionadas umas com as outras. Algo é coeso quando faz exatamente o que se propõe sem ir além disso.

Por exemplo, um objeto que envia um e-mail e também salva um cadastro no banco de dados não é coeso, pois a responsabilidade de salvar coisas no banco de dados não deveria estar nele. Para que esse objeto fosse coeso, ele deveria ter somente métodos relacionados ao envio de e-mail e os detalhes necessários para realizar esse tipo de ação.

Um objeto pode ser considerado coeso quando ele que tem operações que estão focadas em compor uma determinada responsabilidade, não misturando conceitos que não estão ligados. Coesão é um termo que está bastante ligado a ideia de responsabilidade única, já que através dela algo pode ser considerado coeso.

### Juntando tudo

Objetos com grandes responsabilidades podem ser quebrados em partes para terem mais granularidade e focarem em responsabilidades mais bem definidas, o que gera coesao. Já no relacionamento desses objetos entra a composição, que se dá muitas vezes injetando as dependências e fazendo todas essas responsabilidades mais coesas se unirem e formarem um todo dentro da troca de mensagens dos objetos.