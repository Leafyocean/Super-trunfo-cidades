# Super-trunfo-cidades
Programa em C estilo super trunfo de cidades
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_CIDADES 100

// Estrutura que representa uma carta de cidade
typedef struct {
    char estado[50];
    int codigo;
    char nome[100];
    int populacao;
    float pib;
    float area;
    int pontosTuristicos;
    float densidadePopulacional;
    float pibPerCapita;
} Cidade;

// Função para calcular densidade populacional
float calcularDensidade(int populacao, float area) {
    if (area == 0) return 0;
    return populacao / area;
}

// Função para calcular PIB per capita
float calcularPibPerCapita(float pib, int populacao) {
    if (populacao == 0) return 0;
    return pib / populacao;
}

// Função para cadastrar uma cidade
void cadastrarCidade(Cidade* cidade) {
    printf("Digite o nome da cidade: ");
    getchar(); // limpar buffer
    fgets(cidade->nome, 100, stdin);
    cidade->nome[strcspn(cidade->nome, "\n")] = 0; // remover \n

    printf("Digite o estado: ");
    fgets(cidade->estado, 50, stdin);
    cidade->estado[strcspn(cidade->estado, "\n")] = 0;

    printf("Digite o código da cidade: ");
    scanf("%d", &cidade->codigo);

    printf("Digite a população: ");
    scanf("%d", &cidade->populacao);

    printf("Digite o PIB (em bilhões): ");
    scanf("%f", &cidade->pib);

    printf("Digite a área (em km²): ");
    scanf("%f", &cidade->area);

    printf("Digite o número de pontos turísticos: ");
    scanf("%d", &cidade->pontosTuristicos);

    // Calcula os campos derivados
    cidade->densidadePopulacional = calcularDensidade(cidade->populacao, cidade->area);
    cidade->pibPerCapita = calcularPibPerCapita(cidade->pib, cidade->populacao);

    printf("\nCidade cadastrada com sucesso!\n\n");
}

// Função para exibir uma cidade
void exibirCidade(Cidade cidade) {
    printf("------ Carta da Cidade ------\n");
    printf("Nome: %s\n", cidade.nome);
    printf("Estado: %s\n", cidade.estado);
    printf("Código: %d\n", cidade.codigo);
    printf("População: %d habitantes\n", cidade.populacao);
    printf("PIB: %.2f bilhões\n", cidade.pib);
    printf("Área: %.2f km²\n", cidade.area);
    printf("Pontos Turísticos: %d\n", cidade.pontosTuristicos);
    printf("Densidade Populacional: %.2f hab/km²\n", cidade.densidadePopulacional);
    printf("PIB per Capita: %.2f\n", cidade.pibPerCapita);
    printf("----------------------------\n\n");
}

int main() {
    Cidade cidades[MAX_CIDADES];
    int totalCidades = 0;
    int opcao;

    do {
        printf("===== SUPER TRUNFO DE CIDADES =====\n");
        printf("1. Cadastrar nova cidade\n");
        printf("2. Listar todas as cidades\n");
        printf("0. Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);

        switch(opcao) {
            case 1:
                if (totalCidades < MAX_CIDADES) {
                    cadastrarCidade(&cidades[totalCidades]);
                    totalCidades++;
                } else {
                    printf("Limite de cidades atingido!\n");
                }
                break;
            case 2:
                for (int i = 0; i < totalCidades; i++) {
                    exibirCidade(cidades[i]);
                }
                break;
            case 0:
                printf("Encerrando programa...\n");
                break;
            default:
                printf("Opcao invalida.\n");
        }

    } while(opcao != 0);

    return 0;
}
