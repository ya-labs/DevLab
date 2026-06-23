# 4 - Riscos, Limites e Boas Decisões

Trabalhar com AngularJS 1.x hoje é, acima de tudo, tomar boas decisões técnicas em contexto de legado.

Este documento foca em como avaliar risco e decidir com clareza.

---

## 1. Principais riscos em AngularJS legado

### Risco de manutenção

Código antigo sem padrão tende a ficar caro para evoluir.

### Risco de performance

Tela com muitos watchers pode degradar a experiência.

### Risco de acoplamento

Uso excessivo de rootScope e lógica espalhada dificulta previsibilidade.

### Risco de conhecimento

Poucas pessoas dominam AngularJS profundamente hoje.

### Risco de modernização travada

Sem plano, o sistema fica preso em manutenção reativa.

---

## 2. Limites técnicos mais comuns

- arquitetura antiga para demandas modernas muito grandes;
- dificuldade de manter padrão único em código histórico;
- integrações e dependências envelhecidas;
- custo crescente para testar e refatorar partes acopladas.

Esses limites não significam que o sistema precisa morrer.

Significam que ele precisa de governança técnica.

---

## 3. Matriz simples de decisão

Use esta regra prática:

## Manter

Quando o módulo é estável, gera valor e risco está controlado.

## Refatorar

Quando há gargalo técnico recorrente, mas ainda não exige migração imediata.

## Migrar

Quando custo de evolução e risco operacional no legado ficaram maiores que o custo da mudança gradual.

---

## 4. Checklist de diagnóstico inicial

Antes de decidir qualquer movimento grande, responda:

1. Quais módulos têm mais incidentes?
2. Quais telas estão lentas por watchers e digest?
3. Onde existe regra crítica sem testes?
4. Quais dependências estão mais desatualizadas?
5. O time consegue evoluir sem medo de quebrar?

Se as respostas forem ruins em cadeia, o sistema precisa de plano ativo de modernização.

---

## 5. Boas decisões para curto prazo

- corrigir instabilidades antes de reescrever;
- padronizar estrutura mínima de controller, service e rota;
- extrair regra de negócio de controllers gigantes;
- reduzir acoplamento global;
- documentar partes críticas.

---

## 6. Boas decisões para médio prazo

- definir fronteiras por feature;
- criar testes básicos em fluxos críticos;
- aplicar refatoração incremental por módulo;
- preparar pontos de integração para migração futura.

---

## 7. O que evitar

### Evitar promessa de reescrita total rápida

Projetos reais quase nunca suportam isso sem impacto alto.

### Evitar mexer em tudo sem mapa de risco

Sem diagnóstico, cada mudança aumenta chance de regressão.

### Evitar manutenção sem estratégia

Se o time só apaga incêndio, o custo explode com o tempo.

---

## 8. Exemplo de plano prático em 4 etapas

1. Estabilizar: bugs críticos, erros de produção e performance extrema.
2. Organizar: padrão mínimo de código e separação de responsabilidades.
3. Fortalecer: testes nos fluxos de maior risco e documentação de arquitetura.
4. Evoluir: migração progressiva por módulo, sem paralisar o produto.

---

## 9. Relação com outros materiais

Este tema se conecta diretamente com:

- Banco local em Frontend/estudos/angularjs/mobile/Banco local.txt.
- Debug em Frontend/estudos/javascript/documentos-de-estudo/secao-00-primeiros-passos-programacao/4 - Debug.md;
- Tratamento de erros HTTP em Frontend/estudos/javascript/documentos-de-estudo/secao-12-http-integracao/3 - Status HTTP.md.

---

## Conclusão

A melhor decisão em AngularJS legado não é manter para sempre nem migrar por impulso.

A melhor decisão é equilibrar risco, custo e valor de negócio com passos técnicos claros, incrementais e sustentáveis.
