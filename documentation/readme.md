# Manuais disponíveis

- Gnu/Linux (English)
- Distros (English)
- Hardware (English)
- Data Science (English)
- Cloud e Máquinas virtuais (English)
- Web Development (English)
- Compilado (English)

# Boas práticas

1.  Cada um dos manuais tem uma versão pública mas as mudanças nos
    textos e código são realizadas neste repositório centralizado para
    manuais.
2.  Como são documentos que serão editados pelo org, as novas versões
    criadas seguirão a mudanças de acordo com a hierarquia inerente. 
    - nível 1 = major 
    - nível 2 = minor 
    - nível 3 = patch
3.  Um commit deverá conter todos os arquivos ou porções de arquivo
    relacionados a uma tarefa específica. Dessa forma fica mais coerente
    e fácil de entender quais mudanças foram feitas.
    -   Atômico
    -   Consistente
    -   Isolado
    -   Durável
4.  Um commit não deve ser feito como forma de backup do estado atual.
    Quebre tarefas em subtarefas para que os commits ternham uma
    sequência lógica.
5.  Mensagens de commit devem endereçar o porquê daquela mudança, se
    possível referenciar algum problema levantado anteriormente.
6.  Checklist para commits:
    -   Commits devem ser ACID e com um propósito específico
    -   Deixe as mudanças visíveis por meio dos commits
    -   Considere como os comentários poderão ser úteis futuramente
    -   Faça um review antes de mandar para o público

## Links

-   [Git - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
-   [8 Version Control Best Practices \|
    Perforce](https://www.perforce.com/blog/vcs/8-version-control-best-practices)

# Tags e releases

A implantação de tags e releases será feita de forma separada para
manuais individuais e para o compilado.

As tags e releases dos manuais individuais seguirão a forma descrita na
seção boas práticas.

As tags e releases para o manual compilado seguirá uma forma agendada,
feita duas vezes por ano.

- [ ](Arrumar essa tabela)
  ------- -------- ---------
  Mẽs/ano \| Major \|
                   Minor \|
                   Tag

  maio/   2021     2021 \|
                   05 \|
                   2021.05

  novembro/   2021 \|
                   2021\| 11
                   \|
                   2021.11
  ------- -------- ---------

# Document versions and releases

Since this document is one of the biggest document so far because it is
being constantly worked on for future reference, it is only logical that
is has a tags.

History
-------

This document has its beginnings in the year of 2019 when the Linux bug
finally bit its creator. He quickly realised that much of the early use
was around searching for documentation and fixing things up in the
system. The start of this journey also involved a lot of distro hopping
and this meant that a lot of the same work was being done multiple
times. To fix this, he started the document around the fixes used for
his MacBook and the various Arch distributions that he used.
