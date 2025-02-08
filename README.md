# FOOL
## Struttura del progetto
La dir src si divide in:
- compiler
- stack virtual machine
### Compiler
Al suo interno sono presenti
- ```FOOL.g4```: è la grammatica ANTLR4 che definisce la sintassi del linguaggio FOOL.
- ```AST.java```: definisce la struttura dell'Abstract Syntax Tree (AST), ovvero la rappresentazione gererchica del programma dopo il parsing.
- ```ASTGenerationSTVisito.java```: Questo visitor si occupa di generare l'AST a partire dall'albero di parsing creato da ANTLR.
- ```SymbolTableASTVisitor.java```: gestisce la creazione e il popolamento della tabella dei simboli.
- ```TypeCheckASTVisitor.java```: implementa il controllo dei tipi, verificando che tutte le operazioni siano type-safe.
- ```CodeGenerationASTVisitor.java```: genera il codice a partire dall'AST.
- ```/exc```: dir dove sono presenti le classi che gestiscono le varie Exceptions che possono verificarsi durante la compilazione.
### SVM
Macchina virtuale basata su stack che esegue il bytecode generato dal compilatore.

- ```SVM.g4```: definisce le regole di parsing e i token della SVM utilizzando ANTLR. La sintassi, ovvvero le regole di parsing, convertono il codice assembly della SVM in bytecode. Ad esempio l'istuzione: ```PUSH n=INTEGER { code[i++] = PUSH; code[i++] = Integer.parseInt($n.text); }``` traduce ```push 10   →   [PUSH, 10] (bytecode)}```
- ```ExecuteVM.java```: esegue il bytecode generato dal parsing effettuato in SVM.g4. Il ciclo della CPU (fetch-decode-execute) legge un'istruzione, la interpreta e aggiorna lo stack, la memoria o il controllo di flusso. 
