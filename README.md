# PROGRAMASO
Como seu programa deve ser compilado?
Deve-se incluir a biblioteca pthread na compilação do código. Usando GCC/MinGW ou Clang, fica:
$ gcc selecao.c -o selecao -pthread

Como seu programa deve ser executado?
Apenas execute sem passar quaisquer argumentos para ele.

$ ./selecao


Minha solução é simplesmente usar a biblioteca pthread para criar as threads para a execução do código em  paralelo, e usar a implementação de mutex da própria biblioteca para dar lock na memória enquanto uma das threads está usando-a.
O problema que ocorria em tempo de execução era o data race nas variáveis globais, cuja as mesmas são thread-unsafe justamente por causa que este tipo de coisa pode ocorrer. O ideal é evitar o uso de variáveis globais em casos como este.

O código está transcrito abaixo, mas também está adicionado em anexo no arquivo selecao.c
