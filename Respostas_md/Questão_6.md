# Fila duplamente terminada - Deque
```
import Fila from "./Fila";

class Deque {
    constructor(tamanho){        
        this.deque = new Fila(tamanho);
        this.aux = new Fila(tamanho);
    }

    inserirInicio(dado){
        
        if(this.deque.isEmpty()){
            this.deque.enqueue(dado);
        }else{
            while(!this.deque.isEmpty()){
                this.aux.enqueue(this.deque.dequeue());
            }
            this.deque.clear();
            this.deque.enqueue(dado);
            while(!this.aux.isEmpty()){
                this.deque.enqueue(this.aux.dequeue());
            }
            this.aux.clear();
        }
    }
    inserirFim(dado){
        this.deque.enqueue(dado);
    }
    removerInicio(){
        return this.deque.dequeue();
    }
    removerFim(){
        let temp;
        temp = this.deque.size();
        for(let i=0;i<temp-1;i++){
            this.aux.enqueue(this.deque.dequeue());
        }
        let res = this.deque.dequeue();
        this.deque.clear();
        while(!this.aux.isEmpty()){
            this.deque.enqueue(this.aux.dequeue());
        }
        this.aux.clear();
        return res;
    }

}
export default Deque;
```
## Teste
```
import Deque from "../src/Questao6";

let d;
beforeEach(() => {
	d = new Deque(10);
});

test("Teste de inserções", () => {
    d.inserirInicio(1);
    d.inserirInicio(2);
    d.inserirInicio(3);
    d.inserirInicio(4);
    d.inserirInicio(5);
    expect(d.deque.front()).toBe(5);
    expect(d.deque.ultimo()).toBe(1);
    d.inserirFim(10);
    d.inserirFim(11);
    d.inserirFim(12);
    d.inserirFim(13);
    expect(d.deque.ultimo()).toBe(13);
    expect(d.deque.front()).toBe(5);
});

test("teste de remoção", () => {
    d.inserirInicio(1);
    d.inserirInicio(2);
    d.inserirInicio(3);
    d.inserirInicio(4);
    d.inserirInicio(5);
    d.inserirFim(10);
    d.inserirFim(11);
    d.inserirFim(12);
    d.inserirFim(13);
    expect(d.removerInicio()).toBe(5);
    expect(d.removerInicio()).toBe(4);
    expect(d.removerFim()).toBe(13);
    expect(d.removerFim()).toBe(12);
    expect(d.removerFim()).toBe(11);

});
```
