#include <stdio.h>
#include <string.h>

void RegistrarTransacao(char *produto, float quantidade, float preco) {
    FILE *arquivo = fopen("transacoes.txt", "a");
    if (arquivo == NULL) {
        printf("Erro ao abrir arquivo\n");
        return;
    }
    fprintf(arquivo, "Produto: %s | Quantidade: %.2f | Preco: R$ %.2f\n", produto, quantidade, preco);
    fclose(arquivo);
    printf("Transacao registrada com sucesso!\n");
}

void EstacaoDePesagem() {
    char produto[50];
    float peso, precoPorKg, precoTotal;

    printf("\nEstacao de Pesagem\n");
    while (1) {
        printf("Digite o nome do produto (ou 'sair' para encerrar): ");
        scanf("%s", produto);
        if (strcmp(produto, "sair") == 0) break;

        printf("Digite o peso do produto (kg): ");
        scanf("%f", &peso);

        printf("Digite o preco por quilo: ");
        scanf("%f", &precoPorKg);

        precoTotal = peso * precoPorKg;
        printf("Preco total para %s: R$ %.2f\n", produto, precoTotal);
    }
}

void RegistroDeTransacoes() {
    char produto[50];
    float quantidade, preco;

    printf("\nServidor Central - Registro de Transacoes\n");
    while (1) {
        printf("Digite o nome do produto (ou 'sair' para encerrar): ");
        scanf("%s", produto);
        if (strcmp(produto, "sair") == 0) break;

        printf("Digite a quantidade: ");
        scanf("%f", &quantidade);

        printf("Digite o preco: ");
        scanf("%f", &preco);

        RegistrarTransacao(produto, quantidade, preco);
    }
}

void Caixa() {
    int numProdutos;
    char produto[50];
    float preco, quantidade, total = 0.0;

    printf("\nCaixa - Calculo do Valor Total da Compra\n");
    printf("Digite o numero de produtos: ");
    scanf("%d", &numProdutos);

    for (int i = 0; i < numProdutos; i++) {
        printf("Digite o nome do produto: ");
        scanf("%s", produto);

        printf("Digite o preco do produto: ");
        scanf("%f", &preco);

        printf("Digite a quantidade: ");
        scanf("%f", &quantidade);

        total += preco * quantidade;
    }

    printf("Valor total da compra: R$ %.2f\n", total);
}
void Lista ()
{
    FILE *arquivo = fopen("transacoes.txt", "r");
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo de transacoes.\n");
        return;
    }

    char linha[260]; 
    printf("\nLista de Produtos Registrados:\n");

    while (fgets(linha, sizeof(linha), arquivo) != NULL) {
        printf("%s", linha);
    }

    fclose(arquivo);
}

int main() {
    int opcao;

    while (1) {
        printf("\nVerde Vida\n");
        printf("Selecione uma opcao:\n");
        printf("1. Pesagem\n");
        printf("2. Registro de Transacao\n");
        printf("3. Caixa\n");
        printf("4. Lista de Produtos\n");
        printf("5. Sair\n");
        printf("Digite a opcao (1-5): ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                EstacaoDePesagem();
                break;
            case 2:
                RegistroDeTransacoes();
                break;
            case 3:
                Caixa();
                break;
            case 4:
                Lista();
                return 0;
                case 5:
                printf("Encerrando o programa.\n");
                return 0;
            default:
                printf("Opcao invalida! Tente novamente.\n");
        }
    }

    return 0;
}
