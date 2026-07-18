# EN: Especificação de Negócios do PSECO-IGAssistant

## 1. Identificação do documento

**Nome da solução:** PSECO-IGAssistant  
**Tipo de solução:** Aplicação web de apoio à gestão de incidentes em Ecossistemas de Software Proprietário  
**Objetivo do documento:** Especificar o contexto de negócio, os objetivos, os requisitos funcionais, as regras de negócio e os requisitos não funcionais necessários para a implementação da aplicação.

## 2. Visão geral da solução

O PSECO-IGAssistant é uma aplicação web que apoia gestores de TI, responsáveis por incidentes e profissionais seniores na análise de situações de gestão de incidentes em Ecossistemas de Software Proprietário.

A aplicação coleta informações sobre o cenário por meio de três dimensões: técnica, negócio e governança, e social e organizacional. Também permite o envio opcional de áudios e documentos relacionados ao incidente.

Com base nas informações coletadas, a solução identifica características contextuais, solicita a validação do usuário, calcula a estratégia de gestão de incidentes mais aderente ao cenário e apresenta uma recomendação fundamentada. Após a confirmação da estratégia, a aplicação recupera as práticas de Site Reliability Engineering relevantes e gera passos de implementação contextualizados, critérios de aceitação, alertas sobre antipadrões e um playbook final.

A inteligência artificial atua como apoio em atividades específicas, como transcrição de áudio, interpretação de textos, identificação preliminar de características contextuais, recuperação de conhecimento e geração contextualizada de conteúdo. A seleção da estratégia utiliza relações previamente definidas e validadas no framework. As decisões críticas permanecem sob validação humana.

## 3. Atores envolvidos

### 3.1 Usuário responsável pelo incidente

Profissional que descreve o cenário, analisa as características contextuais identificadas, valida a recomendação e utiliza o playbook gerado. Esse papel pode ser desempenhado por um gestor de TI, incident manager, tech lead, coordenador de operações, profissional de SRE, DevOps ou segurança.

### 3.2 Administrador da solução

Responsável pela manutenção dos catálogos, matrizes, modelos de passos de implementação, critérios, antipadrões, prompts, configurações e versões da base de conhecimento do framework.

### 3.3 Serviços externos

Serviços utilizados pela aplicação para tarefas especializadas, como modelos de linguagem, geração de embeddings, transcrição de áudio e integração futura com plataformas corporativas.

# 4. Situação atual

A gestão de incidentes em Ecossistemas de Software Proprietário envolve diferentes organizações, equipes, fornecedores, clientes, componentes, contratos, restrições de acesso e responsabilidades distribuídas.

Atualmente, a análise desses cenários depende principalmente da experiência individual dos profissionais envolvidos. As informações costumam estar distribuídas entre relatos, registros de chamados, documentos técnicos, ferramentas de monitoramento, postmortems, contratos, mensagens e conhecimento tácito das equipes.

Mesmo quando a organização possui processos de gestão de incidentes, nem sempre existe um mecanismo estruturado para relacionar as características do contexto com estratégias de resposta e práticas de SRE adequadas. A seleção das ações tende a ser realizada de maneira manual, com diferentes níveis de consistência e rastreabilidade.

O protótipo atual demonstra a jornada de interação por meio de perguntas abertas, identificação de características contextuais, recomendação de estratégia, validação humana e geração de playbook. Entretanto, a lógica existente no protótipo HTML é demonstrativa e utiliza regras simplificadas. A implementação definitiva deverá utilizar o catálogo oficial de vinte características contextuais, as oito estratégias de gestão de incidentes, as matrizes validadas do framework, a recuperação de conhecimento por RAG e mecanismos de persistência e rastreabilidade.

# 5. Problemas

## 5.1 Coleta de contexto pouco estruturada

As informações necessárias para compreender o incidente podem estar incompletas, dispersas ou descritas de forma diferente por cada profissional.

## 5.2 Dificuldade de interpretar o contexto de forma sistêmica

A análise pode se concentrar apenas nos aspectos técnicos e deixar de considerar restrições de governança, dependências entre atores, contratos, comunicação, liderança e condições de trabalho da equipe.

## 5.3 Seleção de estratégia dependente da experiência individual

A estratégia adotada pode variar conforme o conhecimento e a experiência do responsável pelo incidente, mesmo quando os cenários apresentam características semelhantes.

## 5.4 Falta de ligação explícita entre contexto, estratégia e práticas SRE

As organizações podem conhecer práticas de SRE, mas ter dificuldade para determinar quais delas são diretamente relevantes para um cenário específico de gestão de incidentes.

## 5.5 Recomendações genéricas

Orientações amplas podem não considerar as evidências do caso, a estrutura organizacional, as restrições de acesso, os atores envolvidos e os mecanismos existentes na organização.

## 5.6 Baixa rastreabilidade

Nem sempre é possível explicar quais informações levaram à identificação de uma característica contextual, por que determinada estratégia foi recomendada e quais fontes sustentaram os passos de implementação.

## 5.7 Dependência de conhecimento tácito

Parte relevante do conhecimento sobre incidentes, responsabilidades, dependências e formas de resposta permanece concentrada em pessoas ou documentos pouco acessíveis.

# 6. Efeitos dos problemas

Os problemas identificados podem provocar demora na tomada de decisão, retrabalho, desalinhamento entre equipes, dificuldade de escalonamento, falhas de comunicação e respostas inconsistentes.

A ausência de uma análise sistêmica pode fazer com que restrições contratuais, dependências externas, responsabilidades de parceiros, limitações de acesso e impactos organizacionais sejam percebidos apenas depois do início da resposta.

A seleção inadequada de estratégias e práticas pode direcionar esforço para ações pouco relevantes, enquanto necessidades mais urgentes permanecem sem tratamento.

A falta de rastreabilidade reduz a confiança na recomendação, dificulta auditorias, limita o aprendizado e torna mais difícil revisar ou melhorar o processo posteriormente.

Recomendações excessivamente genéricas também podem ser difíceis de aplicar, pois não indicam responsáveis, evidências, critérios de conclusão ou condições específicas do cenário.

# 7. Objetivos

## 7.1 Objetivo geral

Disponibilizar uma aplicação web assistida por inteligência artificial que permita instanciar o framework de gestão de incidentes em PSECO, apoiando a identificação do contexto, a recomendação de uma estratégia e a geração de práticas SRE e passos de implementação adequados ao cenário analisado.

## 7.2 Objetivos específicos

1. Coletar informações sobre o cenário de incidente nas dimensões técnica, negócio e governança, e social e organizacional.

2. Permitir que o usuário complemente as respostas com áudio e documentos.

3. Interpretar as evidências e identificar características contextuais candidatas.

4. Permitir que o usuário revise e valide as características contextuais identificadas.

5. Aplicar a matriz validada de relações entre características contextuais e estratégias.

6. Recomendar uma estratégia principal e apresentar a justificativa da recomendação.

7. Permitir que o usuário confirme a estratégia ou forneça novas informações para uma nova análise.

8. Recuperar práticas SRE diretamente relacionadas à estratégia confirmada.

9. Gerar passos de implementação contextualizados, critérios de aceitação e antipadrões.

10. Produzir um playbook rastreável, consultável e exportável.

11. Preservar as evidências, decisões e versões utilizadas em cada análise.

# 8. Requisitos funcionais e regras de negócio

## RF01. Iniciar uma nova análise

A aplicação deve permitir que o usuário inicie uma nova análise de cenário de gestão de incidentes.

### Regras de negócio

**RN01.1.** Cada nova análise deve possuir um identificador único.

**RN01.2.** A análise deve registrar a data e a hora de criação.

**RN01.3.** O estado inicial da análise deve ser registrado como “Em preenchimento”.

**RN01.4.** O usuário deve poder cancelar ou reiniciar a análise antes da geração do playbook.

---

## RF02. Coletar o cenário por meio de perguntas abertas

A aplicação deve apresentar três campos de resposta aberta para coletar informações sobre o cenário.

Os campos devem representar:

1. Dimensão técnica: incidente, serviço e impacto operacional.
2. Dimensão de negócio e governança: atores, dependências, responsabilidades, contratos, aprovações e impactos organizacionais.
3. Dimensão social e organizacional: comunicação, colaboração, liderança, autonomia, pressão e sustentabilidade do trabalho.

### Regras de negócio

**RN02.1.** Pelo menos uma das três dimensões deve possuir conteúdo para que a análise seja iniciada.

**RN02.2.** A aplicação deve informar que respostas mais completas aumentam a qualidade da análise.

**RN02.3.** O conteúdo informado deve permanecer disponível durante toda a sessão.

**RN02.4.** O usuário deve poder revisar as respostas antes de solicitar a análise.

---

## RF03. Capturar áudio como complemento das respostas

A aplicação deve permitir que o usuário grave, reproduza, substitua e remova um áudio associado a cada dimensão.

### Regras de negócio

**RN03.1.** O uso de áudio deve ser opcional.

**RN03.2.** O áudio deve permanecer associado à dimensão em que foi gravado.

**RN03.3.** A aplicação deve solicitar permissão para acessar o microfone.

**RN03.4.** O usuário deve ser informado quando a gravação estiver ativa.

**RN03.5.** O áudio deve ser transcrito antes da identificação das características contextuais.

**RN03.6.** A transcrição deve manter referência ao arquivo de áudio de origem.

---

## RF04. Receber documentos de apoio

A aplicação deve permitir o envio opcional de documentos relacionados ao incidente ou ao contexto organizacional.

### Regras de negócio

**RN04.1.** O usuário deve poder visualizar a lista de arquivos enviados.

**RN04.2.** O usuário deve poder remover um arquivo antes do processamento.

**RN04.3.** Os formatos aceitos devem ser configuráveis. A primeira versão deve considerar PDF, DOC, DOCX, TXT, MD, PNG, JPG e JPEG.

**RN04.4.** Os limites de tamanho e quantidade de arquivos devem ser configuráveis.

**RN04.5.** Os documentos devem ser associados à análise correspondente.

**RN04.6.** O conteúdo extraído deve preservar a referência ao documento e, quando possível, à página ou seção de origem.

---

## RF05. Processar e normalizar as evidências

A aplicação deve consolidar as respostas textuais, as transcrições e o conteúdo extraído dos documentos em uma representação normalizada do cenário.

### Regras de negócio

**RN05.1.** A aplicação deve manter separação entre conteúdo original e conteúdo processado.

**RN05.2.** Nenhuma evidência original deve ser substituída pelo texto normalizado.

**RN05.3.** A aplicação deve registrar a origem de cada evidência.

**RN05.4.** Falhas na transcrição ou extração de um documento não devem impedir o uso das demais evidências.

**RN05.5.** O usuário deve ser informado quando algum arquivo ou áudio não puder ser processado.

---

## RF06. Identificar características contextuais candidatas

A aplicação deve analisar as evidências e identificar características contextuais candidatas com base no catálogo oficial CTX01 a CTX20.

### Regras de negócio

**RN06.1.** A identificação deve considerar as definições oficiais e as três dimensões do framework.

**RN06.2.** Cada característica candidata deve ser apresentada com seu código, nome, descrição e evidência associada.

**RN06.3.** A evidência deve indicar o trecho ou a fonte que sustentou a identificação.

**RN06.4.** A aplicação não deve criar uma característica contextual que não exista no catálogo oficial.

**RN06.5.** A ausência de correspondência não deve gerar características padrão automaticamente.

**RN06.6.** Quando não houver evidência suficiente, a aplicação deve informar que não foi possível identificar características com segurança e solicitar complementação.

**RN06.7.** A identificação realizada por inteligência artificial deve ser tratada como candidata até a validação humana.

---

## RF07. Permitir a validação humana das características contextuais

A aplicação deve permitir que o usuário confirme, rejeite ou revise as características contextuais candidatas.

### Regras de negócio

**RN07.1.** Apenas características confirmadas devem participar do cálculo da estratégia.

**RN07.2.** O usuário deve poder remover uma característica que não represente o cenário.

**RN07.3.** O usuário deve poder solicitar nova análise após fornecer informação adicional.

**RN07.4.** A aplicação deve registrar a decisão do usuário e a versão da evidência analisada.

**RN07.5.** A aplicação deve manter a diferença entre características candidatas e características validadas.

---

## RF08. Calcular o suporte contextual das estratégias

A aplicação deve aplicar a matriz validada de relações entre as características contextuais e as estratégias T1 a T8.

### Regras de negócio

**RN08.1.** Uma característica contextual pode estar relacionada a uma ou mais estratégias.

**RN08.2.** Apenas relações presentes na matriz oficial devem ser consideradas.

**RN08.3.** O cálculo deve utilizar somente características validadas pelo usuário.

**RN08.4.** A regra inicial de cálculo deve considerar a quantidade de características validadas que apoiam cada estratégia.

**RN08.5.** O resultado deve manter a lista das características que contribuíram para cada estratégia.

**RN08.6.** A versão da matriz utilizada deve ser registrada na análise.

**RN08.7.** A estratégia não deve ser selecionada diretamente por um modelo de linguagem. O modelo pode apoiar a identificação das características e a explicação do resultado, mas a seleção deve seguir a matriz e as regras definidas.

---

## RF09. Solicitar esclarecimentos quando necessário

A aplicação deve apresentar perguntas de esclarecimento quando houver empate entre estratégias, ausência de evidência suficiente ou inconsistência entre as informações fornecidas.

### Regras de negócio

**RN09.1.** A pergunta deve ser gerada de acordo com a informação que falta para diferenciar as estratégias candidatas.

**RN09.2.** A resposta deve ser incorporada às evidências do cenário.

**RN09.3.** Após a resposta, as características contextuais devem ser novamente identificadas e validadas.

**RN09.4.** A aplicação deve recalcular o suporte das estratégias após a atualização das características.

**RN09.5.** O sistema não deve selecionar automaticamente uma estratégia padrão quando a evidência permanecer insuficiente.

---

## RF10. Apresentar a estratégia recomendada

A aplicação deve apresentar uma estratégia principal de gestão de incidentes após o cálculo do suporte contextual.

### Regras de negócio

**RN10.1.** A recomendação deve exibir o código e o nome da estratégia.

**RN10.2.** A recomendação deve apresentar as características contextuais que sustentaram o resultado.

**RN10.3.** A aplicação deve explicar a relação entre o cenário e a estratégia em linguagem compreensível para o usuário.

**RN10.4.** A aplicação não deve apresentar a estratégia como uma decisão automática definitiva.

**RN10.5.** O resultado deve ser apresentado como recomendação sujeita à confirmação do usuário.

---

## RF11. Registrar a confirmação ou rejeição da estratégia

A aplicação deve permitir que o usuário confirme a estratégia ou informe que ela não representa adequadamente o cenário.

### Regras de negócio

**RN11.1.** A geração do playbook só deve ocorrer após a confirmação da estratégia.

**RN11.2.** Quando o usuário rejeitar a estratégia, a aplicação deve solicitar a indicação das informações ausentes ou incorretas.

**RN11.3.** A rejeição deve retornar o fluxo à coleta e análise de contexto.

**RN11.4.** A aplicação não deve selecionar automaticamente a segunda estratégia mais pontuada.

**RN11.5.** Após a inclusão das novas informações, as características devem ser novamente identificadas, validadas e processadas.

**RN11.6.** A decisão do usuário deve ser registrada para fins de rastreabilidade.

---

## RF12. Recuperar as práticas SRE relevantes

A aplicação deve recuperar as práticas SRE relacionadas à estratégia confirmada por meio da matriz Strategy to SRE Practice.

### Regras de negócio

**RN12.1.** Uma estratégia pode estar relacionada a mais de uma prática SRE.

**RN12.2.** Apenas práticas presentes na matriz oficial devem ser recuperadas.

**RN12.3.** A aplicação deve considerar somente práticas diretamente relevantes à gestão de incidentes.

**RN12.4.** A versão da matriz e do catálogo de práticas deve ser registrada.

**RN12.5.** A aplicação deve apresentar o código, o nome e uma descrição resumida de cada prática selecionada.

---

## RF13. Recuperar conhecimento e evidências por meio de RAG

A aplicação deve utilizar um serviço de RAG para recuperar conteúdo relevante da base de conhecimento do framework e das evidências do cenário.

### Regras de negócio

**RN13.1.** A base de conhecimento do framework deve ser considerada a fonte oficial para conceitos, catálogos, matrizes, templates, critérios e antipadrões.

**RN13.2.** O repositório de evidências deve ser considerado a fonte oficial para documentos, transcrições e informações do caso.

**RN13.3.** O armazenamento vetorial deve conter apenas representações derivadas, como chunks, embeddings, metadados e referências às fontes.

**RN13.4.** Cada conteúdo recuperado deve preservar a referência à fonte original.

**RN13.5.** O serviço de RAG deve permitir atualização e reindexação quando uma fonte for alterada.

**RN13.6.** Conteúdo sem referência de origem não deve ser utilizado como evidência no playbook.

---

## RF14. Coletar informações complementares para os passos de implementação

A aplicação deve identificar quando faltam informações necessárias para adaptar os passos de implementação ao contexto da organização.

### Regras de negócio

**RN14.1.** A aplicação pode apresentar até três perguntas complementares por análise.

**RN14.2.** As perguntas devem estar relacionadas à estratégia confirmada, às práticas SRE e às informações organizacionais necessárias.

**RN14.3.** A aplicação deve evitar solicitar novamente informações já disponíveis nas respostas ou documentos.

**RN14.4.** O usuário deve poder responder que a informação não está disponível.

**RN14.5.** A ausência de uma informação deve ser registrada como restrição ou premissa no playbook.

---

## RF15. Gerar passos de implementação contextualizados

A aplicação deve gerar passos de implementação para as práticas SRE recuperadas.

### Regras de negócio

**RN15.1.** Os passos devem ser derivados de templates mantidos na base de conhecimento.

**RN15.2.** Cada passo deve possuir título, descrição e critério de aceitação.

**RN15.3.** Quando houver informação suficiente, o passo deve indicar papéis, artefatos, dependências ou condições relevantes.

**RN15.4.** A aplicação não deve afirmar que um passo foi executado. Ela deve apenas orientar sua implementação.

**RN15.5.** Os passos devem respeitar as evidências e restrições identificadas no cenário.

**RN15.6.** Informações não presentes nas fontes devem ser apresentadas como sugestões ou premissas, nunca como fatos confirmados.

---

## RF16. Apresentar critérios de aceitação e antipadrões

A aplicação deve complementar os passos com critérios de aceitação e antipadrões relevantes.

### Regras de negócio

**RN16.1.** Cada passo deve possuir pelo menos um critério verificável de conclusão.

**RN16.2.** Os critérios devem ser claros e observáveis.

**RN16.3.** Os antipadrões devem indicar comportamentos ou decisões que podem reduzir a efetividade da prática.

**RN16.4.** Critérios e antipadrões devem manter vínculo com a prática SRE e com a fonte utilizada.

---

## RF17. Gerar o playbook da análise

A aplicação deve consolidar os resultados em um playbook de gestão de incidentes.

### Regras de negócio

**RN17.1.** O playbook deve apresentar, no mínimo:

1. resumo do cenário;
2. características contextuais confirmadas;
3. evidências consideradas;
4. estratégia confirmada;
5. justificativa da recomendação;
6. práticas SRE selecionadas;
7. passos de implementação;
8. critérios de aceitação;
9. antipadrões;
10. premissas e restrições;
11. rastreabilidade das fontes.

**RN17.2.** O playbook deve informar que as orientações precisam ser avaliadas conforme as políticas e responsabilidades da organização.

**RN17.3.** O playbook deve registrar a data de geração e as versões dos catálogos, matrizes e modelos utilizados.

**RN17.4.** O conteúdo deve diferenciar evidência confirmada, interpretação do sistema e sugestão gerada.

---

## RF18. Manter a rastreabilidade da análise

A aplicação deve permitir rastrear a relação entre evidências, características contextuais, estratégia, práticas SRE e passos de implementação.

### Regras de negócio

**RN18.1.** Cada característica deve manter vínculo com as evidências que sustentaram sua identificação.

**RN18.2.** A estratégia deve manter vínculo com as características validadas que contribuíram para seu cálculo.

**RN18.3.** Cada prática deve manter vínculo com a estratégia confirmada e com a matriz utilizada.

**RN18.4.** Cada passo deve manter vínculo com a prática, com o template e com as evidências utilizadas em sua contextualização.

**RN18.5.** A trilha de decisões humanas deve ser preservada.

---

## RF19. Salvar e consultar análises

A aplicação deve salvar as análises para consulta posterior.

### Regras de negócio

**RN19.1.** O histórico deve apresentar o identificador, a data, o estado, a estratégia confirmada e o responsável pela análise.

**RN19.2.** O acesso ao histórico deve respeitar as permissões definidas para o usuário.

**RN19.3.** Alterações posteriores não devem modificar silenciosamente o playbook já gerado.

**RN19.4.** Uma nova geração deve criar uma nova versão do playbook.

**RN19.5.** A aplicação deve preservar a versão das bases e regras utilizadas em cada geração.

---

## RF20. Exportar e imprimir o playbook

A aplicação deve permitir a impressão e a exportação do playbook.

### Regras de negócio

**RN20.1.** A impressão deve ocultar elementos de navegação e manter o conteúdo completo.

**RN20.2.** O formato inicial obrigatório de exportação deve ser PDF.

**RN20.3.** Formatos adicionais, como DOCX, Markdown e JSON, poderão ser habilitados por configuração.

**RN20.4.** O arquivo exportado deve apresentar o identificador da análise, a data e a versão do playbook.

---

## RF21. Administrar a base de conhecimento

A aplicação deve permitir que usuários autorizados mantenham os ativos do framework.

### Regras de negócio

**RN21.1.** Devem ser administráveis:

1. catálogo de características contextuais;
2. catálogo de estratégias;
3. matriz CTX to Strategy;
4. catálogo de práticas SRE;
5. matriz Strategy to SRE Practice;
6. templates de passos;
7. critérios de aceitação;
8. antipadrões;
9. prompts;
10. modelos de perguntas de esclarecimento.

**RN21.2.** Toda alteração deve gerar uma nova versão.

**RN21.3.** Versões utilizadas em análises anteriores não devem ser excluídas enquanto houver registros dependentes.

**RN21.4.** As alterações devem registrar autor, data e justificativa.

**RN21.5.** A publicação de uma nova versão deve exigir confirmação de um usuário autorizado.

# 9. Requisitos não funcionais

## RNF01. Usabilidade

A interface deve apresentar a jornada em etapas claras e permitir que o usuário compreenda sua posição no processo.

Os textos devem utilizar linguagem objetiva, evitando termos técnicos sem explicação.

Mensagens de erro devem informar o problema e orientar a correção.

As ações de avançar, voltar, reiniciar, confirmar e gerar playbook devem ser visualmente distintas.

## RNF02. Acessibilidade

A aplicação deve atender, no mínimo, aos critérios de nível AA das Web Content Accessibility Guidelines.

Todos os campos devem possuir rótulos associados.

A navegação deve ser possível por teclado.

O foco dos componentes interativos deve ser visível.

As cores não devem ser o único recurso para comunicar estado ou severidade.

## RNF03. Responsividade

A aplicação deve funcionar em computadores, tablets e dispositivos móveis.

A apresentação do playbook, das tabelas e dos formulários deve se adaptar ao tamanho da tela sem perda de informação.

## RNF04. Desempenho

A interface deve responder às ações comuns do usuário em até dois segundos, desconsiderando operações externas de IA, transcrição e processamento de documentos.

Durante operações mais longas, a aplicação deve apresentar um indicador de processamento e uma descrição do estágio atual.

O tempo limite para serviços externos deve ser configurável.

## RNF05. Disponibilidade e resiliência

Falhas temporárias em serviços de IA, transcrição ou embeddings devem ser tratadas sem perda das informações já fornecidas.

A aplicação deve permitir nova tentativa quando uma integração externa falhar.

O processamento de um arquivo com erro não deve interromper o processamento dos demais arquivos.

## RNF06. Segurança de acesso

A aplicação deve possuir autenticação e controle de acesso compatíveis com o ambiente organizacional em que for implantada.

As permissões devem separar, no mínimo, o usuário responsável pela análise e o administrador da base de conhecimento.

Sessões inativas devem expirar após período configurável.

Tentativas de acesso não autorizado devem ser registradas.

## RNF07. Proteção de dados e privacidade

Dados em trânsito devem utilizar conexão criptografada.

Dados sensíveis armazenados devem ser protegidos por criptografia compatível com a infraestrutura adotada.

A aplicação deve permitir configurar prazos de retenção para áudios, documentos, evidências e playbooks.

O usuário deve ser informado sobre o tratamento de áudios e documentos antes do envio.

A solução deve apoiar o atendimento às regras aplicáveis de privacidade e proteção de dados, incluindo a LGPD quando utilizada no Brasil.

## RNF08. Auditabilidade

A aplicação deve registrar eventos relevantes, como criação de análise, envio de arquivos, identificação e validação de características, recomendação, confirmação ou rejeição da estratégia, geração do playbook e alteração da base de conhecimento.

Os logs devem registrar data, hora, usuário, ação e resultado.

Informações sensíveis não devem ser gravadas integralmente em logs técnicos.

## RNF09. Explicabilidade

A aplicação deve permitir que o usuário compreenda por que uma característica foi identificada, por que uma estratégia foi recomendada e quais fontes foram utilizadas.

O sistema deve diferenciar resultados gerados por regras determinísticas, resultados sugeridos por inteligência artificial e decisões confirmadas por pessoas.

## RNF10. Confiabilidade da inteligência artificial

As respostas geradas por modelos de linguagem devem ser fundamentadas nas fontes recuperadas sempre que a tarefa depender da base de conhecimento ou das evidências do cenário.

A aplicação deve impedir que conteúdo gerado sem fonte seja apresentado como evidência confirmada.

Prompts, modelos, parâmetros e versões utilizados devem ser registráveis.

A indisponibilidade da IA não deve alterar automaticamente matrizes ou regras do framework.

## RNF11. Manutenibilidade

Catálogos, matrizes, prompts, templates e critérios devem ser externos ao código da interface.

Alterações na base de conhecimento não devem exigir recompilação completa da aplicação.

A solução deve possuir documentação técnica, documentação de APIs e instruções de configuração.

## RNF12. Interoperabilidade

A arquitetura deve permitir integração futura com ferramentas de ITSM, monitoramento, SIEM, CMDB e repositórios corporativos.

Integrações devem utilizar interfaces documentadas e mecanismos seguros de autenticação.

A aplicação deve permitir exportação estruturada dos resultados para consumo por outros sistemas.

## RNF13. Compatibilidade

A aplicação web deve ser compatível com versões atuais dos principais navegadores corporativos.

Recursos de áudio devem apresentar alternativa textual quando o navegador não oferecer suporte à gravação.

## RNF14. Persistência e versionamento

Análises, playbooks, matrizes, catálogos e templates devem possuir controle de versão.

A aplicação deve permitir reconstruir qual conjunto de regras e conteúdos foi utilizado em uma análise anterior.

A exclusão de registros deve seguir política de retenção e autorização.

## RNF15. Escalabilidade

A solução deve permitir aumento da quantidade de análises, usuários, documentos e itens da base de conhecimento sem mudança estrutural do modelo de negócio.

O processamento de documentos e a indexação vetorial devem poder ser executados de forma assíncrona.

## RNF16. Observabilidade

A solução deve disponibilizar métricas sobre disponibilidade, tempo de resposta, falhas de integração, processamento de documentos, consultas ao RAG e geração de playbooks.

Erros devem possuir identificador que permita rastreamento entre interface, backend e serviços externos.

# 10. Premissas da primeira versão

1. A aplicação será disponibilizada como solução web.

2. A primeira versão terá como usuário principal o profissional responsável pela análise do incidente.

3. A seleção da estratégia utilizará a matriz oficial CTX to Strategy.

4. A inteligência artificial não substituirá a confirmação humana das características contextuais e da estratégia.

5. A base de conhecimento do framework será versionada e administrada separadamente do código da interface.

6. O armazenamento vetorial será tratado como índice derivado e manterá referência às fontes oficiais.

7. O protótipo HTML será utilizado como referência de experiência do usuário, mas sua lógica simplificada não será utilizada como regra definitiva de negócio.

# 11. Fora do escopo inicial

1. Executar automaticamente mudanças em produção.

2. Acionar equipes, fornecedores ou mecanismos de escalação sem confirmação humana.

3. Substituir as ferramentas corporativas de ITSM, monitoramento, comunicação ou gestão de mudanças.

4. Avaliar automaticamente se a organização implementou corretamente todas as orientações do playbook.

5. Realizar diagnóstico técnico do incidente ou análise de causa raiz de forma autônoma.

6. Alterar automaticamente os catálogos e matrizes do framework com base no comportamento dos usuários.

# 12. Pontos que precisam de decisão antes da implementação

1. Modelo de autenticação e integração com diretórios corporativos.

2. Idiomas suportados na primeira versão.

3. Limites de tamanho, quantidade e tempo de retenção dos arquivos.

4. Formatos obrigatórios de exportação além do PDF.

5. Política de armazenamento e descarte de áudios.

6. Serviços de LLM, embeddings e transcrição que serão adotados.

7. Necessidade de ambientes separados por organização ou projeto.

8. Integrações corporativas que farão parte da primeira entrega.

9. Critério operacional para encerrar o ciclo de esclarecimento quando a evidência continuar insuficiente.

10. Responsáveis autorizados a publicar novas versões da base de conhecimento.
