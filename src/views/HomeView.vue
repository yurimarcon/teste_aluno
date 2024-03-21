<!-- 
<script setup>
import {onMounted, reactive, ref, computed} from 'vue';
import ListPokemons from '@/components/ListPokemons.vue';
import CardSelected from "@/components/CardSelected.vue";

const pokemons = reactive(ref());

const urlImage = ref('https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/');

const formSearch = ref('');

const selectPokemon = reactive(ref());

let loading = ref(false);

onMounted(() => {
    fetch('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
    .then(res => res.json())
    .then(res => pokemons.value = res.results);
})

const filterSearch = computed(() => {
    if(pokemons.value && formSearch.value) {
        return pokemons.value.filter(pokemon => {
            return pokemon.name.toLowerCase().includes(formSearch.value.toLowerCase());
        })
    }
    return pokemons.value;
});

const selectedPokemon = async (pokemon) => {
    loading.value = true;
    selectPokemon.value = await fetch(pokemon.url)
    .then(res => res.json())
    .then(res => res)
    .catch(err => alert(err))
    .finally(() => loading.value = false)

    console.log("Chamou a API", selectPokemon.value);
}

</script >
<template>
    <div class="container">
        <div class="row pt-4 pb-5">
            <div class="col-sm-12 col-md-6">
                <CardSelected
                    v-if="selectPokemon?.name"
                    :nome="selectPokemon?.name"
                    :xp="selectPokemon?.base_experience"
                    :height="selectPokemon?.height"
                    :img="selectPokemon?.sprites?.other?.dream_world?.front_default"
                    :loading="loading"
                />
            </div>
            <div class="col-sm-12 col-md-6">
                <div class="card card-list">
                    <div class="card-body row">

                        <div class="mb-3">
                            <input type="text" class="form-control" v-model="formSearch" id="formSearch.value" placeholder="Search">
                            <p v-if="filterSearch == 0" class="text-center mt-4">Nenhum Pokemon chamado {{ formSearch }} foi capturado!</p>
                        </div>
                        <ListPokemons
                            v-for="pokemon in filterSearch"
                            :key="pokemon.name"
                            :nome="pokemon.name"
                            :urlImage="urlImage + pokemon.url.split('/')[6] + '.svg'"
                            @click="selectedPokemon(pokemon)"
                        />

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.card-list{
    height: calc(100vh - 140px);
    overflow-x: hidden;
    overflow-y: auto;
}

.card-list .card-body{
    flex: none!important;
}
</style>


 -->








<script setup>
import { onMounted, reactive, ref, computed } from "vue";
import ListPokemons from "../components/ListPokemons.vue"
import CardSelected from "../components/CardSelected.vue"

let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/")
let pokemons = reactive(ref());
let searchPokemonField = ref("")
let pokemonSelected = reactive(ref());
let loading = ref(false)

onMounted(()=>{
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
  .then(res => res.json())
  .then(res => pokemons.value = res.results);
})

const pokemonsFiltered = computed(()=>{
  if(pokemons.value && searchPokemonField.value){
    return pokemons.value.filter(pokemon=>
      pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
    )
  }
  return pokemons.value;
})

const selectPokemon = async (pokemon) => {
  loading.value = true;
  await fetch(pokemon.url)
  .then(res => res.json())
  .then(res => pokemonSelected.value = res)
  .catch(err => alert(err))
  .finally(()=> loading.value = false)

  console.log(pokemonSelected.value)
  
}

</script>

<template>
  <main>
    <div class="container text-body-secondary">
      
      <div class="row mt-4">
        <div class="col-sm-12 col-md-6">
          
          <CardSelected
          :name="pokemonSelected?.name"
          :xp="pokemonSelected?.base_experience"
          :height="pokemonSelected?.height"
          :img="pokemonSelected?.sprites.other.dream_world.front_default"
          :loading="loading"
          />

        </div>
  
        <div class="col-sm-12 col-md-6">
          <div class="card card-list">
            <div class="card-body row">
              
              <div class="mb-3">
                <label 
                hidden 
                for="searchPokemonField" 
                class="form-label">
                Pesqiosar...
                </label>

                <input 
                v-model="searchPokemonField"
                type="text" 
                class="form-control" 
                id="searchPokemonField" 
                placeholder="Pesquisar...">
              </div>

              <ListPokemons 
              v-for="pokemon in pokemonsFiltered"
              :key="pokemon.name"
              :name="pokemon.name"
              :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'"
              @click="selectPokemon(pokemon)"
              />
            </div>
          </div>
        </div>
      </div>

    </div>
  </main>
</template>

<style scoped>
.card-list{
  max-height: 75vh;
  overflow-y: scroll;
  overflow-x: hidden;
}

@media (max-width: 768px) {
  .card-list{
    max-height: 48vh;
  }
}
</style>