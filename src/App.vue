<template>
  <div class="telaFundo">
    <div class="principal">
      <div class="titulo">
        Resultado Alunos 
      </div> 
      <div class="menuNota">
        <div>
          Nome do Aluno: 
        </div>
        <input :class="getInputNameError ()" v-model="nomeAluno"/>
        <div>
          Nota do Aluno:
        </div>
        <input :class="getInputGradeError ()" type="number" v-model="notaAluno"/>
        <div>
          Serie do Aluno:
        </div>
        <input :class="getInputSerieError ()" v-model="serieAluno"/>
        <div>
          <button v-on:click="adicionar()" >
            Adicionar Aluno
          </button>
          <button v-on:click="mostrar ()">
            Mostrar resultados 
          </button>
        </div>
      </div>
    </div>
    <div class="balaoMsg">
      <div v-if="msg" class="msg">
        {{ msg }}
      </div>
    </div>

  <div v-if="mostrando" class="quadros">
    <div v-if="alunos.serieA.alunosAprovados.length > 0 || alunos.serieA.alunosReprovados.length > 0"  class="qA">
      <div>
        Série A
      </div> 
        <div class="tabelas">
          <div class="tabelaApro">
            Alunos Aprovados:
            <div class="listas" v-for="aluno in alunos.serieA.alunosAprovados" :key="aluno.nome">
              {{ aluno.nome }}
            </div>
          </div> 
            <div class="tabelaRepro">
              Alunos Reprovados: 
            <div class="listas" v-for="aluno in alunos.serieA.alunosReprovados" :key="aluno.nome">
              {{ aluno.nome }}
            </div>
          </div>
      </div>     
    </div>

    <div v-if="alunos.serieB.alunosAprovados.length > 0 || alunos.serieB.alunosReprovados.length > 0" class="qA">
      <div>
        Série B
      </div>
      <div class="tabelas">
        <div class="tabelaApro">
          Alunos Aprovados
          <div class="listas" v-for="aluno in alunos.serieB.alunosAprovados" :key="aluno.nome">
            {{ aluno.nome }}
          </div>
        </div>
        <div class="tabelaRepro">
          Alunos Reprovados 
          <div class="listas" v-for="aluno in alunos.serieB.alunosReprovados" :key="aluno.nome">
          {{ aluno.nome }}
          </div>
        </div> 
      </div>
    </div>
    
    <div v-if="alunos.serieC.alunosAprovados.length > 0 || alunos.serieC.alunosReprovados.length > 0" class="qA">
      <div>
        Série C
      </div>
      <div class="tabelas">
        <div class="tabelaApro">
          Alunos Aprovados
          <div class="listas" v-for="aluno in alunos.serieC.alunosAprovados" :key="aluno.nome">
          {{ aluno.nome }}
          </div>
        </div>
        
        <div class="tabelaRepro">
          Alunos Reprovados
          <div class="listas" v-for="aluno in alunos.serieC.alunosReprovados" :key="aluno.nome">
          {{ aluno.nome }}
          </div>
        </div>
      </div>
    </div>
  </div>

</div>

</template>

<script>
  export default {
  data (){
    return {
      listaDeAlunos: [],
      alunos:{
        serieA: {
          alunosAprovados:[],
          alunosReprovados:[]
        },
        serieB: {
          alunosAprovados:[],
          alunosReprovados:[]
        },
        serieC: {
          alunosAprovados:[],
          alunosReprovados:[]
        }
      },
      nomeAluno: undefined, 
      notaAluno: undefined,
      serieAluno: undefined,
      msg: undefined,
      mostrando: undefined,
      inputNameEmpty: false,
      inputGradeEmpty: false,
      inputSerieEmpty: false
    }
  },
  methods: {
    adicionar () {
      if (this.nomeAluno == undefined) {
        this.inputNameEmpty = true
        this.msg = "Nome do aluno não preenchido"
        }  
      if (this.notaAluno == undefined) {
          this.inputGradeEmpty = true
          this.msg = "Nota do aluno não preenchida"
        }  
      if (this.serieAluno == undefined) {
          this.inputSerieEmpty = true
          this.msg = "Série do aluno não preenchida"
        } 
      if (this.nomeAluno && this.notaAluno && this.serieAluno) {
          let aluno= {nome:this.nomeAluno, nota:this.notaAluno, serie:this.serieAluno}
          this.msg = "Aluno cadastrado com sucesso"
          this.inputGradeEmpty = false
          this.inputNameEmpty = false
          this.inputSerieEmpty=  false
          
          if (this.serieAluno.toUpperCase() == "A") {
            if (this.notaAluno >= 6) {
              this.alunos.serieA.alunosAprovados.push(aluno)
            } else {
              this.alunos.serieA.alunosReprovados.push(aluno)
            } 
          } else if (this.serieAluno.toUpperCase() == "B")  {
            if (this.notaAluno >= 6) {
              this.alunos.serieB.alunosAprovados.push(aluno)
            } else {
              this.alunos.serieB.alunosReprovados.push(aluno)
            }
          } else if  (this.serieAluno.toUpperCase() == "C") {
            if (this.notaAluno >= 6) {
              this.alunos.serieC.alunosAprovados.push(aluno)
            } else {
            this.alunos.serieC.alunosReprovados.push(aluno)
            }
          } else {
            this.msg = "Série inválida"
          } 
          this.nomeAluno = undefined
          this.serieAluno = undefined
          this.notaAluno = undefined 
        }
    },
    mostrar () {
      this.mostrando = true
      console.log (this.alunos)
    },
    getInputNameError () {
      if (this.inputNameEmpty == true) {
        return "inputAlert"
      }
    },
    getInputGradeError () {
      if (this.inputGradeEmpty == true) {
        return "inputAlert"
      }
    },
    getInputSerieError () {
      if (this.inputSerieEmpty == true) {
        return "inputAlert"
      }
    }
  }
}   
</script>
<style>
body {
  margin: 0;
}
.telaFundo {
  background-color: black;
  height: 100vh;
}
.principal {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.titulo {
  font-size: 2vw;
}
.menuNota {
  border: 1px solid black;
  border-radius: 7%;
  padding: 1%;
  background-color: #AFE4DE;
}
.inputAlert {
  outline: 1px solid red;
}
button {
  width:fit-content;
  margin: 5px;
}
.balaoMsg {
  display: flex;
  justify-content: center;
}
.quadros {
  display: flex;
  gap: 15vw;
  justify-content: center;
}
.qA {
  border: 1px solid #AFE4DE;
  border-radius: 7%;
  padding: 1%; 
  margin-top: 5vh;
  color: #AFE4DE;
  width: 20vw;
}
.tabelas {
  display: flex;
  justify-content: center;
  padding: 1vh 1vw;
}
.tabelaApro {
  color: green;
}
.tabelaRepro {
  color:red;
}
.msg {
  border: 1px red solid;
  padding: 5px;
  margin: 30px 0 0 15px;
  border-radius: 15%;
  color: white;
}
.listaAluno {
  margin: 15px;
}
.listas {
  padding: 10px;
}
</style> 