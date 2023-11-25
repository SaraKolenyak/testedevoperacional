 Após primeira ánalise, me deparei com aguns setter's e/ou construtores fora de ordem em duas classes (Cliente e Venda), onde os coloquei na ordem para facilitar a leitura do código. A classe "Cliente" não possuía construtor vazio, diferentemente das outras classes, que estão seguindo o padrão "Bean", então o mesmo foi adicionado, apesar de saber que quando compilado, o construtor vazio é criado automaticamente.
  De modo geral, noto que não há estrutura de pacotes ou camadas de serviços, os quais eu acrescentaria.
  Utilizaria-me de bibliotecas do gradle ou maven para facilitar os imports.
  Seria interessante para o usuário ter acesso a um CRUD, para melhor experiência... Não enxergo um modo de o mesmo excluir um item do carrinho, por exemplo, caso desista do produto.
  Com as alterações, utilizaria o Framework Spring para fazer uso da injeção de dependência.
  Organizei as regras de negócio do seguinte modo, inspirando-me na listagem Backlog, para meu melhor entendimento e análise:
  
  REGRAS DE NEGÓCIO
  
  CLIENTE
  O cliente pode fazer compras - OK
  O cliente pode visualizar suas compras - OK
  O cliente poderá ter acesso a apenas o nome da empresa, como infomação da mesma - (O cliente está visualizando também o ID da empresa, além do nome) - Excluí a visualização do id da empresa, deixando apenas o nome, segundo a regra de negócio.
  O cliente deve ver um resumo de sua compra ao finalizá-la - Há o resumo, mas em alguns momentos, ele não segue o correto, conforme as observações.
  
  EMPRESA
  A empresa pode visualizar suas vendas - OK
  A empresa pode visualizar seus produtos  - OK
  A empresa possui uma taxa (Comissão do sistema) para as transações - OK
  O saldo da empresa deve ser alterado já refletindo as taxas - (Ao mostrar o total líquido para a empresa, a taxa é descontada, mas isso não está se aplicando ao saldo.) - Fiz o desconto da mesma.
  A empresa deve vender apenas produtos os quais estejam relacionados a ela - Comprei um Pão Francês na Level Varejo, eu faria uma validação.
  A empresa pode visualizar a taxa em cada venda, quando suas vendas forem listadas - OK

Observações:
** Quando entro na "Level Varejo" e seleciono "1", porque é a forma mais lógica para o usuário de selecionar o primeiro item, o "1" é atribuído ao id 1 (Pão Francês) e então no resumo da compra, aparece apenas o valor (do pão francês), já que o item não pertence a loja, mas ainda assim me é vendido, de forma frustrante, pois eu queria comprar um coturno. Ao acessar minhas compras, vejo que comprei um pão na loja de varejo, o que vai contra uma das regras de negócio.
** Quando a empresa e o id coinscidem, o resumo funciona, mas caso contrário, não me é mostrado o que comprei, apenas o valor e de maneira errônea.
   --Solução: Eu criaria uma lista de produtos dentro da classe Empresa ao invés de a mesma se encontrar na venda, para melhor entendimento e organização/ordenação, já que acessaria apenas os produtos da própria empresa, não havendo mistura. Ou adicionaria uma empresa a um produto, fazendo assim uma composição, onde um produto precisa estar associado a uma empresa. 
  
** Não há como em um único acesso, o usuário fazer 2 ações, como realizar a compra e vê-las após a mesma.

** O cliente não está tendo acesso ao valor do produto, quando esse é listado, o que traz frustração, pois o mesmo não pode selecionar um item sem saber seu preço.

** A seleção de produtos não está intuitiva, é preciso fazer testes para conseguir adicionar o produto.

** Não está sendo feito o controle de estoque.
  -- Solução: Reduzir a quantidade em estoque do produto, quando esse for vendido.
  
** O Administrador não está conseguindo acessar os dados da empresa, conforme solicitado na Regra de Negócio."

