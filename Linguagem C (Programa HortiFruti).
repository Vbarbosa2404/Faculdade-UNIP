#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define NUM_PRODUTOS 10
#define MAX_PRODUTOS 100
#define MAX_FORNECEDORES 10

typedef struct {
    char nome[30];
    float preco;
    int estoque;
} Produto;

typedef struct {
    char nome[30];
    char contato[50];
} Fornecedor;

typedef struct {
    char nome[50];
    float preco_kg;
    float peso;
    float subtotal;
} ProdutoCaixa;

Produto produtos[MAX_PRODUTOS] = {
    {"Banana nanica", 3.50, 50},
    {"Morango", 7.00, 30},
    {"Mamao formosa", 5.00, 20},
    {"Laranja Bahia", 4.00, 40},
    {"Beterraba crua", 2.50, 60},
    {"Cebola crua", 3.00, 80},
    {"Abobora japonesa", 2.00, 70},
    {"Batata doce crua", 3.00, 50},
    {"Banana Terra", 4.50, 40},
    {"Brocolis", 6.00, 25}
};

Fornecedor fornecedores[MAX_FORNECEDORES] = {
    {"Fornecedor A", "fornecedora@example.com"},
    {"Fornecedor B", "fornecedorb@example.com"}
};

int totalProdutos = NUM_PRODUTOS;
int totalFornecedores = 2;

void limparBuffer() {
    int c;
    while ((c = getchar()) != '\n' && c != EOF);
}

void listarProdutos() {
    printf("\nProdutos Disponiveis:\n");
    for (int i = 0; i < totalProdutos; i++) {
        printf("%d. %s - R$%.2f (Estoque: %d)\n",
               i + 1,
               produtos[i].nome,
               produtos[i].preco,
               produtos[i].estoque);
    }
}

void adicionarProduto() {
    if (totalProdutos >= MAX_PRODUTOS) {
        printf("\nLimite maximo de produtos atingido!\n");
    } else {
        limparBuffer();
        printf("\nNome do novo produto: ");
        fgets(produtos[totalProdutos].nome, sizeof(produtos[totalProdutos].nome), stdin);
        produtos[totalProdutos].nome[strcspn(produtos[totalProdutos].nome, "\n")] = '\0';

        printf("Preco: ");
        if (scanf("%f", &produtos[totalProdutos].preco) != 1) {
            printf("\nEntrada invalida para preco!\n");
            limparBuffer();
        } else {
            printf("Quantidade em estoque: ");
            if (scanf("%d", &produtos[totalProdutos].estoque) != 1) {
                printf("\nEntrada invalida para estoque!\n");
                limparBuffer();
            } else {
                totalProdutos++;
                printf("\nProduto adicionado com sucesso!\n");
            }
        }
    }
}

void comprarProduto() {
    int opcao, quantidade;

    listarProdutos();
    printf("\nEscolha o numero do produto que deseja comprar: ");
    if (scanf("%d", &opcao) != 1 || opcao < 1 || opcao > totalProdutos) {
        printf("\nProduto invalido!\n");
        limparBuffer();
    } else {
        printf("Quantidade: ");
        if (scanf("%d", &quantidade) != 1 || quantidade <= 0) {
            printf("\nQuantidade invalida!\n");
            limparBuffer();
        } else if (produtos[opcao - 1].estoque < quantidade) {
            printf("\nEstoque insuficiente!\n");
        } else {
            produtos[opcao - 1].estoque -= quantidade;
            printf("\nCompra realizada com sucesso!\n");
            printf("%d %s adicionados ao seu carrinho.\n", quantidade, produtos[opcao - 1].nome);
        }
    }
}

void listarFornecedores() {
    printf("\nFornecedores Cadastrados:\n");
    for (int i = 0; i < totalFornecedores; i++) {
        printf("%d. %s - Contato: %s\n", i + 1, fornecedores[i].nome, fornecedores[i].contato);
    }
}

void exibirResumo(ProdutoCaixa produtos[], int totalProdutos, float total) {
    printf("\n--- Resumo da Compra ---\n");
    for (int i = 0; i < totalProdutos; i++) {
        printf("%d. %s - %.2f kg x R$ %.2f = R$ %.2f\n",
               i + 1,
               produtos[i].nome,
               produtos[i].peso,
               produtos[i].preco_kg,
               produtos[i].subtotal);
    }
    printf("-----------------------------\n");
    printf("Total a pagar: R$ %.2f\n", total);
    printf("Obrigado por comprar no Hortifruti!\n");
}

void menuCaixa() {
    ProdutoCaixa produtosCaixa[MAX_PRODUTOS];
    int totalProdutos = 0;
    float total = 0.0;
    int continuar;

    printf("\n=== Sistema de Caixa - Hortifruti ===\n");

    do {
        limparBuffer();
        printf("\nDigite o nome do produto: ");
        fgets(produtosCaixa[totalProdutos].nome, sizeof(produtosCaixa[totalProdutos].nome), stdin);
        produtosCaixa[totalProdutos].nome[strcspn(produtosCaixa[totalProdutos].nome, "\n")] = '\0';

        printf("Digite o preco por kg do produto (em R$): ");
        scanf("%f", &produtosCaixa[totalProdutos].preco_kg);

        printf("Digite o peso do produto (em kg): ");
        scanf("%f", &produtosCaixa[totalProdutos].peso);

        produtosCaixa[totalProdutos].subtotal = produtosCaixa[totalProdutos].preco_kg * produtosCaixa[totalProdutos].peso;
        total += produtosCaixa[totalProdutos].subtotal;

        printf("Adicionado: %s - %.2f kg x R$ %.2f = R$ %.2f\n",
               produtosCaixa[totalProdutos].nome,
               produtosCaixa[totalProdutos].peso,
               produtosCaixa[totalProdutos].preco_kg,
               produtosCaixa[totalProdutos].subtotal);

        totalProdutos++;

        printf("\nDeseja adicionar outro produto? (1 - Sim, 0 - Nao): ");
        scanf("%d", &continuar);

    } while (continuar != 0 && totalProdutos < MAX_PRODUTOS);

    exibirResumo(produtosCaixa, totalProdutos, total);
}

int main() {
    int opcao = 0;

    while (opcao != 5) {
        printf("\nMenu Principal:\n");
        printf("1. Gerenciar Cadastro de Produtos\n");
        printf("2. Gerenciar Estoque\n");
        printf("3. Gerenciar Fornecedores\n");
        printf("4. Sistema de Caixa\n");
        printf("5. Sair\n");
        printf("Escolha uma opcao: ");

        if (scanf("%d", &opcao) != 1) {
            printf("\nOpcao invalida!\n");
            limparBuffer();
        } else if (opcao == 1) {
            adicionarProduto();
        } else if (opcao == 2) {
            comprarProduto();
        } else if (opcao == 3) {
            listarFornecedores();
        } else if (opcao == 4) {
            menuCaixa();
        } else if (opcao == 5) {
            printf("\nSaindo do sistema...\n");
        } else {
            printf("\nOpcao invalida! Tente novamente.\n");
        }
    }

    return 0;
}
