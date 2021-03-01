# Testes automatizados alta plataforma

Alfarrábios para os testes automatizados em alta plataforma

## MOCK

Segundo a wikipédia, objetos mock, objetos simulados ou simplesmente mock (do inglês mock object) em desenvolvimento de software são objetos que simulam o comportamento de objetos reais de forma controlada. São normalmente criados para testar o comportamento de outros objetos. Em outras palavras, os objetos mock são objetos “falsos” que simulam o comportamento de uma classe ou objeto “real” para que possamos focar o teste na unidade a ser testada. 

No nosso caso será exatamente isso, uma forma de simular o comportamento de um programa ou variável durante um teste automatizado.

### Mock em programas durante o teste

OBS.: Antes de incluir as linhas abaixo, conforme sua necessidade, não esqueça de, no programa, clicar com botão direto no código e inserir código mock.

- Programas Cobol CICS:
      @MOCK PROGRAM = DJOSR004{
      @BOOK DJOKR004
      @WHEN
      @THEN R004-COD-ERRO = 1
      }
- Progamas Cobol IIB - operação
/* Mock da operação 292018 - Valida Usuário no sistema ACESSO */
      @MOCK IIB OPR=292018.1 SRVC=71739.1 {
      @RQSC
      @BOOK nome do book ou decalaração das variáveis direto aqui
      @WHEN
      @THEN
          RPST.K6000-CD-RTN = 0
          RPST.K6000-NM-USU = 'TESTE AUTOMATIZADO'
          RPST.K6000-CD-TIP-USU = 'F'
} 

- Variáveis:
No programa, antes do local onde você precisa alterar o valor da variável, identifique conforme abaixo para que o teste automatizado reconheça onde deve alterar o valor da variável(O valor 310530 deve se referir ao local onde esta sendo feito o mock. Importante quando temos mais de um no programa):

      *
      * MOCK-POINT MCKV-310530 Teste de mock de variável
      *

No teste inclua conforme abaixo:

      @MOCK POINT=MCKV-310530 {
      @BOOK
           05 WS-RESP                  PIC  9(008) VALUE 0.
      @WHEN
      @THEN
      WS-RESP = 10
      }

A variável WS-RESP assumirá o valor 10 durante o teste.
