<template>
  <div class="content-item__container">
    <Brand  
      v-for="brand in brands"
      :key="brand.id"
      :name="brand.name"
      :value="brand" 
      v-model="selectedBrandsMap[brand.name]"
    />
  </div>
</template>

<script lang="ts">
import Brand from "@/components/Brand.vue";
import { defineComponent } from "vue";

interface brand {
  id: number,
  name: string,
  value: string,
}

export default defineComponent({
  name: "BrandFilter",
  components: {
    Brand,
  },
  props: {
    brands: {
      type: Array as () => brand[],
      required: true
    },
    modelValue: {
      type: Array,
      default: () => [],
    },
  },
  emits: ['update:modelValue'],
  data() {
    return {
      selectedBrandsMap: {} as Record<string, boolean>,  /* Строка делает следующее:

    selectedBrandsMap — это переменная (например, поле в data или свойство объекта).
    {} — пустой объект, который инициализируется как начальное значение.
    as Record<string, boolean> — приведение типа (type assertion), говорящая TypeScript, что этот пустой объект должен рассматриваться как объект, у которого:
        ключи — строки (string),
        значения — булевы (boolean).

    Что такое Record<string, boolean>?

      Это встроенный в TypeScript дженерик-тип, эквивалентный записи типа: { [key: string]: boolean }
      То есть объект, где: ключи — строки, значения — булевы.

    Зачем так писать?

        Чтобы TypeScript знал, что selectedBrandsMap — объект с ключами-строками и булевыми значениями.
        Позволяет безопасно обращаться к selectedBrandsMap[brand.name] и ожидать, что результат — булево.
        Без этого приведения типа TypeScript может считать selectedBrandsMap просто пустым объектом с типом {}, и при обращении к динамическим ключам будет ошибка или предупреждение.

    {} as Record<string, boolean> — это способ сказать TypeScript: «Вот пустой объект, но он будет использоваться как словарь с ключами-строками и булевыми значениями». */
      internalUpdate: false,
    };
  },
  watch: {
    modelValue: {
      immediate: true,
      handler(newVal) {
        if (this.internalUpdate) {
          this.internalUpdate = false;
          return;
        }
        const map: Record<string, boolean> = {};
        this.brands.forEach(brand => {
          map[brand.name] = newVal.includes(brand.name);
        });
        this.selectedBrandsMap = map;
      }
    },
    selectedBrandsMap: {
      deep: true,
      handler(newArr) {
        this.internalUpdate = true;
        const selected = Object.keys(newArr).filter(name => newArr[name]);
        this.$emit('update:modelValue', selected);
      }
    }
  },
});
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.content-item {
  &__container {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }
}
</style>