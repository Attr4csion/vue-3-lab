<template>
<h1>Кинотеатр</h1>
  <div class="cinema">
    
    <div class="filters">
      <label>Фильтр по цене:</label>
      <input type="number" v-model="priceFilter" min="0">
      <label>Фильтр по году выпуска:</label>
      <input type="number" v-model="yearFilter" min="1900" max="2023">
      <label>Фильтр по жанру:</label>
      <select v-model="genreFilter">
        <option value="">Все жанры</option>
        <option v-for="(genre,index) in genres" :key="index" :value="genre">{{ genre }}</option>
      </select>
      <label>Сортировка по рейтингу:</label>
      <select v-model="sortOrder">
        <option value="desc">По убыванию</option>
        <option value="asc">По возрастанию</option>
      </select>
    </div>
    <div class="movies">
      <div v-for="movie in filteredMovies" :key="movie.id" class="movie">
        <img :src="movie.url" :alt="movie.url">
        <h2>{{ movie.title }}</h2>
        <p>Цена билета: {{ movie.price }} руб.</p>
        <p>Год выпуска: {{ movie.year }}</p>
        <p>Жанр: {{ movie.genre }}</p>
        <p>Рейтинг: {{ movie.rating }}/10</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movies: [
        { id: 1, title: 'Тупой и еще тупее', price: 150, year: 2010, genre: 'комедия', rating: 8,url:'' },
        { id: 2, title: 'Джон Уик', price: 200, year: 2015, genre: 'боевик', rating: 7 ,url:''},
        { id: 3, title: 'Хатико', price: 100, year: 2018, genre: 'драма', rating: 9, url:require('@/hatiko.jpeg') },
        { id: 4, title: 'Интерстеллар', price: 250, year: 2020, genre: 'фантастика', rating: 6,url:require('@/Interstellar.jpg') },
        { id: 5, title: 'Тупой и еще тупее', price: 150, year: 2010, genre: 'комедия', rating: 8 ,url:''},
        { id: 6, title: 'Джон Уик', price: 200, year: 2015, genre: 'боевик', rating: 7,url:'' },
        { id: 7, title: 'Хатико', price: 100, year: 2018, genre: 'драма', rating: 9 ,url:''},
        { id: 8, title: 'Интерстеллар', price: 250, year: 2020, genre: 'фантастика', rating: 6 ,url:''},
        { id: 9, title: 'Интерстеллар', price: 250, year: 2020, genre: 'фантастика', rating: 6 ,url:''},

      ]
      ,
      genres: ['комедия', 'боевик', 'драма', 'фантастика',],
      priceFilter: 0,
      yearFilter: 0,
      genreFilter: '',
      sortOrder: 'desc',
    }
  },
  computed: {
    filteredMovies() {
      let filtered = this.movies
      if (this.priceFilter !== 0 && this.priceFilter!=='') {
        filtered = filtered.filter(movie => movie.price <= this.priceFilter)
      }
      if (this.yearFilter !== 0 && this.yearFilter!=='') {
        filtered = filtered.filter(movie => movie.year === this.yearFilter)
      }
      if (this.genreFilter !== '') {
        filtered = filtered.filter(movie => movie.genre === this.genreFilter)
      }
      if (this.sortOrder === 'desc') {
        filtered = filtered.sort((a, b) => b.rating - a.rating)
      } else {
        filtered = filtered.sort((a, b) => a.rating - b.rating)
      }
      return filtered
    }
  },
}
</script>

<style>

*{
  background-color: #e6e6e6;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto';
}
.cinema{
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

.filters{
  align-self: flex-start;
  display: flex;
  flex-direction: column;
  margin-left: 40px;
  
}
.filters input, select{
  display: block;
  width: 100%;
  height: calc(2.25rem + 2px);
  padding: 0.375rem 0.75rem;
  font-family: inherit;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #bdbdbd;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  margin-bottom: 1rem;
}
.filters label{
  display: block;
  margin-bottom: 0.25rem;
}
.movies{
  display: grid;
  /* Автоматически заполняем на всю ширину grid-контейнера */
  grid-template-columns: repeat(auto-fill, 225px);
  width: 70%;
  justify-content: center;
  justify-items: center; /* Размещаем карточку по центру */
  column-gap: 30px; /* Отступ между колонками */
  row-gap: 40px; /* Отступ между рядами */
  margin: 0 auto;
}

.movie{
  background-color:white;
  padding: 1rem;
  width: 240px;
  min-height: 350px;
  box-shadow: 1px 2px 4px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column; /* Размещаем элементы в колонку */
  border-radius: 4px;
  transition: 0.2s;
  position: relative;
  text-overflow: ellipsis; white-space: nowrap; overflow: hidden;

}
.movie img{
  background-size: cover;
  background-repeat: no-repeat;
}
.movie h2,p{
  background-color:white;
}
/* .filters{
display: 
}

.movies{
  display: flex;
  flex-flow: row wrap;
}

.movie{
  
  box-sizing: border-box;
  padding: 5px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis
} */
</style>