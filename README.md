# pti

public class No {
    private long id;
    private Object elemento;
    private No esq;
    private No dir;

    public No(long id, Object elemento, No esq, No dir) {
        this.id = id;
        this.elemento = elemento;
        this.esq = esq;
        this.dir = dir;
    }

    public void setId(long id) {
        this.id = id;
    }

    public long getId() {
        return this.id;
    }

    public void setElemento(Object elemento) {
        this.elemento = elemento;
    }

    public Object getElemento() {
        return elemento;
    }

    public void setEsq(No esq) {
        this.esq = esq;
    }

    public No getEsq() {
        return esq;
    }

    public void setDir(No dir) {
        this.dir = dir;
    }

    public No getDir() {
        return dir;
    }

    public String toString() {
        return getElemento() == null ? "" : (String) getElemento();
    }
}

public class ArvoreBinaria {
    private No raiz;

    public ArvoreBinaria() {
        this.raiz = null;
    }

    public No getArvore() {
        return raiz;
    }

    public void setArvore(No raiz) {
        this.raiz = raiz;
    }

    public void insere(long id, Object elemento) {
        No novoNo = new No(id, elemento, null, null);
        if (raiz == null) {
            raiz = novoNo;
        } else {
            No atual = raiz;
            No pai;
            while (true) {
                pai = atual;
                if (id < atual.getId()) {
                    atual = atual.getEsq();
                    if (atual == null) {
                        pai.setEsq(novoNo);
                        return;
                    }
                } else {
                    atual = atual.getDir();
                    if (atual == null) {
                        pai.setDir(novoNo);
                        return;
                    }
                }
            }
        }
    }

    // Questão A: Contar nós da esquerda festiva
    public int contarEsquerdaFestiva() {
        return preFixEsq(raiz);
    }

    private int preFixEsq(No atual) {
        if (atual == null) {
            return 0;
        }
        int qtdeNoEsquerda = 0;
        if (atual.getEsq() != null) {
            qtdeNoEsquerda++;
        }
        qtdeNoEsquerda += preFixEsq(atual.getEsq());
        qtdeNoEsquerda += preFixEsq(atual.getDir());
        return qtdeNoEsquerda;
    }

    // Questão B: Imprimir os IDs com recuos proporcionais
    public void imprimeEleArvore2() {
        preFix2(raiz, 0);
    }

    private void preFix2(No atual, int recuo) {
        if (atual != null) {
            preFix2(atual.getDir(), recuo + 4);
            for (int i = 0; i < recuo; i++) {
                System.out.print(" ");
            }
            System.out.println(atual.getId());
            preFix2(atual.getEsq(), recuo + 4);
        }
    }
}

public class ExemploDeArvoreBinaria {
    public static void main(String[] args) {
        System.out.println("\nQuestão A");
        ArvoreBinaria treeone = new ArvoreBinaria();
        treeone.insere(10, "A");
        treeone.insere(5, "B");
        treeone.insere(15, "C");
        treeone.insere(12, "D");
        treeone.insere(7, "E");
        treeone.insere(12, "F");
        treeone.insere(6, "G");
        treeone.insere(8, "H");
        treeone.insere(17, "I");
        treeone.insere(11, "J");
        treeone.insere(14, "K");
        treeone.insere(3, "L");
        treeone.imprimeEleArvore();
        System.out.println("Quantidade de Nós à Esquerda: " + treeone.contarEsquerdaFestiva());

        System.out.println("\nQuestão B");
        ArvoreBinaria treetwo = new ArvoreBinaria();
        treetwo.insere(888, "A");
        treetwo.insere(555, "B");
        treetwo.insere(333, "C");
        treetwo.insere(111, "D");
        treetwo.insere(444, "E");
        treetwo.insere(999, "F");
        treetwo.imprimeEleArvore2();
    }
}
