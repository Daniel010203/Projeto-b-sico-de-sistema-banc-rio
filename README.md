# Projeto de Sistema Bancário Simples

Este projeto é um sistema bancário simples desenvolvido em Python, voltado para proporcionar soluções práticas e seguras para sistemas financeiros. 

## Funcionalidades

Vou explicar cada parte do código:

1. **Importação do Módulo `textwrap`**:
   ```python
   import textwrap
   ```
   Este trecho importa o módulo `textwrap`, que fornece algumas funções para lidar com formatação e quebra de texto.

2. **Função `menu()`**:
   ```python
   def menu():
       menu_text = """\n
       ================ MENU ================
       [d]\tDepositar em conta
       [s]\tSacar de conta
       [e]\tExtrato bancário
       [nc]\tNova conta
       [lc]\tListar contas
       [nu]\tNovo cliente do banco
       [q]\tSair
       => """
       return input(textwrap.dedent(menu_text))
   ```
   Esta função exibe um menu de operações bancárias e solicita ao usuário que insira sua escolha. `textwrap.dedent()` é usado para remover a indentação do texto do menu.

3. **Função `depositar(saldo, valor, extrato)`**:
   ```python
   def depositar(saldo, valor, extrato):
       if valor > 0:
           saldo += valor
           extrato += f"Depósito em conta:\tR$ {valor:.2f}\n"
           print("\n=== Tudo certo, seu depósito foi realizado com sucesso! ===")
       else:
           print("\n@@@ Operação falhou! O valor informado é inválido, tente novamente. @@@")

       return saldo, extrato
   ```
   Esta função realiza a operação de depósito em conta. Ela recebe o saldo atual, o valor a ser depositado e o extrato atual como argumentos, e retorna o saldo atualizado e o extrato atualizado. Se o valor do depósito for maior que zero, o saldo é aumentado e o registro do depósito é adicionado ao extrato. Caso contrário, uma mensagem de erro é exibida.

4. **Função `sacar(saldo, valor, extrato, limite, numero_saques, limite_saques)`**:
   ```python
   def sacar(saldo, valor, extrato, limite, numero_saques, limite_saques):
       excedeu_saldo = valor > saldo
       excedeu_limite = valor > limite
       excedeu_saques = numero_saques >= limite_saques

       if excedeu_saldo:
           print("\n@@@ Operação falhou! Você não tem saldo suficiente. @@@")

       elif excedeu_limite:
           print("\n@@@ Operação falhou! O valor do saque excede o limite. @@@")

       elif excedeu_saques:
           print("\n@@@ Operação falhou! Número máximo de saques excedido. @@@")

       elif valor > 0:
           saldo -= valor
           extrato += f"Saque:\t\tR$ {valor:.2f}\n"
           numero_saques += 1
           print("\n=== Saque realizado com sucesso! ===")

       else:
           print("\n@@@ Operação falhou! O valor informado é inválido. @@@")

       return saldo, extrato
   ```
   Esta função realiza a operação de saque em conta. Ela recebe o saldo atual, o valor a ser sacado, o extrato atual, o limite de saque, o número de saques realizados e o limite de saques como argumentos, e retorna o saldo atualizado e o extrato atualizado. Verifica se o saque excede o saldo, o limite de saque ou o número máximo de saques permitidos. Se não houver nenhum problema, o saque é realizado e registrado no extrato.

5. **Função `exibir_extrato(saldo, extrato)`**:
   ```python
   def exibir_extrato(saldo, extrato):
       print("\n================ EXTRATO ================")
       print("Não foram realizadas movimentações." if not extrato else extrato)
       print(f"\nSaldo:\t\tR$ {saldo:.2f}")
       print("==========================================")


   ```
   Esta função exibe o extrato bancário, incluindo as movimentações (depósitos e saques) e o saldo atual.

6. **Função `criar_usuario(usuarios)`**:
   ```python
   def criar_usuario(usuarios):
       cpf = input("Informe o CPF (somente número): ")
       usuario = filtrar_usuario(cpf, usuarios)

       if usuario:
           print("\n@@@ Já existe usuário com esse CPF! @@@")
           return

       nome = input("Informe o nome completo: ")
       data_nascimento = input("Informe a data de nascimento (dd-mm-aaaa): ")
       endereco = input("Informe o endereço (logradouro, nro - bairro - cidade/sigla estado): ")

       usuarios.append({"nome": nome, "data_nascimento": data_nascimento, "cpf": cpf, "endereco": endereco})

       print("=== Usuário criado com sucesso! ===")
   ```
   Esta função permite a criação de um novo usuário no sistema bancário. Ela solicita informações como CPF, nome, data de nascimento e endereço, e adiciona essas informações à lista de usuários.

7. **Função `filtrar_usuario(cpf, usuarios)`**:
   ```python
   def filtrar_usuario(cpf, usuarios):
       usuarios_filtrados = [usuario for usuario in usuarios if usuario["cpf"] == cpf]
       return usuarios_filtrados[0] if usuarios_filtrados else None
   ```
   Esta função filtra os usuários com base no CPF fornecido.

8. **Função `criar_conta(agencia, numero_conta, usuarios)`**:
   ```python
   def criar_conta(agencia, numero_conta, usuarios):
       cpf = input("Informe o CPF do usuário: ")
       usuario = filtrar_usuario(cpf, usuarios)

       if usuario:
           print("\n=== Conta criada com sucesso! ===")
           return {"agencia": agencia, "numero_conta": numero_conta, "usuario": usuario}

       print("\n@@@ Usuário não encontrado, fluxo de criação de conta encerrado! @@@")

   ```
   Esta função permite a criação de uma nova conta bancária associada a um usuário existente. Ela solicita o CPF do usuário e, se o usuário existir, cria a conta e a associa ao usuário.

9. **Função `listar_contas(contas)`**:
   ```python
   def listar_contas(contas):
       for conta in contas:
           linha = f"""\
               Agência:\t{conta['agencia']}
               C/C:\t\t{conta['numero_conta']}
               Titular:\t{conta['usuario']['nome']}
           """
           print("=" * 100)
           print(textwrap.dedent(linha

## Importância de um Sistema Bancário com Funcionalidades Práticas e Seguras

Um sistema bancário eficiente e seguro é fundamental para garantir a confiança dos clientes e a integridade do sistema financeiro como um todo. Algumas das razões pelas quais funcionalidades práticas e seguras são essenciais incluem:

1. **Facilidade de Uso**: Funcionalidades práticas, como cadastro simplificado de clientes e realização rápida de transações, tornam a experiência do usuário mais agradável e intuitiva.

2. **Eficiência Operacional**: Com um sistema que oferece funcionalidades práticas, os processos operacionais dentro de uma instituição financeira podem ser otimizados, resultando em maior produtividade e redução de custos.

3. **Redução de Fraudes**: Medidas de segurança, como autenticação de dois fatores e monitoramento de atividades suspeitas, ajudam a mitigar o risco de fraudes e protegem tanto os clientes quanto o próprio banco.

4. **Proteção dos Dados do Cliente**: Um sistema seguro garante a proteção dos dados pessoais e financeiros dos clientes, ajudando a cumprir regulamentações de privacidade e a manter a confiança do público.

5. **Prevenção de Problemas Financeiros**: Funcionalidades que permitem aos clientes monitorar suas finanças e tomar decisões informadas contribuem para a prevenção de problemas financeiros, como gastos excessivos ou falta de fundos.

Portanto, investir em um sistema bancário com funcionalidades práticas e seguras é essencial para proporcionar uma experiência positiva aos clientes, garantindo a estabilidade e a confiança no sistema financeiro.



Agora, vou abordar como esse código pode ser utilizado por instituições financeiras e a importância das regras de segurança de acesso:

### Utilização por Instituições Financeiras:

Este código fornece funcionalidades básicas para operações bancárias, como depósito, saque, exibição de extrato, criação de contas e usuários. As instituições financeiras podem utilizar esse código como uma base para construir um sistema bancário mais completo.

### Importância das Regras de Segurança de Acesso:

1. **Autenticação Segura:** É fundamental implementar um sistema de autenticação robusto para garantir que apenas os clientes autorizados possam acessar suas contas e realizar transações.

2. **Autorização Adequada:** Além da autenticação, é importante definir permissões adequadas para cada tipo de usuário. Por exemplo, os clientes devem ter permissões limitadas em comparação com os funcionários do banco.

3. **Proteção de Dados Pessoais:** Dados sensíveis, como números de CPF e informações financeiras, devem ser protegidos adequadamente para evitar vazamentos e uso indevido.

4. **Registro de Atividades:** Manter registros detalhados de todas as atividades realizadas no sistema pode ajudar a detectar atividades

 suspeitas e investigar possíveis fraudes.

5. **Atualizações de Segurança:** O código deve ser regularmente atualizado para corrigir vulnerabilidades de segurança conhecidas e incorporar as melhores práticas de segurança da informação.

### Casos de Falhas em Transações Bancárias:

1. **Fraude de Identidade:** Um exemplo comum de falha em transações bancárias é a fraude de identidade, onde um indivíduo obtém acesso não autorizado à conta de outra pessoa e realiza transações fraudulentas. Para evitar isso, é fundamental implementar medidas robustas de autenticação e verificação de identidade.

2. **Vazamento de Dados:** Casos de vazamento de dados podem expor informações sensíveis dos clientes, como números de cartão de crédito e senhas, tornando-os vulneráveis a fraudes. Para evitar isso, é crucial proteger adequadamente os dados do cliente e adotar práticas de segurança cibernética eficazes.

3. **Ataques de Engenharia Social:** Os ataques de engenharia social visam enganar os clientes ou funcionários do banco para divulgar informações confidenciais ou realizar ações prejudiciais. A educação e conscientização sobre segurança cibernética podem ajudar a mitigar esse tipo de ameaça.

4. **Falhas de Segurança de Aplicativos:** Vulnerabilidades em aplicativos bancários podem ser exploradas por invasores para acessar contas de clientes ou realizar transações não autorizadas. Realizar testes de segurança regulares e adotar práticas de desenvolvimento seguro de software são essenciais para prevenir esse tipo de falha.

Em suma, o código deve ser desenvolvido com foco na segurança e proteção dos dados do cliente, seguindo as melhores práticas de segurança da informação e mantendo-se atualizado sobre as ameaças emergentes no cenário de segurança cibernética.
