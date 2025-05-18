<template>

  <div class="filter-catalog__item">
    <div class="filter-catalog__item-title">price Range</div>
    <div class="filter-catalog__item-content content-item">
      <div class="content-item__container">
        <div class="content-item__price price-filter">
          <div class="price-filter__slider" id="range-slider"></div>
          <div class="price-filter__inputs">
            <label class="price-filter__label">
              <input type="number" min="500" max="120000" placeholder="500" class="price-filter__input" id="min_num">
              <span class="price-filter__text">eur</span>
            </label>
            <label class="price-filter__label">
              <input type="number" min="500" max="120000" placeholder="120000" class="price-filter__input" id="max_num">
              <span class="price-filter__text">eur</span>
            </label>
          </div>
        </div>
      </div> 
    </div>
  </div>

</template>