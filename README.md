### "Hello, I Want To Play A Game"
  
#### **Background**: 
***Usuário está na interface de envio de mensagem***

**Cenário**: ***Envio de mensagem efetuado com sucesso***   
	**Dado** que o usuário tenha escrito uma mensagem para o destinatário   
	**E** o campo mensagem tenha menos de 100 caracteres   
	**E** o campo número do destinatário esteja preenchido   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 201   
	**E** exibir mensagem “Mensagem enviada com sucesso”   

**Cenário**: ***Mensagem com mais de 100 Caracteres***   
	**Dado** que o usuário tenha escrito uma mensagem para o destinatário   
	**E** o campo mensagem tenha mais do que 100 caracteres   
	**E** o campo número do destinatário esteja preenchido   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 400   
	**E** exibir mensagem “O Campo mensagem deve conter até 100 caracteres”   

**Cenário**: ***Número de destinatário com mais de 11 dígitos***   
	**Dado** que o usuário tenha escrito uma mensagem para o destinatário   
	**E** o campo número do destinatário esteja preenchido com mais de 11 dígitos   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 400   
	**E** exibir mensagem “Por favor insira um número com 11 dígitos”   

**Cenário**: ***Número de destinatário com menos de 11 dígitos***   
	**Dado** que o usuário tenha escrito uma mensagem para o destinatário   
	**E** o campo número do destinatário esteja preenchido com menos de 11 dígitos   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 400   
	**E** exibir mensagem “Por favor insira um número com 11 dígitos”   

**Cenário**: ***Enviar com o campo “Mensagem” Vazio***   
	**Dado** que o usuário não tenha escrito uma mensagem   
	**E** o campo número do destinatário esteja preenchido corretamente   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 400   
	**E** exibir mensagem “O Campo mensagem não pode estar vazio”   

**Cenário**: ***Enviar com o campo “Destinatário” Vazio***   
	**Dado** que o usuário tenha escrito uma mensagem   
	**E** o campo número do destinatário esteja vazio   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 400   
	**E** exibir mensagem “O Campo Destinatário não pode estar vazio”   

**Cenário**: ***Enviar com ambos os campos “Destinatário” e “Mensagem” Vazios***   
	**Dado** que o usuário não tenha escrito uma mensagem   
	**E** o campo número do destinatário esteja vazio   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 400   
	**E** exibir mensagem “Por favor, insira a mensagem e o número do destinatário”   

**Cenário**: ***Enviar mais de uma mensagem no mês***   
	**Dado** que queira enviar uma mensagem   
	**E** o campo de mensagem esteja preenchido corretamente   
	**E** o campo número do destinatário esteja preenchido corretamente   
	**E** o destinatário já tenha recebido uma mensagem no mesmo mês   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 422    
	**E** exibir mensagem “Número máximo de mensagens atingido neste mês!”   

**Cenário**: ***Teste de tipagem do campo “Destinatário”***   
	**Dado** que queira enviar uma mensagem   
	**E** o campo de mensagem esteja preenchido corretamente   
	**E** tenha inserido o campo destinatário com “ABC”   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 400    
	**E** exibir mensagem “Campo destinatário está com o formato inválido”   


**Cenário**: ***Teste de tipagem do campo “Mensagem”***   
	**Dado** que queira enviar uma mensagem   
	**E** o campo de destinatário esteja preenchido corretamente   
	**E** tenha inserido o campo mensagem com 123   
	**Quando** enviar uma requisição para o POST/dev/lambdastresstest   
	**Então** devo visualizar um retorno 400    
	**E** exibir mensagem “Campo Mensagem está com o formato inválido”   
  #
  
# Report de bugs e testes manuais
  
**Cenário**: ***Ao tentar enviar uma mensagem de teste, foi possível efetuar o envio com mais de 100 caracteres no campo mensagem.***   
**Resultado esperado:** Uma mensagem de erro informando que “Não é possível enviar uma mensagem com mais de 100 caracteres”.    


**Cenário**: ***Foi possível enviar uma mensagem com o campo de ‘mensagem’, vazio.***   
**Resultado Esperado:** Uma mensagem informando “Por favor digite a mensagem”    


**Cenário**: ***Foi possível enviar uma mensagem com o campo de ‘destinatário’, vazio.***   
Resultado Esperado: Uma mensagem informando “Por favor insira o número do destinatário”.     


**Cenário**: ***Foi possível enviar mais de uma mensagem para o mesmo destinatário no mês, utilizei método de enviar a mesma mensagem para o mesmo destinatário mais de uma vez e foi retornado status de “Enviado com sucesso”.***    

**Resultado esperado:** Uma mensagem informando que aquele destinatário em específico não pode receber mais do que uma mensagem no mesmo mês.


**Cenário**: ***Quando tentei inserir um número no campo mensagem (Sem aspas), foi possível enviar, recebendo retorno 200.***    
**Resultado Esperado:** ***Uma mensagem informando que a mensagem está inválida.***   

#

# Sugestões de Melhorias:

Em todos os testes, o status response (da aplicação) estava com uma numeração específica de cada teste (400, 200, ou 422) porém no status code do Postman, era sempre reportado o Erro 200. Seria interessante que fosse desenvolvido na aplicação os padrões corretos de retorno em arrays específicos para cada erro.

Fiz a utilização de automação dentro do próprio Postman para verificação de tempo de resposta e para a checagem dos status code.


