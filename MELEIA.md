useTasks.ts - refatoração
=========================
 
1. createTask e updateTask tinham código duplicado
--------------------------------------------------
As duas funções faziam exatamente a mesma coisa:
verificar título vazio, setar submitting, tratar erro no catch, setar submitting de volta no finally.
 
Criei uma função submitTask que faz tudo isso, e as duas passaram a chamar ela.
Se precisar mudar alguma coisa nessa lógica, muda em um lugar só.
 
 
2. apiRequest - função genérica pra chamadas de API
---------------------------------------------------
As 5 funções do hook faziam fetch da mesma forma, com o mesmo if response.ok e o mesmo throw.
Coloquei isso numa função separada fora do hook.
 
Agora as funções só passam a URL e o método, o resto fica centralizado.
 
 
3. useCallback
--------------
As funções eram recriadas toda vez que o componente renderizava.
Envolvi todas com useCallback pra evitar isso.
 
O useEffect também precisou receber fetchTasks no array de dependências,
que é o jeito certo de fazer quando usa useCallback.
 