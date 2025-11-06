# Relatório – Threads e Eventos em Java

## Atividade 01 – Execuções com Threads sem Sincronização

### Descrição
O programa **MeuDadoThreads.java** foi executado duas vezes, cada uma gerando um log de execução independente. O objetivo dessa atividade foi observar o comportamento das threads produtor e consumidor sem utilizar de métodos de sincronização.
### Observações
- As duas execuções apresentaram resultados diferentes na ordem das mensagens.
- Isso ocorre porque as threads competem pelo processador sem controle sobre a ordem de execução.
- Em algumas execuções, o consumidor tenta consumir antes do produtor disponibilizar um dado, ou há alternâncias irregulares entre as saídas.
### Conclusão
O comportamento não deterministico demonstra que é preciso fazer uso de sincronização. Sem controle, as threads podem se sobrepor, causar inconsistências e gerar resultados imprevisíveis.

## Atividade 02 – Threads com Sincronização (`wait()` e `notify()`)

### Descrição
Nesta parte, o código foi modificado para incluir métodos sincronizados, controlando o acesso ao recurso compartilhado com `synchronized`, `wait()` e `notify()`.
### Log Resumido
```
Produtor: 0
Consumidor: 0
Produtor: 1
Consumidor: 1
...
Produtor: 29
Consumidor: 29
```

### Observações
- O produtor e o consumidor alternam de forma ordenada.
- O consumidor **aguarda** o produtor disponibilizar o dado.
- A execução torna-se **determinística e previsível**.

### Conclusão
Com a sincronização, as threads passam a cooperar corretamente. Cada valor é produzido e consumido em sequência, sem interferência. Esse controle elimina as condições de corrida.

## ⚙️ Atividade 03 – Uso de Eventos (`MeuDadoEventJava`)

### Log de Execução
```
Consumidor usando Eventos: 0
Produtor usando Eventos: 0
Produtor usando Eventos: 1
Consumidor usando Eventos: 1
...
Produtor usando Eventos: 29
Consumidor usando Eventos: 29
```

### Observações
- A comunicação entre produtor e consumidor ocorre através de **eventos de espera e notificação**.
- A execução apresenta comportamento ordenado e sincronizado.
- O uso de `wait()` e `notify()` garante que o consumidor apenas leia valores quando disponíveis e o produtor apenas escreva quando o dado anterior for consumido.

## 🧠 Conclusão Geral

A evolução das três atividades demonstra claramente a importância do controle de concorrência:

1. **Sem sincronização**, as threads atuam de forma independente, resultando em saídas inconsistentes.
2. **Com sincronização explícita**, há cooperação entre produtor e consumidor, garantindo segurança no acesso.
3. **Com eventos**, a comunicação entre threads é ainda mais estruturada, utilizando sinalização de estados com `wait()` e `notify()` para coordenar as ações de forma eficiente e segura.

As atividaddes ilustram o conceito fundamental da **programação concorrente em Java**, mostrando como pequenas alterações na forma de sincronizar as threads transformam completamente o comportamento de um sistema.

