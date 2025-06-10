QUESTÃO 1

#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

int buscaLinear(const vector<string>& livros, const string& titulo) {
    for (int i = 0; i < livros.size(); i++) {
        if (livros[i] == titulo) {
            return i;
        }
    }
    return -1;
}
int buscaBinaria(const vector<string>& livrosOrdenados, const string& titulo) {
    int esquerda = 0, direita = livrosOrdenados.size() - 1;

    while (esquerda <= direita) {
        int meio = esquerda + (direita - esquerda) / 2;

        if (livrosOrdenados[meio] == titulo) {
            return meio;
        } else if (livrosOrdenados[meio] < titulo) {
            esquerda = meio + 1;
        } else {
            direita = meio - 1;
        }
    }

    return -1;
}

int main() {
    vector<string> livros = {
        "A Culpa é das Estrelas", "A Droga da Obediência", "A Estrada", "A Fera de Gaia", "A Menina que Roubava Livros",
        "A Montanha Mágica", "A Revolução dos Bichos", "A Sombra do Vento", "A Teia de Charlotte", "1984",
        "Admirável Mundo Novo", "Alice no País das Maravilhas", "O Alquimista", "Cem Anos de Solidão", "A Hora da Estrela",
        "A Metamorfose", "As Crônicas de Nárnia: O Leão, a Feiticeira e o Guarda-Roupa", "Assassinato no Expresso do Oriente",
        "Corte de Espinhos e Rosas", "Crepúsculo", "Dom Casmurro", "Duna", "Ensaio sobre a Cegueira", "Fahrenheit 451",
        "Frankenstein", "O Grande Gatsby", "Harry Potter e a Pedra Filosofal", "Jogos Vorazes",
        "Memórias Póstumas de Brás Cubas", "O Código Da Vinci", "O Cortiço", "O Guia do Mochileiro das Galáxias",
        "O Iluminado", "O Ladrão de Raios", "O Pequeno Príncipe", "O Poder do Hábito", "O Silmarillion",
        "O Sol é Para Todos", "O Senhor dos Anéis: A Sociedade do Anel", "Onde Vivem os Monstros",
        "Orgulho e Preconceito", "O Retrato de Dorian Gray", "Percy Jackson e o Ladrão de Raios",
        "Sapiens: Uma Breve História da Humanidade", "O Hobbit", "Um Estudo em Vermelho", "Vidas Secas"
    };

    string livroBuscado = "O Hobbit";

    // Busca Linear
    int indiceLinear = buscaLinear(livros, livroBuscado);
    cout << "Busca Linear - Índice: " << indiceLinear << endl;

    // Busca Binária (lista precisa estar ordenada)
    vector<string> livrosOrdenados = livros;
    sort(livrosOrdenados.begin(), livrosOrdenados.end());

    int indiceBinaria = buscaBinaria(livrosOrdenados, livroBuscado);
    cout << "Busca Binária - Índice na lista ordenada: " << indiceBinaria << endl;

    return 0;
}

_____________________________________________________________________________________________________________________________

QUESTÃO 2 

#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Struct para representar um paciente
struct Paciente {
    string nome;
    int prioridade; // 1 = urgente, 5 = não urgente
};

// Função para imprimir os pacientes
void imprimirPacientes(const vector<Paciente>& pacientes) {
    for (const auto& p : pacientes) {
        cout << p.nome << " (Prioridade: " << p.prioridade << ")\n";
    }
    cout << endl;
}

// Bubble Sort
void bubbleSort(vector<Paciente>& pacientes) {
    int n = pacientes.size();
    for (int i = 0; i < n - 1; i++) {
        bool trocou = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (pacientes[j].prioridade > pacientes[j + 1].prioridade) {
                swap(pacientes[j], pacientes[j + 1]);
                trocou = true;
            }
        }
        if (!trocou) break; // Otimização: já está ordenado
    }
}

// Selection Sort
void selectionSort(vector<Paciente>& pacientes) {
    int n = pacientes.size();
    for (int i = 0; i < n - 1; i++) {
        int indiceMenor = i;
        for (int j = i + 1; j < n; j++) {
            if (pacientes[j].prioridade < pacientes[indiceMenor].prioridade) {
                indiceMenor = j;
            }
        }
        if (indiceMenor != i) {
            swap(pacientes[i], pacientes[indiceMenor]);
        }
    }
}

int main() {
    // Lista original
    vector<Paciente> lista = {
        {"Ana", 5}, {"Pedro", 2}, {"Carla", 4}, {"Lucas", 1},
        {"Mariana", 3}, {"Fernanda", 5}, {"Rafael", 2}, {"Beatriz", 4},
        {"Guilherme", 1}, {"Sofia", 3}
    };

    // Cópias para cada algoritmo
    vector<Paciente> listaBubble = lista;
    vector<Paciente> listaSelection = lista;

    // Ordenação
    cout << "Original:\n";
    imprimirPacientes(lista);

    bubbleSort(listaBubble);
    cout << "Ordenado com Bubble Sort:\n";
    imprimirPacientes(listaBubble);

    selectionSort(listaSelection);
    cout << "Ordenado com Selection Sort:\n";
    imprimirPacientes(listaSelection);

    return 0;
}

________________________________________________________________________________

QUESTÃO 3

#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>
#include <chrono>
using namespace std;
using namespace std::chrono;

// Geração de vetor aleatório
vector<int> gerarVetorAleatorio(int tamanho, int min, int max) {
    vector<int> vetor;
    srand(time(0));
    for (int i = 0; i < tamanho; i++) {
        vetor.push_back(rand() % (max - min + 1) + min);
    }
    return vetor;
}

// Bubble Sort
void bubbleSort(vector<int>& v) {
    int n = v.size();
    for (int i = 0; i < n - 1; i++) {
        bool trocou = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (v[j] > v[j + 1]) {
                swap(v[j], v[j + 1]);
                trocou = true;
            }
        }
        if (!trocou) break;
    }
}

// QuickSort
int particionar(vector<int>& v, int inicio, int fim) {
    int pivo = v[fim];
    int i = inicio - 1;
    for (int j = inicio; j < fim; j++) {
        if (v[j] < pivo) {
            i++;
            swap(v[i], v[j]);
        }
    }
    swap(v[i + 1], v[fim]);
    return i + 1;
}

void quickSort(vector<int>& v, int inicio, int fim) {
    if (inicio < fim) {
        int p = particionar(v, inicio, fim);
        quickSort(v, inicio, p - 1);
        quickSort(v, p + 1, fim);
    }
}

// Função para imprimir vetor (opcional)
void imprimir(const vector<int>& v) {
    for (int num : v)
        cout << num << " ";
    cout << endl;
}

int main() {
    vector<int> dados = gerarVetorAleatorio(50, 1, 500);

    vector<int> bubble = dados;
    vector<int> quick = dados;

    // Bubble Sort com medição de tempo
    auto inicioBubble = high_resolution_clock::now();
    bubbleSort(bubble);
    auto fimBubble = high_resolution_clock::now();
    auto tempoBubble = duration_cast<microseconds>(fimBubble - inicioBubble).count();

    // QuickSort com medição de tempo
    auto inicioQuick = high_resolution_clock::now();
    quickSort(quick, 0, quick.size() - 1);
    auto fimQuick = high_resolution_clock::now();
    auto tempoQuick = duration_cast<microseconds>(fimQuick - inicioQuick).count();

    cout << "Tempo Bubble Sort: " << tempoBubble << " microssegundos\n";
    cout << "Tempo QuickSort: " << tempoQuick << " microssegundos\n";

    return 0;
}
