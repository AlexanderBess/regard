<template>
  <div id="app">
    Ответы по задачам №1 и №3 можно увидеть в коносли
    <AComponent/>
  </div>
</template>

<script>
import AComponent from "@/components/A";

export default {
  name: 'App',
  components: {
    AComponent
  },
  mounted() {
    const a = { b: { c: 3, d: [3, 4] }, a: 12 }
    console.log('Решение задачи №1:', this.copy(a, ['a.a', 'b.c', 'b.d.0', 'b.c.e']))
    console.log('Решение задачи №3:', this.booleanToInt({ a: { b: true }, c: false, d: 'qwerty' }))
  },
  methods: {
    /**
     * Задача №1
     * Функция копирования свойств объекта по заданным путям.
     * @param {Object} obj - Исходный объект.
     * @param {Array} paths - Массив путей, которые нужно скопировать.
     * @returns {Object} - Новый объект с скопированными свойствами.
     */
    copy(obj, paths) {
      // Проверка наличия объекта и массива путей
      if (typeof obj !== 'object' || !Array.isArray(paths)) {
        throw new Error('Некорректные входные данные');
      }

      // Функция для рекурсивного копирования значений по указанному пути
      const copyValue = (source, path) => {
        const keys = path.split('.');
        let value = source;
        for (const key of keys) {
          if (value && typeof value === 'object' && key in value) {
            value = value[key];
          } else {
            // Если какой-то из ключей не найден, возвращаем undefined
            return undefined;
          }
        }
        return value;
      };

      // Создаем новый объект для сохранения скопированных значений
      const result = {};

      // Проходим по каждому пути и копируем соответствующие значения
      for (const path of paths) {
        const value = copyValue(obj, path);
        if (value !== undefined) {
          // Если значение не undefined, добавляем его в новый объект
          const keys = path.split('.');
          let current = result;
          for (let i = 0; i < keys.length - 1; i++) {
            const key = keys[i];
            current[key] = current[key] || {};
            current = current[key];
          }
          current[keys[keys.length - 1]] = value;
        }
      }

      return result;
    },

    /**
     * Задача №3
     * Функция преобразования булевого значения в числовое.
     * @param {any} input - Входное значение для преобразования.
     * @returns {any} - Преобразованное значение.
     */
    booleanToInt(input) {
      // Проверка, является ли входное значение булевым типом
      if (typeof input === 'boolean') {
        // Если булево значение, возвращаем 1 для true и 0 для false
        return input ? 1 : 0;
      }

      // Проверка, является ли входное значение массивом
      if (Array.isArray(input)) {
        // Если массив, рекурсивно вызываем функцию для каждого элемента массива
        return input.map(item => this.booleanToInt(item));
      }

      // Проверка, является ли входное значение объектом (не включая null)
      if (typeof input === 'object' && input !== null) {
        // Если объект, создаем новый объект и рекурсивно вызываем функцию для каждого свойства
        const result = {};
        for (const key in input) {
          result[key] = this.booleanToInt(input[key]);
        }
        return result;
      }

      // Если входное значение не является булевым, массивом или объектом, возвращаем его без изменений
      return input;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
