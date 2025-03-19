# Escalonador-RR

Trabalho efetuado para a disciplina de Arquitetura de Computadores e Sistemas Operacionais, no período 2024.2, pelos alunos Pedro Freitas de Moura, Kaique Fabricio Eufrásio e Pedro Salazar Pessoa Machado.
---

## OBJETIVO: 

Desenvolver um simulador que aplica o algoritmo de escalonamento de processos utilizando a estratégia Round Robin com Feedback, com o objetivo de aprofundar o entendimento sobre o gerenciamento de processos em sistemas operacionais. 


## INTRODUÇÃO 

Este programa apresenta um simulador de escalonador Round Robin com Feedback, utilizado para gerenciar a execução de processos em sistemas operacionais. O algoritmo organiza os processos em filas circulares de alta e baixa prioridade, alternando entre elas conforme eventos específicos. Em um primeiro plano, os processos começam na fila de alta prioridade, mas podem ser realocados para a fila de baixa prioridade caso excedam seu quantum de execução. 

O sistema de feedback permite que processos retornem à fila de alta prioridade após determinados eventos, como a conclusão de operações de I/O. As operações de entrada/saída são tratadas por uma fila específica de I/O, na qual os processos aguardam até que a operação seja finalizada. Ao término da operação de I/O, o processo é reinserido na fila de alta prioridade para garantir maior prioridade na próxima execução. 

Essa dinâmica otimiza o uso da CPU, aumentando o throughput à medida em que os outros processos aguardam suas operações de I/O. O simulador ilustra o funcionamento eficiente do escalonador, evidenciando como o Round Robin com Feedback gerencia múltiplas filas e integra I/O, equilibrando responsividade, gerenciamento e prioridade na execução de processos. 


## PREMISSAS

1. **Limite máximo de processos criados:** Não houve a imposição de um limite, tendo em vista que foi feita a simulação por meio de uma fila adaptada à implementação de lista encadeada e memória dinâmica, para que, desse modo, o programa saiba lidar com o caso do computador ficar sem memória utilizável.
2. **O valor direcionado à fatia de tempo dada aos processos que são executados (QUANTUM):** Idealmente, o valor para o quantum dever ser maior que o valor usual de duração de uma interação ou funcionalidade do processo. Haja vista a possibilidade de diferentes quantidades de processos da simulação, foi alinhada a escolha de um valor arbitrário (4 unidades de tempo) para o quantum e, além disso, cada processo posuindo a necessidade de tempo de CPU maior que 4, para que, assim, cada um seja executado pelo menos uma vez.
3. **Os tempos de serviço e de I/O são adquiridos por arquivo .txt para cada processo:** 

Padrão do arquivo: Para cada processo, uma linha do arquivo de entrada é utilizada e lida em ordem crescente de tempo de chegada. Cada linha é distribuída seguindo o modelo: 
pid ; tempo_chegada ; t_cpu ; qua_io ; tipo_io ; duracao_io; tempo_inicio_io; 

pid = Identificação do processo; 

tempo_entrada = Momento em que o processo entra; 

tempo_CPU = Tempo necessário para execução completa do processo; 

quantidade_io = Número de requisições de I/O do processo; 

tipo_io = Tipo das requisições solicitadas pelo processo; 

duracao_io = Tempo de duração do I/O do processo; 

tempo_inicio_io = Momento em que a solicitação do I/O.  

 
Para cada tipo de I/O são dados os valores: 

DISCO: 0 

FITA MAGNÉTICA: 1 

IMPRESSORA: 2 

4. **Tempo de duração de cada tipo de I/O (disco, fita magnética e impressora):** o tempo de duração de cada I/O pertence a um processo é fornecida pelo arquivo de entrada. Assim como diferentes dispositivos podem atuar em performances diferentes, foi optado por deixar a duração como variável.
5. **Gerência de Processos:**
   1. **Definição do PID de cada processo:** Obtido no arquivo de texto (formato .txt).
   2. **Informações do PCB (Contexto de software – prioridade, PID, PPID, status):** O PID de cada processo é obtido no arquivo de entrada, assim como seu tempo de chegada, assim como seu tempo de chegada, tempo de serviço e lista de I/Os. Não utilizamos prioridade dinâmica para os processos, com a prioridade de cada processo sendo definida somente por qual fila de prioridade ele está situado. Também adicionamos valores de tempo de chegada do processo e qual seu próximo I/O.
   3. **Escalonador (três filas, sendo elas uma fila de alta e uma de baixa prioridade para a execução dos processos na CPU e uma fila de I/O):** O escalonador foi desenvolvido por meio de uma fila de alta e uma de baixa prioridade, bem como uma fila de I/O.
