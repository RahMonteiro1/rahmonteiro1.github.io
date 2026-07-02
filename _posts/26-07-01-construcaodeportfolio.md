---
layout: post
title: "Construindo este portfólio"
categories: [aprendizado]
tags: [jekyll, ruby, debugging]
status: "concluído"
---

### Contexto
Antes de ter qualquer projeto pra mostrar aqui, tive uma tarefa até então inédita para realizar: fazer este próprio site rodar localmente antes de enviá-lo. 
Escolhi o template gratuito Centrarium, do Jekyll Themes, para servir de base ao meu portfólio. No entanto, ele foi escrito para uma versão do Ruby de 2018 e, descobri, entre outras coisas, que rodá-lo em um ambiente atual não era algo garantido de cara.

### O que tentei
Fui, na prática, decifrando vários logs sequenciais do Prompt de Comando, em camadas. Cada comando que eu executava gerava um erro, e uma vez que o resolvia, um próximo ocupava o seu lugar.
Os erros mais signifacativos eram ocasionados por gems encadeadas e dependentes que quebravam por motivos distintos — bibliotecas que saíram do núcleo do Ruby, uma versão do Bundler travada num método que não existe mais, um conversor de Markdown que separou uma peça essencial numa gem à parte. 
A correção de cada um deles veio a partir de algumas pesquisas e testes, que me levaram a entender por que aquele tipo de erro estava ocorrendo.

### O que aprendi
No total, ocorreram algumas categorias diferentes de problema, e reconhecê-las acabou me economizando mais tempo e energia do que tentar resolver qualquer erro individualmente:

**Dependências travadas no tempo.** O Gemfile.lock guardava a versão de
uma ferramenta (Bundler) datada de 2018. O sistema insistia em obedecer essa trava mesmo rodando num Ruby que não existia quando ela foi escrita.

**Bibliotecas nativas sem binário pronto.** Uma das gems (ffi) precisa de
código compilado especificamente pra cada combinação de sistema operacional
e versão do Ruby. Uma versão antiga dela não tinha esse binário pronto, e a tentativa de compilar na hora expôs o problema de forma quase imediata.

**O núcleo da linguagem encolhendo.** Bibliotecas como csv, webrick e rexml deixaram de ser incluídas juntamente com o Ruby. Não foi um defeito, mas sua importação manual foi necessária.

### Próximos passos
O site subiu, e tal processo foi concluído, tornando-o o primeiro experimento registrado aqui.