<template>
  <header>
    <div>
      <ul>
        <li>
          <router-link to="/" active-class="active">Anasayfa</router-link>
        </li>
        <li>
          <router-link to="/favorites" active-class="active"
            >Favorilerim</router-link
          >
        </li>
      </ul>
      <span> Movie App | kablosuzkedi </span>
    </div>
  </header>
</template>

<style>
header {
  width: 100%;
}

header > div {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  width: 100%;
}
</style>
