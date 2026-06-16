# A arquitetura do Azure

A arquitetura do Microsoft Azure baseia-se em uma vasta rede global de datacenters organizados em regiões físicas e zonas de disponibilidade. Ela fornece infraestrutura, plataformas e serviços em nuvem gerenciados pela Microsoft, englobando computação, armazenamento, rede, inteligência artificial e análises

## Regiões

As regiões do Azure são áreas geográficas específicas ao redor do globo onde a Microsoft mantém e opera conjuntos de datacenters. Eles fornecem infraestrutura de computação em nuvem com alta disponibilidade e baixa latência. Globalmente, são mais de 60 regiões disponíveis, oferecendo a maior presença no setor.

## O que são e como funcionam?

- Latência e Proximidade:  Cada região agrupa datacenters conectados por uma rede local dedicada e de altíssima velocidade. Ao criar serviços (como máquinas virtuais), escolher a região mais próxima dos seus usuários garante respostas mais rápidas e melhor experiência.

- Empresas possuem exigências legais sobre onde dados de clientes podem ser armazenados. As regiões estão agrupadas em "geografias" (como Américas, Europa e Ásia) que garantem a soberania e as leis de privacidade dos dados.

# Par de regiões

Um par de regiões do Azure é formado por duas regiões localizadas na mesma área geográfica (como o mesmo continente ou país), que estão a pelo menos 480 km de distância uma da outra. Esse design estratégico é a base da resiliência e da recuperação de desastres na nuvem da Microsoft Azure.

## Para que serve?

Os pares de regiões garantem que os seus dados permaneçam seguros e disponíveis em situações de emergência (falhas físicas, desastres naturais ou interrupções em grande escala). Eles oferecem recursos de replicação de dados em várias regiões de forma contínua.

Principais beneficios:

- Atualizações Sequenciais: Em caso de interrupção generalizada, a recuperação de uma das regiões do par é priorizada pelo Azure, minimizando o tempo de inatividade. As atualizações do sistema do Azure são aplicadas em uma região de cada vez para evitar falhas simultâneas.

- Isolamento Físico: Embora estejam conectadas por uma rede de alta velocidade e baixa latência, a distância entre elas assegura que um problema regional severo (como quedas de energia amplas) não afete o datacenters da outra região.

- Residência de Dados: Os pares mantêm os dados dentro do mesmo limite geopolítico, o que ajuda a cumprir leis rigorosas de privacidade e conformidade de dados.

## Como funciona na prática?

Quando você usa replicação geográfica para serviços como armazenamento, banco de dados ou máquinas virtuais (VMs), o Azure grava os dados na região primária e os replica automaticamente para a região secundária pareada.Um exemplo clássico para usuários na América do Sul: a região Sul do Brasil é emparelhada com o Centro-Sul dos EUA.

## Regiões não emparelhadas

Embora o padrão seja o emparelhamento bidirecional (Região A aponta para a Região B e vice-versa), existem algumas exceções assimétricas. Por exemplo, o Sul do Brasil faz backup para os EUA, mas essa rota não é de mão dupla. Em casos raros onde a expansão global exige, o Azure também permite criar arquiteturas personalizadas com regiões não emparelhadas, assumindo que você gerencie as políticas de recuperação de desastres.