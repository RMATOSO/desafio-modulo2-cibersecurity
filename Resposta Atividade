# Desafio Módulo 2 — Cibersegurança (Santander/DIO)

## Sobre o desafio

Este projeto reproduz, de forma controlada, o funcionamento de um ransomware: um ataque em que os arquivos da vítima são criptografados e só voltam a ficar acessíveis mediante pagamento de resgate. A ideia aqui é entender os dois lados do ataque na prática — o que criptografa o arquivo e o que devolve o acesso — usando o mesmo tipo de criptografia (AES) que ransomwares reais usam.

O repositório original do desafio trazia dois scripts com os nomes trocados de propósito:

| Arquivo | O nome sugere | O que o código realmente faz |
|---|---|---|
| decrypter.py | descriptografar | criptografa o teste.txt |
| encrypter.py | criptografar | descriptografa o arquivo criptografado |

Não é erro, é a própria lição do desafio: não dá pra confiar no nome ou na aparência de um arquivo. A análise tem que ser sempre sobre o comportamento real do código — é assim que um analista de segurança investigaria um incidente de verdade.

## Como funciona

Os dois scripts usam a biblioteca pyaes, que implementa o AES (Advanced Encryption Standard) em modo CTR (Counter Mode) — um jeito de usar um algoritmo de bloco como se fosse uma cifra de fluxo, o que permite criptografar arquivos de qualquer tamanho.

decrypter.py lê o teste.txt, criptografa o conteúdo com uma chave fixa (testeransomwares), apaga o original e salva o resultado como teste.txt.ransomwaretroll.

encrypter.py faz o caminho inverso: lê o .ransomwaretroll, descriptografa com a mesma chave e recria o teste.txt original.

A chave fica escrita direto no código. Isso é proposital para fins didáticos, mas na prática é uma falha grave: qualquer pessoa com acesso ao código já tem acesso à chave, sem precisar quebrar criptografia nenhuma.

## Como executar

```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install pyaes

python decrypter.py
python encrypter.py
```

## O que acontece

Depois de rodar decrypter.py, o teste.txt desaparece e surge o teste.txt.ransomwaretroll, com conteúdo binário ilegível. Depois de rodar encrypter.py, o arquivo original volta, com o texto legível de novo:

Este eh um arquivo descriptografado e perfeitamente legivel

## O que fica de aprendizado

A criptografia usada aqui é simétrica: a mesma chave criptografa e descriptografa, então ela precisa ser protegida a qualquer custo. Deixar essa chave escrita no código é uma vulnerabilidade séria — num ataque real ela nunca fica exposta assim, é gerada na hora do ataque e mantida só com quem atacou.

A inversão proposital entre os nomes dos arquivos reforça outro ponto: nome de arquivo não prova nada, o que importa é o comportamento.

E a defesa mais eficaz contra ransomware continua sendo a mais simples: backup atualizado e desconectado da rede. Se o atacante não consegue te deixar sem alternativa, o resgate perde o sentido.

## Próximo passo

Como extensão deste desafio, criei uma segunda versão (decrypter_v2.py e encrypter_v2.py) corrigindo o principal problema do exemplo original: a chave fixa no código. Está detalhado na seção seguinte.